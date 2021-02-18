---
title: 安裝適用於身分識別的 Microsoft Defender 感應器快速入門
description: 安裝適用於身分識別的 Microsoft Defender 的步驟四可協助您安裝適用於身分識別的 Defender 感應器。
ms.date: 02/17/2021
ms.topic: quickstart
ms.openlocfilehash: a9837c36dcdb90dba124eda5f8d6b9f082787d74
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097399"
---
# <a name="quickstart-install-the-microsoft-defender-for-identity-sensor"></a>快速入門：安裝適用于身分識別感應器的 Microsoft Defender

在此快速入門中，您將會在網域控制站上安裝[!INCLUDE [Product long](includes/product-long.md)] 感應器。 若您想要使用無訊息安裝，請參閱[無訊息安裝](silent-installation.md)一文。

## <a name="prerequisites"></a>先決條件

- 已[連線到 Active Directory](install-step2.md) 的[[!INCLUDE [Product short](includes/product-short.md)] 執行個體](install-step1.md)。
- 您[[!INCLUDE [Product short](includes/product-short.md)] 感應器安裝套件](install-step3.md)的已下載複本，以及存取金鑰。
- 請確定電腦上已安裝 Microsoft .Net Framework 4.7 或更新版本。 若未安裝 Microsoft .Net Framework 4.7 或更新版本，[!INCLUDE [Product short](includes/product-short.md)] 感應器安裝套件會加以安裝，這可能需要將伺服器重新開機。
- 針對 AD FS 伺服器上的感應器安裝，如果您使用外部 SQL server，請將 SQL server 設定為允許 *目錄服務***帳戶 (設定**  >  **目錄服務** 使用者  >  **名稱**) *連接*、*登入*、*讀取* 和 *選取* **AdfsConfiguration** 資料庫的許可權。

## <a name="install-the-sensor"></a>安裝感應器

在網域控制站上執行下列步驟。

1. 確認電腦已連線到相關的[ [!INCLUDE [Product short](includes/product-short.md)] 雲端服務](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server)端點 (s) 。
1. 將安裝檔案從 zip 檔案解壓縮。 從 ZIP 檔案直接安裝將會失敗。
1. 以提升的權限 ( **[以系統管理員身分執行]** ) 執行 **Azure ATP sensor setup.exe**，並依照安裝程式精靈的指示執行。
1. 在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

    ![[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器安裝語言](media/sensor-install-language.png)

1. 安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 若是網域控制站，會安裝[!INCLUDE [Product short](includes/product-short.md)] 感應器。 若是專用伺服器，則會安裝[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器。

    例如，針對[!INCLUDE [Product short](includes/product-short.md)] 感應器，會顯示下列畫面，讓您知道您的專用伺服器上已安裝[!INCLUDE [Product short](includes/product-short.md)] 感應器：

    ![[!INCLUDE [Product short](includes/product-short.md)] 感應器安裝](media/sensor-install-deployment-type.png)

    按一下 [下一步] 。

    > [!NOTE]
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，就會發出警告。 此警告不會妨礙您按一下 [下一步] 及繼續安裝。 若在只需較少資料儲存空間的小型實驗室測試環境中安裝[!INCLUDE [Product short](includes/product-short.md)]，這仍是可行的做法。 如果是生產環境，強烈建議使用[!INCLUDE [Product short](includes/product-short.md)] 的[容量規劃](capacity-planning.md)指南，確保您的網域控制站或專用伺服器符合必要需求。

1. 在 [設定感應器] 下，輸入從上一個步驟複製的安裝路徑和存取金鑰 (視您的環境而定)：

    ![[!INCLUDE [Product short](includes/product-short.md)] 感應器設定影像](media/sensor-install-config.png)

    - 安裝路徑：安裝[!INCLUDE [Product short](includes/product-short.md)] 感應器的位置。 根據預設，此路徑為 %programfiles%\Azure Advanced Threat Protection sensor。 保留預設值。
    - 存取金鑰：從上一個步驟中的[!INCLUDE [Product short](includes/product-short.md)] 入口網站擷取。

1. 按一下 [Install] 。 安裝[!INCLUDE [Product short](includes/product-short.md)] 感應器時將安裝及設定下列元件︰

    - KB 3047154 (僅適用於 Windows Server 2012 R2)

        > [!IMPORTANT]
        >
        > - 請勿將 KB 3047154 安裝於虛擬主機 (執行虛擬化的主機；可在虛擬機器上執行)。 這可能會導致連接埠鏡像無法正常運作。
        > - 如果[!INCLUDE [Product short](includes/product-short.md)] 感應器電腦上已安裝 Wireshark，在執行 Wireshark 之後，您將需要重新啟動[!INCLUDE [Product short](includes/product-short.md)] 感應器，因為其使用相同的驅動程式。

    - [!INCLUDE [Product short](includes/product-short.md)] 感應器服務與[!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務
    - Microsoft Visual C++ 2013 可轉散發元件

## <a name="post-installation-steps-for-ad-fs-servers"></a>AD FS 伺服器的後續安裝步驟

當您完成 AD FS 伺服器上的感應器安裝之後，請使用下列步驟來設定 Defender 的身分識別。

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中， 選取 [設定]

1. 在 [ **系統**] 底下，選取 [ **感應器**]。

    ![[!包含 [Product short] (include/product-short. md) ] 感應器設定頁面](media/sensor-config.png)

1. 選取您安裝在 AD FS 伺服器上的感應器。
1. 在快顯視窗的 [ **解析程式網域控制站** ] 欄位中，輸入解析程式網域控制站的 FQDN，然後按一下加號圖示 **(+)**]，再按一下 [ **儲存**]。  

    ![[!包含 [Product short] (include/product-short. md) ] 設定 AD FS 感應器解析程式](media/sensor-config-adfs-resolver.png)

    將感應器初始化可能需要幾分鐘的時間，此時 AD FS 感應器服務狀態應該會從 [ **已停止** ] 變更為 [ **正在** 執行]。

## <a name="next-steps"></a>後續步驟

[!INCLUDE [Product short](includes/product-short.md)] 感應器的設計是讓對您網域控制站資源與網路活動的影響減到最小。 若要建立效能評定，請參閱[[!INCLUDE [Product short](includes/product-short.md)] 的方案容量](capacity-planning.md)。

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://aka.ms/MDIcommunity) \(英文\)！
