---
title: "變更 ATA 設定 - ATA 主控台 IP 位址 | Microsoft Advanced Threat Analytics"
description: "描述如何變更用來在 ATA 閘道上建立 ATA 主控台捷徑的 ATA 主控台 IP 位址。"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*適用於︰Advanced Threat Analytics 1.7 版*



# 變更 ATA 設定 - ATA 主控台 URL

>[!div class="step-by-step"]
[« ATA 中心憑證](modifying-ata-config-centercert.md)
[網域連線密碼 »](modifying-ata-config-dcpassword.md)

## 變更 ATA 主控台 URL
根據預設，ATA 主控台 URL 是當您安裝 ATA 中心時，為 ATA 主控台 IP 位址所選擇的 IP 位址。

在下列情況下將使用 URL：

-   安裝 ATA 閘道 – 安裝 ATA 閘道時，它會在 ATA 中心自行登錄。 此登錄程序透過連接至 ATA 主控台來完成。 如果您對 ATA 主控台 URL 輸入 FQDN，必須確定 ATA 閘道可將 FQDN 解析為 ATA 主控台繫結到的 IP 位址。

-   警示 – 當 ATA 送出 SIEM 或電子郵件警示，它會包含可疑活動的連結。 連結的主機部分是 ATA 主控台的 URL 設定。

-   如果您從內部憑證授權單位 (CA) 安裝了憑證，可能需要將 URL 對應到憑證中的主體名稱；如此一來，使用者連接 ATA 主控台時，不會收到警告訊息。

-   為 ATA 主控台 URL 使用 FQDN，可讓您修改 ATA 主控台所使用的 IP 位址，而不會中斷過去送出的警示，或需要重新下載 ATA 閘道套件。 您只需要使用新的 IP 位址來更新 DNS。

> [!NOTE]
> 修改 ATA 主控台 URL 後，您應該於安裝新的 ATA 閘道前下載 ATA 閘道安裝套件。

如果您需要修改 ATA 主控台的 URL，請在 ATA 中央伺服器上依照下列步驟。

1.  開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [中心]。

4.  在 [主控台 IP 位址] 下，選取其中一個現有的 IP 位址

5.  在 [主控台 URL] 下，視需要修改 URL：

    ![ATA 主控台 URL](media/ATA-chge-center-URL.png)
6.  按一下 [儲存]。

>[!div class="step-by-step"]
[« ATA 中心憑證](modifying-ata-config-centercert.md)
[網域連線密碼 »](modifying-ata-config-dcpassword.md)


## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->


