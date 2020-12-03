---
title: 安裝 Microsoft Defender 以進行身分識別 VPN 整合
description: 藉由整合 VPN 來收集 Microsoft Defender 身分識別的帳戶處理資訊。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e7c406a198eb78c98c795ba43d9b4076610540c7
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543955"
---
# <a name="integrate-vpn"></a>整合 VPN

[!INCLUDE [Product long](includes/product-long.md)] 可以從 VPN 解決方案收集計量資訊。 設定了 ATA 之後，使用者的設定檔頁面會包含來自 VPN 連線的資訊，例如 IP 位址與連線的原始位置。 這提供使用者活動的額外資訊以及異常 VPN 連線的新增偵測，使調查程序更完整。 將外部 IP 位址解析為位置的呼叫是匿名的。 不會在此呼叫中傳送個人識別資訊。

[!INCLUDE [Product short](includes/product-short.md)] 藉由接聽轉送至感應器的 RADIUS 帳戶處理事件，與您的 VPN 解決方案整合 [!INCLUDE [Product short](includes/product-short.md)] 。 這項機制依據標準 RADIUS 計量 ([RFC 2866](https://tools.ietf.org/html/rfc2866)) 運作，並且支援下列 VPN 廠商：

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>先決條件

若要啟用 VPN 整合，請確定已設定了下列參數：

- 開啟 [!INCLUDE [Product short](includes/product-short.md)] 感應器和/或獨立感應器上的埠 UDP 1813 [!INCLUDE [Product short](includes/product-short.md)] 。

> [!NOTE]
> 藉由啟用 **Radius 帳戶** 處理， [!INCLUDE [Product short](includes/product-short.md)] 感應器將會啟用預先布建的 Windows 防火牆原則（稱為 **[!INCLUDE [Product long](includes/product-long.md)] 感應器**），以允許埠 UDP 1813 上的連入 Radius 帳戶處理。

下列範例會使用 Microsoft 路由及遠端存取伺服器 (RRAS) 來描述 VPN 設定程序。

如果您使用協力廠商 VPN 解決方案，請參考其文件以了解如何啟用 RADIUS 計量的相關指示。

## <a name="configure-radius-accounting-on-the-vpn-system"></a>在 VPN 系統上設定 RADIUS 計量

請在 RRAS 伺服器上執行下列步驟。

1. 開啟路由及遠端存取主控台。
1. 在伺服器名稱上按一下滑鼠右鍵，然後按一下 [屬性]。
1. 在 [安全性] 索引標籤的 [計量提供者] 下，選取 [RADIUS 計量]，然後按一下 [設定]。

    ![RADIUS 設定](media/radius-setup.png)

1. 在 [ **新增 RADIUS 伺服器** ] 視窗中，輸入最接近的感應器 (的 **伺服器名稱** ， [!INCLUDE [Product short](includes/product-short.md)]) 具有網路連線能力。 為了達到高可用性，您可以新增額外 [!INCLUDE [Product short](includes/product-short.md)] 的感應器做為 RADIUS 伺服器。 在 [連接埠] 下，確定已設為預設的 1813。 按一下 [變更]，並鍵入新的共用祕密英數字元字串。 記下新的共用密碼字串，因為您稍後需要在設定期間填寫它 [!INCLUDE [Product short](includes/product-short.md)] 。 選取 [傳送 RADIUS 計量開啟及計量關閉訊息] 方塊，然後在所有已開啟的對話方塊上按一下 [確定]。

    ![VPN 設定](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-product-short"></a>在中設定 VPN [!INCLUDE [Product short](includes/product-short.md)]

[!INCLUDE [Product short](includes/product-short.md)] 收集 VPN 資料，以協助分析電腦連線到網路的位置，以及偵測可疑的 VPN 連線。

若要在中設定 VPN 資料 [!INCLUDE [Product short](includes/product-short.md)] ：

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，按一下 [設定] 齒輪，然後按一下 [ **VPN**]。
1. 開啟 [Radius 帳戶處理]，然後輸入先前在 RRAS VPN 伺服器上設定的 [共用祕密]。 然後按一下 [儲存]。

    ![設定 [！包含 [Product short] (include/product-short. md) ] VPN](media/vpn-radius.png)

啟用此功能之後，所有 [!INCLUDE [Product short](includes/product-short.md)] 感應器都會在埠1813上接聽 RADIUS 帳戶處理事件，而您的 VPN 設定已完成。

 [!INCLUDE [Product short](includes/product-short.md)]感應器收到 VPN 事件並將它們傳送至 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務進行處理之後，實體設定檔將會指出不同的存取 vpn 位置，而設定檔中的活動會指出位置。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
