---
title: 設定 Microsoft Defender 的身分識別感應器設定概念
description: 安裝適用于身分識別的 Microsoft Defender 的步驟5可協助您針對身分識別獨立感應器設定 Defender 的設定。
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27431aca85e794ecd31029b6286e3146f01fa7ec
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848494"
---
# <a name="configure-product-long-sensor-settings"></a>設定 [!INCLUDE [Product long](includes/product-long.md)] 感應器設定

在本文中，您將瞭解如何正確地設定 [!INCLUDE [Product long](includes/product-long.md)] 感應器設定，以開始查看資料。 您必須執行額外的設定和整合，才能利用的 [!INCLUDE [Product short](includes/product-short.md)] 完整功能。

## <a name="prerequisites"></a>先決條件

- 已[連線到 Active Directory](install-step2.md) 的[[!INCLUDE [Product short](includes/product-short.md)] 執行個體](install-step1.md)。
- 您[](install-step3.md) 感應器安裝套件[!INCLUDE [Product short](includes/product-short.md)]的已下載複本，以及存取金鑰。

## <a name="configure-sensor-settings"></a>進行感應器設定

[!INCLUDE [Product short](includes/product-short.md)]安裝感應器之後，請執行下列動作來設定 [!INCLUDE [Product short](includes/product-short.md)] 感應器設定。

1. 按一下 [ **啟動** ] 以開啟瀏覽器並登入 [!INCLUDE [Product short](includes/product-short.md)] 入口網站。

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，移 **Configuration** 至 [設定]，然後在 [**系統**] 底下選取 [**感應器**]。

    ![[感應器] 頁面](media/sensor-config.png)

1. 按一下您想要設定的感應器，然後輸入下列資訊：

    ![進行感應器設定](media/sensor-config-2.png)

    - **描述**：輸入感應器的描述 [!INCLUDE [Product short](includes/product-short.md)] (選擇性) 。
    - **網域控制站 (FQDN)** 獨立感應器所需的 ([!INCLUDE [Product short](includes/product-short.md)] ，無法變更 [!INCLUDE [Product short](includes/product-short.md)] 感應器) ：輸入網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**

    下列資訊適用於您在 **網域控制站** 清單中輸入的伺服器：
    - 所有透過獨立感應器透過埠鏡像監視流量的網域控制站 [!INCLUDE [Product short](includes/product-short.md)] ，都必須列在 [ **網域控制站** ] 清單中。 如果網域控制站未列在 **網域控制站** 清單中，可能無法如預期般偵測可疑活動。
    - 清單中應至少有一個網域控制站是通用類別目錄。 這可讓您 [!INCLUDE [Product short](includes/product-short.md)] 解析樹系中其他網域的電腦與使用者物件。

    - **擷取網路介面卡** (必填)︰

    - 針對 [!INCLUDE [Product short](includes/product-short.md)] 感應器，則是用來與組織中其他電腦通訊的所有網路介面卡。
    - 針對 [!INCLUDE [Product short](includes/product-short.md)] 專用伺服器上的獨立感應器，請選取設定為目的地鏡像埠的網路介面卡。 這些網路介面卡會接收鏡像網域控制站流量。

1. 按一下 **[儲存]** 。

## <a name="validate-installations"></a>驗證安裝

若要驗證 [!INCLUDE [Product short](includes/product-short.md)] 感應器是否已成功部署，請檢查下列各項：

1. 檢查名稱為 [Azure 進階威脅感應器]  的服務是否正在執行。 儲存 [!INCLUDE [Product short](includes/product-short.md)] 感應器設定之後，可能需要幾秒鐘的時間才會啟動服務。

1. 如果服務未啟動，請檢閱位於下列預設資料夾 "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs" 中的 "Microsoft.Tri.sensor-Errors.log" 檔案。

    >[!NOTE]
    > 經常更新的版本， [!INCLUDE [Product short](includes/product-short.md)] 若要檢查最新版本，請在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，移至 [設定 **]，** 然後 [ **關於**]。

1. 移至您的 [!INCLUDE [Product short](includes/product-short.md)] 實例 URL。 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，搜尋搜尋列中的某個內容，例如網域上的使用者或群組。

1. [!INCLUDE [Product short](includes/product-short.md)]使用下列步驟來確認任何網域裝置上的連線能力：
    1. 開啟命令提示字元
    1. 輸入 `nslookup`
    1. 輸入 **伺服器** ，然後輸入安裝感應器之網域控制站的 FQDN 或 IP 位址 [!INCLUDE [Product short](includes/product-short.md)] 。 例如， `server contosodc.contoso.azure`
        - 請務必將 contosodc 取代為您的感應器和功能變數名稱的 FQDN，以分別取代為 azure 和 contoso。 [!INCLUDE [Product short](includes/product-short.md)]
    1. 輸入 `ls -d contoso.azure`
    1. 針對您想要測試的每個感應器重複步驟 3 和 4。
    1. 從 [!INCLUDE [Product short](includes/product-short.md)] 主控台開啟您執行連線能力測試的電腦的實體設定檔。
    1. 檢查相關的邏輯活動並確認連線能力。

    > [!NOTE]
    >如果您想要測試的網域控制站是第一個部署的感應器，請至少等候 15 分鐘，以允許資料庫後端完成必要微服務的初始部署，然後再嘗試確認該網域控制站的相關邏輯活動。

## <a name="next-steps"></a>後續步驟

- [Proxy 設定](configure-proxy.md)
- [進階稽核原則](configure-windows-event-collection.md)
- [設定[!INCLUDE [Product short](includes/product-short.md)] 以對 SAM 發出遠端呼叫](install-step8-samr.md)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://aka.ms/MDIcommunity) \(英文\)！
