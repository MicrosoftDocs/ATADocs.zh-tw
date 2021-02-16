---
title: 適用于身分識別多重樹系支援的 Microsoft Defender
description: 支援 Microsoft Defender 中的多個 Active Directory 樹系以進行身分識別。
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: c0a5c135d73ecbcdd23b6ed2ea8a12a212a0f23d
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533659"
---
# <a name="microsoft-defender-for-identity-multi-forest-support"></a>適用于身分識別多重樹系支援的 Microsoft Defender

## <a name="multi-forest-support-set-up"></a>設定多重樹系支援

[!INCLUDE [Product long](includes/product-long.md)] 支援具有多個樹系的組織，讓您能夠輕鬆地跨樹系監視活動和分析使用者。

企業組織通常有數個 Active Directory 樹系，通常用於不同用途，包括來自公司合併和收購、地理分佈和安全性界限的舊版基礎結構 (紅色樹系)。 您可以使用保護多個樹系 [!INCLUDE [Product short](includes/product-short.md)] ，讓您能夠透過單一窗格來監視和調查整個網路。

支援多個 Active Directory 樹系的功能可提供以下功能：

- 透過單一管理點來檢視和調查多個樹系中使用者執行的活動。
- 提供了進階 Active Directory 整合和帳戶解析，以改進偵測及減少誤判。
- 更好的控制和更簡單的部署方式。 改進了當您的網域控制站全都從單一主控台監視時，跨組織涵蓋範圍的健康情況警示和報告 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="defender-for-identity-detection-activity-across-multiple-forests"></a>Defender 用於跨多個樹系的身分識別偵測活動

若要偵測跨樹系活動， [!INCLUDE [Product short](includes/product-short.md)] 感應器會查詢遠端樹系中的網域控制站，以建立所有相關實體的設定檔， (包括遠端樹系中的使用者和電腦) 。

- [!INCLUDE [Product short](includes/product-short.md)] 感應器可以安裝在所有樹系的網域控制站上，甚至是沒有信任的樹系。
- 在 [目錄服務] 頁面上新增其他認證，以支援您環境中任何未受信任的樹系。
  - 至少需要一個認證，才能支援具有雙向信任的所有樹系。
  - 只有具有非 Kerberos 信任或無信任的每個樹系都需要額外的認證。
  - 預設限制為每個實例10個不受信任的樹系 [!INCLUDE [Product short](includes/product-short.md)] 。 若您的組織的樹系數目超過 10 個，請連絡客戶支援。

![[!INCLUDE [Product short](includes/product-short.md)] 歡迎階段 1](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>規格需求

- 您在主控台的 [ [!INCLUDE [Product short](includes/product-short.md)] **目錄服務** ] 下設定的使用者必須在所有其他樹系中受信任，而且至少必須有唯讀許可權，才能在網域控制站上執行 LDAP 查詢。
- 如果 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器是安裝在獨立電腦上，而不是直接安裝在網域控制站上，請確定允許電腦使用 LDAP 與所有遠端樹系網域控制站進行通訊。

- 為了 [!INCLUDE [Product short](includes/product-short.md)] 與 [!INCLUDE [Product short](includes/product-short.md)] 感應器和 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器通訊，請在安裝感應器的每部電腦上開啟下列埠 [!INCLUDE [Product short](includes/product-short.md)] ：

  |通訊協定|傳輸|Port|去/從|方向|
  |----|----|----|----|----|
  |**內部連接埠**||||
  |SSL (*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)] 雲端服務|輸出|
  |**內部連接埠**||||
  |LDAP|TCP 和 UDP|389|網域控制站|輸出|
  |安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
  |LDAP 至通用類別|TCP|3268|網域控制站|輸出|
  |LDAPS 至通用類別|TCP|3269|網域控制站|輸出|

## <a name="multi-forest-support-network-traffic-impact"></a>多重樹系支援的網路流量影響

對應您的樹系時 [!INCLUDE [Product short](includes/product-short.md)] ，它會使用會影響下列各項的處理常式：

- [!INCLUDE [Product short](includes/product-short.md)]感應器執行之後，它會查詢遠端 Active Directory 樹系，並取得使用者和機器資料的清單以供建立設定檔。
- 每隔5分鐘，每個感應器都會從 [!INCLUDE [Product short](includes/product-short.md)] 每個樹系的每個網域查詢一個網域控制站，以對應網路中的所有樹系。
- 每個 [!INCLUDE [Product short](includes/product-short.md)] 感應器藉由登入和檢查信任類型，在 Active Directory 中使用 "trustedDomain" 物件來對應樹系。
- 當 [!INCLUDE [Product short](includes/product-short.md)] 感應器偵測到跨樹系活動時，您也可能會看到特定流量。 發生這種情況時， [!INCLUDE [Product short](includes/product-short.md)] 感應器會傳送 LDAP 查詢到相關的網域控制站，以便抓取實體資訊。

## <a name="known-limitations"></a>已知的限制

- 儀表板中不會顯示一個樹系中的使用者在另一個樹系中存取資源所執行的互動式登入 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)
- [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
