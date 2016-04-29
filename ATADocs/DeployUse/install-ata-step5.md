---
# required metadata

title: 安裝 ATA - 步驟 5 | Microsoft Advanced Threat Analytics
description: 安裝 ATA 的步驟 5 協助您設定 ATA 閘道的設定。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安裝 ATA - 步驟 5

>[!div class="step-by-step"]
[« 步驟 4](install-ata-step4.md)
[步驟 6 »](install-ata-step6.md)


## 步驟 5： 設定 ATA 閘道設定
安裝 ATA 閘道後，執行下列步驟來設定 ATA 閘道的設定。

1.  在 ATA 閘道電腦的 ATA 主控台中，按一下 [組態]****，然後選取 [ATA 閘道]**** 頁面。

2.  輸入下列資訊。



  - **描述**： <br>輸入 ATA 閘道的描述 (可選填)。
  - **網域控制站** (必填)： <br>請參閱以下控制站清單的其他資訊。<br>輸入您網域控制站的完整 FQDN，然後按一下加號將它新增至清單。 例如，**dc01.contoso.com**<br /><br />![範例 FDQN 影像](media/ATAGWDomainController.png)<br>清單中第一個網域控制站中的物件會透過 LDAP 查詢同步。 根據網域大小，這可能需要一些時間。<br>
  **注意：** <br>請確定第一個網域控制站並**不是**唯讀狀態。 唯讀網域控制站應於初始同步完成後才新增。<br>


 - **擷取網路介面卡** (必填)︰<br>選取連線到已設定為目的地鏡像連接埠的交換器之網路介面卡，以接收網域控制站的流量。|選取擷取網路介面卡。
    ![設定閘道設定影像](media/ATA-Config-GW-Settings.jpg)

3.  按一下 [儲存] ****。

    > [!NOTE]
    > 第一次啟動 ATA 閘道服務時會花幾分鐘時間，因為它要建立 ATA 閘道使用的網路擷取剖析器快取。

下列資訊適用於您在**網域控制站**清單中輸入的伺服器。

-   ATA 閘道會使用清單中的第一個網域控制站，以透過 LDAP 查詢同步處理網域中的物件。 根據網域大小，這可能需要一些時間。

-   所有透過連接埠鏡像受 ATA 閘道監視流量的網域控制站，都必須列在**網域控制站**清單中。 如果網域控制站未列在**網域控制站**清單中，可能無法如預期般偵測可疑的活動。

-   請確定第一個網域控制站並**不是**唯讀網域控制站 (RODC)。

    唯讀網域控制站應於初始同步完成後才新增。

-   清單中至少有一個網域控制站是通用類別目錄伺服器。 這會讓 ATA 解析樹系中其他網域的電腦與使用者物件。

進行下一個排定的 ATA 閘道與 ATA 中心間的同步時，設定的變更將套用至 ATA 閘道。

### 驗證安裝︰
若要驗證 ATA 閘道是否已成功部署，請檢查下列各項︰

1.  檢查 Microsoft Advanced Threat Analytics 閘道服務是否正在執行。 您儲存 ATA 閘道設定後，可能需幾分鐘時間來啟動服務。

2.  如果服務未啟動，請檢閱位於下列資料夾「%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs」的「Microsoft.Tri.Gateway Errors.log」檔案，搜尋「傳輸」或「服務啟動」的項目。

3.  請檢查下列 Microsoft ATA 閘道效能計數器：

    -   **NetworkListener 擷取的郵件數 / 秒**︰這個計數器會追蹤 ATA 每秒擷取的訊息數量。 值應該介於一百五十上下至數千，視受監視的網域控制站數目和每個網域控制站忙碌程度而定。 單數或雙數值表示連接埠鏡像組態有問題。

    -   **EntityTransfer 活動傳輸 / 秒**︰這個值應介於每幾秒鐘數百的範圍內。

4.  如果這是第一個安裝的 ATA 閘道器，請於幾分鐘後登入 ATA 主控台，然後將開啟的螢幕向右撥動，以開啟 [通知] 窗格。 您應該會在主控台右邊的通知列中看到**最近已了解的實體**清單。

5.  若要驗證安裝已順利完成︰

    主控台的 [搜尋] 列中搜尋項目，例如您網域中的使用者或群組。

    開啟效能監視器。 在效能樹狀目錄中，按一下 [效能監視器]****，然後按一下加號圖示以 [新增計數器]****。 展開 [Microsoft ATA 閘道]****，向下捲動至 [網路接聽程式每秒擷取的訊息]****，並加以新增。 接著，請確定您有在圖形上看到活動。

    ![新增效能計數器影像](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« 步驟 4](install-ata-step4.md)
[步驟 6 »](install-ata-step6.md)

## 另請參閱

- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [設定事件收集](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 必要條件](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


