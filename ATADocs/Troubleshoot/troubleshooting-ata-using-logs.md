---
title: "使用 ATA 記錄檔來疑難排解 ATA | Microsoft Advanced Threat Analytics"
description: "描述如何使用 ATA 記錄檔來疑難排解問題"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 4f02b0fba381eb76ad500e198392ec7624a3028a


---

# 使用 ATA 記錄檔來疑難排解 ATA
ATA 記錄提供深入解析，說明 ATA 的每個元件在任何指定時間點執行的動作。

## ATA 閘道記錄檔
在本節中，對 ATA 閘道的每個參考也都適用於 ATA 輕量型閘道。 

ATA 閘道記錄檔位於名為 **Logs** 的子資料夾下。 在預設安裝位置中，其位於︰**C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**。

ATA 閘道有下列記錄檔︰

-   **Microsoft.Tri.Gateway.log** – 此記錄檔包含 ATA 閘道 (包括解決方式和錯誤) 中發生的所有事件。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

-   **Microsoft.Tri.Gateway-Resolution.log** – 此記錄檔包含 ATA 閘道中流量所看見的實體解決詳細資料。 其主要用途是調查實體的解析問題。

-   **Microsoft.Tri.Gateway-Errors.log** – 此記錄檔只包含 ATA 閘道所捕捉的錯誤。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – 此記錄檔群組所有類似的錯誤和例外狀況，並測量其計數。
    每當 ATA 閘道服務啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 其主要用途是了解 ATA 閘道是否有任何新的錯誤或問題。由於錯誤會經過分組，因此更容易閱讀及查看是否有新類型的錯誤或問題。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。

## ATA 中心記錄檔
ATA 中心記錄位於名為 **Logs** 的子資料夾中。 在預設安裝位置中，其位於︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**。

ATA 中心有下列記錄檔︰

-   **Microsoft.Tri.Center.log** – 此記錄檔包含 ATA 中心 (包括偵測和錯誤) 中發生的所有事件。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

-   **Microsoft.Tri.Center-Detection.log** – 此記錄檔只包含 ATA 中心的偵測詳細資料。 其主要用途是調查偵測問題。

-   **Microsoft.Tri.Center-Errors.log** – 此記錄檔只包含 ATA 中心所捕捉的錯誤。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – 此記錄檔群組所有類似的錯誤和例外狀況，並測量其計數。
    每當 ATA 中心服務啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 其主要用途是了解 ATA 閘道是否有任何新的錯誤或問題。由於錯誤會經過分組，因此更容易閱讀及查看是否有新類型的錯誤或問題。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。

## ATA 主控台記錄檔
ATA 主控台記錄 (管理 API 記錄) 位於名為 **Logs** 的子資料夾中。 在預設安裝位置中，其位於︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Management\Logs**。

ATA 主控台有下列記錄檔︰

-   **w3wp.log** – 此記錄檔包含管理程序 (IIS) 中發生的所有項目。


-   **w3wp-Errors.log** – 此記錄檔只包含管理程序 (IIS) 所捕捉的錯誤。


-   **8e75f9f1-ExceptionStatistics.log** – 此記錄檔群組所有類似的錯誤和例外狀況，並測量其計數。
    每當閘道服務將啟動時，這個檔案開始是空的，而且會每分鐘更新一次。 其主要用途是了解 ATA 閘道是否有任何新的錯誤或問題。由於錯誤會經過分組，因此更容易閱讀及查看是否有新類型的錯誤或問題。

> [!NOTE]
> 前兩個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。

## ATA 部署記錄檔
對於安裝產品的使用者，ATA 部署記錄位於暫存記錄中。 在預設安裝位置中，其位於︰**C:\Users\Administrator\AppData\Local\Temp** (或 %temp% 上方的一個目錄)。

ATA Center 部署記錄檔︰

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - 此記錄檔會列出 ATA 中心的部署程序步驟。 其主要用途是追蹤 ATA 中心部署程序。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - 此記錄檔會列出 ATA 中心上 MongoDB 部署程序的步驟。 其主要用途是追蹤 MongoDB 部署程序。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - 此記錄檔會列出 ATA 中心二進位檔的部署程序步驟。 其主要用途是追蹤 ATA 中心二進位檔的部署。

ATA 閘道和 ATA 輕量型閘道部署記錄：

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - 此記錄檔會列出 ATA 閘道的部署程序步驟。 其主要用途是追蹤 ATA 閘道部署程序。

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - 此記錄檔會列出 ATA 閘道二進位檔的部署程序步驟。 其主要用途是追蹤 ATA 閘道二進位檔的部署。

## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


