---
title: 安裝適用於身分識別的 Microsoft Defender
description: 在安裝適用於身分識別的 Microsoft Defender 的這個步驟中，您會設定資料來源。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7624f2d959e37b2bf88d4b14c31c5a6f1ddd6853
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848222"
---
# <a name="configure-event-collection"></a>設定事件收集

為增強偵測功能，[!INCLUDE [Product long](includes/product-long.md)] 需要列於[設定事件收集](configure-windows-event-collection.md#configure-event-collection)中的 Windows 事件。 [!INCLUDE [Product short](includes/product-short.md)] 感應器可以自動讀取這些事件；如果沒有部署[!INCLUDE [Product short](includes/product-short.md)] 感應器，則有兩種方法可以將其轉送到[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器：一種是將[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器設定為接聽 SIEM 事件，另一種是[設定 Windows 事件轉送](configure-event-forwarding.md)。

> [!NOTE]
>
> - [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不支援收集能針對多種偵測提供資料的 Windows 事件追蹤 (ETW) 記錄項目。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。
> - 在設定事件收集之前，請務必執行[!INCLUDE [Product short](includes/product-short.md)] 稽核指令碼，以確保網域控制站已正確設定為可記錄必要的事件。

除了收集和分析進出網域控制站的網路流量之外，[!INCLUDE [Product short](includes/product-short.md)] 可以使用 Windows 事件進一步加強偵測。 這些事件可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可為[!INCLUDE [Product short](includes/product-short.md)] 提供透過網域控制站網路流量無法取得的額外資訊。

## <a name="ntlm-authentication-using-windows-event-8004"></a>使用 Windows 事件 8004 的 NTLM 驗證

設定 Windows 事件 8004 收集：

1. 瀏覽至：電腦設定\原則\Windows 設定\安全性設定\本機原則\安全性選項
1. 設定 **網域群組原則**，如下所示：
    - 網路安全性：限制 NTLM:限制 NTLM: 送往遠端伺服器的連出 NTLM 流量 = **全部稽核**
    - 網路安全性:限制 NTLM:限制 NTLM: 稽核這個網域的 NTLM 驗證 = **全部啟用**
    - 網路安全性:限制 NTLM:限制 NTLM: 稽核連入 NTLM 流量 = **啟用所有帳戶的稽核**

當 Windows 事件 8004 由[!INCLUDE [Product short](includes/product-short.md)] 感應器剖析時，會使用伺服器存取的資料加強[!INCLUDE [Product short](includes/product-short.md)] NTLM 驗證活動。

## <a name="siemsyslog"></a>SIEM/Syslog

[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器預設已設定為會接收 Syslog 資料。 若要讓[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器能夠取用該資料，您必須將 Syslog 資料轉送至感應器。

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] 只接聽 IPv4，而不會接聽 IPv6。

> [!IMPORTANT]
>
> - 請勿將所有 Syslog 資料都轉送給[!INCLUDE [Product short](includes/product-short.md)] 感應器。
> - [!INCLUDE [Product short](includes/product-short.md)] 支援來自 SIEM/Syslog 伺服器的 UDP 流量。

如需如何設定轉送特定事件到另一部伺服器的資訊，請參閱您的 SIEM/Syslog 伺服器產品的文件。

> [!NOTE]
> 如果您未使用 SIEM/Syslog 伺服器，則可將 Windows 網域控制站設定為轉送所有必要事件以供[!INCLUDE [Product short](includes/product-short.md)] 收集及分析。

## <a name="configuring-the-product-short-sensor-to-listen-for-siem-events"></a>設定[!INCLUDE [Product short](includes/product-short.md)] 感應器以接聽 SIEM 事件

- 將 SIEM 或 Syslog 伺服器設定為轉送所有必要事件至[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器的其中一個 IP 位址。 如需有關如何設定 SIEM 的詳細資訊，請參閱您的 SIEM 線上說明或每部 SIEM 伺服器之特定格式需求的技術支援選項。

[!INCLUDE [Product short](includes/product-short.md)] 支援下列格式的 SIEM 事件：

### <a name="rsa-security-analytics"></a>RSA 安全性分析

&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

- Syslog Header 是選擇性參數。

- 所有欄位之間都必須以 "\n" 字元分隔。
- 欄位依序說明如下︰
    1. RsaSA 常數 (必須出現)。
    2. 實際事件的時間戳記 (請確定其不是抵達 SIEM 或傳送至[!INCLUDE [Product short](includes/product-short.md)] 的時間戳記)。 精確度最好在毫秒以內，這很重要。
    3. Windows 事件識別碼
    4. Windows 事件提供者名稱
    5. Windows 事件記錄檔名稱
    6. 接收事件的電腦名稱 (在此案例中是 DC)
    7. 驗證的使用者名稱
    8. 來源主機名稱
    9. NTLM 的結果碼
- 順序很重要，而且訊息中不應包含任何其他東西。

### <a name="microfocus-arcsight"></a>MicroFocus ArcSight

CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

- 必須符合通訊協定定義。

- 沒有 syslog 標頭。
- 標頭部分 (以管線符號分隔的部分) 必須存在 (如通訊協定中所述)。
- 事件的 _延伸_ 部分必須有下列索引鍵︰
  - externalId = Windows 事件識別碼
  - rt = 實際事件的時間戳記 (請確定其不是抵達 SIEM 或傳送至[!INCLUDE [Product short](includes/product-short.md)] 的時間戳記)。 精確度最好在毫秒以內，這很重要。
  - cat = Windows 事件記錄檔名稱
  - shost = 來源主機名稱
  - dhost = 接收事件的電腦 (在此案例中是 DC)
  - duser = 驗證的使用者
- _延伸_ 部分的順序不重要。
- 這兩個欄位必須是自訂索引鍵和 keyLable：
  - "EventSource"
  - "Reason or Error Code" = NTLM 的結果碼

### <a name="splunk"></a>Splunk

&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

電腦會嘗試驗證帳戶的認證。

驗證套件：MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

登入帳戶：系統管理員

來源工作站：SIEM

錯誤碼：0x0

- Syslog Header 是選擇性參數。

- 所有欄位之間都必須以 "\r\n" 字元分隔。 請注意，這些是控制字元 CRLF (以十六進位表示則為 0D0A)，而不是常值字元。
- 欄位格式是「索引鍵=值」。
- 下列索引鍵必須存在且具有值︰
  - EventCode = Windows 事件識別碼
  - Logfile = Windows 事件記錄檔名稱
  - SourceName = Windows 事件提供者名稱
  - TimeGenerated = 實際事件的時間戳記 (請確定其不是抵達 SIEM 或傳送至[!INCLUDE [Product short](includes/product-short.md)] 的時間戳記)。 必須符合 yyyyMMddHHmmss.FFFFFF 的格式，精確度最好在毫秒以內，這很重要。
  - ComputerName = 來源主機名稱
  - Message = 來自 Windows 事件的原始事件文字
- Message 索引鍵和值必須是最後一個。
- 「索引鍵=值」對的順序不重要。

### <a name="qradar"></a>QRadar

QRadar 可讓您透過代理程式收集事件。 如果使用代理程式收集資料，則會收集不含毫秒資料的時間格式。 因為[!INCLUDE [Product short](includes/product-short.md)] 需要毫秒資料，所以必須將 QRadar 設定為使用無代理程式 Windows 事件收集。 如需詳細資訊，請參閱 [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar：使用 MSRPC 通訊協定的無代理程式 Windows 事件收集") \(英文\)。

```text
<13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0
```

所需欄位如下：

- 用於收集的代理程式類型

- Windows 事件記錄檔提供者名稱
- Windows 事件記錄檔來源
- DC 完整網域名稱
- Windows 事件識別碼

TimeGenerated 是實際事件的時間戳記 (請確定其不是抵達 SIEM 或傳送至[!INCLUDE [Product short](includes/product-short.md)] 的時間戳記)。 必須符合 yyyyMMddHHmmss.FFFFFF 的格式，精確度最好在毫秒以內，這很重要。

Message 是來自 Windows 事件的原始事件文字

確定「索引鍵=值」組之間有 \t。

>[!NOTE]
> 不支援使用 WinCollect 進行 Windows 事件收集。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] SIEM 記錄參考](cef-format-sa.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
