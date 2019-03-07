---
title: 安裝 Azure ATP 感應器快速入門 |Microsoft Docs
description: 安裝 Azure ATP 的步驟四可協助您安裝 Azure ATP 感應器。
author: mlottner
ms.author: mlottner
ms.date: 03/03/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 99045c4d8982c34d3defa681417a3b3963c563ac
ms.sourcegitcommit: 929f28783110c7e114ab36d4cccd50563f4030df
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/04/2019
ms.locfileid: "57253924"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>快速入門：安裝 Azure ATP 感應器

在此快速入門中，您會在網域控制站上安裝 Azure ATP 感應器。 若您想要使用無訊息安裝，請參閱[無訊息安裝](atp-silent-installation.md)一文。

## <a name="prerequisites"></a>必要條件

- [連線到 Active Directory](install-atp-step2.md) 的 [Azure ATP 執行個體](install-atp-step1.md)。
- 您 [ATP 感應器安裝套件](install-atp-step3.md)的已下載複本，以及存取金鑰。
- 請確定電腦上已安裝 Microsoft .Net Framework 4.7。 如果未安裝 .Net Framework 4.7，Azure ATP 感應器安裝套件會予以安裝，這可能需要將伺服器重新開機。

## <a name="install-the-sensor"></a>安裝感應器

在網域控制站上執行下列步驟。

1. 確認機器是否可以連線到相關的 Azure ATP 雲端服務端點：
   - 歐洲
      - [https://triprd1wceuw1sensorapi.atp.azure.com](https://triprd1wceuw1sensorapi.atp.azure.com) 
      - [https://triprd1wceun1sensorapi.atp.azure.com](https://triprd1wceun1sensorapi.atp.azure.com)
   - 美國 
      - [https://triprd1wcuse1sensorapi.atp.azure.com](https://triprd1wcuse1sensorapi.atp.azure.com)
      - [https://triprd1wcusw1sensorapi.atp.azure.com](https://triprd1wcusw1sensorapi.atp.azure.com)
      - [https://triprd1wcuswb1sensorapi.atp.azure.com](https://triprd1wcuswb1sensorapi.atp.azure.com)
   - 亞洲
      - [https://triprd1wcasse1sensorapi.atp.azure.com](https://triprd1wcasse1sensorapi.atp.azure.com)

2. 將安裝檔案從 zip 檔案解壓縮。 從 ZIP 檔案直接安裝將會失敗。

3. 執行 **Azure ATP sensor setup.exe** 並按照安裝精靈的指示操作。

4. 在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

    ![Azure ATP 獨立感應器安裝語言](media/sensor-install-language.png)


5. 安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 若是網域控制站，會安裝 Azure ATP 感應器。 若是專用伺服器，則會安裝 Azure ATP 獨立感應器。
    
    例如，針對 Azure ATP 感應器，會顯示下列畫面，讓您知道您的專用伺服器上已安裝 Azure ATP 感應器：
    
    ![Azure ATP 感應器安裝](media/sensor-install-deployment-type.png)

   按一下 [下一步] 。

    > [!NOTE] 
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，就會發出警告。 該警告並不會使您無法按一下 [下一步] 和繼續進行安裝。 在不需要這麼多資料儲存空間的小型實驗室測試環境中，這可能仍是安裝 Azure ATP 的最佳選擇。 針對生產環境，強烈建議使用 Azure ATP 的 [容量規劃](atp-capacity-planning.md)指南，確保您的網域控制站或專用伺服器符合必要需求。

6. 在 [設定感應器] 下，輸入從上一個步驟複製的安裝路徑和存取金鑰 (視您的環境而定)：

    ![Azure ATP 感應器設定影像](media/sensor-install-config.png)

      - 安裝路徑：安裝 Azure ATP 感應器的位置。 根據預設，此路徑為 %programfiles%\Azure Advanced Threat Protection sensor。 保留預設值。

     - 存取金鑰：從上一個步驟中的 Azure ATP 入口網站擷取。
    
7. 按一下 [安裝]。 安裝 Azure ATP 感應器期間將安裝及設定下列元件︰

    - KB 3047154 (僅適用於 Windows Server 2012 R2)

        > [!IMPORTANT]
        > - 請勿將 KB 3047154 安裝於虛擬主機 (執行虛擬化的主機；可在虛擬機器上執行)。 這可能會導致連接埠鏡像無法正常運作。 
        > - 如果 ATP 感應器電腦上已安裝 Wireshark，您將需要重新啟動 ATP 感應器，因為它使用相同的驅動程式。

    - Azure ATP 感應器服務和 Azure ATP 感應器更新程式服務
    - Microsoft Visual C++ 2013 可轉散發元件


## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 步驟 3 - 下載感應器安裝程式](install-atp-step3.md)
> [步驟 5 - 進行感應器設定 »](install-atp-step5.md)

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
