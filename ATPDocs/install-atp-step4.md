---
title: 安裝 Azure ATP 感應器快速入門
description: 安裝 Azure ATP 的步驟四可協助您安裝 Azure ATP 感應器。
author: shsagir
ms.author: shsagir
ms.date: 07/29/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a6861b96143d1baafb315f276a278ff0b98f795f
ms.sourcegitcommit: 3cddeab2d22385a0efe8f95a196576de30c9a60d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87379863"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>快速入門：安裝 Azure ATP 感應器

在此快速入門中，您會在網域控制站上安裝 Azure ATP 感應器。 若您想要使用無訊息安裝，請參閱[無訊息安裝](atp-silent-installation.md)一文。

## <a name="prerequisites"></a>先決條件

- [連線到 Active Directory](install-atp-step2.md) 的 [Azure ATP 執行個體](install-atp-step1.md)。
- 您 [ATP 感應器安裝套件](install-atp-step3.md)的已下載複本，以及存取金鑰。
- 請確定電腦上已安裝 Microsoft .Net Framework 4.7 或更新版本。 若未安裝 Microsoft .Net Framework 4.7 或更新版本，Azure ATP 感應器安裝套件會予以安裝，這可能需要重新啟動伺服器。

## <a name="install-the-sensor"></a>安裝感應器

在網域控制站上執行下列步驟。

1. 確認機器是否可以連線到相關的 [Azure ATP 雲端服務](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server)端點：
1. 將安裝檔案從 zip 檔案解壓縮。 從 ZIP 檔案直接安裝將會失敗。
1. 執行 **Azure ATP sensor setup.exe** 並按照安裝精靈的指示操作。
1. 在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

    ![Azure ATP 獨立感應器安裝語言](media/sensor-install-language.png)

1. 安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 若是網域控制站，會安裝 Azure ATP 感應器。 若是專用伺服器，則會安裝 Azure ATP 獨立感應器。

    例如，針對 Azure ATP 感應器，會顯示下列畫面，讓您知道您的專用伺服器上已安裝 Azure ATP 感應器：

    ![Azure ATP 感應器安裝](media/sensor-install-deployment-type.png)

    按一下 [下一步] 。

    > [!NOTE]
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，就會發出警告。 此警告不會妨礙您按一下 [下一步] 及繼續安裝。 若在只需較少資料儲存空間的小型實驗室測試環境中安裝 Azure ATP，這仍是可行的做法。 針對生產環境，強烈建議使用 Azure ATP 的 [容量規劃](atp-capacity-planning.md)指南，確保您的網域控制站或專用伺服器符合必要需求。

1. 在 [設定感應器] 下，輸入從上一個步驟複製的安裝路徑和存取金鑰 (視您的環境而定)：

    ![Azure ATP 感應器設定影像](media/sensor-install-config.png)

    - 安裝路徑：安裝 Azure ATP 感應器的位置。 根據預設，此路徑為 %programfiles%\Azure Advanced Threat Protection sensor。 保留預設值。
    - 存取金鑰：從上一個步驟中的 Azure ATP 入口網站擷取。

1. 按一下 [安裝] 。 安裝 Azure ATP 感應器期間將安裝及設定下列元件︰

    - KB 3047154 (僅適用於 Windows Server 2012 R2)

        > [!IMPORTANT]
        >
        > - 請勿將 KB 3047154 安裝於虛擬主機 (執行虛擬化的主機；可在虛擬機器上執行)。 這可能會導致連接埠鏡像無法正常運作。
        > - 如果 ATP 感應器電腦上已安裝 Wireshark，您將需要重新啟動 ATP 感應器，因為它使用相同的驅動程式。

    - Azure ATP 感應器服務和 Azure ATP 感應器更新程式服務
    - Microsoft Visual C++ 2013 可轉散發元件

## <a name="next-steps"></a>後續步驟

Azure ATP 感應器的設計是讓對您網域控制站資源和網路活動的影響減到最小。 若要建立效能評定，請參閱 [Azure ATP 解決方案的方案容量](atp-capacity-planning.md)。

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
