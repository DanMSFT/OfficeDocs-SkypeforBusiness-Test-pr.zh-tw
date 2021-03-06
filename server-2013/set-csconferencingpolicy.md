﻿---
title: Set-CsConferencingPolicy
TOCTitle: Set-CsConferencingPolicy
ms:assetid: 2ddcf4ea-ae6c-40fa-9499-4e3b1b140e68
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg425788(v=OCS.15)
ms:contentKeyID: 49290450
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferencingPolicy

 

_**上次修改主題的時間：** 2015-04-21_

修改現有的會議原則。會議原則可指定會議所能使用的功能，包括會議是否可以加入 IP 音訊和視訊，乃至於會議出席人數的上限等等。Lync Server 2010 中已導入此 Cmdlet。

## 語法

    Set-CsConferencingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferencingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowAnnotations <$true | $false>] [-AllowAnonymousParticipantsInMeetings <$true | $false>] [-AllowAnonymousUsersToDialOut <$true | $false>] [-AllowConferenceRecording <$true | $false>] [-AllowExternalUserControl <$true | $false>] [-AllowExternalUsersToRecordMeeting <$true | $false>] [-AllowExternalUsersToSaveContent <$true | $false>] [-AllowIPAudio <$true | $false>] [-AllowIPVideo <$true | $false>] [-AllowLargeMeetings <$true | $false>] [-AllowMultiView <$true | $false>] [-AllowNonEnterpriseVoiceUsersToDialOut <$true | $false>] [-AllowOfficeContent <$true | $false>] [-AllowParticipantControl <$true | $false>] [-AllowPolls <$true | $false>] [-AllowQandA <$true | $false>] [-AllowSharedNotes <$true | $false>] [-AllowUserToScheduleMeetingsWithAppSharing <$true | $false>] [-AppSharingBitRateKb <Int64>] [-AudioBitRateKb <UInt32>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisablePowerPointAnnotations <$true | $false>] [-EnableAppDesktopSharing <None | SingleApplication | Desktop>] [-EnableDataCollaboration <$true | $false>] [-EnableDialInConferencing <$true | $false>] [-EnableFileTransfer <$true | $false>] [-EnableMultiViewJoin <$true | $false>] [-EnableOnlineMeetingPromptForLyncResources <$true | $false>] [-EnableP2PFileTransfer <$true | $false>] [-EnableP2PRecording <$true | $false>] [-EnableP2PVideo <$true | $false>] [-FileTransferBitRateKb <Int64>] [-Force <SwitchParameter>] [-MaxMeetingSize <UInt32>] [-MaxVideoConferenceResolution <CIF | VGA>] [-TotalReceiveVideoBitRateKb <Int64>] [-VideoBitRateKb <Int64>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會修改會議原則 SalesConferencingPolicy 的屬性值；特別是，此命令會將 AllowConferenceRecording 屬性的值設為 False。為達成此目的，命令會呼叫 **Set-CsConferencingPolicy** Cmdlet 並使用 Identity 參數與 AllowConferenceRecording 參數。

    Set-CsConferencingPolicy -Identity SalesConferencingPolicy -AllowConferenceRecording $False

## 範例 2

在範例 2 中，設定為在組織中使用之所有會議原則中相同的兩個屬性值 (AllowAnonymousParticipantsInMeetings 和 EnableDialInConferencing) 皆會經過修改。為達成此目的，命令會先使用 **Get-CsConferencingPolicy** Cmdlet 傳回所有可用會議原則的集合。然後，此集合會管線傳送到 **Set-CsConferencingPolicy** Cmdlet，以將集合中每項原則之 AllowAnonymousParticipantsInMeetings 和 EnableDialInConferencing 屬性的值設為 False。

    Get-CsConferencingPolicy | Set-CsConferencingPolicy -AllowAnonymousParticipantsInMeetings $False -EnableDialInConferencing $False

## 範例 3

範例 3 所示的命令會修改已在網站範圍設定之所有會議原則的 MaxVideoConferenceResolution 屬性。為了執行此工作，命令會先呼叫 **Get-CsConferencingPolicy** Cmdlet 搭配 Filter 參數；篩選值 "site:\*" 可將傳回的資料限制在網站範圍設定的原則。然後再將篩選後的集合管線傳送到 **Set-CsConferencingPolicy** Cmdlet，以將集合中每項原則的 MaxVideoConferenceResolution 屬性設為 "CIF"。

    Get-CsConferencingPolicy -Filter "site:*" | Set-CsConferencingPolicy  -MaxVideoConferenceResolution CIF

## 範例 4

範例 4 會擷取會議大小上限大於 (-gt) 100 的所有原則，並將關聯的屬性值 (MaxMeetingSize) 變更為 100。為達成此目的，命令會先呼叫 **Get-CsConferencingPolicy** Cmdlet 以傳回設定供組織使用之所有會議原則的集合。然後，此集合會管線傳送到 **Where-Object** Cmdlet，這會只挑出 MaxMeetingSize 大於 100 的原則。接著將篩選後的集合管線傳送到 **Set-CsConferencingPolicy** Cmdlet，以取得集合中的每個原則，並將其 MaxMeetingSize 屬性設為 100。

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100} | Set-CsConferencingPolicy -MaxMeetingSize 100 

## 詳細描述

會議是 Lync Server 中十分重要的部分，其讓使用者群組可以共同在線上檢視投影片和視訊、共用應用程式、交換檔案，甚至進行通訊及共同作業。

對於系統管理員來說，最重要的是保有對於會議與會議設定的控制權。在某些案例中，可能會有安全性考量：根據預設，任何人 (包含未授權的使用者在內) 都可參與會議，並儲存這些會議期間所發佈的任何投影片或講義。在其他案例中，可能會有頻寬上的考量：有許多同時進行的會議，每個會議都包含數百位參與者且都會使用視訊播放和檔案共用，而這可能會在您的網路上造成大混亂。此外，有時可能也會有法律顧慮。例如，會議參與者預設可以在共用內容上加上註解；不過封存會議時並不會儲存這些註解。如果組織需要保留一份所有電子通訊的記錄，您可能會想停用註解。

當然，需要管理會議設定是一回事，實際管理這些設定又是另一回事。在 Lync Server 中，會議由會議原則管理。(在舊版軟體中，這些稱為會議原則)。但如上述，會議原則會判斷可在會議中使用的特性與功能；範圍從會議是否可包含 IP 音訊和視訊到可出席會議的人數上限都涵蓋在內。會議原則可以在全域範圍、網站範圍或個別使用者範圍設定。這可為系統管理員在決定哪些使用者可以使用哪些功能時提供了很大的彈性。

您可以在建立原則時設定原則屬性值。此外，您可以隨時使用 **Set-CsConferencingPolicy** Cmdlet 修改現有原則的屬性值。

誰可以執行此 Cmdlet：下列群組的成員預設會獲授權可以在本機上執行 **Set-CsConferencingPolicy** Cmdlet：RTCUniversalServerAdmins。若要傳回所有獲指派此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferencingPolicy"}

## 參數


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>參數</th>
<th>必要</th>
<th>類型</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowAnnotations</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許參與者在會議進行期間，在共用的任何內容上於螢幕上輸入註解。此設定會決定是否允許在會議中使用白板功能。預設值為 True。</p>
<p>請注意，註解不會和其他會議內容一起封存。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不包括註解。但是，使用者可以參與其他允許使用註解的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnonymousParticipantsInMeetings</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許匿名使用者參與會議。如果設定為 False，則只允許授權的使用者 (也就是，已登入 Active Directory 網域服務 或同盟協力廠商之 Active Directory 的使用者) 可以出席會議。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許匿名參與者。但是，使用者可以參與其他允許匿名參與者的會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowAnonymousUsersToDialOut</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許匿名使用者 (例如，未獲授權的使用者) 使用撥出電話來加入會議。利用撥出電話，會議伺服器將撥電話給該使用者；當該使用者接聽電話時，即會加入會議。</p>
<p>請注意，即使此設定設為 False，仍允許電話撥入式會議。</p>
<p>此設定會套用到會議召集人：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許匿名參與者以撥出方式加入會議；但是，使用者可以參與允許匿名使用者以撥出方式加入的其他會議。</p>
<p>預設值為 False ($False)。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowConferenceRecording</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者錄製會議。預設值為 False。</p>
<p>此設定會套用到參與會議的所有使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalUserControl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許外部使用者 (匿名使用者或同盟使用者) 取得共用應用程式或桌面的控制權。預設值為 False。</p>
<p>此設定會強制執行於個別使用者層級上，並套用到會議與對等的通訊工作階段。這表示可能允許在工作階段中的某些使用者將共用應用程式或桌面的控制權轉讓給外部使用者，而其他使用者則不得放棄控制權。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalUsersToRecordMeeting</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>表示是否允許外部使用者 (匿名使用者或同盟使用者) 記錄會議。預設值為 False。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許外部使用者記錄會議。但是，使用者可以參與允許外部使用者記錄會議的其他會議。</p>
<p>請注意，唯有當 AllowConferenceRecording 屬性已設定為 True 時，此設定才會生效。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalUsersToSaveContent</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許外部使用者 (也就是，目前未登入您網路的使用者) 儲存講義、投影片及其他會議內容。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許外部使用者儲存內容。但是，使用者可以參與其他允許外部使用者儲存內容的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowIPAudio</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議中是否允許電腦音訊。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許 IP 音訊。但是，使用者可以參與其他允許 IP 音訊的會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowIPVideo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議中是否允許電腦視訊。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許 IP 視訊。但是，使用者可以參與其他允許 IP 視訊的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowLargeMeetings</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，所有線上會議都會視為「大型會議」。針對大型會議，系統會限制預設傳送給參與者的通知數目，以及傳送的會議名冊大小。</p>
<p>預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMultiView</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時 (預設值)，可讓使用者排程允許多重檢視的會議；也就是用戶端可以在指定會議期間接收多個視訊資料流。此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不包括多重檢視。但是，使用者可以參與其他允許多重檢視的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowNonEnterpriseVoiceUsersToDialOut</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許未啟用 Enterprise Voice 的使用者使用撥出電話來加入會議。利用撥出電話，會議伺服器將撥電話給該使用者；當該使用者接聽電話時，即會加入會議。</p>
<p>請注意，即使此設定設為 False，仍允許電話撥入式會議。</p>
<p>此設定會套用到會議召集人：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許未啟用 Enterprise Voice 的使用者透過撥出電話加入會議；但是，使用者可以參與允許未啟用 Enterprise Voice 的使用者透過撥出電話加入的其他會議。</p>
<p>預設值為 False ($False)。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowOfficeContent</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設定為 False 時，可防止使用者在其會議中使用 Office 內容。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowParticipantControl</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議期間是否允許會議參與者取得共用應用程式或桌面的控制權。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則使用者建立並受此原則影響的會議將不允許參與者控制。但使用者仍可參與其他允許參與者控制的會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPolls</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議期間是否允許使用者進行線上投票。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許投票。但是，使用者可以參與其他允許投票的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowQandA</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True (預設值) 時，使用者將可在自己召集的任何線上會議中包含問答管理員。設為 False 時，使用者將無法在自己的任何會議中包含問答管理員。</p>
<p>此設定會套用至召集會議的使用者：如果設為 False，則使用者所建立受此原則影響的任何會議將允許使用問答管理員。然而，使用者可在其他允許投票的會議中使用問答管理員。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSharedNotes</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時 (預設值)，會自動以會議參與者等資訊及會議期間共用之內容的詳細資訊，來更新連結至會議之所有開啟的 OneNote 筆記本。</p></td>
</tr>
<tr class="even">
<td><p><em>AllowUserToScheduleMeetingsWithAppSharing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出是否允許使用者召集包含應用程式共用的會議。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許應用程式共用。但是，使用者可以參與其他允許應用程式共用的會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingBitRateKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>用於應用程式共用的位元速率 (KB)。預設值為 50000。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBitRateKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>用於音訊傳輸的位元速率 (KB)。音訊位元速率可以是介於 20 與 200 (含) 之間的任何整數，預設值為 200。</p>
<p>此設定會在每個使用者層級針對會議與對等通訊工作階段強制執行。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>在執行命令前先提示確認。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>選用</p></td>
<td><p>System.Strkng</p></td>
<td><p>讓系統管理員能夠提供有關會議原則的其他文字。例如，Description 可能指出應指派原則的使用者。</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePowerPointAnnotations</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True ($True) 時，使用者無法將註釋新增至會議所使用的 PowerPoint 投影片。但是根據 AllowAnnotations 屬性的值，使用者仍然可以存取其他白板功能。預設值為 False，表示允許 PowerPoint 註釋。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAppDesktopSharing</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.EnableAppDesktopSharing</p></td>
<td><p>指出會議期間是否允許參與者共用應用程式 (或其桌面)。允許的值包括：</p>
<p>Desktop。允許使用者共用他們的整個桌面。</p>
<p>SingleApplication。允許使用者共用單一應用程式。</p>
<p>None。不允許使用者共用應用程式或他們的桌面。</p>
<p>此設定會強制執行於個別使用者層級上。這表示可能允許會議中的某些使用者共用其桌面或應用程式，而相同會議中的其他使用者則無法進行共用。</p>
<p>預設值為 Desktop。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDataCollaboration</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出使用者是否可以召集包含資料共同作業活動 (如白板作業和註釋) 的會議。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許資料共用作業。但是，使用者可以參與其他允許資料共用作業的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDialInConferencing</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出使用者是否能夠利用公用交換電話網路 (PSTN) 電話撥入來加入會議。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許電話撥入式會議。但是，使用者可以參與其他允許電話撥入式會議的會議。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議期間是否允許將檔案傳輸給所有的會議參與者。預設值為 True。</p>
<p>此設定會套用到會議組織者：如果設定為 False，則受此原則影響的使用者所建立的會議將不允許檔案傳輸。但是，使用者可以參與其他允許檔案傳輸的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMultiViewJoin</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時 (預設值)，用戶端會嘗試使用多重檢視加入會議 (可讓用戶端在會議期間接收多個視訊資料流)。如果加入的會議不允許多重檢視，則會忽略此參數。此設定會強制執行於個別使用者層級上，並套用到會議與對等的通訊工作階段。這表示可能允許工作階段中的某些使用者具有多個視訊資料流，而相同會議中的其他使用者則不具有多個視訊資料流。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineMeetingPromptForLyncResources</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，使用者將會在每次使用 Outlook 進行包含受益於線上開會的受邀者 (例如會議室) 的會議排程時收到提示。預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableP2PFileTransfer</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>指出會議期間是否允許對等檔案傳輸 (也就是，不包含所有參與者的檔案傳輸)。預設值為 True ($True)。</p>
<p>此設定會強制執行於個別使用者層級上。這表示可能允許對等通訊工作階段中的某位使用者傳輸檔案，但不允許其他使用者這樣做。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableP2PRecording</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果為 True，使用者就可以記錄對等會議工作階段。預設值為 False。</p>
<p>此設定會強制執行於個別使用者層級上。這表示可能允許對等通訊工作階段中的某位使用者記錄工作階段，但不允許其他使用者這樣做。</p></td>
</tr>
<tr class="even">
<td><p><em>EnableP2PVideo</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>如果為 True，使用者就可以參與對等視訊會議工作階段。預設值為 False。</p>
<p>此設定會強制執行於個別使用者層級上。這表示可能允許對等通訊工作階段中的某位使用者使用視訊，但不允許其他使用者這樣做。</p></td>
</tr>
<tr class="odd">
<td><p><em>FileTransferBitRateKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>用於檔案傳輸的位元速率 (KB)。預設值為 50000。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>要修改之會議原則的唯一識別碼。會議原則可以在全域、網站或個別使用者範圍設定。若要修改全域原則，請使用下列語法：-Identity global。若要修改網站原則，請使用類似下列的語法：-Identity site:Redmond。若要修改個別使用者原則，請使用類似下列的語法：-Identity SalesConferencingPolicy。</p>
<p>請注意，指定 Identity 時不得使用萬用字元。如果您未指定 Identity，則 <strong>Set-CsConferencingPolicy</strong> Cmdlet 會自動修改全域會議原則。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>選用</p></td>
<td><p>會議原則</p></td>
<td><p>允許您將物件參考傳遞給 Cmdlet，而非設定個別的參數值。</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxMeetingSize</em></p></td>
<td><p>選用</p></td>
<td><p>System.UInt32</p></td>
<td><p>表示允許出席會議之人員的數目上限。達到參與者的數目上限時，嘗試加入會議的任何人都會被拒絕，並收到會議已滿的通知。此值指定的參與者人數可以是任何 32 位元的整數 (任何介於 1 和 4,294,967,295 之間的值)，但是建議數值為介於 2 和 250 (含) 之間的整數；預設值為 250。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>根據 Microsoft 測試所得，共用集區部署的上限為 250。如需支援超過 250 位參與者之會議的資訊，請參閱 <a href="http://go.microsoft.com/fwlink/?linkid=242073">http://go.microsoft.com/fwlink/?linkID=242073</a> 上的＜Microsoft Lync Server 2010 對大型會議的支援＞。</td>
</tr>
</tbody>
</table>

</div>
<p>此設定會套用到會議召集人：受此原則影響的使用者所建立的會議將不允許超過指定的參與者人數。但是，使用者可以參與其他允許額外參與者的會議。</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoConferenceResolution</em></p></td>
<td><p>選用</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MaxVideoConferenceResolution</p></td>
<td><p>表示會議視訊的解析度上限。允許的值為：</p>
<p>CIF。Common Intermediate Format (CIF) 的解析度為 352 x 288 像素。</p>
<p>VGA。VGA 的解析度為 640 像素 X 480 像素。</p>
<p>預設值為 VGA。</p></td>
</tr>
<tr class="odd">
<td><p><em>TotalReceiveVideoBitRateKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>表示在會議中使用之所有視訊的最大允許位元速率 (KB/秒)；也就是所有視訊資料流的合併總計。預設值為每秒 50000 千位元。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBitRateKb</em></p></td>
<td><p>選用</p></td>
<td><p>System.Int64</p></td>
<td><p>用於視訊傳輸的位元速率 (以 KB 為單位)。預設值為 50000。</p>
<p>此設定會在每個使用者層級針對會議與對等通訊工作階段強制執行。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>說明執行命令時若不實際執行命令的後果。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy 物件。**Set-CsConferencingPolicy** Cmdlet 接受管線傳送的會議原則物件執行個體。

## 傳回類型

**Set-CsConferencingPolicy** Cmdlet 不會傳回值或物件，而會設定 Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy 物件的執行個體。

## 請參閱

#### 其他資源

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)

