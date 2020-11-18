---
title: 用於識別網路名稱解析的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別的 Advanced Network Name 解析功能和用途。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9b9688031ea9916a09b8beaa2ce5c67633fd935f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847236"
---
# <a name="what-is-network-name-resolution"></a>什麼是網路名稱解析？

網路名稱解析 (NNR) 是功能的主要元件  [!INCLUDE [Product long](includes/product-long.md)] 。 [!INCLUDE [Product short](includes/product-short.md)] 根據網路流量、Windows 事件和 ETW 來捕獲活動-這些活動通常包含 IP 資料。

您可以使用 NNR， [!INCLUDE [Product short](includes/product-short.md)] (包含 IP 位址) 的原始活動，以及每個活動相關的電腦之間相互關聯。 根據未經處理的活動， [!INCLUDE [Product short](includes/product-short.md)] 分析實體（包括電腦），並產生可疑活動的安全性警示。

為將 IP 位址解析成電腦名稱，[!INCLUDE [Product short](includes/product-short.md)] 感應器會使用下列方法來查閱 IP 位址：

- 透過 RPC 的 NTLM (TCP 連接埠 135)
- NetBIOS (UDP 連接埠 137)
- RDP (TCP 連接埠 3389) - 只有 **Client hello** 的第一個封包
- 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

為獲得最佳結果，建議使用所有方法。 如果無法這麼做，您應該使用 DNS 查閱方法與至少一個其他方法。

> [!NOTE]
> 不會在任何連接埠上執行任何驗證。

[!INCLUDE [Product short](includes/product-short.md)] 根據網路流量評估並決定裝置作業系統。 在抓取電腦名稱稱之後， [!INCLUDE [Product short](includes/product-short.md)] 感應器會檢查 Active Directory 並使用 TCP 指紋來查看是否有相關聯的電腦物件具有相同的電腦名稱稱。 使用 TCP 指紋有助於識別未註冊和非 Windows 的裝置，在您的調查過程中提供協助。
當 [!INCLUDE [Product short](includes/product-short.md)] 感應器找到相互關聯時，感應器會將 IP 與電腦物件產生關聯。

在沒有擷取到名稱的情況下，會使用 IP 和偵測到的相關活動建立 **無法解析的電腦設定檔 (依 IP)**。

![無法解析的電腦設定檔](media/unresolved-computer-profile.png)

如果要偵測下列威脅，NNR 資料可說是不可或缺：

- 可疑的身分識別竊取 (票證傳遞)
- 可疑的 DCSync 攻擊 (目錄服務的複寫)
- 網路對應偵察 (DNS)

若要改善您判斷警示是否為 **真肯定 (TP)** 或 **假正面 (FP)** 的能力，可將 [!INCLUDE [Product short](includes/product-short.md)] 電腦名稱稱的確定性程度解析為每個安全性警示的辨識項。

例如，當電腦名稱被解析為 **高確定度** 時，將能提升安全性警示結果為 **確判** (**TP**) 的信賴度。

辨識項會包含時間、IP，以及 IP 所解析至的電腦名稱。 當解析確定度為 **低** 時，請使用此資訊來調查並確認哪一個裝置是目前 IP 的真正來源。
在確認裝置之後，您便可以判斷該警示是否為 **誤判** (**FP**)，類似下列範例：

- 可疑的身分識別竊取 (票證傳遞)：警示是針對相同的電腦觸發。
- 可疑的 DCSync 攻擊 (目錄服務的複寫)：警示是從網域控制站觸發。
- 網路對應偵察 (DNS)：警示是從 DNS 伺服器觸發。

    ![辨識項確定度](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>先決條件

|通訊協定|傳輸|Port|裝置|方向|
|--------|--------|------|-------|------|
|透過 RPC 的 NTLM *|TCP|135|網路上的所有裝置|輸入|
|NetBIOS|UDP|137|網路上的所有裝置|輸入|
|RDP|TCP|3389|網路上的所有裝置|輸入|
|DNS|UDP|53|網域控制站|輸出|

\* 其中一個方法是必要的，但我們建議使用這些方法。

為了確保 [!INCLUDE [Product short](includes/product-short.md)] 在理想情況下運作且環境已正確設定，請 [!INCLUDE [Product short](includes/product-short.md)] 檢查每個感應器的解決狀態，併發出每個方法的健康情況警示，並 [!INCLUDE [Product short](includes/product-short.md)] 使用每個方法提供具有低成功率的活動名稱解析的感應器清單。

> [!NOTE]
> 若要在中停用選擇性的 NNR 方法 [!INCLUDE [Product short](includes/product-short.md)] ，以符合您的環境需求，請開啟支援電話。

每個健康情況警示都會提供方法、感應器、有問題的原則以及設定建議的特定詳細資料。

![低成功率網路名稱解析 (NNR) 警示](media/nnr-success-rate.png)

### <a name="configuration-recommendations"></a>組態建議

- 透過 RPC 的 NTLM：
  - 檢查是否已 [!INCLUDE [Product short](includes/product-short.md)] 在環境中的所有電腦上，針對來自感應器的輸入通訊開啟 TCP 通訊埠135。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。

- NetBIOS：
  - 檢查是否已在 [!INCLUDE [Product short](includes/product-short.md)] 環境中的所有電腦上開啟 UDP 埠137以進行來自感應器的輸入通訊。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。
- Rdp：
  - 檢查是否已 [!INCLUDE [Product short](includes/product-short.md)] 在環境中的所有電腦上，針對來自感應器的輸入通訊開啟 TCP 通訊埠3389。
  - 檢查所有網路設定 (防火牆)，因為這可能會導致無法與相關通訊埠通訊。
- 反向 DNS：
  - 檢查感應器是否可以連線到 DNS 伺服器，以及是否已啟用反向查閱區域。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [設定事件收集](configure-event-collection.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
