---
title: "安裝 ATA - 步驟 5 | Microsoft Advanced Threat Analytics"
description: "安裝 ATA 的步驟 5 協助您設定 ATA 閘道的設定。"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 6400a0eabefac91b418e00eb670b1329fa1b5fb5


---

# 安裝 ATA - 步驟 5

>[!div class="step-by-step"]
[«步驟 4](install-ata-step4.md)
[步驟 6»](install-ata-step6.md)


## 步驟 5： 設定 ATA 閘道設定
安裝 ATA 閘道後，執行下列步驟來設定 ATA 閘道的設定。

1.  在 ATA 主控台中，按一下 [設定]，然後選取 [ATA 閘道] 頁面。

2.  輸入下列資訊。

  - **描述**： <br>輸入 ATA 閘道的描述 (可選填)。
  - **連接埠鏡像網域控制站 (FQDN)** (ATA 閘道的必要項，無法針對 ATA 輕量型閘道進行設定)︰ <br>輸入您網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**<br /><br />![範例 FDQN 影像](media/ATAGWDomainController.png)

下列資訊適用於您在 [網域控制站] 清單中輸入的伺服器： -   所有透過連接埠鏡像受 ATA 閘道監視流量的網域控制站，都必須列在 [網域控制站] 清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑的活動。
-   清單中至少有一個網域控制站是通用類別目錄伺服器。 這會讓 ATA 解析樹系中其他網域的電腦與使用者物件。

 - **擷取網路介面卡** (必填)︰<br>
     - 針對專用伺服器上的 ATA 閘道，請選取設定為目的地鏡像連接埠的網路介面卡。 這些介面卡將會接收鏡像網域控制站的流量。
     - 針對 ATA 輕量型閘道，則應該是用來與組織中其他電腦通訊的所有網路介面卡。

![設定閘道設定影像](media/ATA-Config-GW-Settings.jpg)

 - **網域同步器候選**<br>
任何設為網域同步器候選的 ATA 閘道皆可負責進行 ATA 與 Active Directory 網域之間的同步處理。 取決於網域大小，初始同步處理可能需要一些時間，而且會耗用大量資源。根據預設，只會將 ATA 閘道設為網域同步器候選。 <br>建議不要將任何遠端站台的 ATA 閘道設為網域同步器候選。<br>如果網域控制站是唯讀的，請勿將其設定為網域同步器候選。 如需詳細資訊，請參閱 [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features)。

> [!NOTE] 
> 第一次啟動 ATA 閘道服務時會花幾分鐘時間，因為它要建立網路擷取剖析器的快取。<br>
> 進行下一個排定的 ATA 閘道與 ATA 中心間的同步時，設定的變更將套用至 ATA 閘道。



    

3. 您也可以選擇設定 [Syslog 接聽程式和 Windows 事件轉寄集合](configure-event-collection.md)。 
4. 啟用 [Update ATA Gateway automatically] (自動更新 ATA 閘道) 後，在未來版本中，當您更新 ATA 中心時，所有 ATA 閘道都會自動更新。
3.  按一下 **[儲存]**。


## 驗證安裝
若要驗證 ATA 閘道是否已成功部署，請檢查下列各項︰

1.  檢查名為 **Microsoft Advanced Threat Analytics 閘道**的服務是否正在執行。 您儲存 ATA 閘道設定後，可能需幾分鐘時間來啟動服務。

2.  如果服務未啟動，請檢閱位於預設資料夾 “%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs” 中的 “Microsoft.Tri.Gateway-Errors.log” 檔案。

3.  請查看 [ATA 疑難排解](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors)以取得協助。

4.  如果這是第一個安裝的 ATA 閘道器，請於幾分鐘後登入 ATA 主控台，然後將開啟的螢幕向右撥動，以開啟 [通知] 窗格。 您應該會在主控台右邊的通知列中看到**最近已了解的實體**清單。

5.  按一下桌面上的 [Microsoft Advanced Threat Analytics] 捷徑以連線到 ATA 主控台。 以您安裝 ATA 中心的相同使用者認證登入。
6.  主控台的 [搜尋] 列中搜尋項目，例如您網域中的使用者或群組。
7.  開啟效能監視器。 在效能樹狀目錄中，按一下 [效能監視器]，然後按一下加號圖示以 [新增計數器]。 展開 [Microsoft ATA 閘道]，向下捲動至 [Network Listener PEF Captured Messages/Sec] 並加以新增。 接著，請確定您有在圖形上看到活動。

    ![新增效能計數器影像](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[«步驟 4](install-ata-step4.md)
[步驟 6»](install-ata-step6.md)

## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


