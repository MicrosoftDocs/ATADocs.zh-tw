---
title: 卸載適用于身分識別感應器的 Microsoft Defender
description: 本文說明如何從網域控制站卸載適用于身分識別感應器的 Microsoft Defender。
ms.date: 12/22/2020
ms.topic: how-to
ms.openlocfilehash: 4d93637cabc0169efa0c3d62b4342578c4f006e1
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533336"
---
# <a name="uninstall-the-microsoft-defender-for-identity-sensor"></a>卸載適用于身分識別感應器的 Microsoft Defender

本文說明如何 [!INCLUDE [Product long](includes/product-long.md)] 在下列情況下，從網域控制站卸載感應器：

1. 從網域控制站卸載感應器
1. 移除孤立的感應器
1. 移除重複的感應器

## <a name="uninstall-a-sensor-from-a-domain-controller"></a>從網域控制站卸載感應器

下列步驟說明如何從網域控制站卸載感應器。

1. 使用本機系統管理員許可權登入網域控制站。
1. 在 Windows [**開始**] 功能表中，按一下 [**設定**]  >  **主控台**[  >  **新增/移除程式**]。
1. 選取感應器安裝，按一下 [ **卸載**]，然後依照指示移除感應器。

## <a name="remove-an-orphaned-sensor"></a>移除孤立的感應器

當刪除網域控制站但未先卸載感應器，而感應器仍然出現在入口網站時，就可能發生此情況 [!INCLUDE [Product short](includes/product-short.md)] 。

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，移至 [設定 **]，** 然後在 [ **系統** ] 區段下選取 [ **感應器**]。
1. 找出孤立的感應器，並在資料列的結尾按一下 [ **刪除** ] (垃圾桶圖示) 。

    ![刪除孤立的 [！從感應器頁面包含 [Product short] (include/product-short. md) ] 感應器](media/delete-orphaned-sensor.png)

## <a name="remove-a-duplicate-sensor"></a>移除重複的感應器

此案例可能會在就地感應器升級之後發生，而感應器會在入口網站中出現兩次 [!INCLUDE [Product short](includes/product-short.md)] 。

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，移至 [設定 **]，** 然後在 [ **系統** ] 區段下選取 [ **感應器**]。
1. 找出孤立的感應器，並在資料列的結尾按一下 [ **刪除** ] (垃圾桶圖示) 。

## <a name="see-also"></a>另請參閱

- [以無訊息方式卸載 [!INCLUDE [Product short](includes/product-short.md)] 感應器](silent-installation.md#silently-uninstall-sensor)
