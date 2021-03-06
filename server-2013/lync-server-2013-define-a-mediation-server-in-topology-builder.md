﻿---
title: Lync Server 2013：在拓撲產生器中定義中繼伺服器
TOCTitle: 在拓撲產生器中定義中繼伺服器
ms:assetid: 59d8f5ba-5064-4ea5-b4bf-2b9736e0fedd
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/Gg398391(v=OCS.15)
ms:contentKeyID: 49291010
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在 Lync Server 2013 的拓撲產生器中定義中繼伺服器

 

_**上次修改主題的時間：** 2013-03-25_

遵循本主題中的步驟，在先前未部署 企業語音的網站上，使用 拓撲產生器來定義與 前端集區組合的獨立 中繼伺服器或集區。

您可以使用屬於 Administrators 群組成員的帳戶來定義拓撲。

## 定義與 前端集區組合的 中繼伺服器

遵循本主題中的步驟，在先前尚未部署 企業語音的網站上，使用 拓撲產生器來定義與 前端集區組合的 中繼伺服器。

## 將 中繼伺服器新增至 前端集區

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 拓撲產生器的主控台樹狀目錄中，展開您要定義 前端集區的網站名稱。

3.  在主控台樹狀目錄中，以滑鼠右鍵按一下所需的 前端集區類型，然後按一下 \[新增 前端集區..\] 。

4.  完整瀏覽 \[定義新前端集區\] 精靈，直到到達 \[選取組合的伺服器角色\] 頁面為止。

5.  在 \[選取組合的伺服器角色\] 中，勾選 \[組合 中繼伺服器\] 選項。
    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><ul>
    <li><p>如果您選取的 前端集區類型是 Enterprise Edition，則將會在該 前端集區的所有 前端伺服器上安裝 中繼伺服器元件。</p></li>
    <li><p>中繼伺服器所使用的 [下一個躍點集區] 將會是已在其中組合 中繼伺服器的 前端集區。</p></li>
    <li><p>中繼伺服器所使用的 [Edge 集區] 將會是與已在其中組合 中繼伺服器的 前端集區相關聯的相同 Edge 集區。</p></li>
    </ul></td>
    </tr>
    </tbody>
    </table>


6.  按一下 \[成為預設\] ，使用這個 前端集區，將通話從 Microsoft Office Communications Server 2007 R2 路由傳送至 PSTN。

7.  將一或多個對等裝置關聯至 前端集區之後，按一下 \[完成\] 。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在您繼續進行 企業語音部署程序的下一個步驟之前，請確保 中繼伺服器集區 (例如，已與 中繼伺服器元件組合的 前端集區) 會使用您指定的 FQDN。</td>
    </tr>
    </tbody>
    </table>


8.  接著，遵循＜部署指南＞文件中的 [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)中的程序，先將 中繼伺服器新增至您的拓撲，然後視需要繼續進行下一個步驟來修改 中繼伺服器的聆聽連接埠。您必須在每次使用 拓撲產生器來定義或修改拓撲之前，發行您的拓撲。

## 定義獨立的 中繼伺服器

遵循本主題中的步驟，在先前尚未部署 企業語音的網站上，使用 拓撲產生器來定義獨立的 中繼伺服器或集區。

如果您已經在此網站上部署了已與 前端集區組合的 中繼伺服器，則您可以略過本節和 [在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)，繼續進行 [在 Lync Server 2013 中設定主幹](lync-server-2013-configuring-trunks.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本節假設您已經依據＜部署指南＞文件中的 <a href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">在 Lync Server 2013 中定義和設定前端集區或 Standard Edition Server</a>和 <a href="lync-server-2013-publish-the-topology.md">在 Lync Server 2013 中發行拓撲</a>，至少設定了一個 前端集區。</td>
</tr>
</tbody>
</table>


## 新增中繼伺服器

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 拓撲產生器的主控台樹狀目錄中，展開您要定義 中繼伺服器的網站名稱。

3.  在主控台樹狀目錄中，以滑鼠右鍵按一下 \[中繼集區\] 節點，然後按一下 \[ 中繼伺服器集區\] 。

4.  在 \[定義新的中繼集區\] 中，鍵入 中繼伺服器集區的完整網域名稱 (FQDN)。

5.  接著執行下列其中一項作業：
    
      - 如果您想要在集區中部署多部 中繼伺服器以提供高可用性，則請選取 \[多部電腦集區\] 。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您必須部署 DNS 負載平衡以支援擁有多部 中繼伺服器的 中繼伺服器集區。如需詳細資訊，請參閱規劃文件中 <a href="lync-server-2013-dns-load-balancing.md">Lync Server 2013 中的 DNS 負載平衡</a>的＜在 中繼伺服器集區上使用 DNS 負載平衡＞一節的說明。</td>
        </tr>
        </tbody>
        </table>
    
      - 如果您因為不需要高可用性而只想在集區裡部署一部 中繼伺服器的話，請選取 **\[單一電腦集區\]** 。略過下列步驟。

6.  如果您在上一個步驟中，在 \[定義此集區中的電腦\] 項目上選取了 \[多部電腦集區\] ，則可按一下 \[電腦 FQDN\] 、鍵入集區中每一部伺服器的 FQDN，然後按一下 \[新增\] 。針對您要新增至集區的其他所有 中繼伺服器重複執行此步驟。在定義集區中的所有電腦之後，按 \[下一步\] 。

7.  在 **\[選取下一個躍點\]** 頁面上，依序按一下 **\[下一個躍點集區\]** 與要使用此 中繼伺服器集區的前端集區 FQDN，然後按 **\[下一步\]** 。

8.  在 **\[選取 Edge Server\]** 頁面上，執行下列其中一項：
    
      - 如果您想要將 PSTN 連線能力提供給啟用 企業語音的外部使用者，則可在 \[選取此中繼伺服器所使用的 Edge 集區\] 下方，按一下將使用此 中繼伺服器集區的 Edge Server 集區 FQDN，以便為外部使用者提供 PSTN 連線能力，然後按\[下一步\] 。
    
      - 如果您不打算為外部使用者啟用 企業語音，或是不想為位於內部網路之外的使用者提供 PSTN 連線能力，請按 \[下一步\] 。

9.  接著，遵循部署文件中＜ [在 Lync Server 2013 中發行拓撲](lync-server-2013-publish-the-topology.md)＞裡的步驟，將中繼伺服器新增至拓撲。每次使用拓撲產生器建立或修改拓撲時，您必須發行拓撲，以便使用資料安裝執行 Lync Server 的伺服器所需的檔案。接著，視需要進行後續步驟，修改中繼伺服器上的聆聽連接埠。

## 定義 中繼伺服器聆聽連接埠

遵循本主題中的步驟，使用 拓撲產生器，來定義 中繼伺服器或集區將用來接受來自閘道對等之連入連線的聆聽連接埠。

## 修改 中繼伺服器聆聽連接埠

1.  啟動拓撲產生器：依序按一下 \[開始\]、\[所有程式\]、\[Microsoft Lync Server 2013\] 和 \[Lync Server 拓撲產生器\]。

2.  在 拓撲產生器的控制台樹狀目錄中，展開 \[中繼集區\] 節點，然後以滑鼠右鍵按一下先前建立的 中繼伺服器。

3.  根據預設，中繼伺服器上的 SIP 聆聽連接埠分別是 5070 (供來自 Lync Server 的 TLS 流量使用)、5067 (供來自對等閘道、PBX 或 SBC 的 TLS 流量使用)。TCP 連接埠預設是停用的。如果您的閘道不支援 TLS，則必須啟用 TCP 連接埠。

4.  指定 中繼伺服器將用來接受來自 PSTN 閘道之連入連線所需的 TLS 或 TCP 聆聽連接埠範圍。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若未勾選 [啟用 TCP 連接埠] ，則不一定要輸入 TCP 連接埠範圍。此為選用設定。</td>
    </tr>
    </tbody>
    </table>


接下來， [在 Lync Server 2013 中於拓撲產生器內定義閘道](lync-server-2013-define-a-gateway-in-topology-builder.md)，並遵循 [在 Lync Server 2013 中安裝中繼伺服器的檔案](lync-server-2013-install-the-files-for-mediation-server.md)中的程序，在集區中的每部 中繼伺服器上安裝檔案。

