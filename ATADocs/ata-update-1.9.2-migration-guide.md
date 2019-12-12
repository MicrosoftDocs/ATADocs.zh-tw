---
title: Advanced Threat Analytics 更新至 1.9.2 移轉指南 | Microsoft Docs
description: 將 ATA 更新至 1.9.2 版的程序
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 22420ea90bc922684a4e99ad303bba831f3a45e7
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196069"
---
# <a name="ata-version-192"></a>ATA 1.9.2 版


我們很高興能宣布 Microsoft Advanced Threat Analytics 1.9 版更新 2 現已可供使用。

本文說明 Microsoft Advanced Threat Analytics (ATA) 1.9 版更新 2 中所修正的問題。 此更新的組建編號為 1.9.7478。

## <a name="improvements-included-in-this-update"></a>此更新包含的改善

此更新包含 Windows Server 2019 (包含 Core 版本，但不包含 Nano) 作為中心、閘道及輕量型閘道元件的支援作業系統。

此更新也包含效能和穩定性改善，以及針對客戶所回報之問題的修正。

## <a name="fixed-issues-included-in-this-update"></a>此更新包含的問題修正

- 修正目錄資料會顯示直接管理員及遞迴成員資格的問題。
- 修正 ATA 中心 URL 設定不一定會顯示本機 IP 或本機電腦名稱的問題。
- 修正在健康情況警示包含不存在的閘道時會引發的健康情況警示下載問題。
- 修正翻譯問題。
- 修正 MongoDB 資料庫版本未更新的問題。
- 修正在 Active Directory 同步期間發生高記憶體問題的罕見案例。
- 修正主控台僅允許選取不支援憑證的罕見案例。
- 修正接收到「基於異常行為懷疑身分遭竊」訊息之誤判實例的罕見案例。
- 修正在警示自動更新時發生時間軸跳躍的罕見案例。

## <a name="get-this-update"></a>取得此更新

若要取得此更新的獨立套件，請移至 Microsoft 下載中心網站：[立即下載 ATA 1.9.2 套件](https://www.microsoft.com/en-us/download/details.aspx?id=56725)。

### <a name="prerequisites"></a>必要條件

若要安裝此更新，您必須已安裝下列其中一個 ATA 版本： 
- 適用於 ATA 1.9 的更新 1 (1.9.7412 版)
- ATA 1.9 (1.9.7312 版)
- 適用於 ATA 1.8 的更新 1 (1.8.6765 版)
- ATA 1.8 (1.8.6645 版)

### <a name="restart-requirement"></a>重新啟動需求

套用此更新後，您的電腦可能需要重新啟動。

### <a name="update-replacement-information"></a>更新取代資訊

此更新會取代 ATA 1.9.1 版 (1.9.7412)。


## <a name="see-also"></a>請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA 版本](ata-versions.md)