---
title: "管理 Advanced Threat Analytics 遙測設定 | Microsoft Docs"
description: "描述 ATA 所收集的資料，並提供關閉資料收集的步驟。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 1b6da432e81bc42b772b2146213d2f24bee6231a


---

適用於︰Advanced Threat Analytics 1.7 版



# <a name="manage-telemetry-settings"></a>管理遙測設定
Advanced Threat Analytics (ATA) 會收集有關 ATA 的匿名遙測資料，並透過 HTTPS 連線將資料傳輸至 Microsoft 伺服器。  Microsoft 將使用此資料以協助改善未來的 ATA 版本。

## <a name="data-collected"></a>收集的資料
收集的匿名資料包含下列內容︰

-   來自 ATA 中心和 ATA 閘道的效能計數器

-   來自 ATA 授權複本的產品識別碼

-   ATA 中心的部署日期

-   已部署的 ATA 閘道數目

-   下列匿名 Active Directory 資訊︰

    -   依字母順序排序時，名稱會是第一個網域的網域識別碼

    -   網域控制站數量

    -   透過連接埠鏡像 ATA 所監視的網域控制站數量

    -   站台數量

    -   電腦數量

    -   群組數量

    -   使用者數量

-   可疑活動  - 對各項可疑活動收集的匿名資料如下︰

    (**不會**收集電腦名稱、使用者名稱和 IP 位址)

    -   可疑的活動類型

    -   可疑的活動識別碼

    -   狀態

    -   開始與結束時間

    -   提供輸入

- 健全狀況問題 - 為每個健全狀況問題收集下列匿名資料︰

    (不會收集電腦名稱、使用者名稱和 IP 位址)

    -   健全狀況問題類型

    -   健全狀況問題識別碼

    -   狀態

    -   開始與結束時間

- ATA 主控台 URL 位址 - 使用 ATA 主控台時的 URL 位址，即造訪 ATA 主控台中的哪些頁面。


### <a name="disable-data-collection"></a>停用資料收集
請執行下列步驟，以停止收集及將遙測資料傳送到 Microsoft：

1.  登入 ATA 主控台，按一下工具列中的三個點，然後選取 [關於]。

2.  取消選取**將使用資訊傳送給我們，以於未來協助改善客戶經驗**的核取方塊。

## <a name="see-also"></a>另請參閱
- [1.6 版的新功能](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


