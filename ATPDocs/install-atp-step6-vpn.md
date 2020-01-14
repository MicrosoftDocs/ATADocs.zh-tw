---
title: 安裝 Azure 進階威脅防護 VPN 整合 | Microsoft Docs
description: 整合 VPN 以收集 Azure ATP 的計量資訊。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 11/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a7af39b227f3bd79fb667b87602e3ac5154d6491
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907753"
---
# <a name="integrate-vpn"></a>整合 VPN

Azure 進階威脅防護 (ATP) 可以從 VPN 解決方案收集計量資訊。 設定了 ATA 之後，使用者的設定檔頁面會包含來自 VPN 連線的資訊，例如 IP 位址與連線的原始位置。 這提供使用者活動的額外資訊以及異常 VPN 連線的新增偵測，使調查程序更完整。 將外部 IP 位址解析為位置的呼叫是匿名的。 不會在此呼叫中傳送個人識別資訊。

Azure ATP 會透過接聽轉寄到 Azure ATP 感應器的 RADIUS 計量事件來與您的 VPN 解決方案整合。 這項機制依據標準 RADIUS 計量 ([RFC 2866](https://tools.ietf.org/html/rfc2866)) 運作，並且支援下列 VPN 廠商：

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>先決條件

若要啟用 VPN 整合，請確定已設定了下列參數：

-   開啟 Azure ATP 感應器和/或 Azure ATP 獨立感應器上的連接埠 UDP 1813。


下列範例會使用 Microsoft 路由及遠端存取伺服器 (RRAS) 來描述 VPN 設定程序。

如果您是使用協力廠商 VPN 解決方案，請參考其文件以取得如何啟用 RADIUS 計量的相關指示。

## <a name="configure-radius-accounting-on-the-vpn-system"></a>在 VPN 系統上設定 RADIUS 計量

請在 RRAS 伺服器上執行下列步驟。
 
1.  開啟路由及遠端存取主控台。
2.  在伺服器名稱上按一下滑鼠右鍵，然後按一下 [屬性]  。
3.  在 [安全性]  索引標籤的 [計量提供者]  下，選取 [RADIUS 計量]  ，然後按一下 [設定]  。

    ![RADIUS 設定](./media/radius-setup.png)

4.  在 [新增 RADIUS 伺服器]  視窗中，輸入最接近之 Azure ATP 感應器 (具有網路連線能力) 的**伺服器名稱**。 如需高可用性，您可以新增額外的 Azure ATP 感應器作為 RADIUS 伺服器。 在 [連接埠]  下，確定已設為預設的 1813。 按一下 [變更]  ，並鍵入新的共用祕密英數字元字串。 記下新的共用祕密字串，因為您必須在稍後的 Azure ATP 設定期間填寫它。 選取 [傳送 RADIUS 計量開啟及計量關閉訊息]  方塊，然後在所有已開啟的對話方塊上按一下 [確定]  。
 
     ![VPN 設定](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>在 ATP 中設定 VPN

Azure ATP 會收集 VPN 資料，這些資料有助於分析電腦連線到網路的來源位置，因此能夠偵測可疑的 VPN 連線。

在 ATP 中設定 VPN 資料：

1.  在 Azure ATP 入口網站中，按一下設定齒輪，然後按一下 [VPN]  。
 

2.  開啟 [Radius 帳戶處理]  ，然後輸入先前在 RRAS VPN 伺服器上設定的 [共用祕密]  。 然後按一下 [儲存]  。
 

  ![設定 Azure ATP VPN](./media/atp-vpn-radius.png)


啟用此選項之後，所有 Azure ATP 感應器都會接聽連接埠 1813 上的 RADIUS 計量事件，您的 VPN 設定即已完成。 

 Azure ATP 感應器接收 VPN 事件並將它們傳送至 Azure ATP 雲端服務進行處理之後，實體設定檔會指出不同的 VPN 存取的位置，且設定檔中的活動將指出的位置。



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
