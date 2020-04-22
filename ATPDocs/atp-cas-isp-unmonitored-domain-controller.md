---
title: Azure 進階威脅防護未受監視的網域控制站評量
description: 此文章提供 Azure ATP 未受監視網域控制站身分識別安全性狀態評量報告的概觀。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b82aa4af317b1eb913794f164449716180842c3c
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "77478814"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>安全性評估：未受監視的網域控制站

## <a name="what-are-unmonitored-domain-controllers"></a>什麼是未受監視的網域控制站？

Azure ATP 解決方案的必要部分，其感應器部署在所有組織網域控制站上，進而提供所有裝置上所有使用者活動的全方位檢視。

基於此原因，Azure ATP 會持續監視您的環境，以找出未安裝 Azure ATP 感應器的網域控制站，並回報這些未受監視網域控制站的資訊以協助您管理環境的各層面。

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>未受監視的網域控制站會對組織造成什麼風險？

為了以最高效率操作，必須使用 Azure ATP 感應器來監視所有網域控制站。 若組織無法針對未受監視的網域控制站進行補救，則將無法完全洞悉其環境的各層面，而且其資產可能會面臨遭惡意攻擊的風險。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告表格來探索哪些網域控制站是未受監視的。
    ![針對未受監視的網域控制站進行補救](media/atp-cas-isp-unmonitored-domain-controller-1.png)
1. 透過[安裝並設定監視感應器](atp-sensor-monitoring.md#domain-controller-status)，以在那些網域控制站上採取適當的動作。

## <a name="see-also"></a>另請參閱

- [監視您的網域控制站涵蓋範圍](atp-sensor-monitoring.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
