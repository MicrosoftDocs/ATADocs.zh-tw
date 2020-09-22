---
title: 使用記錄進行 Azure 進階威脅防護疑難排解
description: 描述如何使用 Azure ATP 記錄檔對問題進行疑難排解
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/05/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 7839a19cef4543685c548dc3c1f386d46384d214
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912325"
---
# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>使用 ATP 記錄疑難排解 Azure 進階威脅防護 (ATP) 感應器的問題

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

ATP 記錄提供每個 Azure ATP 感應器元件在指定時點所執行之動作的見解。

Azure ATP 記錄位於名為 **Logs** 的子資料夾中，而其也正是 ATP 的安裝位置所在。預設的位置是：**C:\Program Files\Azure Advanced Threat Protection Sensor\\**。 在預設的安裝位置中，此記錄位於 **C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs** 下。

Azure ATP 感應器的記錄包括：

- **Microsoft.Tri.Sensor.log** - 此記錄包含 Azure ATP 感應器中所發生的一切 (包括解決方法與錯誤)。 其主要用途是按發生時間順序，取得所有作業的整體狀態。

- **Microsoft.Tri.Center-Errors.log** - 此記錄檔只包含 ATP 感應器攔截到的錯誤。 其主要用途是執行健康情況檢查，並調查需要與特定時間相互關聯的問題。

- **Microsoft.Tri.Gateway.Updater.log** - 感應器更新程式程序會使用此記錄更新 ATP 感應器 (如有設定為自動執行此作業時)。

> [!NOTE]
> 前三個記錄檔有大小上限 50 MB。 到達該大小時，會開啟新的記錄檔，並將上一個記錄檔重新命名為「&lt;原始檔案名稱&gt;-Archived-00000」，該數字隨每次重新命名遞增。 根據預設，如果已經有超過 10 個相同類型的檔案，就會刪除最舊的檔案。

## <a name="azure-atp-deployment-logs"></a>Azure ATP 部署記錄

對於安裝產品的使用者，Azure ATP 部署記錄位於暫存記錄中。 在預設安裝位置中，可以找到： **C:\Users\Administrator\AppData\Local\Temp** (或超過% Temp% ) 的一個目錄。

Azure ATP 感應器部署記錄：

- **Azure 進階威脅防護 Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - 此記錄檔提供感應器部署的整個程序，可以在先前所述的暫存資料夾中找到，也可以在 C:\Windows\Temp 中找到。

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** - 此記錄會列出 Azure ATP 感應器部署程序的步驟。 其主要用途在追蹤 Azure ATP 感應器部署程序。

- **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** - 此記錄檔會列出 Azure ATP 感應器二進位檔部署程序的步驟。 其主要用途在追蹤 Azure ATP 感應器二進位檔的部署。

> [!NOTE]
> 除了此處提及的部署記錄之外，其他開頭為 "Azure Advanced Threat Protection" 的記錄也可提供部署程序的其他資訊。

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](prerequisites.md)
- [Azure ATP 容量規劃](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)