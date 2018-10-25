---
title: 安裝 Azure 進階威脅防護 | Microsoft Docs
description: 安裝 Azure ATP 的步驟 5 可協助您設定 Azure ATP 獨立感應器的設定。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b7ddaca0f0c5691c90873cef9af6cef13fa9650a
ms.sourcegitcommit: e783df4c9d928fedf6dc3c65d58d9b530cdd2ff2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2018
ms.locfileid: "49800030"
---
適用於：Azure 進階威脅防護



# <a name="install-azure-atp---step-5"></a>安裝 Azure ATP - 步驟 5

> [!div class="step-by-step"]
> [«步驟 4](install-atp-step4.md)
> [步驟 6»](install-atp-step6-vpn.md)



## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>步驟 5： 設定 Azure ATP 感應器的設定
安裝 Azure ATP 感應器之後，請執行下列步驟以設定 Azure ATP 感應器的設定。

1.  在 Azure ATP 入口網站中，移至 [設定]，然後選取 [系統] 下方的 [感應器]。
   
     ![設定感應器設定的影像](media/atp-sensor-config.png)


2.  按一下您想要設定的感應器，然後輸入下列資訊：

    ![設定感應器設定的影像](media/atp-sensor-config-2.png)

  - **描述**：輸入 Azure ATP 感應器的描述 (選擇性)。
  - **網域控制站 (FQDN)** (Azure ATP 獨立感應器的必要項，Azure ATP 感應器的此設定則無法變更)：輸入您的網域控制站完整 FQDN，然後按一下加號將它加入清單。 例如，**dc01.contoso.com**

      下列資訊適用於您在**網域控制站**清單中輸入的伺服器：
      - 所有透過連接埠鏡像受 Azure ATP 獨立感應器監視流量的網域控制站，都必須列在 [網域控制站] 清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑的活動。
      - 清單中應至少有一個網域控制站是通用類別目錄。 這讓 Azure ATP 能夠解析樹系中其他網域的電腦與使用者物件。

  - **擷取網路介面卡** (必填)︰
   
     - 針對 Azure ATP 感應器，則應該是用來與組織中其他電腦通訊的所有網路介面卡。
    - 針對專用伺服器上的 Azure ATP 獨立感應器，請選取設定為目的地鏡像連接埠的網路介面卡。 這些介面卡會接收鏡像網域控制站的流量。

    - **網域同步器候選**：Azure ATP 感應器並非預設為網域同步器候選，但 Azure ATP 獨立感應器則是。 若要手動將 Azure ATP 感應器選取為網域同步器候選，請將 [設定] 畫面中的 [網域同步器候選] 切換選項切換為 [開啟]。 
    
        網域同步器是負責進行 Azure ATP 與 Active Directory 網域之間的同步處理。 根據網域的大小而定，首次同步處理可能需要一些時間，而且會耗用大量資源。 
   建議您不要讓任何遠端站台 Azure ATP 感應器成為網域同步器候選。
   如果網域控制站是唯讀的，請勿將其設定為網域同步器候選。 如需 Azure ATP 網域同步處理的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md#azure-atp-sensor-features)
  
3. 按一下 **[儲存]**。


## <a name="validate-installations"></a>驗證安裝
若要驗證 Azure ATP 感應器是否已成功部署，請檢查下列步驟︰

1.  檢查名稱為 [Azure 進階威脅感應器] 的服務是否正在執行。 儲存 Azure ATP 感應器設定之後，服務可能需要幾秒鐘的時間來啟動。

2.  如果服務未啟動，請檢閱位於下列預設資料夾 "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs" 中的 "Microsoft.Tri.sensor-Errors.log" 檔案。
 
 >[!NOTE]
 > Azure ATP 的版本經常更新，若要檢查是否有最新版本，請在 Azure ATP 入口網站中，移至 [設定]，然後移至 [關於]。 

3.  移至您的工作區 URL。 在 Azure ATP 入口網站的搜尋列中搜尋某個項目，例如網域中的使用者或群組。



> [!div class="step-by-step"]
> [«步驟 4](install-atp-step4.md)
> [步驟 6»](install-atp-step6-vpn.md)



## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
