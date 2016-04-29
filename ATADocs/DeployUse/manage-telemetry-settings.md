---
# required metadata

title: 管理遙測設定 | Microsoft Advanced Threat Analytics
description: 描述 ATA 所收集的資料，並提供關閉資料收集的步驟。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 管理遙測設定
Advanced Threat Analytics (ATA) 會收集有關 ATA 的匿名遙測資料，並透過 HTTPS 連線將資料傳輸至 Microsoft 伺服器。  Microsoft 將使用此資料以協助改善未來的 ATA 版本。

## 收集的資料
收集的資料包含下列內容︰

-   來自 ATA 中心和 ATA 閘道的效能計數器

-   授權 ATA 後的產品識別碼

-   ATA 中心的部署日期

-   已部署的 ATA 閘道數目

-   下列的 Active Directory 資訊︰

    -   依字母順序排序時，名稱會是第一個網域的網域識別碼

    -   網域控制站數量

    -   透過連接埠鏡像 ATA 所監視的網域控制站數量

    -   站台數量

    -   電腦數量

    -   群組數量

    -   使用者數量

-   可疑活動  – 收集每個可疑活動的資料如下︰

    (**不會**收集電腦名稱、使用者名稱和 IP 位址)

    -   可疑的活動類型

    -   可疑的活動識別碼

    -   狀態

    -   開始與結束時間

    -   提供輸入

### 停用資料收集
若要停止收集及傳送遙測資料至 Microsoft，請遵循下列步驟。

1.  登入 ATA 主控台 在工具列中選取三個點並選取 [關於]****。

2.  取消選取**將使用資訊傳送給我們，以於未來協助改善客戶經驗**的核取方塊。

## 另請參閱
- [1.5 版有什麼新功能](whats-new-version-1.5.md)
- [1.4 版有什麼新功能](whats-new-version-1.4.md)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


