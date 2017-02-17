---
title: "Advanced Threat Analytics 1.5 版的新功能 | Microsoft Docs"
description: "列出 ATA 1.5 版的新功能以及已知問題"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 08da33114bc3f0c9aafb9914b9d77a88fac009f4


---

# <a name="whats-new-in-ata-version-15"></a>ATA 1.5 版的新功能
這些版本資訊提供此版 Advanced Threat Analytics 中已知問題的相關資訊。

## <a name="whats-new-in-the-ata-15-update"></a>什麼是 ATA 1.5 更新的新功能？
更新至 ATA 1.5 提供下列各方面的改良︰

-   更快速的偵測時間

-   增強對 NAT (網路位址轉譯) 裝置的自動偵測演算法

-   增強對未加入網域裝置的名稱解析程序

-   支援在產品更新期間的資料移轉

-   針對涉及上千個實體的可疑活動提供更好的 UI 回應性

-   改良監視警示的自動解析

-   增強的監視和疑難排解有更多的效能計數器

## <a name="known-issues"></a>已知問題
下列已知問題存在於此版本中。

### <a name="new-ata-gateway-installation-fails"></a>新 ATA 閘道器安裝失敗
將 ATA 部署更新至 ATA 1.5 版之後，您會在安裝新 ATA 閘道時收到下列錯誤︰未安裝 Microsoft Advanced Threat Analytics 閘道

![ATA GW 錯誤](media/ata-install-error.png)

<b>因應措施︰</b>傳送電子郵件給 <ataeval@microsoft.com> 以要求因應措施步驟。
### <a name="deployment"></a>部署
指定給「資料庫資料路徑」和「資料庫日誌路徑」的資料夾必須是空的 (沒有檔案或子資料夾)。
如果不是空的，將不會進行部署。

### <a name="installation-from-zip-file"></a>從 Zip 檔案安裝
安裝 ATA 閘道時，請務必從 zip 檔案解壓縮檔案至本機目錄，並從該處安裝。 請勿直接從 zip 檔案內部安裝 ATA 閘道，否則安裝將會失敗。

### <a name="configuration"></a>設定
設定 ATA 閘道組態之後，當 ATA 閘道第一次啟動時，會顯示「未同步處理」標籤，直到服務完全啟動為止，在服務第一次啟動時，這可能需要多達 10 分鐘。

### <a name="network-capture-software"></a>網路擷取軟體
在 ATA 閘道上，您可以安裝的唯一支援網路擷取軟體是 [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) (Microsoft 網路監視器 3.4)。 請勿安裝 Microsoft Message Analyzer 或其他任何網路擷取軟體。 安裝其他軟體將會造成 ATA 閘道停止正常運作。

### <a name="kb-on-virtualization-host"></a>虛擬化主機上的 KB
請勿在虛擬化主機上安裝 KB 3047154。 這可能會導致連接埠鏡像無法正常運作。

## <a name="see-also"></a>另請參閱

[將 ATA 更新為 1.5 版 - 移轉指南](ata-update-1.5-migration-guide.md)

[將 ATA 更新至 1.6 版 - 移轉指南](ata-update-1.6-migration-guide.md)

[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


