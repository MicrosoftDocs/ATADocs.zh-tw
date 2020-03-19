---
title: 進行 Azure ATP 感應器設定的概念
description: 安裝 Azure ATP 的步驟 5 可協助您設定 Azure ATP 獨立感應器的設定。
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ffa60672b7d649e6a78ac2afa33405328ac40b95
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413684"
---
# <a name="configure-azure-atp-sensor-settings"></a>進行 Azure ATP 感應器設定

在本文中，您將了解如何正確進行 Azure ATP 感應器設定，以開始查看資料。 您需要進行額外的設定及整合，才能利用 Azure ATP 的完整功能。  

## <a name="prerequisites"></a>先決條件

- [連線到 Active Directory](install-atp-step2.md) 的 [Azure ATP 執行個體](install-atp-step1.md)。
- 您 [ATP 感應器安裝套件](install-atp-step3.md)的已下載複本，以及存取金鑰。

## <a name="configure-sensor-settings"></a>進行感應器設定

在安裝 Azure ATP 感應器之後，請執行下列操作來進行 Azure ATP 感應器設定。

1. 按一下 [啟動]  以開啟瀏覽器，然後登入 Azure ATP 入口網站。

1.  在 Azure ATP 入口網站中，移至 [設定]  ，然後選取 [系統]  下方的 [感應器]  。
   
    ![設定感應器設定的影像](media/atp-sensor-config.png)


1. 按一下您想要設定的感應器，然後輸入下列資訊：

   ![設定感應器設定的影像](media/atp-sensor-config-2.png)

   - **描述**：輸入 Azure ATP 感應器的描述 (選擇性)。
   - **網域控制站 (FQDN)** (此為 Azure ATP 獨立感應器的必要項目，Azure ATP 感應器無法變更此項目)：輸入您網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**

     下列資訊適用於您在**網域控制站**清單中輸入的伺服器：
     - 所有透過連接埠鏡像受 Azure ATP 獨立感應器監視流量的網域控制站，都必須列在 [網域控制站]  清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑活動。
     - 清單中應至少有一個網域控制站是通用類別目錄。 這讓 Azure ATP 能夠解析樹系中其他網域的電腦與使用者物件。

   - **擷取網路介面卡** (必填)︰
   
    - 如果為 Azure ATP 感應器，應是用來與組織中其他電腦通訊的所有網路介面卡。
    - 如果為專用伺服器上的 Azure ATP 獨立感應器，請選取設定為目的地鏡像連接埠的網路介面卡。 這些網路介面卡會接收鏡像網域控制站流量。

 
1. 按一下 **[儲存]** 。


## <a name="validate-installations"></a>驗證安裝
若要驗證 Azure ATP 感應器是否已成功部署，請檢查下列項目︰

1. 檢查名稱為 [Azure 進階威脅感應器]  的服務是否正在執行。 儲存 Azure ATP 感應器設定之後，服務可能需要幾秒鐘的時間來啟動。

1. 如果服務未啟動，請檢閱位於以下預設資料夾 "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs" 中的 "Microsoft.Tri.sensor-Errors.log" 檔案。
 
   >[!NOTE]
   > Azure ATP 的版本經常更新，若要檢查是否有最新版本，請在 Azure ATP 入口網站中，移至 [設定]  ，然後移至 [關於]  。 

1. 前往您的 Azure ATP 執行個體 URL。 在 Azure ATP 入口網站的搜尋列中搜尋某個項目，例如網域上的使用者或群組。

1. 使用下列步驟來確認任何網域裝置上的 ATP 連線能力：
    1. 開啟命令提示字元
    1. 輸入 ```nslookup```
    1. 輸入 **server**，然後輸入已安裝 ATP 感應器之網域控制站的 FQDN 或 IP 位址。 例如， ```server contosodc.contoso.azure```
        - 請務必將 contosodc.contoso.azure 和 contoso.azure 分別取代成您 Azure ATP 感應器的 FQDN 和網域。
    1. 輸入 ```ls -d contoso.azure```
    1. 針對您想要測試的每個感應器重複步驟 3 和 4。  
    1. 從 Azure ATP 主控台中，開啟您執行連線能力測試之來源電腦的實體設定檔。 
    1. 檢查相關的邏輯活動並確認連線能力。 

    > [!NOTE] 
    >如果您想要測試的網域控制站是第一個部署的感應器，請至少等候 15 分鐘，以允許資料庫後端完成必要微服務的初始部署，然後再嘗試確認該網域控制站的相關邏輯活動。

## <a name="next-steps"></a>後續步驟

- [Proxy 設定](configure-proxy.md)
- [進階稽核原則](atp-advanced-audit-policy.md)
- [設定 Azure ATP 對 SAM 發出遠端呼叫](install-atp-step8-samr.md)


## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
