﻿---
title: Stop-CsClsLogging
TOCTitle: Stop-CsClsLogging
ms:assetid: 63d0f0d6-5eec-4a16-b834-37611c584f52
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ619180(v=OCS.15)
ms:contentKeyID: 49291122
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stop-CsClsLogging

 

_**上次修改主題的時間：** 2015-03-09_

停止指定的集中式記錄服務案例。集中式記錄提供一種方法，讓管理員同時啟用或停用多部電腦上的 Lync Server 2013 追蹤功能。 Lync Server 2013 中已導入此 Cmdlet。

## 語法

    Stop-CsClsLogging -Scenario <String> [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## 範例

## 範例 1

範例 1 所示的命令會停止拓撲中所有伺服器的 CPS 記錄案例。

    Stop-CsClsLogging -Scenario "cps"

## 範例 2

在範例 2 中，集區 atl-cs-001.litwareinc.com 中所有伺服器上的 CPS 記錄案例都會停止。

    Stop-CsClsLogging -Scenario "cps" -Pools "atl-cs-001.litwareinc.com"

## 詳細描述

集中式記錄服務 (取代 Microsoft Lync Server 2010 中使用的 OCSLogger 與 OCSTracer 工具) 提供一種方法，讓管理員管理所有執行 Lync Server 2013 之電腦與集區的記錄和追蹤。集中式記錄可讓管理員利用單一命令，來停止、啟動及設定一或多個集區與電腦的記錄；例如，您可以使用一個命令，在所有 Address Book Server 上啟用通訊錄服務記錄功能。這和必須在每部伺服器上個別管理 (包括個別停止和啟動) 的 OCSLogger 與 OCSTracer 工具不同。此外，集中式記錄服務也提供一種方法，讓管理員使用 Windows PowerShell 命令列介面與 [Search-CsClsLogging](search-csclslogging.md) Cmdlet，從命令中搜尋追蹤記錄。

集中式記錄是以一系列預先定義的案例為主來建立，可提供比舊版 Lync Server 更精確的記錄方法。這些案例可為您預先決定伺服器元件與記錄功能；因此，啟用 RGS 案例的管理員確信將只會記錄與「回應群組」服務有關的資訊，而非不相關的服務，例如音訊會議提供者服務。

您也可以使用 [New-CsClsScenario](new-csclsscenario.md) Cmdlet，定義自訂的案例。

[Start-CsClsLogging](start-csclslogging.md) Cmdlet 提供一種方法，讓系統管理員可以在一部或一組電腦上開始記錄指定的案例。根據預設，該記錄作業在期間的時間限制逾期之前都會持續執行。不過，系統管理員可以使用 **Stop-CsClsLogging** Cmdlet，隨時手動停止記錄作業。

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
<td><p><em>Scenario</em></p></td>
<td><p>必要</p></td>
<td><p>System.Strkng</p></td>
<td><p>要停止的集中式記錄案例名稱。使用以下命令可以傳回可用的案例 (與其名稱) 名稱：</p>
<p>Get-CsClsScenario | Select-Object Name</p></td>
</tr>
<tr class="even">
<td><p><em>AsXml</em></p></td>
<td><p>選用</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>指定時，會使用 XML 傳回資訊。</p></td>
</tr>
<tr class="odd">
<td><p><em>Computers</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員在指定的伺服器或一組伺服器上停止記錄功能。若要在單一伺服器上停止記錄功能，請指定該伺服器的完整網域名稱。例如：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔電腦的 FQDN 來指定多個伺服器：</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>如果未加上 Computers 參數或 Pools 參數， <strong>Stop-CsClsLogging</strong> Cmdlet 將針對拓撲中的所有集區執行命令。</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>選用</p></td>
<td><p>System.String[]</p></td>
<td><p>可讓管理員在集區中的每個伺服器上停止記錄功能。若要在集區中停止記錄功能，請指定該集區的完整網域名稱。例如：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>您可以使用逗號分隔集區的 FQDN 來指定多個集區：</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## 輸入類型

無。 **Stop-CsClsLogging** Cmdlet 不接受管線傳送的輸入。

## 傳回類型

字串值或 XML 輸出。 **Stop-CsClsLogging** Cmdlet 不會傳回物件。

## 請參閱

#### 其他資源

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

