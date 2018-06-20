---
title: 安裝 Azure 進階威脅防護 - 步驟 3 | Microsoft Docs
description: 安裝 Azure ATP 的步驟三協助您下載 Azure ATP 獨立感應器安裝套件。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: aa07d6ce4418c051362652e70968a8e41313affb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444934"
---
適用於：Azure 進階威脅防護



# <a name="install-azure-atp---step-3"></a>安裝 Azure ATP - 步驟 3

>[!div class="step-by-step"]
[« 步驟 2](install-atp-step2.md)
[步驟 4 »](install-atp-step4.md)

## <a name="step-3-download-the-azure-atp-sensor-setup-package"></a>步驟 3： 下載 Azure ATP 感應器安裝套件
設定網域連線設定後，您可以下載 Azure ATP 感應器安裝套件。 Azure ATP 感應器安裝套件可以安裝在專用伺服器或網域控制站上。 當直接安裝在網域控制站上時，它會安裝為 Azure ATP 感應器，當安裝在專用的伺服器上且使用連接埠鏡像時，則會安裝為 Azure ATP 獨立感應器。 如需 Azure ATP 感應器的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。 

按一下頁面頂端步驟清單中的 [下載]，以移至 [感應器] 頁面。

![Azure ATP 感應器的組態設定](media/atp-sensor-config.png)

> [!NOTE] 
> 若稍後要存取感應器設定畫面，請按一下**設定圖示** (右上角) 並選取 [設定]，然後在 [系統] 下，按一下 [感應器]。  

1.  按一下 [感應器]。
2.  將封裝儲存在本機。
3.  複製 [存取金鑰]。 Azure ATP 感應器連線到您的 Azure ATP 工作區需要存取金鑰。 存取金鑰是部署感應器的單次密碼，其後所有的通訊都是使用驗證的憑證和 TLS 加密來執行。 如果需要重新產生新的存取金鑰，您可以使用 [重新產生] 按鈕，且它不會對先前部署的感應器有任何影響，因為它只用於感應器的初始註冊。
4.  將套件複製到您要安裝 Azure ATP 感應器的專用伺服器或網域控制站。 您也可以從專用伺服器或網域控制站開啟 Azure ATP 工作區入口網站，並跳過此步驟。

ZIP 檔案包含下列檔案：

-   Azure ATP 感應器安裝程式

-   包含連線至 Azure ATP 雲端服務所需資訊的組態設定檔


>[!div class="step-by-step"]
[« 步驟 2](install-atp-step2.md)
[步驟 4 »](install-atp-step4.md)


## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)

- [設定事件收集](configure-event-collection.md)

- [Azure ATP 必要條件](atp-prerequisites.md)

- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)