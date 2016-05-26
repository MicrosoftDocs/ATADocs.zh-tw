---
# required metadata

title: 變更 ATA 設定 - ATA 中心憑證  | Microsoft Advanced Threat Analytics
description: 說明更新或取代 ATA 中心伺服器上本機電腦存放區中憑證的兩階段程序。 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 變更 ATA 設定 - ATA 中心憑證

>[!div class="step-by-step"]
[« ATA 中心伺服器的 IP 位址](modifying-ata-config-centerip.md)
[ATA 主控台 IP 位址 »](modifying-ata-config-consoleip.md)

## 變更 ATA 中心憑證
如果您的憑證過期，且在 ATA 中心伺服器的本機電腦存放區中安裝新憑證後需要更新或更換，請遵循此兩階段程序取代憑證︰

-   第一階段 – 更新您想 ATA 中心服務使用的憑證。 此時 ATA 中心服務仍會繫結至原始憑證。 當 ATA 閘道同步處理其設定時，它們將擁有兩個可有效相互驗證的潛在憑證。 只要 ATA 閘道可以用原始憑證來連接，就不會嘗試新的憑證。

-   第二階段 – 當所有 ATA 閘道與更新的組態同步後，您可以啟動 ATA 中心服務所繫結的新憑證。 當您啟動新憑證時，ATA 中心服務會繫結到憑證。 ATA 閘道將無法正確相互地驗證 ATA 中心服務，並會嘗試驗證第二個憑證。 連接到 ATA 中心服務後，ATA 閘道將提取最新的設定，並為 ATA 中心提供單一憑證。 (除非您已重新啟動此程序。)

> [!NOTE]
> -   如果在第一階段 ATA 閘道已離線且從未取得更新的組態，您需要在 ATA 閘道上手動更新設定的 JSON 檔案。
> -   您使用的憑證必須受 ATA 閘道所信任。
> -   如果您需要在啟用新的憑證後部署新的 ATA 閘道，則需要再次下載 ATA 閘道安裝套件。

1.  開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項，然後選取 [設定].

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [ATA 中心].

4.  在 [憑證]下，選取清單中其中一個憑證。

5.  按一下 [儲存].

6.  您會看到有多少 ATA 閘道已同步到最新設定的通知。

7.  當所有 ATA 閘道同步後，按一下 [啟動] 啟動新的憑證。
    >[!IMPORTANT]
    >啟用新設定之前，請先驗證所有 ATA 閘道均已與最新設定同步。 在所有 ATA 閘道同步之前啟用新設定，可能會導致 ATA 閘道器無法如預期般運作。 如果有任何一個 ATA 閘道尚未同步，當您按一下 [啟用] 時，就會收到此錯誤︰
    >
    >    ![ATA 閘道同步錯誤](media/ataGW-not-synced.png)

8.  啟動變更後，請確定所有 ATA 閘道都能同步處理其設定。

>[!div class="step-by-step"]
[« ATA 中心伺服器的 IP 位址](modifying-ata-config-centerip.md)
[ATA 主控台 IP 位址 »](modifying-ata-config-consoleip.md)

## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


