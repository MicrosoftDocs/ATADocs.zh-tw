---
title: 使用記錄檔針對 Advanced Threat Analytics 進行疑難排解 | Microsoft Docs
description: 描述如何使用 ATA 記錄檔來疑難排解問題
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 307e7ff1e41b166088cb31822070116f134b36e3
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195607"
---
# <a name="troubleshooting-ata-using-the-ata-logs"></a>使用 ATA 記錄檔來疑難排解 ATA

適用對象：*Advanced Threat Analytics 1.9 版*

ATA 記錄提供深入解析，說明 ATA 的每個元件在任何指定時間點執行的動作。

## <a name="ata-gateway-logs"></a>ATA 閘道記錄檔
在本節中，對 ATA 閘道的每個參考也都適用於 ATA 輕量型閘道。 

ATA 閘道記錄檔位於安裝 ATA、稱為 **Logs** 的子資料夾中，預設位置為：**C:\Program Files\Microsoft Advanced Threat Analytics\\**。 在預設安裝位置中，它位於：**C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**。

ATA 閘道有下列記錄檔︰

-   **Microsoft.Tri.Gateway.log** – 此記錄檔包含 ATA 閘道 (包括解決方式和錯誤) 中發生的所有事件。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

-   **Microsoft.Tri.Gateway-Resolution.log** – 此記錄檔包含 ATA 閘道中流量所看見的實體解決詳細資料。 其主要用途是調查實體的解析問題。

-   **Microsoft.Tri.Gateway-Errors.log** – 此記錄檔只包含 ATA 閘道所捕捉的錯誤。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – 此記錄檔群組所有類似的錯誤和例外狀況，並測量其計數。
    每當 ATA 閘道服務啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 其主要用途是了解 ATA 閘道是否有任何新的錯誤或問題 (由於錯誤會經過分組，因此更容易快速了解是否出現任何新的問題)。
-   **Microsoft.Tri.Gateway.Updater.log** - 此記錄檔用於閘道更新程式程序中，該程序負責更新 ATA 閘道 (如果設定為自動執行)。 如果是 ATA 輕量型閘道更新程式，閘道更新程式程序也負責 ATA 輕量型閘道的資源限制。
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** - 此記錄檔會將所有類似的錯誤和例外狀況分組，並測量其計數。 每當 ATA 更新程式服務啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 它可讓您了解 ATA 更新程式是否有任何新的錯誤或問題。 這些錯誤會分組，方便您快速了解是否偵測到任何新的錯誤或問題。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。 根據預設，如果已經有超過 10 個相同類型的檔案，就會刪除最舊的檔案。

## <a name="ata-center-logs"></a>ATA 中心記錄檔
ATA 中心記錄位於名為 **Logs** 的子資料夾中。 在預設安裝位置中，它位於：**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**"。
> [!Note]
> ATA 主控台記錄檔先前位於 IIS 記錄檔之下，現在則位於 ATA 中心記錄檔之下。

ATA 中心有下列記錄檔︰

-   **Microsoft.Tri.Center.log** – 此記錄檔包含 ATA 中心 (包括偵測和錯誤) 中發生的所有事件。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

-   **Microsoft.Tri.Center-Detection.log** – 此記錄檔只包含 ATA 中心的偵測詳細資料。 其主要用途是調查偵測問題。

-   **Microsoft.Tri.Center-Errors.log** – 此記錄檔只包含 ATA 中心所捕捉的錯誤。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – 此記錄檔群組所有類似的錯誤和例外狀況，並測量其計數。
    每當 ATA 中心服務啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 其主要用途是了解 ATA 中心是否有任何新的錯誤或問題。由於錯誤會經過分組，因此更容易快速了解是否有新的錯誤或問題。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。 根據預設，如果已經有超過 10 個相同類型的檔案，就會刪除最舊的檔案。


## <a name="ata-deployment-logs"></a>ATA 部署記錄檔
對於安裝產品的使用者，ATA 部署記錄位於暫存記錄中。 在預設安裝位置中，它位於：**C:\Users\Administrator\AppData\Local\Temp** (或 %temp% 的上一層目錄)。

ATA Center 部署記錄檔︰

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS.log** - 此記錄檔會列出 ATA 中心的部署程序步驟。 其主要用途是追蹤 ATA 中心部署程序。

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_0_MongoDBPackage.log** - 此記錄檔會列出 ATA 中心上 MongoDB 部署程序的步驟。 其主要用途是追蹤 MongoDB 部署程序。

-   **Microsoft Advanced Threat Analytics Center_YYYYMMDDHHMMSS_1_MsiPackage.log** - 此記錄檔會列出 ATA 中心二進位檔的部署程序步驟。 其主要用途是追蹤 ATA 中心二進位檔的部署。

ATA 閘道和 ATA 輕量型閘道部署記錄：

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS.log** - 此記錄檔會列出 ATA 閘道的部署程序步驟。 其主要用途是追蹤 ATA 閘道部署程序。

-   **Microsoft Advanced Threat Analytics Gateway_YYYYMMDDHHMMSS_001_MsiPackage.log** - 此記錄檔會列出 ATA 閘道二進位檔的部署程序步驟。 其主要用途是追蹤 ATA 閘道二進位檔的部署。


> [!NOTE] 
> 除了此處所提及的部署記錄之外，另有其他開頭為 "Microsoft Advanced Threat Analytics" 的記錄，也可提供部署處理序的其他資訊。


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
