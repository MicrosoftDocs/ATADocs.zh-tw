---
title: 適用于身分識別未受監視網域控制站評定的 Microsoft Defender
description: 本文概述適用于身分識別之未受監視的網域控制站身分識別安全性狀態評估報告的 Microsoft Defender。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f3cf20aed80167b581a78fea5306916578bbd4c6
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848324"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>安全性評估：未受監視的網域控制站

## <a name="what-are-unmonitored-domain-controllers"></a>什麼是未受監視的網域控制站？

解決方案的必要部分 [!INCLUDE [Product long](includes/product-long.md)] 需要將其感應器部署在所有組織網域控制站上，以提供每個裝置的所有使用者活動全方位的觀點。

基於這個理由， [!INCLUDE [Product short](includes/product-short.md)] 持續監視您的環境以識別沒有安裝感應器的網域控制站 [!INCLUDE [Product short](includes/product-short.md)] ，並報告這些未受監視的伺服器，以協助您管理整個環境的涵蓋範圍。

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>未受監視的網域控制站會對組織造成什麼風險？

若要以最有效率的方式操作，所有網域控制站都必須與 [!INCLUDE [Product short](includes/product-short.md)] 感應器監視。 若組織無法針對未受監視的網域控制站進行補救，則將無法完全洞悉其環境的各層面，而且其資產可能會面臨遭惡意攻擊的風險。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告表格來探索哪些網域控制站是未受監視的。
    ![針對未受監視的網域控制站進行補救](media/cas-isp-unmonitored-domain-controller-1.png)
1. 透過[安裝並設定監視感應器](sensor-monitoring.md#domain-controller-status)，以在那些網域控制站上採取適當的動作。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="see-also"></a>另請參閱

- [監視您的網域控制站涵蓋範圍](sensor-monitoring.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
