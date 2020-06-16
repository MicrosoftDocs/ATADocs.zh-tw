---
title: 安裝 Advanced 威脅分析-步驟3
description: 安裝 ATA 的步驟 3 協助您下載 ATA 閘道安裝套件。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2649e5ece9a1613c8c0f396c7fc906219c178046
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775211"
---
# <a name="install-ata---step-3"></a>安裝 ATA - 步驟 3

*適用於：Advanced Threat Analytics 1.9 版*

> [!div class="step-by-step"]
> [« 步驟 2](install-ata-step2.md)
> [步驟 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>步驟 3： 下載 ATA 閘道安裝套件

設定網域連線設定後，您可以下載 ATA 閘道安裝套件。 ATA 閘道可以安裝在專用伺服器或網域控制站上。 如果您將其安裝在網域控制站上，它會作為 ATA 輕量型閘道安裝。 如需 ATA 輕量閘道的詳細資訊，請參閱[Ata 架構](ata-architecture.md)。 

在頁面頂端的步驟清單中，按一下 [**下載閘道設定**]，以移至 [**閘道**] 頁面。

![ATA 閘道組態設定](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> 若要稍後存取 [閘道設定] 畫面，請按一下**設定圖示** (右上角)，選取 [設定]****，然後在 [系統]**** 下，按一下 [閘道]****。  

1.  按一下 [Gateway Setup (閘道安裝)] ****。
  ![下載 ATA 閘道安裝程式](media/download-gateway-setup.png)
2.  將封裝儲存在本機。
3.  將封裝複製到 ATA 閘道安裝所在的專用伺服器或網域控制站。 您也可以從專用伺服器或網域控制站開啟 ATA 主控台，並跳過此步驟。

ZIP 檔案包含下列檔案：

-   ATA 閘道安裝程式

-   包含連線至 ATA 中心所需資訊的組態設定檔


> [!div class="step-by-step"]
> [« 步驟 2](install-ata-step2.md)
> [步驟 4 »](install-ata-step4.md)


## <a name="related-videos"></a>相關影片
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](https://aka.ms/atapoc)
- [ATA 調整大小工具](https://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
