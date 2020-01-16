---
title: 使用 Azure 進階威脅防護來監視網域控制站與安裝在您網域控制站上的感應器 | Microsoft Docs
description: 描述如何使用 Azure ATP 來監視 Azure ATP 感應器和感應器涵蓋範圍
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bdb731d3f5b509eaad9f4c3046f73e52220ba096
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75908555"
---
# <a name="monitoring-your-domain-controller-coverage"></a>監視您的網域控制站涵蓋範圍

當第一個 Azure ATP 感應器安裝到您網路的任何網域控制站且經過設定後，Azure ATP 就會開始監視您網域控制站的環境。 

設定期間，建議至少為每一網域選取一個 Azure ATP 感應器網域控制站，作為網域同步器候選。 網域同步器感應器的其中一項作業，是確保特定感應器會主動搜尋網域控制站。 起始設定結束後，可在網域控制站與網域同步器候補狀態間進行切換。 當沒有選取任何網域控制站做為候選網域同步器時，只有您的網域控制站上只會發生被動監視網路活動的情況。 如需設定 Azure 感應器，以及將其設定為**網域同步器候補**的詳細資訊，請參閱 [Azure ATP 感應器設定](install-atp-step5.md)。 

當 Azure ATP 感應器已安裝到您網路的網域控制站，並經過設定後，感應器會持續和 Azure ATP 服務通訊，傳送感應器狀態、健全狀況和版本資訊，以及收集到的 Active Directory 事件及變更。  

### <a name="domain-controller-status"></a>網域控制站狀態

Azure ATP 會持續監視您的環境，尋找是否有導入您環境但未受監視的網域控制站，且據此向您回報來協助您管理環境的整個涵蓋範圍。 

1. 如果要為偵測到的已監視/未監視網域控制站檢查狀態，請前往 Azure ATP 入口網站的 [設定]  區域，在 [系統]  區段下選取 [感應器]  。
   
    ![Azure ATP 感應器狀態監視](media/atp-sensors-status-monitoring.png)

2. 您目前的已監視和未監視網域控制站都會顯示在畫面的頂端。 如果要下載您網域控制站的監視狀態詳細資料，請選取 [下載詳細資料]  。 

網域控制站涵蓋範圍 Excel 下載會為您組織中偵測到的所有控制站提供以下資訊：

|標題|說明|
|----|----|
|主機名稱|電腦名稱|
|網域名稱|網域名稱|
|受監視|Azure ATP 監視狀態|
|感應器類型|Azure ATP 感應器或 Azure ATP 獨立感應器|
|組織單位|Active Directory 中的位置 |
|作業系統版本| 偵測到的作業系統版本|
|IP 位址|偵測到的 IP 位址| 

### <a name="search-domain-controllers"></a>搜尋域控制站

管理您的各種感應器與網域控制站可能是一個挑戰。 若要更輕鬆地尋找並識別，可以使用 Azure ATP 感應器清單中的搜尋功能來搜尋網域控制站。 

1. 若要搜尋您的網域控制站，請移至 Azure ATP 入口網站的 [設定]  區域 (在 [系統]  區段下)，然後選取 [感應器]  。
1. 在網域控制器表格清單中的 [網域控制器]  欄中選取篩選選項。 
1. 輸入您要搜尋的名稱。 目前搜尋欄位中不支援萬用字元。 

    ![Azure ATP 搜尋網域控制站](media/search-sensor.png)

> [!NOTE]
> 只有 Azure ATP 系統管理員才可修改 Azure ATP 入口網站設定頁面。


## <a name="see-also"></a>另請參閱

- [Azure ATP 架構](atp-architecture.md)
- [設定 Azure ATP 感應器](install-atp-step5.md)
- [多重樹系支援](atp-multi-forest.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
