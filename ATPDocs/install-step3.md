---
title: 快速入門：下載適用於身分識別的 Microsoft Defender 感應器安裝套件
description: 在安裝適用於身分識別的 Microsoft Defender 中，其步驟 3 可協助您下載適用於身分識別的 Defender 感應器安裝套件。
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: f0eb884a7367ae50e076e0298f720a94def7da8c
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543122"
---
# <a name="quickstart-download-the-product-long-sensor-setup-package"></a>快速入門：下載 [!INCLUDE [Product long](includes/product-long.md)] 感應器安裝套件

在此快速入門中，您將會從入口網站下載 [!INCLUDE [Product long](includes/product-long.md)] 感應器安裝套件。

## <a name="prerequisites"></a>先決條件

- [連線到 Active Directory](install-step2.md) 的 [[!INCLUDE [Product short](includes/product-short.md)] 執行個體](install-step1.md)。

## <a name="download-the-setup-package"></a>下載安裝套件

設定網域連線設定後，您即可下載 [!INCLUDE [Product short](includes/product-short.md)] 感應器安裝套件。 如需 [!INCLUDE [Product short](includes/product-short.md)] 感應器的詳細資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)。

按一下頁面頂端步驟清單中的 [下載]，以移至 [感應器] 頁面。

![[!INCLUDE [Product short](includes/product-short.md)] 感應器組態設定](media/sensor-config.png)

若稍後要前往 [感應器設定] 畫面，請選取 [設定]，然後在 [系統] 底下，按一下 [感應器]。  

1. 按一下 [下載] 將套件儲存在本機。
1. 複製 **存取** **金鑰**。 [!INCLUDE [Product short](includes/product-short.md)] 感應器連線到 [!INCLUDE [Product short](includes/product-short.md)] 執行個體需要存取金鑰。 存取金鑰是部署感應器的單次密碼，其後所有的通訊都是使用驗證的憑證和 TLS 加密來執行。 如果需要重新產生新的存取金鑰，您可以使用 [重新產生] 按鈕，而且它不會對先前部署的感應器有任何影響，因為它只會用於感應器的初始註冊。
1. 將套件複製到您要安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器的專用伺服器或網域控制站。 或者，您也可以從專用伺服器或網域控制站開啟 [!INCLUDE [Product short](includes/product-short.md)] 入口網站並跳過此步驟。

ZIP 檔案包含下列檔案：

- [!INCLUDE [Product short](includes/product-short.md)] 感應器安裝程式

- 包含連線至 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務所需資訊的組態設定檔

## <a name="next-steps"></a>下一步

> [!div class="step-by-step"]
> [« 步驟 2 - 連線到 Active Directory](install-step2.md)
> [步驟 4 - 安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器 »](install-step4.md)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://aka.ms/MDIcommunity) \(英文\)！
