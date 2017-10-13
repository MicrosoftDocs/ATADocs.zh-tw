---
title: "安裝 Advanced Threat Analytics - 步驟 7 | Microsoft Docs"
description: "在這個安裝 ATA 的步驟中，您要整合您的 VPN。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02649a6acb6a083145ba81b3b9c1647e7f8ea2a
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2017
---
適用於︰Advanced Threat Analytics 1.8 版



# <a name="install-ata---step-7"></a>安裝 ATA - 步驟 7

>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)
[步驟 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>步驟 7. 整合 VPN

### <a name="configuring-vpn"></a>設定 VPN

ATA 會收集 VPN 資料，這些資料有助於描繪電腦連線到網路的來源位置，而且有助於偵測異常 VPN 連線。

在 ATA 中設定 VPN 資料：

1. 移至 設定，然後按一下VPN 索引標籤。

2. 輸入您 RADIUS 伺服器的**帳戶共用密碼**。 若要取得共用密碼，請參閱您的 VPN 文件。

 ![設定 ATA VPN](media/vpn.png)

3.  一旦啟用此選項，所有 ATA 閘道與輕量型閘道都會在連接埠 1813 上接聽 RADIUS 帳戶處理事件。 

4.  在設定此選項之後，VPN 的 RADIUS 帳戶處理事件應該會被轉送到任何 ATA 閘道或 ATA 輕量型閘道。

5.  在 ATA 閘道接收 VPN 事件並將它們傳送給 ATA 中心進行處理之後，ATA 中心必須有網際網路連線，HTTPS 連接埠 443 才能將 VPN 事件中的外部 IP 地址解析為其地理位置。

將外部 IP 位址解析為位置的呼叫是匿名的。 不會在此呼叫中傳送個人識別資訊。

支援的 VPN 廠商如下：
- Microsoft
- F5
- Check Point
- Cisco ASA




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

