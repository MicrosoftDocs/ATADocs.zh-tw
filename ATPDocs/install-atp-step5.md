---
title: 進行 Azure ATP 感應器設定快速入門 |Microsoft Docs
description: 安裝 Azure ATP 的步驟 5 可協助您設定 Azure ATP 獨立感應器的設定。
author: mlottner
ms.author: mlottner
ms.date: 03/03/2018
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9b51c781cee16d4f158cc0e0528d4f80683aabad
ms.sourcegitcommit: 929f28783110c7e114ab36d4cccd50563f4030df
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/04/2019
ms.locfileid: "57253941"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>快速入門：進行 Azure ATP 感應器設定

在此快速入門中，您將會進行 Azure ATP 感應器設定，以開始查看資料。 您需要進行額外的設定及整合，才能利用 Azure ATP 的功能。  

## <a name="prerequisites"></a>必要條件

- [連線到 Active Directory](install-atp-step2.md) 的 [Azure ATP 執行個體](install-atp-step1.md)。
- 您 [ATP 感應器安裝套件](install-atp-step3.md)的已下載複本，以及存取金鑰。

## <a name="configure-sensor-settings"></a>進行感應器設定

在安裝 Azure ATP 感應器之後，請執行下列操作來進行 Azure ATP 感應器設定。

1. 按一下 [啟動] 以開啟瀏覽器，然後登入 Azure ATP 入口網站。

2.  在 Azure ATP 入口網站中，移至 [設定]，然後選取 [系統] 下方的 [感應器]。
   
    ![設定感應器設定的影像](media/atp-sensor-config.png)


3. 按一下您想要設定的感應器，然後輸入下列資訊：

   ![設定感應器設定的影像](media/atp-sensor-config-2.png)

   - **描述**：輸入 Azure ATP 感應器的描述 (選擇性)。
   - **網域控制站 (FQDN)** (此為 Azure ATP 獨立感應器的必要項目，Azure ATP 感應器無法變更此項目)：輸入您網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**

     下列資訊適用於您在**網域控制站**清單中輸入的伺服器：
     - 所有透過連接埠鏡像受 Azure ATP 獨立感應器監視流量的網域控制站，都必須列在 [網域控制站] 清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑活動。
     - 清單中應至少有一個網域控制站是通用類別目錄。 這讓 Azure ATP 能夠解析樹系中其他網域的電腦與使用者物件。

   - **擷取網路介面卡** (必填)︰
   
    - 如果為 Azure ATP 感應器，應是用來與組織中其他電腦通訊的所有網路介面卡。
    - 如果為專用伺服器上的 Azure ATP 獨立感應器，請選取設定為目的地鏡像連接埠的網路介面卡。 這些網路介面卡會接收鏡像網域控制站流量。

  - **網域同步器候選項目**： 
    
    - 網域同步器是負責進行 Azure ATP 與 Active Directory 網域之間的同步處理。 根據網域的大小而定，首次同步處理可能需要很多時間，而且會耗用大量資源。 Azure ATP 建議至少為每一網域設定一個網域控制站，作為網域同步器候選。 如果無法選取至少一個網域控制站作為網域同步器候選，則代表 Azure ATP 只會被動地掃描您的網路，且無法收集到所有 Active Directory 變更和實體詳細資料。 為每一網域至少提供一個指定的**網域同步器候補**，能夠確保 Azure ATP 隨時都會主動掃描您的網路，以及能夠收集所有 Active Directory 變更和實體值。
  
    - 根據預設，Azure ATP 感應器不是網域同步器的候選，但 Azure ATP 獨立感應器是。 若要手動將 Azure ATP 感應器設定為網域同步器候選，請將 [設定] 畫面中的 [網域同步器候選] 切換選項切換為 [開啟]。
        
    - 建議您不要讓任何遠端站台 Azure ATP 感應器成為網域同步器候選。
   
    - 請勿將唯讀網域控制站設為網域同步器候選。 如需 Azure ATP 網域同步處理的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md#azure-atp-sensor-features)。
  
3. 按一下 **[儲存]**。


## <a name="validate-installations"></a>驗證安裝
若要驗證 Azure ATP 感應器是否已成功部署，請檢查下列項目︰

1. 檢查名稱為 [Azure 進階威脅感應器] 的服務是否正在執行。 儲存 Azure ATP 感應器設定之後，服務可能需要幾秒鐘的時間來啟動。

2. 如果服務未啟動，請檢閱位於以下預設資料夾 "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs" 中的 "Microsoft.Tri.sensor-Errors.log" 檔案。
 
   >[!NOTE]
   > Azure ATP 的版本經常更新，若要檢查是否有最新版本，請在 Azure ATP 入口網站中，移至 [設定]，然後移至 [關於]。 

3. 前往您的 Azure ATP 執行個體 URL。 在 Azure ATP 入口網站的搜尋列中搜尋某個項目，例如網域上的使用者或群組。

4. 使用下列步驟來確認任何網域裝置上的 ATP 連線能力：
    1. 開啟命令提示字元
    2. Type ```nslookup```
    3. 輸入 **server**，然後輸入已安裝 ATP 感應器之網域控制站的 FQDN 或 IP 位址。 例如， ```server contosodc.contoso.azure``` 
        - 請務必將 contosodc.contoso.azure 和 contoso.azure 分別取代成您 Azure ATP 感應器的 FQDN 和網域。
    4. Type ```ls -d contoso.azure```
    5. 針對您想要測試的每個感應器重複步驟 3 和 4。  
    6. 從 Azure ATP 主控台中，開啟您執行連線能力測試之來源電腦的實體設定檔。 
    7. 檢查相關的邏輯活動並確認連線能力。 

    > [!NOTE] 
    >如果您想要測試的網域控制站是第一個部署的感應器，請至少等候 15 分鐘，以允許資料庫後端完成必要微服務的初始部署，然後再嘗試確認該網域控制站的相關邏輯活動。

## <a name="next-steps"></a>後續步驟

- [Proxy 設定](configure-proxy.md)
- [進階稽核原則](atp-advanced-audit-policy.md)
- [設定 Azure ATP 對 SAM 發出遠端呼叫](install-atp-step8-samr.md)


## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
