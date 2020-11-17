---
title: 變更 Advanced 威脅分析設定-網域連線密碼
description: 描述如何變更 ATA 閘道上的網域連線密碼。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d310ec8659fcb2fa2a128f24b9b243939dc438eb
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690375"
---
# <a name="change-ata-configuration---domain-connectivity-password"></a>變更 ATA 設定 - 網域連線密碼

[!INCLUDE [Banner for top of topics](includes/banner.md)]

## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼

如果您修改網域連線密碼，請確定輸入的密碼正確。 否則 ATA 閘道服務會停止在 ATA 閘道上執行。

如果您懷疑此情況已發生，請於 ATA 閘道上的 Microsoft.Tri.Gateway Errors.log 檔案查看下列錯誤︰`The supplied credential is invalid.`

若要修正此問題，請遵循此程序來更新 ATA 中心上的網域連線密碼︰

1. 在 ATA 中心上開啟 ATA 主控台。

1. 選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.png)

1. 選取 [目錄服務]。

    ![ATA 閘道變更密碼影像](media/ATA-GW-change-DC-password.png)

1. 在 [密碼] 下，變更密碼。

    如果 ATA 中心有連線到網域，請使用 [測試連線] 按鈕來驗證認證

1. 按一下 [檔案] 。

1. 變更密碼後，手動檢查 ATA 閘道服務是否正在 ATA 閘道伺服器上執行。



## <a name="see-also"></a>另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
