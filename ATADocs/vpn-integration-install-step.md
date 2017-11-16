---
title: "安裝 Advanced Threat Analytics - 步驟 7 | Microsoft Docs"
description: "在這個安裝 ATA 的步驟中，您要整合您的 VPN。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2eab8649f225071ad548a8134b385d46f02b3222
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2017
---
適用於︰Advanced Threat Analytics 1.8 版



# <a name="install-ata---step-7"></a>安裝 ATA - 步驟 7

>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)
[步驟 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>步驟 ７： 整合 VPN

Microsoft Advanced Threat Analytics (ATA) 1.8 版可以從 VPN 解決方案收集計量資訊。 設定了 ATA 之後，使用者的設定檔頁面會包含來自 VPN 連線的資訊，例如 IP 位址與連線的原始位置。 這會透過提供其他與使用者活動相關的資訊，來補充調查程序。 將外部 IP 位址解析為位置的呼叫是匿名的。 不會在此呼叫中傳送個人識別資訊。

ATA 會透過接聽轉送到 ATA 閘道的 RADIUS 計量事件，與您的 VPN 解決方案相整合。 這項機制依據標準 RADIUS 計量 ([RFC 2866](https://tools.ietf.org/html/rfc2866)) 運作，並且支援下列 VPN 廠商：

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>必要條件

若要啟用 VPN 整合，請確定已設定了下列參數：

-   啟動您 ATA 閘道和 ATA 輕量型閘道上的連接埠 UDP 1813。

-   將 ATA 中心連線到網際網路，如此即可查詢連入 IP 位址的位置。

下列範例會使用 Microsoft 路由及遠端存取伺服器 (RRAS) 來描述 VPN 設定程序。

如果您是使用協力廠商 VPN 解決方案，請參考其文件以了解如何啟用 RADIUS 帳戶處理的相關指示。

## <a name="configure-radius-accounting-on-the-vpn-system"></a>在 VPN 系統上設定 RADIUS 計量

請在 RRAS 伺服器上執行下列步驟。
 
1.  開啟路由及遠端存取主控台。
2.  在伺服器名稱上按一下滑鼠右鍵，然後按一下 [屬性]。
3.  在 [安全性] 索引標籤的 [計量提供者] 下，選取 [RADIUS 計量]，然後按一下 [設定]。

    ![RADIUS 設定](./media/radius-setup.png)

4.  在 [新增 RADIUS 伺服器] 視窗中，鍵入最接近之 ATA 閘道或 ATA 輕量型閘道的**伺服器名稱**。 在 [連接埠] 下，確定已設為預設的 1813。 按一下 [變更]，並鍵入您能記住的新共用祕密英數字元字串。 您稍後必須在 ATA 設定中填入它。 選取 [傳送 RADIUS 計量開啟及計量關閉訊息] 方塊，然後在所有已開啟的對話方塊上按一下 [確定]。
 
     ![VPN 設定](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>在 APA 中設定 VPN

ATA 會收集 VPN 資料，這些資料有助於描繪電腦連線到網路的來源位置，而且有助於偵測異常 VPN 連線。

在 ATA 中設定 VPN 資料：

1.  在 ATA 主控台中，開啟 [ATA 設定] 頁面，並前往 [VPN]。
 
  ![ATA 設定功能表](./media/config-menu.png)

2.  開啟 [Radius 帳戶處理]，然後輸入先前在 RRAS VPN 伺服器上設定的 [共用祕密]。 然後按一下 [儲存]。
 

  ![設定 ATA VPN](./media/vpn.png)


啟用 ATA VPN 之後，所有 ATA 閘道及輕量型閘道就會在連接埠 1813 上接聽 RADIUS 計量事件。 

您的設定已完成，且已經可以在使用者的設定檔頁面中看到 VPN 活動：
 
   ![VPN 設定](./media/vpn-user.png)

在 ATA 閘道接收 VPN 事件並將它們傳送給 ATA 中心進行處理之後，ATA 中心必須有網際網路連線，HTTPS 連接埠 443 才能將 VPN 事件中的外部 IP 地址解析為其地理位置。





>[!div class="step-by-step"]
[« 步驟 6](install-ata-step5.md)
[步驟 8 »](install-ata-step7.md)



## <a name="related-videos"></a>相關影片
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

