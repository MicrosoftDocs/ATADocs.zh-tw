---
# required metadata

title: 變更 ATA 設定 - ATA 中心 IP 位址 | Microsoft Advanced Threat Analytics
description: 描述如何變更 IP 位址、連接埠或您 ATA 中心的憑證。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 變更 ATA 設定 - ATA 中心 IP 位址

>[!div class="step-by-step"]
[ATA 中心憑證 »](modifying-ata-config-centercert.md)

初始部署後，請小心修改 ATA Center。 更新 IP 位址和連接埠或憑證時，請使用下列程序。

## 變更 ATA 中心伺服器所使用的 IP 位址
如果您要變更 ATA 中心 IP 位址和連接埠或憑證，請考量下列事項。

ATA 閘道會在本機儲存它們要連接的 ATA 中心之 IP 位址。 它們會定期連接到 ATA 中心，並提取組態變更。 要變更 ATA 閘道如何連線到 ATA 中心有兩個階段。

-   第一階段 – 更新您想要 ATA 中心服務使用的 IP 位址和連接埠。 此時 ATA 中心仍然在接聽原始 IP 位址，下次 ATA 閘道同步其設定時，ATA 中心將會有兩個 IP 位址。 只要 ATA 閘道可以用原始 (第一) IP 位址來連接，它就不會嘗試新的IP 位址和連接埠。

-   第二階段 – 當所有 ATA 閘道與更新的組態同步後，啟動 ATA 中心所接聽的新 IP 位址和連接埠。 當您啟動新 IP 位址時，ATA 中心服務會繫結到新 IP 位址。 ATA 閘道將無法連接到原始位址，現在將嘗試連線到 ATA 中心的第二個 (新) IP 位址。 以新 IP 位址連接到 ATA 中心後，ATA 閘道將提取最新的設定，並為 ATA 中心提供單一憑證。 (除非您已重新啟動此程序。)

> [!NOTE]
> -   如果在第一階段 ATA 閘道已離線且從未取得更新的組態，您需要在 ATA 閘道上手動更新設定的 JSON 檔案。
> -   如果 ATA 中心伺服器上安裝了新 IP 位址，您可以在進行變更時，從 IP 位址清單中加以選取。 不過，如果基於某些原因無法於 ATA 中心伺服器上安裝 IP 位址，您可以選取自訂的 IP 位址並以手動方式新增。 除非伺服器上已安裝 IP 位址，否則您無法啟動新的 IP 位址。
> -   如果您需要在啟用新的 IP 位址後部署新的 ATA 閘道，您需要再次下載 ATA 閘道安裝套件。

1.  開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項，然後選取 [設定].

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [一般].

4.  在 [ATA 中心服務的 IP 位址: 連接埠] 下，選取其中一個現有的 IP 位址，或選取 [新增自訂 IP 位址] 並輸入 IP 位址。

5.  按一下 [儲存].

6.  您會看到有多少 ATA 閘道已同步到最新設定的通知。

    ![ATA 中心同步處理閘道影像](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >啟用新設定之前，請先驗證所有 ATA 閘道均已與最新設定同步。 在所有 ATA 閘道同步之前啟用新設定，可能會導致 ATA 閘道器無法如預期般運作。 如果有任何一個 ATA 閘道尚未同步，當您按一下 [啟用] 時，就會收到此錯誤︰
    >
    >    ![ATA 閘道同步錯誤](media/ataGW-not-synced.png)


7.  當所有 ATA 閘道同步後，按一下 [啟動] 啟動新的 IP 位址。

    > [!NOTE]
    > 如果您已輸入自訂的 IP 位址，直到您在 ATA 中心上安裝 IP 位址之前，您將無法按 [啟動]。

8.  啟動變更後，請確定所有 ATA 閘道都能同步處理其設定。 通知列會指示有多少 ATA 閘道已順利同步處理其設定。

>[!div class="step-by-step"]
[變更 ATA 中心憑證 »](modifying-ata-config-centercert.md)


## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


