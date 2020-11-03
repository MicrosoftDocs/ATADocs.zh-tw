---
title: 使用記錄針對 Microsoft Defender 進行身分識別進行疑難排解
description: 說明如何使用 Microsoft Defender 進行身分識別記錄來針對問題進行疑難排解
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: ea19abd7497d0d925e764a80666dc595862566f9
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274996"
---
# <a name="troubleshooting-product-long-sensor-using-the-product-short-logs"></a>[!INCLUDE [Product long](includes/product-long.md)]使用記錄針對感應器進行疑難排解 [!INCLUDE [Product short](includes/product-short.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

這些 [!INCLUDE [Product short](includes/product-short.md)] 記錄可讓您深入瞭解每個 [!INCLUDE [Product long](includes/product-long.md)] 感應器元件在任何指定時間點的執行狀況。

[!INCLUDE [Product short](includes/product-short.md)]記錄檔位於已安裝之 **記錄** 檔的子資料夾中， [!INCLUDE [Product short](includes/product-short.md)] 預設位置為： **C:\Program Files\Azure Advanced 威脅防護感應器 \\** 。 在預設的安裝位置中，此記錄位於 **C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs** 下。

[!INCLUDE [Product short](includes/product-short.md)]感應器具有下列記錄：

- **：此** 記錄檔包含感應器中發生的所有內容 [!INCLUDE [Product short](includes/product-short.md)] (包括) 的解決方式和錯誤。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

- **Microsoft.tri.sensor-errors.log** –此記錄只包含感應器攔截到的錯誤， [!INCLUDE [Product short](includes/product-short.md)] 。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

- ：此記錄檔可用於感應器 **更新程式進程** ， [!INCLUDE [Product short](includes/product-short.md)] 如果設定為自動進行，則負責更新感應器的程式。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。 根據預設，如果已經有超過 10 個相同類型的檔案，就會刪除最舊的檔案。

## <a name="product-short-deployment-logs"></a>[!INCLUDE [Product short](includes/product-short.md)] 部署記錄檔

[!INCLUDE [Product short](includes/product-short.md)]部署記錄檔位於安裝產品之使用者的 temp 目錄中。 在預設安裝位置中，可以找到： **C:\Users\Administrator\AppData\Local\Temp** (或超過% Temp% ) 的一個目錄。

[!INCLUDE [Product short](includes/product-short.md)] 感應器部署記錄：

- **Azure 進階威脅防護 Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - 此記錄檔提供感應器部署的整個程序，可以在先前所述的暫存資料夾中找到，也可以在 C:\Windows\Temp 中找到。

- **Azure 進階威脅防護 Sensor_YYYYMMDDHHMMSS 記錄** 檔-此記錄檔會列出部署感應器的過程中的步驟 [!INCLUDE [Product short](includes/product-short.md)] 。 它的主要用途是追蹤 [!INCLUDE [Product short](includes/product-short.md)] 感應器部署流程。

- **Azure 進階威脅防護 Sensor_YYYYMMDDHHMMSS_001_MsiPackage .log** ：此記錄檔會列出部署感應器二進位檔的程式中的步驟 [!INCLUDE [Product short](includes/product-short.md)] 。 其主要用途是追蹤感應器二進位檔的部署 [!INCLUDE [Product short](includes/product-short.md)] 。

> [!NOTE]
> 除了此處提及的部署記錄之外，其他開頭為 "Azure Advanced Threat Protection" 的記錄也可提供部署程序的其他資訊。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規劃](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 [!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)
