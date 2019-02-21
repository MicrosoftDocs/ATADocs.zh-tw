---
title: 下載 Azure ATP 感應器安裝套件快速入門 | Microsoft Docs
description: 安裝 Azure ATP 的步驟三可協助您下載 Azure ATP 感應器安裝套件。
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: get-started-article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 24aab8277d412bf245db3e260412e085f049e082
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263745"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>快速入門：下載 Azure ATP 感應器安裝套件

在此快速入門中，您將會從入口網站下載 Azure ATP 感應器安裝套件。

## <a name="prerequisites"></a>必要條件

- [連線到 Active Directory](install-atp-step2.md) 的 [Azure ATP 執行個體](install-atp-step1.md)。

## <a name="download-the-setup-package"></a>下載安裝套件

設定網域連線設定後，您可以下載 Azure ATP 感應器安裝套件。 Azure ATP 感應器安裝套件可以安裝在專用伺服器或網域控制站上。 當直接安裝在網域控制站上時，其安裝形式為 Azure ATP 感應器；當安裝在專用伺服器上而且使用連接埠鏡像時，其安裝形式則為 Azure ATP 獨立感應器。 如需 Azure ATP 感應器的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。 

按一下頁面頂端步驟清單中的 [下載]，以移至 [感應器] 頁面。

![Azure ATP 感應器的組態設定](media/atp-sensor-config.png)

 若稍後要存取感應器設定畫面，請按一下**設定圖示** (右上角)，選取 [設定]，然後在 [系統] 下，按一下 [感應器]。  

1. 按一下 [感應器]。
2. 將封裝儲存在本機。
3. 複製存取**金鑰**。 Azure ATP 感應器連線到您的 Azure ATP 執行個體需要存取金鑰。 存取金鑰是部署感應器的單次密碼，其後所有的通訊都是使用驗證的憑證和 TLS 加密來執行。 如果需要重新產生新的存取金鑰，您可以使用 [重新產生] 按鈕，而且它不會對先前部署的感應器有任何影響，因為它只會用於感應器的初始註冊。
4. 將套件複製到您要安裝 Azure ATP 感應器的專用伺服器或網域控制站。 或者，您也可以從專用伺服器或網域控制站開啟 Azure ATP 入口網站並跳過此步驟。

ZIP 檔案包含下列檔案：

- Azure ATP 感應器安裝程式

- 包含連線至 Azure ATP 雲端服務所需資訊的組態設定檔

## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 步驟 2 - 連線到 Active Directory](install-atp-step2.md)
> [步驟 4 - 安裝 Azure ATP 感應器 »](install-atp-step4.md)

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
