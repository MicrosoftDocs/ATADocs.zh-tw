---
title: Azure 進階威脅防護與 Windows Defender ATP 的整合 | Microsoft Docs
description: 如何將 Azure 進階威脅防護與 Windows Defender ATP 整合，以獲得完整的威脅偵測涵蓋範圍
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/18/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: de847403a509617a2c8dc6d8036633ff355f3492
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906535"
---
# <a name="integrate-azure-atp-with-windows-defender-atp"></a>整合 Azure ATP 與 Windows Defender ATP

Azure 進階威脅防護可讓您將 Azure ATP 與 Windows Defender ATP 整合，以獲得更加完整的威脅防護解決方案。 在 Azure ATP 監視您網域控制站上流量的同時，Windows Defender ATP 會監視您的端點，使兩者能一起提供可供您保護環境的單一介面。

藉由將 Windows Defender ATP 整合到 Azure ATP 中，您就可以利用這兩個服務的完整功能並保護您的環境，包括：

- Azure ATP 感應器和獨立感應器：可直接放置在網域控制站，或是從您的網域控制站連接埠鏡像至 ATP，來擷取並剖析多個通訊協定 (例如 Kerberos、DNS、RPC、NTLM 和其他通訊協定) 的網路流量，以進行驗證、授權和資訊收集。 

-   端點行為感應器：這些感應器內嵌於 Windows 10 中，可收集和處理作業系統的行為訊號 (例如處理序、登錄、檔案和網路通訊)，並將此感應器資料傳送至您私人獨立的 Windows Defender ATP 雲端執行個體。

- 雲端安全性分析：利用巨量資料、機器學習和整個 Windows 生態系統的獨特 Microsoft 檢視 (例如 [Microsoft 惡意軟體移除工具](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx))、企業雲端產品 (例如 Office 365) 和線上資產 (例如 Bing 和 SmartScreen URL 評價)，行為訊號會轉譯為針對進階威脅的深入解析、偵測及建議回應。

- 威脅情報：威脅情報由 Microsoft 的獵人及安全性小組所產生，再由合作夥伴所提供的威脅情報所強化，可讓 Windows Defender ATP 識別攻擊者工具、技術和程序，並在於收集的感應器資料中觀察到這些活動時產生警示。

Azure ATP 技術可偵測多種可疑的活動，專注於網路攻擊狙殺鏈的數個階段，包括︰

- 「偵查」階段，此時攻擊者會收集有關環境的建構方式、有哪些不同的資產，以及存在何種實體等資訊。 他們通常會在此著手規劃下一階段的攻擊。

- 橫向移動週期，此時攻擊者會將時間與精力放在在網路內部分散攻擊面。

- 「網域支配 (持續性)」階段，此時攻擊者會擷取資訊，以便使用各種進入點、認證和技術繼續進行攻擊活動。

同時，Windows Defender ATP 會利用 Microsoft 的技術和專業知識來偵測複雜的網路攻擊，提供：

- 以行為為基礎、運用雲端技術的進階攻擊偵測<br></br>尋找順利通過所有其他防禦的攻擊 (入侵後偵測)，針對在端點上嘗試隱藏其活動之已知和未知的敵人，提供可採取動作的相關警示。

- 可供進行鑑識調查及緩解問題的豐富時間表<br></br>透過豐富的電腦時間表，輕鬆地調查任何電腦上的入侵範圍或可疑的行為。 範圍遍布整個網路的檔案、URL 和網路連線清查。 針對任何檔案或 URL 使用深層收集和分析 (「引爆」) 來取得額外的深入解析。

- 內建獨一無二的威脅情報知識庫<br></br>絕佳的威脅視野能結合第一方和第三方情報來源，針對每個威脅情報偵測提供執行者詳細資料和意圖內容。

## <a name="prerequisites"></a>先決條件

若要啟用這項功能，您需要同時有 Azure ATP 和 Windows Defender ATP 的授權。 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>如何將 Azure ATP 與 Windows Defender ATP 整合

1. 在 Azure ATP 入口網站中，開啟 [設定]  。 

    ![Azure ATP 設定功能表](./media/atp-configuration-wd.png)
2. 在 [設定] 清單中，選取 [Windows Defender ATP]  ，然後將整合切換至 [開啟]  。 

    ![啟用 Windows Defender 整合](./media/enable-integration.png)


3. 在 [Windows Defender ATP 入口網站](https://securitycenter.windows.com/preferences/advanced)中，移至 [設定]  ，[進階功能]  ，然後將 [Azure ATP 整合]  設為 [開啟]  。 

    ![Windows Defender ATP 啟用整合](./media/wd-atp-enable.png)

4. 若要檢查整合狀態，請在 Azure ATP 入口網站中，前往 [設定]   > [Windows Defender ATP 整合]  。 您可以查看整合狀態，若發生問題，您將會看到錯誤。 

## <a name="how-it-works"></a>運作方式

當 Azure ATP 和 Windows Defender ATP 完全整合之後，在 Azure ATP 入口網站中的小型設定檔快顯視窗和實體設定檔頁面中，每個存在於 Windows Defender ATP 中的實體都會包含徽章，表示它已與 Windows Defender ATP 整合。 

 ![Windows Defender ATP 警示](./media/profile-alerts-wd.png)

如果實體包含 Windows Defender ATP 中的警示，則徽章旁會顯示數字，讓您知道發生多少警示。

 ![Azure ATP 警示](./media/atp-integrated-wd-icon-alerts.png)

如果您按一下徽章，系統就會將您帶回到 Windows Defender ATP 入口網站，您可在其中檢視並解決警示。 如果 Windows Defender ATP 無法辨識實體，則徽章會呈現灰色。 

 ![Windows Defender ATP 呈現灰色](./media/wd-grey.png)

從 Windows Defender ATP 入口網站，按一下端點以檢視 Azure ATP 警示。 如果您在 Windows Defender ATP 中按一下此實體的警示，該實體的設定檔頁面會在 Azure ATP 中開啟。 
 
 > [!NOTE]
 > 目前，Azure ATP 與 Windows Defender ATP 的整合僅支援來自內部部署 AD 的使用者與電腦。 來自 Azure AD 以及在 Azure 中管理之虛擬機器的使用者不會在整合中出現 

![Windows Defender ATP 警示](./media/wd-atp-alerts.png)


## <a name="see-also"></a>另請參閱

- [使用 Azure ATP 調查橫向移動路徑](use-case-lateral-movement-path.md)
- [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 架構](atp-architecture.md)
- [安裝 ATP](install-atp-step1.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)

