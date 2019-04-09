---
title: Azure 進階威脅防護網路名稱解析 | Microsoft Docs
description: 此文章提供 Azure ATP 進階網路名稱解析功能與用法的概觀。
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c985dfc4a7d847113838befb3040931434603a7f
ms.sourcegitcommit: 4072bb8accd439590412f1380694f19aeaaa7a28
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2019
ms.locfileid: "59233168"
---
# <a name="what-is-network-name-resolution"></a>什麼是網路名稱解析？

網路名稱解析 (NNR) 是 Azure ATP 功能的主要元件。 Azure ATP 會以網路流量、Windows 事件與 ETW 來擷取活動 - 這些活動通常包含 IP 資料。  

使用 NNR，Azure ATP 就能在未經處理的活動 (包含 IP 位址)，以及涉及各活動的相關電腦間建立相互關聯。 根據未經處理的活動，Azure ATP 會分析電腦等實體，並針對可疑活動產生安全性警訊。

若要將 IP 位址解析為電腦名稱，ATP 感應器會使用下列其中一種方法查詢 IP 後方之電腦名稱的 IP 位址：

1. 透過 RPC 的 NTLM (TCP 連接埠 135)
2. NetBIOS (UDP 連接埠 137)
3. RDP (TCP 連接埠 3389) - 只有 **Client hello** 的第一個封包
4. 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

> [!NOTE]
>不會在任何連接埠上執行任何驗證。

在擷取電腦名稱之後，Azure ATP 感應器會在 Active Directory 中檢查，以尋找具有該相同電腦名稱的相關電腦物件。 若感應器找到該相互關聯，感應器會將此 IP 與該電腦物件關聯。

如果要偵測下列威脅，NNR 資料可說是不可或缺：

- 可疑的身分識別竊取 (票證傳遞)
- 可疑的 DCSync 攻擊 (目錄服務的複寫)
- 網路對應偵察 (DNS)

為了協助您判斷警示為**確判 (TP)** 或**誤判 (FP)**，Azure ATP 會包含解析至每個安全性警示之辨識項的電腦命名確定度。 
 
例如，當電腦名稱被解析為**高確定度**時，將能提升安全性警示結果為**確判** (**TP**) 的信賴度。 

辨識項會包含時間、IP，以及 IP 所解析至的電腦名稱。 當解析確定度為**低**時，請使用此資訊來調查並確認哪一個裝置是目前 IP 的真正來源。 在確認裝置之後，您便可以判斷該警示是否為**誤判** (**FP**)，類似下列範例：

- 可疑的身分識別竊取 (票證傳遞)：警示是針對相同的電腦觸發。
- 可疑的 DCSync 攻擊 (目錄服務的複寫)：警示是從網域控制站觸發。
- 網路對應偵察 (DNS)：警示是從 DNS 伺服器觸發。

    ![辨識項確定度](media/nnr-high-certainty.png)


### <a name="prerequisites"></a>必要條件
|通訊協定|  傳輸|  Port|   Device| 方向|
|--------|--------|------|-------|------|
|透過 RPC 的 NTLM| TCP |135|   網路上的所有裝置| 輸入|
|NetBIOS|   UDP|    137|    網路上的所有裝置| 輸入|
|DNS|   UDP|    53| 網域控制站| 輸出|
|

當連接埠 3389 在環境中的裝置上開放時，Azure ATP 感應器會將它用於網路名稱解析用途。
開放連接埠 3389 **不是需求**，它只是在該連接埠已針對其他用途開放之情況下可提供電腦名稱的額外方法。

若要確定 Azure ATP 在理想情況下運作且環境已正確設定，Azure ATP 會檢查每個感應器的解析狀態並針對每個方法發出監視警示，提供使用每個方法進行主動式名稱解析成功率低的 Azure ATP 感應器清單。

每個監視警示都提供方法、感應器、有問題支援則與設定建議的特定詳細資料。

![低成功率網路名稱解析 (NNR) 警示](media/atp-nnr-success-rate.png)


### <a name="configuration-recommendations"></a>設定建議

- NTLM 上的 RPC：
    - 檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 135。
    - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。

- NetBIOS：
    - 檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 137。
    - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。
- 反向 DNS：
    - 檢查感應器是否可以連線到 DNS 伺服器，以及是否已啟用反向查閱區域。


## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [設定事件收集](configure-event-collection.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
