---
# required metadata

title: 變更 ATA 設定 - ATA 主控台 IP 位址 | Microsoft Advanced Threat Analytics
description: 描述如何變更用來在 ATA 閘道上建立 ATA 主控台捷徑的 ATA 主控台 IP 位址。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 變更 ATA 設定 - ATA 主控台 IP 位址

>[!div class="step-by-step"]
[« ATA 中心憑證](modifying-ata-config-centercert.md)
[IIS 憑證 »](modifying-ata-config-iiscert.md)

## 變更 ATA 主控台 IP 位址
根據預設，ATA 主控台 URL 是當您安裝 ATA 中心時，為 ATA 主控台 IP 位址所選擇的 IP 位址。

在下列情況下將使用 URL：

-   安裝 ATA 閘道 – 安裝 ATA 閘道時，它會在 ATA 中心自行登錄。 此登錄程序透過連接至 ATA 主控台來完成。 如果您對 ATA 主控台 URL 輸入 FQDN，必須確定 ATA 閘道可將 FQDN 解析為 ATA 主控台在 IIS 繫結到的 IP 位址。 此外，此 URL 是用來建立 ATA 閘道上 ATA 主控台的捷徑。

-   警示 – 當 ATA 送出 SIEM 或電子郵件警示，它會包含可疑活動的連結。 連結的主機部分是 ATA 主控台的 URL 設定。

-   如果您從內部憑證授權單位 (CA) 安裝了憑證，可能需要將 URL 對應到憑證中的主體名稱；如此一來，使用者連接 ATA 主控台時，不會收到警告訊息。

-   為 ATA 主控台 URL 使用 FQDN，可讓您修改 IIS 為 ATA 主控台所使用的 IP 位址，而不會中斷過去送出的警示，或需要重新下載 ATA 閘道套件。 您只需要使用新的 IP 位址來更新 DNS。

> [!NOTE]
> 修改 ATA 主控台 URL 後，您應該於安裝新的 ATA 閘道前下載 ATA 閘道安裝套件。

如果您需要修改 IIS 為 ATA 主控台所使用的 IP 位址，請遵循下列 ATA 中央伺服器上的步驟。

1.  在 ATA 中心伺服器上安裝 IP 位址。

2.  開啟 Internet Information Services (IIS) 管理員。

3.  展開伺服器名稱，然後展開 [網站].

4.  選取 Microsoft ATA 主控台的網站，在 [動作] 窗格中按一下 [繫結].

    ![ATA 主控台繫結動作影像](media/ATA-console-change-IP-bindings.jpg)

5.  選取 [HTTP] 並按一下 [編輯] 以選取新的 IP 位址。 選取相同的 IP 位址並對 **HTTPS** 執行相同動作。

    ![編輯網站繫結影像](media/ATA-change-console-IP.jpg)

6.  在 [動作] 窗格中，按一下 [管理網站] 下的 [重新啟動].

7.  開啟系統管理員命令提示字元，並輸入下列命令來更新 HTTP.SYS 驅動程式︰

    -   若要新增新 IP 位址 - `netsh http add iplisten ipaddress=newipaddress`

    -   若要查看新位址是否正在使用 - `netsh http show iplisten`

    -   若要刪除舊 IP 位址 - `netsh http delete iplisten ipaddress=oldipaddress`

8.  如果 ATA 主控台 URL 仍在使用 IP 位址，請於部署新的 ATA 閘道器前，先將 ATA 主控台 URL 更新至新的 IP 位址，並下載 ATA 閘道安裝套件。

9. 如果 ATA 主控台 URL 是 FQDN，請使用 FQDN 的新 IP 位址來更新 DNS。

>[!div class="step-by-step"]
[« ATA 中心憑證](modifying-ata-config-centercert.md)
[IIS 憑證 »](modifying-ata-config-iiscert.md)


## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


