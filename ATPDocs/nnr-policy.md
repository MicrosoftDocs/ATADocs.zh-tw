---
title: Azure 進階威脅防護網路名稱解析
description: 此文章提供 Azure ATP 進階網路名稱解析功能與用法的概觀。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4c98696b11ba329b6b907003b86cc5bd3d111cdf
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912700"
---
# <a name="what-is-network-name-resolution"></a>什麼是網路名稱解析？

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

網路名稱解析 (NNR) 是 Azure ATP 功能的主要元件。 Azure ATP 會以網路流量、Windows 事件與 ETW 來擷取活動 - 這些活動通常包含 IP 資料。

您可以使用 NNR，Azure ATP (包含 IP 位址) 的原始活動，以及與每個活動相關的電腦之間建立關聯。 根據未經處理的活動，Azure ATP 會分析電腦等實體，並針對可疑活動產生安全性警訊。

為將 IP 位址解析成電腦名稱稱，Azure ATP 感應器會使用下列方法來查閱 IP 位址：

- 透過 RPC 的 NTLM (TCP 連接埠 135)
- NetBIOS (UDP 連接埠 137)
- RDP (TCP 連接埠 3389) - 只有 **Client hello** 的第一個封包
- 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

為獲得最佳結果，建議使用所有方法。 如果無法這麼做，您應該使用 DNS 查閱方法與至少一個其他方法。

> [!NOTE]
> 不會在任何連接埠上執行任何驗證。

Azure ATP 會根據網路流量評估及判斷裝置作業系統。 在擷取電腦名稱之後，Azure ATP 感應器會檢查 Active Directory 並使用 TCP 指紋，以尋找具有該相同電腦名稱的相關電腦物件。 使用 TCP 指紋有助於識別未註冊和非 Windows 的裝置，在您的調查過程中提供協助。
當 Azure ATP 感應器找到相互關聯時，感應器會在 IP 與電腦物件之間建立關聯。

在沒有擷取到名稱的情況下，會使用 IP 和偵測到的相關活動建立**無法解析的電腦設定檔 (依 IP)**。

![無法解析的電腦設定檔](media/unresolved-computer-profile.png)

如果要偵測下列威脅，NNR 資料可說是不可或缺：

- 可疑的身分識別竊取 (票證傳遞)
- 可疑的 DCSync 攻擊 (目錄服務的複寫)
- 網路對應偵察 (DNS)

為了協助您判斷警示為**確判 (TP)** 或**誤判 (FP)**，Azure ATP 會包含解析至每個安全性警示之辨識項的電腦命名確定度。

例如，當電腦名稱被解析為**高確定度**時，將能提升安全性警示結果為**確判** (**TP**) 的信賴度。

辨識項會包含時間、IP，以及 IP 所解析至的電腦名稱。 當解析確定度為**低**時，請使用此資訊來調查並確認哪一個裝置是目前 IP 的真正來源。
在確認裝置之後，您便可以判斷該警示是否為**誤判** (**FP**)，類似下列範例：

- 可疑的身分識別竊取 (票證傳遞)：警示是針對相同的電腦觸發。
- 可疑的 DCSync 攻擊 (目錄服務的複寫)：警示是從網域控制站觸發。
- 網路對應偵察 (DNS)：警示是從 DNS 伺服器觸發。

    ![辨識項確定度](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>必要條件

|通訊協定|傳輸|Port|裝置|方向|
|--------|--------|------|-------|------|
|透過 RPC 的 NTLM *|TCP|135|網路上的所有裝置|輸入|
|NetBIOS|UDP|137|網路上的所有裝置|輸入|
|RDP|TCP|3389|網路上的所有裝置|輸入|
|DNS|UDP|53|網域控制站|輸出|

\* 其中一個方法是必要的，但我們建議使用這些方法。

為了確保 Azure ATP 在理想情況下運作，而且環境已正確設定，Azure ATP 會檢查每個感應器的解決狀態，併發出每個方法的健康情況警示，並使用每個方法提供具有低成功率的主動名稱解析的 Azure ATP 感應器清單。

> [!NOTE]
> 若要停用 Azure ATP 中的選擇性 NNR 方法以符合您的環境需求，請開啟支援通話。

每個健康情況警示都會提供方法、感應器、有問題的原則以及設定建議的特定詳細資料。

![低成功率網路名稱解析 (NNR) 警示](media/atp-nnr-success-rate.png)

### <a name="configuration-recommendations"></a>組態建議

- 透過 RPC 的 NTLM：
  - 檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 TCP 135。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。

- NetBIOS：
  - 檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 UDP 137。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。
- Rdp：
  - 檢查是否已開啟 TCP 通訊埠3389，以在環境中的所有電腦上從 Azure ATP 感應器進行輸入通訊。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。
- 反向 DNS：
  - 檢查感應器是否可以連線到 DNS 伺服器，以及是否已啟用反向查閱區域。

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](prerequisites.md)
- [設定事件收集](configure-event-collection.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
