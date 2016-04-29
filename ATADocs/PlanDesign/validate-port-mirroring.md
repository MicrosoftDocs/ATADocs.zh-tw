---
# required metadata

title: 驗證連接埠鏡像 | Microsoft Advanced Threat Analytics
description: 描述如何驗證已正確設定連接埠鏡像
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 驗證連接埠鏡像
下列步驟會引導您逐步完成驗證已正確設定連接埠鏡像的程序。 若要讓 ATA 正常運作，ATA 閘道必須能夠看到網域控制站之間的流量。 ATA 使用的主要資料來源是對進出網域控制站的網路流量的深度封包檢查。 若要讓 ATA 查看網路流量，必須設定連接埠鏡像。 連接埠鏡像會將流量從一個連接埠 (來源連接埠) 複製到另一個連接埠 (目的地連接埠)。

1.  安裝 [Microsoft 網路監視器 3.4](http://www.microsoft.com/download/details.aspx?id=4865) 或另一個網路探查工具。

    > [!IMPORTANT]
    > 請勿在 ATA 閘道上安裝 Microsoft Message Analyzer 或其他流量擷取軟體。

2.  開啟網路監視器並建立新的 [擷取] 索引標籤。

    1.  只選取 [擷取]**** 網路介面卡或連接到設定為連接埠鏡像目的地的交換器連接埠之網路介面卡。

    2.  確定已啟用 P-Mode

    3.  按一下 [新增擷取]****。

        ![建立新的擷取索引標籤影像](media/ATA-Port-Mirroring-Capture.jpg)

3.  在 [顯示篩選] 視窗中，輸入下列篩選︰**KerberosV5 或 LDAP**，然後按一下 [套用]****。

    ![套用 KerberosV5 或 LDAP 篩選影像](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  按一下 [啟動]****，啟動擷取工作階段。 如果您看不到網域控制站之間的流量，請檢閱您的連接埠鏡像組態。

    > [!NOTE]
    > 請務必確定您可以看到網域控制站之間的流量。
    >
    > ![啟動擷取工作階段影像](media/ATA-Port-Mirroring-Capture-traffic.jpg)

5.  如果您只看到一個方向的流量，您應該和網路或虛擬化小組合作，以協助疑難排解您的連接埠鏡像組態。

## 另請參閱

- [設定連接埠鏡像](configure-port-mirroring.md)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


