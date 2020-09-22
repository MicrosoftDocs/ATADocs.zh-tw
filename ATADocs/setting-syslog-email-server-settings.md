---
title: 在 Advanced 威脅分析中設定電子郵件通知設定
description: 說明當 ATA 偵測到可疑的活動時，如何通知您 (透過電子郵件或 ATA 事件轉寄)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8fe6d1eb34fc651791a84227f64ddee868c2fb97
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912034"
---
# <a name="provide-ata-with-your-email-server-settings"></a>使用電子郵件伺服器設定提供 ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

當 ATA 偵測到可疑的活動時，就會通知您。 若要讓 ATA 能夠傳送電子郵件通知，您必須先進行**電子郵件伺服器設定**。

1. 在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management]**** 圖示。

1. 輸入您的使用者名稱和密碼，然後按一下 [登入]****。

1. 選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.png)

1. 在 [通知]**** 區段中的 [郵件伺服器]**** 下，輸入下列資訊︰


   |              欄位              |                                                                                                 描述                                                                                                  |               值                |
   |---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
   | SMTP 伺服器的端點 (必要) |                                                            輸入您 SMTP 伺服器的 FQDN，並選擇性地變更連接埠號碼 (預設值 25)。                                                            | 例如：<br />smtp.contoso.com |
   |               SSL               |                                              如果 SMTP 伺服器需要 SSL，請切換 SSL。 **注意︰** 如果啟用 SSL，您也需要變更連接埠號碼。                                               |        預設會停用         |
   |         驗證          | 如果您的 SMTP 伺服器需要驗證，請啟用。 **注意︰** 如果啟用驗證，您必須提供有權連線到 SMTP 伺服器的電子郵件帳戶使用者名稱和密碼。 |        預設會停用         |
   |      傳送來源 (必要)       |                                                                        輸入電子郵件傳送者的電子郵件地址。                                                                         | 例如：<br />ATA@contoso.com  |

    ![ATA 電子郵件伺服器設定影像](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>使用 Syslog 伺服器設定提供 ATA
當 ATA 偵測到可疑的活動時，就會將通知傳送至 Syslog 伺服器來通知您。 如果您啟用 Syslog 通知，就可以為其進行下列設定。

1. 設定 Syslog 通知前，請先洽詢您的 SIEM 系統管理員以了解下列資訊︰

   - SIEM 伺服器的 FQDN 或 IP 位址

   - SIEM 伺服器正在接聽的連接埠

   - 應使用的傳輸：UDP、TCP 或 TLS (安全 Syslog)

   - 要用來傳送資料 RFC 3164 或 5424 的格式

1. 在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management]**** 圖示。

1. 輸入您的使用者名稱和密碼，然後按一下 [登入]****。

1. 選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.png)

1. 在 [通知] 區段下，選取 [Syslog 伺服器]****，然後輸入下列資訊：

   |欄位|描述|
   |---------|---------------|
   |Syslog 伺服器端點|Syslog 伺服器的 FQDN，選擇性地變更連接埠號碼 (預設值 514)|
   |傳輸|可以是 UDP、TCP 或 TLS (安全 Syslog)|
   |格式|這是 ATA 用來將事件傳送至 SIEM 伺服器 - RFC 5424 或 RFC 3164 的格式。|

    ![ATA Syslog 伺服器設定影像](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
