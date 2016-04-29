---
# required metadata

title: 變更 ATA 組態 - 擷取網路介面卡的名稱 | Microsoft Advanced Threat Analytics
description: 描述如何變更已設定為擷取網路介面卡的網路介面卡的名稱，而不需要結束 ATA 閘道連線
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3225a81e-0395-43ca-9a48-0cbe7171e5de

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 變更 ATA 組態 - 擷取網路介面卡的名稱

>[!div class="step-by-step"]
[« 網域連線密碼](modifying-ata-config-dcpassword.md)

## 變更 ATA 閘道擷取網路介面卡的名稱
如果您變更目前設定為擷取網路介面卡的網路介面卡的名稱，這將導致 ATA 閘道伺服器無法啟動。 為了順利變更名稱，而不需要結束 ATA 閘道連線，請遵循此程序 ︰

1.  在 [ATA 閘道] 組態頁面中，取消選取要重新命名的網路介面卡，然後選取另一張網路介面卡作為其位置的擷取網路介面卡。 這可以是暫時的網路介面卡，甚至是管理網路介面卡。 在此期間，ATA 不會擷取網域控制站的連接埠鏡像流量。 儲存新組態。

2.  在 [ATA 閘道] 上，開啟 [控制台] 並選取 [網路連線] 以重新命名網路介面卡。

3.  然後，回到 ATA 主控台的 [ATA 閘道] 組態頁面。 您可能要重新整理頁面，然後您應會在清單中看到包含新名稱的網路介面卡。 取消選取您在步驟 1 中選取的介面卡，並選取最近命名的介面卡。 最後，儲存新組態。

如果未遵循此程序重新命名網路介面卡，ATA 閘道將無法啟動，且 Microsoft.Tri.Gateway-Errors.log 記錄檔的 ATA 閘道會出現此錯誤。 在下列範例中，**擷取**會是您設定的網路介面卡的原始名稱︰

`Error [NetworkListener] Microsoft.Tri.Infrastructure.ExtendedException: Unavailable network adapters [UnavailableCaptureNetworkAdapterNames=Capture]`

若要修正這個問題，請將網路介面卡重新命名為設定 ATA 時所初次呼叫的名稱，然後進行上述程序以變更名稱。

>[!div class="step-by-step"]
[« 網域連線密碼](modifying-ata-config-dcpassword.md)


## 另請參閱
- [使用 ATA 主控台](/advanced-threat-analytics/understand/working-with-ata-console)
- [安裝 ATA](install-ata.md)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


