---
# required metadata

title: 變更 ATA 設定 - 網域連線密碼 | Microsoft Advanced Threat Analytics
description: 描述如何變更 ATA 閘道上的網域連線密碼。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 變更 ATA 設定 - 網域連線密碼

>[!div class="step-by-step"]
[« IIS 憑證](modifying-ata-config-iiscert.md)
[擷取網路介面卡名稱 »](modifying-ata-config-nicname.md)

## 變更網域連線密碼
如果您修改網域連線密碼，請確定輸入的密碼正確。 否則 ATA 服務會停止在 ATA 閘道上執行。

如果您懷疑此情況已發生，請於 ATA 閘道的上的 Microsoft.Tri.Gateway Errors.log 檔案查看下列項目︰
`The supplied credential is invalid.`

若要修正此問題，請遵循此程序來更新 ATA 閘道上的網域連線密碼︰

1.  ATA 閘道上開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [ATA 閘道]****。

    ![ATAA 閘道變更密碼的影像](media/ATA-GW-change-DC-password.JPG)

4.  在 [網域連線設定]**** 下變更密碼。

5.  按一下 [儲存] ****。

6.  變更密碼後，手動檢查 ATA 閘道服務是否正在 ATA 閘道伺服器上執行。

>[!div class="step-by-step"]
[« IIS 憑證](modifying-ata-config-iiscert.md)
[擷取網路介面卡名稱 »](modifying-ata-config-nicname.md)

## 另請參閱
- [使用 ATA 主控台](/advanced-threat-analytics/understand/working-with-ata-console)
- [安裝 ATA](install-ata.md)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


