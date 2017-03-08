---
title: "變更 Advanced Threat Analytics 設定 - 網域連線密碼 | Microsoft Docs"
description: "描述如何變更 ATA 閘道上的網域連線密碼。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e9cb7bcf6f32559f7b2f330df4333c3fdc55a283
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
適用於︰Advanced Threat Analytics 1.7 版



# <a name="change-ata-configuration---domain-connectivity-password"></a>變更 ATA 設定 - 網域連線密碼

>[!div class="step-by-step"]
[« ATA 主控台 URL](modifying-ata-config-consoleurl.md)


## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼
如果您修改網域連線密碼，請確定輸入的密碼正確。 否則 ATA 閘道服務會停止在 ATA 閘道上執行。

如果您懷疑此情況已發生，請於 ATA 閘道上的 Microsoft.Tri.Gateway Errors.log 檔案查看下列項目︰`The supplied credential is invalid.`

若要修正此問題，請遵循此程序來更新 ATA 中心上的網域連線密碼︰

1.  在 ATA 中心上開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [目錄服務]。

    ![ATAA 閘道變更密碼的影像](media/ATA-GW-change-DC-password.png)

4.  在 [密碼] 下，變更密碼。

    如果 ATA 中心有連線到網域，請使用 [測試連線] 按鈕來驗證認證

5.  按一下 [儲存]。

6.  變更密碼後，手動檢查 ATA 閘道服務是否正在 ATA 閘道伺服器上執行。

>[!div class="step-by-step"]
[« ATA 主控台 URL](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
