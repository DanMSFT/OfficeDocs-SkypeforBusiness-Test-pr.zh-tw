﻿---
title: New-CsFIPSConfiguration
TOCTitle: New-CsFIPSConfiguration
ms:assetid: 9ce030fb-fb6b-47a2-9fb9-69e8369b43be
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205114(v=OCS.15)
ms:contentKeyID: 49291808
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsFIPSConfiguration

 

_**上次修改主題的時間：** 2014-10-29_

建立新的美國聯邦資訊處理標準 (FIPS) 組態設定資訊集合。FIPS 標準美國政府所設定的安全性標準，所有由非軍方之政府機構與政府合約商維護的電腦中，都必須使用這套標準。Lync Server 2013 中已導入此 Cmdlet。

## 語法

    New-CsFIPSConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-RequireFIPSCompliantMedia <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## 範例

## 範例 1

範例 1 所示的命令會建立一組僅在記憶體中的新 FIPS 組態設定，然後在稍後使用這些設定來更新 FIPS 組態設定的全域集合。為達成此目的，範例中的第一個命令會使用 **New-CsFIPSConfiguration** Cmdlet 搭配 InMemory 參數，以建立 Identity 為 "global" 的新 FIPS 組態設定集合；產生的設定物件會以變數 $x 儲存。

第二個命令會接著使用 **Set-CsFIPSConfiguration** Cmdlet 和 Instance 參數，以儲存在 $x 中的新集合取代 FIPS 設定的現有全域集合。

雖然此範例可運作正常，但是使用 **Set-CsFIPSConfiguration** Cmdlet 可以更容易修改 FIPS 組態設定。

    $x = New-CsFIPSConfiguration -Identity "global" -RequireFIPSCompliantMedia $False -InMemory
    
    Set-CsFIPSConfiguration -Instance $x

## 詳細描述

美國聯邦資訊處理標準 (FIPS) 是一系列的標準與準則，所有涉及美國政府工作的電腦，都必須加以遵循。例如管理密碼編譯、加密、數位簽章的 FIPS 標準 (如需詳細資訊，請參閱 <http://www.itl.nist.gov/fipspubs/by-num.htm>)。Lync Server 2013 可讓您選擇將軟體設成只使用符合 FIPS 標準的演算法。您如有參與美國政府 (或其他必須遵循 FIPS 的機構) 的工作，您可以啟用 Lync Server 2013 中的 FIPS 規範。

不過請注意，內部部署版的 Lync Server 只有一個 FIPS 組態設定的全域集合，亦即您只可針對整個 Lync Server 實作啟用或停用 FIPS 規範，而無法選擇只為如個別網站或個別的登錄器集區啟用或停用 FIPS 規範。啟用 FIPS 規範之後，有可能會在和未完全遵循 FIPS 標準的組織通訊時發生問題。亦即，**New-CsFIPSConfiguration** Cmdlet 的主要功能在管理 商務用 Skype Online 的 FIPS 規範。

預設會停用 Lync Server 2013的 FIPS 規範。

若要傳回所有指派至此 Cmdlet 的角色型存取控制 (RBAC) 角色清單 (包括您自行建立的自訂 RBAC 角色)，請在 Windows PowerShell 命令列介面提示字元中執行下列命令：

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsFIPSConfiguration"}

**Lync Server 控制台：**Lync Server 控制台不提供 New-CsFIPSConfiguration Cmdlet 所執行的功能。

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
<td><p><em>Identity</em></p></td>
<td><p>必要</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>新 FIPS 組態設定集合的唯一識別碼。由於 Lync Server 2013只支援單一 FIPS 設定全域集合，因此使用此參數的唯一方式，是在記憶體中建立「新」的全域集合。若要執行此作業，必須使用 InMemory 參數以。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>執行命令前先要求您確認。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>隱藏執行命令時可能發生的非嚴重錯誤訊息。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>建立物件參照，但而不實際將物件認可為永久變更。若將此參數所呼叫的 Cmdlet 輸出指派給變數，將可變更物件參照的屬性，然後呼叫此 Cmdlet 的對應 Set- Cmdlet 認可這些變更。</p></td>
</tr>
<tr class="odd">
<td><p><em>RequireFIPSCompliantMedia</em></p></td>
<td><p>選用</p></td>
<td><p>System.Boolean</p></td>
<td><p>設為 True 時，Lync Server 2013只會允許實體使用 FIPS 相容演算法進行驗證和授權的媒體工作階段。</p>
<p>請注意，如果您必須遵循 FIPS 規範，使用者便無法使用 Microsoft Lync Server 2010 A/V Edge Server 連線至系統，而是需要您將所有 Edge Server 升級為 Lync 2013。</p>
<p>預設值為 False。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>選用</p></td>
<td><p>System.Guid</p></td>
<td><p>要建立新 FIPS 組態設定之 商務用 Skype Online 租用戶帳戶的全域唯一識別碼 (GUID)。例如：</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>您可以執行此命令，為每個租用戶傳回租用戶識別碼：</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>描述執行命令後的結果，但無須實際執行命令。</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。**New-CsFIPSConfiguration** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

**New-CsFIPSConfiguration** Cmdlet 會建立 Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration 物件的新執行個體。

## 請參閱

#### 其他資源

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

