---
title: 使用 Microsoft Defender 的身分識別，監視網域控制站和安裝在網域控制站上的感應器
description: 說明如何使用 Defender 進行身分識別監視適用于身分識別感應器和感應器涵蓋範圍的 Microsoft Defender
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: af05ee5bbd064e31b231ad36374b4c069d8f7cfc
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275394"
---
# <a name="monitoring-your-domain-controller-coverage"></a>監視您的網域控制站涵蓋範圍

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

當第一個感應器在 [!INCLUDE [Product long](includes/product-long.md)] 您網路中的任何網域控制站上安裝並設定時，就會 [!INCLUDE [Product short](includes/product-short.md)] 開始監視網域控制站的環境。

在 [!INCLUDE [Product short](includes/product-short.md)] 網路中的網域控制站上安裝並設定感應器之後，感應器會以持續的方式與服務通訊，以傳送 [!INCLUDE [Product short](includes/product-short.md)] 感應器狀態、健康情況和版本資訊，並收集 Active Directory 事件和變更。

## <a name="domain-controller-status"></a>網域控制站狀態

[!INCLUDE [Product short](includes/product-short.md)] 持續監視環境中引入未受監視的網域控制站，並報告這些控制器以協助您管理整個環境的涵蓋範圍。

1. 若要檢查偵測到的受監視和未受監視網域控制站的狀態及其狀態，請移至入口網站的 [設定 **] 區域，** [!INCLUDE [Product short](includes/product-short.md)] 然後在 [ **系統** ] 區段下選取 [ **感應器** ]。

    ![[!包含 [Product short] (include/product-short. md) ] 感應器狀態監視](media/sensors-status-monitoring.png)

1. 您目前的已監視和未監視網域控制站都會顯示在畫面的頂端。 如果要下載您網域控制站的監視狀態詳細資料，請選取 [下載詳細資料]。

網域控制站涵蓋範圍 Excel 下載會為您組織中偵測到的所有控制站提供以下資訊：

|標題|描述|
|----|----|
|Hostname (主機名稱)|電腦名稱|
|網域名稱|網域名稱|
|Monitored|[!INCLUDE [Product short](includes/product-short.md)] 監視狀態|
|感應器類型|[!INCLUDE [Product short](includes/product-short.md)] 感應器或 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器|
|組織單位|Active Directory 中的位置 |
|作業系統版本| 偵測到的作業系統版本|
|IP 位址|偵測到的 IP 位址|

## <a name="search-domain-controllers"></a>搜尋域控制站

管理您的各種感應器與網域控制站可能是一個挑戰。 為了更輕鬆地尋找和識別，可以使用 [感應器] 清單中的搜尋功能來搜尋網域控制站 [!INCLUDE [Product short](includes/product-short.md)] 。

1. 若要搜尋您的網域控制站，請移至入口網站的 [設定 **] 區域，** [!INCLUDE [Product short](includes/product-short.md)] 然後在 [ **系統** ] 區段中選取 [ **感應器** ]。
1. 在網域控制器表格清單中的 [網域控制器] 欄中選取篩選選項。
1. 輸入您要搜尋的名稱。 目前搜尋欄位中不支援萬用字元。

    ![[!包含 [Product short] (include/product-short. md) ] 搜尋網域控制站](media/search-sensor.png)

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] 只有系統管理員可以修改入口網站設定頁面 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 建築](architecture.md)
- [設定 [!INCLUDE [Product short](includes/product-short.md)] 感應器](install-step5.md)
- [多重樹系支援](multi-forest.md)
- [查看 [!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)
