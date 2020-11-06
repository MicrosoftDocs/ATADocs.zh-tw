---
title: 在適用於身分識別的 Microsoft Defender 中驗證連接埠鏡像
description: 描述如何驗證已在適用於身分識別的 Microsoft Defender 中正確設定連接埠鏡像
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7a665a20da3940b3146a007eea6ee75bd35d7930
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274050"
---
# <a name="validate-port-mirroring"></a>驗證連接埠鏡像

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

此文章僅適用於您部署[!INCLUDE [Product long](includes/product-long.md)] 獨立感應器 (而非[!INCLUDE [Product short](includes/product-short.md)] 感應器) 的情況。

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不會收集 Windows 事件追蹤 (ETW) 的記錄項目，無法提供多種偵測的資料。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。

下列步驟會引導您逐步完成驗證已正確設定連接埠鏡像的程序。 若要讓[!INCLUDE [Product short](includes/product-short.md)] 正常運作，[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器必須能夠看到進出網域控制站的流量。 [!INCLUDE [Product short](includes/product-short.md)] 使用的主要資料來源是對進出網域控制站的網路流量進行的深度封包檢查。 若要讓[!INCLUDE [Product short](includes/product-short.md)] 看到網路流量，必須設定連接埠鏡像。 連接埠鏡像會將流量從一個連接埠 (來源連接埠) 複製到另一個連接埠 (目的地連接埠)。

## <a name="validate-port-mirroring-using-net-mon"></a>使用 Net Mon 驗證連接埠鏡像

1. 在您想要驗證的[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器上安裝 [Microsoft 網路監視器 3.4](https://www.microsoft.com/download/details.aspx?id=4865) \(英文\)。

    > [!IMPORTANT]
    > 如果您選擇安裝 Wireshark 以驗證連接埠鏡像，請在驗證之後重新啟動[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器服務。

1. 開啟網路監視器並建立新的 [擷取] 索引標籤。

    1. 只選取 [擷取]  網路介面卡或連接到設定為連接埠鏡像目的地的交換器連接埠之網路介面卡。

    1. 確定已啟用 P-Mode

    1. 按一下 [新增擷取]  。

        ![建立新的擷取索引標籤影像](media/port-mirroring-capture.png)

1. 在 [顯示篩選器] 視窗中，輸入下列篩選： **KerberosV5 OR LDAP** ，然後按一下 [套用]  。

    ![套用 KerberosV5 或 LDAP 篩選影像](media/port-mirroring-filter-settings.png)

1. 按一下 [啟動]  ，啟動擷取工作階段。 如果您看不到網域控制站之間的流量，請檢閱您的連接埠鏡像組態。

    ![啟動擷取工作階段影像](media/port-mirroring-capture-traffic.png)

    > [!NOTE]
    > 請務必確定您可以看到網域控制站之間的流量。

1. 如果您只看到一個方向的流量，請和網路或虛擬化小組合作，以協助針對您的連接埠鏡像組態進行疑難排解。

## <a name="see-also"></a>另請參閱

- [設定事件轉寄](configure-event-forwarding.md)
- [設定連接埠鏡像](configure-port-mirroring.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
