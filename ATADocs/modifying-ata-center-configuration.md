---
title: "變更 Advanced Threat Analytics ATA 中心設定 | Microsoft Docs"
description: "描述如何變更您 ATA 中心的 IP 位址、連接埠、主控台 URL 或憑證。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/30/2017
---
適用於︰Advanced Threat Analytics 1.8 版



<a id="modifying-the-ata-center-configuration" class="xliff"></a>

# 修改 ATA 中心設定


初始部署後，請小心修改 ATA Center。 更新 IP 位址、連接埠、主控台 URL 和憑證時，請使用下列程序。

<a id="the-ata-center-ip-address" class="xliff"></a>

## ATA 中心 IP 位址

ATA 閘道會在本機儲存它們要連接的 ATA 中心之 IP 位址。 它們會定期連接到 ATA 中心，並提取組態變更。 要變更 ATA 閘道如何連線到 ATA 中心有兩個階段。

-   第一階段 – 更新您想要 ATA 中心服務使用的 IP 位址和連接埠。 此時 ATA 中心仍然在接聽原始 IP 位址，下次 ATA 閘道同步其設定時，ATA 中心將會有兩個 IP 位址。 只要 ATA 閘道可以用原始 (第一) IP 位址來連接，它就不會嘗試新的IP 位址和連接埠。

-   第二階段 – 當所有 ATA 閘道與更新的組態同步後，啟動 ATA 中心所接聽的新 IP 位址和連接埠。 當您啟動新 IP 位址時，ATA 中心服務會繫結到新 IP 位址。 ATA 閘道將無法連接到原始位址，現在將嘗試連線到 ATA 中心的第二個 (新) IP 位址。 以新 IP 位址連接到 ATA 中心後，ATA 閘道將提取最新的設定，並為 ATA 中心提供單一憑證。 (除非您已重新啟動此程序。)

> [!NOTE]
> -   如果在第一階段 ATA 閘道已離線且從未取得更新的組態，您需要在 ATA 閘道上手動更新設定的 JSON 檔案。
> -   如果 ATA 中心伺服器上安裝了新 IP 位址，您可以在進行變更時，從 IP 位址清單中加以選取。 不過，如果基於某些原因無法於 ATA 中心伺服器上安裝 IP 位址，您可以選取自訂的 IP 位址並以手動方式新增。 除非伺服器上已安裝 IP 位址，否則您無法啟動新的 IP 位址。
> -   如果您需要在啟用新的 IP 位址後部署新的 ATA 閘道，您需要再次下載 ATA 閘道安裝套件。

<a id="the-console-url" class="xliff"></a>

## 主控台 URL

在下列情況下將使用 URL：

-   安裝 ATA 閘道 – 安裝 ATA 閘道時，它會在 ATA 中心自行登錄。 此登錄程序透過連接至 ATA 主控台來完成。 如果您對 ATA 主控台 URL 輸入 FQDN，必須確定 ATA 閘道可將 FQDN 解析為 ATA 主控台繫結到的 IP 位址。

-   警示 – 當 ATA 送出 SIEM 或電子郵件警示，它會包含可疑活動的連結。 連結的主機部分是 ATA 主控台的 URL 設定。

-   如果您從內部憑證授權單位 (CA) 安裝了憑證，可能需要將 URL 對應到憑證中的主體名稱；如此一來，使用者連接 ATA 主控台時，不會收到警告訊息。

-   為 ATA 主控台 URL 使用 FQDN，可讓您修改 ATA 主控台所使用的 IP 位址，而不會中斷過去送出的警示，或需要重新下載 ATA 閘道套件。 您只需要使用新的 IP 位址來更新 DNS。

> [!NOTE]
> 修改 ATA 主控台 URL 後，您應該於安裝新的 ATA 閘道前下載 ATA 閘道安裝套件。

<a id="the-ata-center-certificate" class="xliff"></a>

## ATA 中心憑證
如果您的憑證即將過期，且在 ATA 中心伺服器的本機電腦存放區中安裝新憑證後需要更新或更換，請遵循此兩階段程序取代憑證︰

-   第一階段 – 更新您想 ATA 中心服務使用的憑證。 此時 ATA 中心服務仍會繫結至原始憑證。 當 ATA 閘道同步處理其設定時，它們將擁有兩個可有效相互驗證的潛在憑證。 只要 ATA 閘道可以用原始憑證來連接，就不會嘗試新的憑證。

-   第二階段 – 當所有 ATA 閘道與更新的組態同步後，您可以啟動 ATA 中心服務所繫結的新憑證。 當您啟動新憑證時，ATA 中心服務會繫結到憑證。 ATA 閘道將無法正確相互地驗證 ATA 中心服務，並會嘗試驗證第二個憑證。 連接到 ATA 中心服務後，ATA 閘道將提取最新的設定，並為 ATA 中心提供單一憑證。 (除非您已重新啟動此程序。)

> [!NOTE]
> -   如果在第一階段 ATA 閘道已離線且從未取得更新的組態，您需要在 ATA 閘道上手動更新設定的 JSON 檔案。
> -   您使用的憑證必須受 ATA 閘道所信任。
> -   憑證也可用於 ATA 主控台，所以應符合 ATA 主控台位址以避免瀏覽器警告
> -   如果您需要在啟用新的憑證後部署新的 ATA 閘道，則需要再次下載 ATA 閘道安裝套件。

<a id="changing-the-ata-center-configuration" class="xliff"></a>

## 變更 ATA 中心設定

1.  開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.png)

3.  選取 [中心]。

  ![變更 ATA 組態](media/change-center-config.png)

4.  在 [URL] 下，選取 [Add custom DNS name / IP address (新增自訂 DNS 名稱/IP 位址)]，然後選取新的 DNS 或 IP 位址；或在 [憑證] 下，選取新的憑證。

5.  按一下 [儲存]。

6.  您會看到有多少 ATA 閘道已同步到最新設定的通知。

    >[!IMPORTANT]
    >啟用新設定之前，請先驗證所有 ATA 閘道均已與最新設定同步。 在所有 ATA 閘道同步之前啟用新設定，可能會導致 ATA 閘道器無法如預期般運作。 如果有任何一個 ATA 閘道尚未同步，當您按一下 [啟用] 時，就會收到此錯誤︰


7.  當所有 ATA 閘道同步後，按一下 [啟動] 啟動新的 IP 位址或憑證。

    > [!NOTE]
    > 如果您已輸入自訂的 IP 位址，直到您在 ATA 中心上安裝 IP 位址之前，您將無法按 [啟動]。

8.  啟動變更後，請確定所有 ATA 閘道都能同步處理其設定。 通知列會指示有多少 ATA 閘道已順利同步處理其設定。




<a id="see-also" class="xliff"></a>

## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [查看 ATA 論壇！](https://aka.ms/ata-forum)
