---
title: 適用于身分識別的 Microsoft Defender 實用資源清單
description: 本文提供適用于身分識別的 Microsoft Defender 實用資源清單
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 8a814a51fdc63f59b36288922017280e0d7f3968
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533302"
---
# <a name="microsoft-defender-for-identity-readiness-guide"></a>Microsoft Defender 身分識別就緒指南

本文提供可協助您開始使用的資源就緒藍圖清單 [!INCLUDE [Product long](includes/product-long.md)] 。

## <a name="understanding-microsoft-defender-for-identity"></a>瞭解 Microsoft Defender 的身分識別

[!INCLUDE [Product long](includes/product-long.md)] 是一項雲端服務，可協助您識別及保護您的企業免于多種類型的 advanced 目標網路攻擊和內部威脅。

若要深入瞭解 [!INCLUDE [Product short](includes/product-short.md)]：

- [[!INCLUDE [Product short](includes/product-short.md)] 概述](what-is.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 簡介影片 (25 分鐘) -Full](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [[!INCLUDE [Product short](includes/product-short.md)] 深入探討影片 (75 分鐘) -Full](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>部署決定

[!INCLUDE [Product short](includes/product-short.md)] 是由位於 Azure 中的雲端服務，以及可安裝在網域控制站上的整合式感應器所組成。 若您使用實體伺服器，容量規劃非常重要。 使用調整大小工具來為您的感應器配置空間：

- 重設[ [!INCLUDE [Product short](includes/product-short.md)] 大小工具](https://aka.ms/aatpsizingtool)-調整大小工具會將流量監視的數量自動收集 [!INCLUDE [Product short](includes/product-short.md)] 。 其會自動為感應器提供支援能力以及資源建議。
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規劃指引](capacity-planning.md)

## <a name="deploy-defender-for-identity"></a>部署適用于身分識別的 Defender

使用這些資源可協助您設定 [!INCLUDE [Product short](includes/product-short.md)] 、連線 Active Directory、下載感應器套件、設定事件收集，以及選擇性地與您的 VPN 整合，以及設定 honeytoken 帳戶和排除專案。

- [試用 [!INCLUDE [Product short](includes/product-short.md)] EMS E5 (的一部分) ](https://aka.ms/aatptrial)  試用版的有效期為90天。
- [ [!INCLUDE [Product short](includes/product-short.md)] 設定](install-step1.md)請遵循下列步驟， [!INCLUDE [Product short](includes/product-short.md)] 在您的環境中進行部署。
- [[!INCLUDE [Product short](includes/product-short.md)]與 Microsoft Defender For Endpoint 整合](integrate-mde.md)

## <a name="defender-for-identity-settings"></a>適用于身分識別設定的 Defender

建立實例時 [!INCLUDE [Product short](includes/product-short.md)] ，會自動設定必要的基本設定。 中有數個額外的可設定設定 [!INCLUDE [Product short](includes/product-short.md)] ，可改善您環境的偵測和警示精確度，例如 VPN 整合、SAM 必要許可權，以及 advanced 稽核原則設定。

- [VPN 整合](install-step6-vpn.md)
- [SAM-R 必要權限](install-step8-samr.md)
- [稽核原則設定](configure-windows-event-collection.md) –在部署之前和之後先行審核網域控制站健全狀況 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="work-with-defender-for-identity"></a>使用 Defender 進行身分識別

在 [!INCLUDE [Product short](includes/product-short.md)] 啟動並執行之後，請在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站啟用時間表中查看安全性警示。 啟用時間表是登入入口網站之後的預設登陸頁面 [!INCLUDE [Product short](includes/product-short.md)] 。 根據預設，所有開啟的安全性警訊都會顯示在活動時間軸上。 您也可以查看指派給每個警訊的嚴重性。 向下鑽研實體 (電腦、裝置、使用者) 並開啟具有詳細資訊的設定檔頁面，以調查每個警訊。 橫向移動路徑會顯示可在您網路中進行的潛在移動，以及面臨風險的敏感性使用者。 使用橫向移動路徑偵測圖表來調查及補救公開。 這些資源可協助您處理 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示：

- [ [!INCLUDE [Product short](includes/product-short.md)] 安全性警示指南](suspicious-activity-guide.md)瞭解如何分級並採取您的偵測的後續步驟 [!INCLUDE [Product short](includes/product-short.md)] 。
- [[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑](use-case-lateral-movement-path.md)
- [將群組標記為機密](sensitive-accounts.md)掌握機密安全性群組的認證暴露。

## <a name="security-best-practices"></a>安全性最佳做法

- [ [!INCLUDE [Product short](includes/product-short.md)] 常見問題](technical-faq.yml)-本文提供有關的常見問題清單 [!INCLUDE [Product short](includes/product-short.md)] ，並提供見解和解答。

## <a name="community-resources"></a>社群資源

Blog： [ [!INCLUDE [Product short](includes/product-short.md)] blog](https://aka.ms/aatpblog)

公共團體： [ [!INCLUDE [Product short](includes/product-short.md)] Tech 團體](https://aka.ms/AatpCom)

私人團體： [ [!INCLUDE [Product short](includes/product-short.md)] Yammer 群組](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all&preserve-view=true)

Channel 9：[Microsoft 安全性 Channel 9 頁面](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>另請參閱

- [使用機密帳戶](sensitive-accounts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
