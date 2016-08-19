---
title: "變更 ATA 設定 - 網域連線密碼 | Microsoft ATA"
description: "描述如何變更 ATA 閘道上的網域連線密碼。"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 7b8904bcb379004b2038e6b9a14c87c3914f1e1f


---

# 變更 ATA 設定 - 網域連線密碼

>[!div class="step-by-step"]
[« IIS 憑證](modifying-ata-config-iiscert.md)


## 變更網域連線密碼
如果您修改網域連線密碼，請確定輸入的密碼正確。 否則 ATA 閘道服務會停止在 ATA 閘道上執行。

如果您懷疑此情況已發生，請於 ATA 閘道的上的 Microsoft.Tri.Gateway Errors.log 檔案查看下列項目︰
`The supplied credential is invalid.`

若要修正此問題，請遵循此程序來更新 ATA 閘道上的網域連線密碼︰

1.  ATA 閘道上開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [一般]。

    ![ATAA 閘道變更密碼的影像](media/ATA-GW-change-DC-password.JPG)

4.  在 [一般] 下，變更密碼。

5.  按一下 **[儲存]**。

6.  變更密碼後，手動檢查 ATA 閘道服務是否正在 ATA 閘道伺服器上執行。

>[!div class="step-by-step"]
[« IIS 憑證](modifying-ata-config-iiscert.md)

## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


