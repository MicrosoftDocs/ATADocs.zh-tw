---
title: 安裝 Advanced Threat Analytics - 步驟 5 | Microsoft Docs
description: 安裝 ATA 的步驟 5 協助您設定 ATA 閘道的設定。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 50a46bad5f138344cc3e62a3fca236e98e71f904
ms.sourcegitcommit: 6f1406f28c4c2af6a36bc691ebaf4e819adc6b4b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2018
ms.locfileid: "43675163"
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="install-ata---step-5"></a>安裝 ATA - 步驟 5

>[!div class="step-by-step"]
[«步驟 4](install-ata-step4.md)
[步驟 6»](install-ata-step6.md)


## <a name="step-5-configure-the-ata-gateway-settings"></a>步驟 5： 設定 ATA 閘道設定
安裝 ATA 閘道後，執行下列步驟來設定 ATA 閘道的設定。

1.  在 ATA 主控台中，移至 [設定]，在 [系統] 下選取 [閘道]。
   
     ![設定閘道設定影像](media/ata-gw-config-1.png)


2.  按一下您想要設定的閘道，然後輸入下列資訊：

    ![設定閘道設定影像](media/ATA-Gateways-config-2.png)

  - **描述**：輸入 ATA 閘道的描述 (選擇性)。
  - **連接埠鏡像的網域控制站 (FQDN)** (如果是 ATA 閘道則必填，無法針對 ATA 輕量型閘道變更)︰輸入您網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**

    下列資訊適用於您在**網域控制站**清單中輸入的伺服器：
    - 所有透過連接埠鏡像受 ATA 閘道監視流量的網域控制站，都必須列在**網域控制站**清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑的活動。
    - 清單中應至少有一個網域控制站是通用類別目錄。 這會讓 ATA 解析樹系中其他網域的電腦與使用者物件。

  - **擷取網路介面卡** (必填)︰
  - 針對專用伺服器上的 ATA 閘道，請選取設定為目的地鏡像連接埠的網路介面卡。 這些介面卡會接收鏡像網域控制站的流量。
  - 針對 ATA 輕量型閘道，則應該是用來與組織中其他電腦通訊的所有網路介面卡。
  
  - **網域同步器候選**：任何設為網域同步器候選的 ATA 閘道皆可負責進行 ATA 與 Active Directory 網域之間的同步處理。 根據網域的大小而定，首次同步處理可能需要一些時間，而且會耗用大量資源。 根據預設，只有 ATA 閘道會設為網域同步器候選。
   建議停用所有遠端站台 ATA 閘道，使它們不會成為網域同步器候選。
   如果網域控制站是唯讀的，請勿將其設定為網域同步器候選。 如需詳細資訊，請參閱 [ATA 架構](ata-architecture.md#ata-lightweight-gateway-features)。

  > [!NOTE] 
  > 安裝後第一次啟動 ATA 閘道服務時會花幾分鐘時間，因為它要建立網路擷取剖析器的快取。
  > 在 ATA 閘道與 ATA 中心進行下一次的排程同步時，設定的變更便會套用至 ATA 閘道。

3. 您也可以選擇設定 [Syslog 接聽程式和 Windows 事件轉寄集合](configure-event-collection.md)。 
4. 啟用 [自動更新 ATA 閘道]，使您於未來將 ATA 中心更新為新的版本時，此 ATA 閘道也會自動更新。

5. 按一下 **[儲存]**。


## <a name="validate-installations"></a>驗證安裝
若要驗證 ATA 閘道是否已成功部署，請檢查下列步驟︰

1.  檢查名為 **Microsoft Advanced Threat Analytics 閘道**的服務是否正在執行。 儲存 ATA 閘道設定後，可能需幾分鐘時間來啟動服務。

2.  如果服務未啟動，請檢閱位於預設資料夾 “%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs” 中的 “Microsoft.Tri.Gateway-Errors.log” 檔案，然後查看 [ATA 疑難排解](troubleshooting-ata-known-errors.md) 取得協助。

3.  如果這是第一個安裝的 ATA 閘道，請於幾分鐘後登入 ATA 主控台，然後將開啟的螢幕向右撥動，以開啟 [通知] 窗格。 您應該會在主控台右邊的通知列中看到**最近已了解的實體**清單。

4.  按一下桌面上的 [Microsoft Advanced Threat Analytics] 捷徑以連線到 ATA 主控台。 以您安裝 ATA 中心的相同使用者認證登入。
5.  主控台的 [搜尋] 列中搜尋項目，例如您網域中的使用者或群組。
6.  開啟效能監視器。 在效能樹狀目錄中，按一下 [效能監視器]，然後按一下加號圖示以 [新增計數器]。 展開 [Microsoft ATA 閘道]，向下捲動至 [Network Listener PEF Captured Messages/Sec] 並加以新增。 接著，請確定您有在圖形上看到活動。

    ![新增效能計數器影像](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[«步驟 4](install-ata-step4.md)
[步驟 6»](install-ata-step6.md)



## <a name="related-videos"></a>相關影片
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

