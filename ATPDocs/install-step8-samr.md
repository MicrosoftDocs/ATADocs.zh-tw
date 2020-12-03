---
title: 設定 SAM-R 以在 Microsoft Defender 中針對身分識別啟用橫向移動路徑偵測
description: 說明如何設定 Microsoft Defender 以進行身分識別，以對 SAM 進行遠端呼叫
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 24c1d6baf99e3d65a96897d2d0b90ffe94ad42eb
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543938"
---
# <a name="configure-product-long-to-make-remote-calls-to-sam"></a>設定[!INCLUDE [Product long](includes/product-long.md)] 以對 SAM 發出遠端呼叫

[!INCLUDE [Product long](includes/product-long.md)][橫向移動路徑](use-case-lateral-movement-path.md)偵測依賴于識別特定電腦上本機系統管理員的查詢。 這些查詢是使用 SAM-R 通訊協定執行，並使用在 [!INCLUDE [Product short](includes/product-short.md)] [!INCLUDE [Product short](includes/product-short.md)] 安裝步驟2期間建立的服務帳戶  [。連接到 AD](install-step2.md)。

## <a name="configure-sam-r-required-permissions"></a>設定 SAM-R 所需的權限

若要確保 Windows 用戶端和伺服器允許您 [!INCLUDE [Product short](includes/product-short.md)] 的帳戶執行 SAM-R， **Group Policy** [!INCLUDE [Product short](includes/product-short.md)] 除了 **網路存取** 原則中列出的已設定帳戶之外，還必須修改群組原則，才能新增服務帳戶。 請務必將群組原則套用到 **網域控制站以外** 的所有電腦。

> [!Note]
> 在施行此類新原則之前，請務必確認您環境的安全，以及任何變更都不會影響應用程式的相容性。 若要這麼做，請先予以啟用，然後以稽核模式驗證建議變更的相容性，再對您的實際執行環境做出變更。

1. 找出原則：

   - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
   - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項

    ![找出原則](media/samr-policy-location.png)

1. 將 [!INCLUDE [Product short](includes/product-short.md)] 服務新增至可在新式 Windows 系統上執行此動作的核准帳戶清單。

    ![新增服務](media/samr-add-service.png)

3. **AATP service** (在 [!INCLUDE [Product short](includes/product-short.md)] 安裝期間建立的服務) 現在具有在環境中執行 SAM 的必要許可權。

如需 SAM-R 和此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(部分為機器翻譯\)。

## <a name="see-also"></a>另請參閱

- [調查橫向移動路徑攻擊 [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
