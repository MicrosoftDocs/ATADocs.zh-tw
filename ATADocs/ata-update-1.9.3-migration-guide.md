---
title: 1.9.3 遷移指南的 Advanced 威脅分析更新
description: 將 ATA 更新至版本1.9.3 的程式
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/14/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 0148d8b37e116f1b2574fbedacfce6d02e0b88f2
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690817"
---
# <a name="ata-version-193"></a>ATA 版本1.9。3

我們很高興宣佈推出 Microsoft Advanced 威脅分析 1.9 Update 3。

本文說明 Microsoft Advanced 威脅分析 (ATA) 1.9 版的 Update 3 中已修正的問題。 此更新的組建編號為1.9.7576。

## <a name="improvements-included-in-this-update"></a>此更新包含的改善

- 已將 MongoDB 升級至版本3.6.18，以改善支援能力和安全性更新。
- 已將啟動程式和 jQuery npm 封裝升級至版本3.4.1，以取得安全性更新。
- 改進入口網站協助工具功能。
- 在過去三周) 之前，將中央憑證到期的提前通知提前三個月後到期 (。 此外，此通知現在提供更新憑證失敗嚴重性的清楚描述。
- 改進在測試目錄服務連線時，認證驗證錯誤所提供的詳細資料。
- 如果有效能計數器相關問題，則錯誤記錄檔現在會包含更詳細的資訊。
- 部署記錄現在包含有關閘道部署期間連線問題的詳細資訊。
- 一般效能改進。

## <a name="fixed-issues-included-in-this-update"></a>此更新包含的問題修正

- 修正某些部署未正確設定安全性記錄許可權的問題。
- 修正某些語言缺少某些翻譯的問題。
- 修正當您流覽帳戶設定檔頁面面時，可能會出現錯誤訊息的問題。
- 修正一些協助工具功能無法正常運作的問題。

## <a name="how-to-get-this-update"></a>如何取得此更新

您可以從 Microsoft Update 或手動下載，取得 Microsoft ATA 的更新。

### <a name="microsoft-update"></a>Microsoft Update

此更新於 Microsoft Update 提供。 如需如何使用 Microsoft Update 的詳細資訊，請參閱[如何透過 Windows Update 取得更新](https://support.microsoft.com/help/3067639)。

### <a name="microsoft-download-center"></a>Microsoft 下載中心

若要取得此更新的獨立套件，請移至 Microsoft 下載中心網站： [立即下載 ATA 1.9.3 套件](https://www.microsoft.com/download/details.aspx?id=56725)。

### <a name="prerequisites"></a>先決條件

若要安裝此更新，您必須已安裝下列其中一個 ATA 版本：

- 適用于 ATA 1.9 (版本 1.9.7478) 的 Update 2
- 適用于 ATA 1.9 (版本 1.9.7475) 的 Update 2
- 適用於 ATA 1.9 的更新 1 (1.9.7412 版)
- ATA 1.9 (1.9.7312 版)
- 適用於 ATA 1.8 的更新 1 (1.8.6765 版)
- ATA 1.8 (1.8.6645 版)

### <a name="restart-requirement"></a>重新啟動需求

套用此更新後，您的電腦可能需要重新啟動。

### <a name="update-replacement-information"></a>更新取代資訊

此更新取代 ATA 1.9 (版本 1.9.7478) 的 Update 2。

## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA 版本](ata-versions.md)
