---
title: "使用 ATA 主控台 | Microsoft Advanced Threat Analytics"
description: "描述如何登入 ATA 主控台和主控台的元件"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 7f9ca7dcb227f5dde1225c55150fd1c737722ce1


---

# 使用 ATA 主控台

使用 ATA 主控台監視及回應 ATA 偵測到的可疑活動。

## 啟用 ATA 主控台的存取權
任何身為 ATA 中心伺服器上之本機系統管理員群組成員的使用者都有權限可登入 ATA 主控台並管理 ATA 設定。
為了讓使用者登入 ATA 主控台，而不用成為本機系統管理員，請將他們新增至本機群組︰**Microsoft Advanced Threat Analytics 系統管理員**。

## 登入 ATA 主控台

1. 在 ATA 中心伺服器中，按一下桌面上的 **Microsoft ATA 主控台**圖示，或開啟瀏覽器並瀏覽到 ATA 主控台。

    ![ATA 伺服器圖示](media/ata-server-icon.png)

>[!NOTE]
> 您也可以從 ATA 中心或 ATA 閘道開啟瀏覽器，然後瀏覽到您在為 ATA 主控台安裝 ATA 中心時設定的 IP 位址。    

2.  輸入您的使用者名稱和密碼，然後按一下 [登入]。

![ATA 登入畫面影像](media/ATA-log-in-screen.jpg)

> [!NOTE]
> 您必須以特定使用者身分登入，該特定使用者為本機系統管理員群組或 Microsoft Advanced Threat Analytics 系統管理員群組成員。

## ATA 主控台

ATA 主控台可讓您依時間順序快速檢視所有可疑的活動。 不但讓您能夠深入了解任何活動，還能根據這些活動執行動作。 主控台也會顯示警示和通知，以反白顯示 ATA 網路相關問題或視為可疑的新活動。

以下是 ATA 主控台的重要元素。


### 攻擊時間表

這是您登入 ATA 主控台時會前往的預設登陸頁面。 根據預設，所有開啟的可疑活動都會顯示在攻擊時間表上。 您可以篩選攻擊時間表，顯示所有、開啟、關閉或已解析的可疑活動。 您也可以查看指派給每個活動的嚴重性。

![ATA 攻擊時間表影像](media/attack-timeline.png)

如需詳細資訊，請參閱[處理可疑活動](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities)。

### 通知列

偵測到新的可疑活動時，通知列會自動在右側開啟。 如果從上次登入之後有新的可疑活動，通知列會在您成功登入後開啟。 您可以隨時按一下右側箭號來存取通知列。

![ATA 通知列影像](media/notification-bar.png)

### 篩選窗格

您可以根據狀態和嚴重性，篩選要顯示在攻擊時間表的可疑活動，或者要顯示在實體設定檔可疑活動索引標籤中的可疑活動。

### 搜尋列

您可以在上層功能表找到搜尋列。 您可以搜尋 ATA 中的特定使用者、電腦或群組。 若要試試看，請開始輸入。

![ATA 主控台搜尋影像](media/ATA-console-search.png)

### 健全狀況中心

健康情況中心會在 ATA 部署未正常運作時向您提出警示。

![ATA 健全狀況中心影像](media/health-center.png)

每當您的系統發生問題，例如連線錯誤或中斷與 ATA 閘道的連線，[健全狀況中心] 圖示會顯示一個紅點來告知您。 ![ATA 健全狀況中心有紅點的影像](media/ATA-Health-Center-Alert-red-dot.png)

健康情況中心警示可以關閉或解決，並且根據其嚴重性分類為 [高]、[中] 或 [低]。 如果您解除 ATA 服務偵測為仍在作用中的警示，它會自動移至開啟的警示清單。 如果系統偵測到已不再構成警示 (情況已修正)，它會自動移至已解除的清單。

### 使用者和電腦設定檔

ATA 會為網路中每個使用者和電腦建置設定檔。 在使用者設定檔中，ATA 會顯示一般資訊，例如群組成員資格、最近的登入和最近存取的資源。

![使用者設定檔](media/user-profile.png)

在電腦設定檔中，ATA 會顯示一般資訊，例如最近的登入和最近存取的資源。

![電腦設定檔](media/computer-profile.png)

ATA 會在下列頁面上提供實體 (電腦、裝置、使用者) 的其他資訊︰[摘要]、[活動] 和 [可疑的活動]。

ATA 無法完全解析的設定檔將會利用旁邊的半實心圓形圖示來識別。


![ATA 無法解析的設定檔影像](media/ATA-Unresolved-Profile.jpg)

### 小型設定檔

在主控台中出現單一實體的任何位置，例如使用者或電腦，如果您將滑鼠停留在實體上，就會自動開啟小型設定檔，顯示下列資訊 (如果有的話)︰

![ATA 小型設定檔影像](media/ATA-mini-profile.jpg)

-   Name

-   圖片

-   電子郵件

-   電話

-   根據嚴重性分類的可疑活動數目



## 另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


