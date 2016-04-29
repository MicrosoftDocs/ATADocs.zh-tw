---
# required metadata

title: ATA 1.5 版的新功能 | Microsoft Advanced Threat Analytics
description: 列出 ATA 1.5 版的新功能以及已知問題
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 1.5 版的新功能
這些版本資訊提供此版 Advanced Threat Analytics 中已知問題的相關資訊。

## 什麼是 ATA 1.5 更新的新功能？
更新至 ATA 1.5 提供下列各方面的改良︰

-   更快速的偵測時間

-   增強對 NAT (網路位址轉譯) 裝置的自動偵測演算法

-   增強對未加入網域裝置的名稱解析程序

-   支援在產品更新期間的資料移轉

-   針對涉及上千個實體的可疑活動提供更好的 UI 回應性

-   改良監視警示的自動解析

-   增強的監視和疑難排解有更多的效能計數器

## 已知問題
下列已知問題存在於此版本中。

### 新 ATA 閘道器安裝失敗
將 ATA 部署更新至 ATA 1.5 版之後，您會在安裝新 ATA 閘道時收到下列錯誤︰
未安裝 Microsoft Advanced Threat Analytics 閘道

![ATA GW 錯誤](media/ATA-GW-error.png)

<b>因應措施︰</b> 傳送電子郵件給 <ataeval@microsoft.com> 以要求因應措施步驟。
### 部署
指定給「資料庫資料路徑」和「資料庫日誌路徑」的資料夾必須是空的 (沒有檔案或子資料夾)。
如果不是空的，將不會進行部署。

### 從 Zip 檔案安裝
安裝 ATA 閘道時，請務必從 zip 檔案解壓縮檔案至本機目錄，並從該處安裝。 請勿直接從 zip 檔案內部安裝 ATA 閘道，否則安裝將會失敗。

### 設定
設定 ATA 閘道組態之後，當 ATA 閘道第一次啟動時，會顯示「未同步處理」標籤，直到服務完全啟動為止，在服務第一次啟動時，這可能需要多達 10 分鐘。

### 網路擷取軟體
在 ATA 閘道上，您可以安裝的唯一支援網路擷取軟體是 [Microsoft 網路監視器 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865)。 請勿安裝 Microsoft Message Analyzer 或其他任何網路擷取軟體。 安裝其他軟體將會造成 ATA 閘道停止正常運作。

### 虛擬化主機上的 KB
請勿在虛擬化主機上安裝 KB 3047154。 這可能會導致連接埠鏡像無法正常運作。

## 另請參閱
[如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


