---
title: 使用 Azure 進階威脅防護監視網域控制站和安裝在網域控制站上的感應器
description: 描述如何使用 Azure ATP 來監視 Azure ATP 感應器和感應器涵蓋範圍
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ac4c0b9bd4e8a99d5edaaec2746f3ce7d413005c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912556"
---
# <a name="monitoring-your-domain-controller-coverage"></a>監視您的網域控制站涵蓋範圍

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

當第一個 Azure ATP 感應器安裝到您網路的任何網域控制站且經過設定後，Azure ATP 就會開始監視您網域控制站的環境。

當 Azure ATP 感應器已安裝到您網路的網域控制站，並經過設定後，感應器會持續和 Azure ATP 服務通訊，傳送感應器狀態、健全狀況和版本資訊，以及收集到的 Active Directory 事件及變更。

## <a name="domain-controller-status"></a>網域控制站狀態

Azure ATP 會持續監視您的環境，尋找是否有導入您環境但未受監視的網域控制站，且據此向您回報來協助您管理環境的整個涵蓋範圍。

1. 如果要為偵測到的已監視/未監視網域控制站檢查狀態，請前往 Azure ATP 入口網站的 [設定]**** 區域，在 [系統]**** 區段下選取 [感應器]****。

    ![Azure ATP 感應器狀態監視](media/atp-sensors-status-monitoring.png)

1. 您目前的已監視和未監視網域控制站都會顯示在畫面的頂端。 如果要下載您網域控制站的監視狀態詳細資料，請選取 [下載詳細資料]****。

網域控制站涵蓋範圍 Excel 下載會為您組織中偵測到的所有控制站提供以下資訊：

|標題|描述|
|----|----|
|主機名稱|電腦名稱|
|網域名稱|網域名稱|
|Monitored|Azure ATP 監視狀態|
|感應器類型|Azure ATP 感應器或 Azure ATP 獨立感應器|
|組織單位|Active Directory 中的位置 |
|作業系統版本| 偵測到的作業系統版本|
|IP 位址|偵測到的 IP 位址|

## <a name="search-domain-controllers"></a>搜尋域控制站

管理您的各種感應器與網域控制站可能是一個挑戰。 若要更輕鬆地尋找並識別，可以使用 Azure ATP 感應器清單中的搜尋功能來搜尋網域控制站。

1. 若要搜尋您的網域控制站，請移至 Azure ATP 入口網站的 [設定]**** 區域 (在 [系統]**** 區段下)，然後選取 [感應器]****。
1. 在網域控制器表格清單中的 [網域控制器]**** 欄中選取篩選選項。
1. 輸入您要搜尋的名稱。 目前搜尋欄位中不支援萬用字元。

    ![Azure ATP 搜尋網域控制站](media/search-sensor.png)

> [!NOTE]
> 只有 Azure ATP 系統管理員才可修改 Azure ATP 入口網站設定頁面。

## <a name="see-also"></a>另請參閱

- [Azure ATP 架構](architecture.md)
- [設定 Azure ATP 感應器](install-step5.md)
- [多重樹系支援](multi-forest.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
