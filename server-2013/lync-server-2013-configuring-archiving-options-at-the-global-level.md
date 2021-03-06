﻿---
title: 在全域層級設定封存選項
TOCTitle: 在全域層級設定封存選項
ms:assetid: bfe415f7-2abf-41ee-a1cb-cf48b2d59c0c
ms:mtpsurl: https://technet.microsoft.com/zh-tw/library/JJ205233(v=OCS.15)
ms:contentKeyID: 49292183
ms.date: 08/10/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 在全域層級設定封存選項

 

_**上次修改主題的時間：** 2012-10-10_

當您新增封存至拓撲並發行拓撲時，Lync Server 會建立封存的全域設定。依預設，全域設定不會啟用任何封存選項。全域設定控制您的整體部署啟用哪些選項，除非您設定網站或集區設定，否則後者優先於全域設定。

如需關於封存組態如何運作的詳細資訊，包含全域、網站與集區設定的階層，請參閱規劃文件、部署文件或作業文件中的[在 Lync Server 2013 中封存的運作方式](lync-server-2013-how-archiving-works.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398811.note(OCS.15).gif" title="note" alt="note" />附註：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必須先在 [封存] 組態中指定所有適當選項，才能啟用封存功能。</td>
</tr>
</tbody>
</table>


## 在全域層級設定封存選項

1.  使用指派到 CsArchivingAdministrator 或 CsAdministrator 角色的使用者帳戶，登入內部部署中的任何電腦。

2.  開啟瀏覽器視窗，然後輸入 Admin URL 以開啟 Lync Server 2013 控制台。如需關於可用來啟動 Lync Server 2013 控制台不同方法的詳細資訊，請參閱[開啟 Lync Server 系統管理工具](lync-server-2013-open-lync-server-administrative-tools.md)。

3.  在左側導覽列中，依序按一下 \[監控和封存\]及 \[封存組態\]。

4.  在 \[封存組態\] 頁面上，依序按一下 \[通用\]、\[編輯\] 和 \[顯示詳細資料\]。

5.  在 \[編輯封存組態 - 通用\] 的 \[封存組態\] 下拉式清單中，選取下列期中一個封存選項：
    
      - **停用封存**
    
      - **封存 IM 工作階段**
    
      - **封存 IM 與 Web 會議工作階段**

6.  另外在 \[編輯封存組態 - 通用\] 頁面上執行下列步驟：
    
      - 若要在封存無法使用時封鎖活動，請選取 \[封存失敗時封鎖立即訊息 (IM) 和 Web 會議工作階段\] 核取方塊。
    
      - 若要使用 Microsoft Exchange Server 存放封存資料，請按一下 \[Microsoft Exchange 整合\] 核取方塊。
    
      - 若要啟用資料清除，請選取 \[啟用封存資料的清除\] 核取方塊，然後執行下列其中一項：
        
          - 若要指定在特定天數後進行清除，請按一下 \[在最大持續期限 (天) 後清除匯出的封存資料和儲存的封存資料\]，然後指定天數。
        
          - 若要限制只清除已匯出的封存資料，請按一下 \[只清除匯出的封存資料\]。

7.  按一下 \[認可\]。

