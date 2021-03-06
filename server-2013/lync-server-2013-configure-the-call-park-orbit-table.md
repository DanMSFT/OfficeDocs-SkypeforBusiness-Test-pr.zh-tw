﻿---
title: Lync Server 2013：設定通話駐留軌道表格
TOCTitle: 設定通話駐留軌道表格
ms:assetid: e5cc0c19-7b2c-48e7-a21d-cfb23c842f0f
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg399020(v=OCS.15)
ms:contentKeyID: 49292631
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 中設定通話駐留軌道表格

 

_**上次修改主題的時間：** 2012-09-10_

通話駐留使用軌道來駐留通話。使用者可以駐留並擷取通話之前，您必須設定 通話駐留軌道表。您需要指定組織將保留用於駐留通話的分機號碼範圍 (軌道)，並透過指定處理各個範圍的 通話駐留集區，以定義這些範圍的路由。當您定義軌道範圍時，目標是要有足夠的軌道，以便不會太快重複使用任何一個軌道，但也不要有太多軌道，以免限制使用者或其他服務可用的分機數目。您可以為每個部署 通話駐留應用程式 的 Lync Server 集區，建立多個 通話駐留軌道範圍。每個 通話駐留軌道範圍必須要有通用的唯一名稱和一組唯一的分機。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />重要事項：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>軌道範圍通常包含 100 或更少的軌道。每個範圍還可以更大，只要不超過每個範圍 10,000 個軌道的上限，而且每個集區的軌道數小於 50,000 個即可。如果範圍太小，則重複使用軌道的速度會更快速。</td>
</tr>
</tbody>
</table>


針對軌道範圍使用虛擬分機 (沒有為其指派使用者或電話的分機) 區塊。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支援將直接向內撥號 (DID) 號碼指派為 通話駐留範圍表中的範圍號碼。</td>
</tr>
</tbody>
</table>


## 本章節內容

[在 Lync Server 2013 中建立或修改通話駐留軌道範圍](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)

