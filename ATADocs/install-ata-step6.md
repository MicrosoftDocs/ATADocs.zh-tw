---
title: "安裝 Advanced Threat Analytics - 步驟 6 | Microsoft Docs"
description: "在安裝 ATA 的這個步驟中，您要設定資料來源。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ac591d960028268f6c1ebd74706839a3b91597da
ms.sourcegitcommit: 9ce330726e5de8c05eae6a20d3e6c1d8bef3cd0e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
*適用於︰Advanced Threat Analytics 1.8 版*



# <a name="install-ata---step-6"></a>安裝 ATA - 步驟 6

>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)

## <a name="step-6-configure-event-collection-and-vpn"></a>步驟 6： 設定事件收集和 VPN
### <a name="configure-event-collection"></a>設定事件收集
為增強偵測功能，ATA 需要下列 Windows 事件：4776、4732、4733、4728、4729、4756、4757。 這些事件可透過 ATA 輕量型閘道自動讀取；如果未部署 ATA 輕量型閘道，則可以透過下列兩個方式之一轉送至 ATA 閘道：藉由將 ATA 閘道設定為接聽 SIEM 事件，或藉由[設定 Windows 事件轉送](configure-event-collection.md)。

> [!NOTE]
> 針對 ATA 1.8 版及更新版本，ATA 輕量型閘道不再需要事件收集設定。 ATA 輕量型閘道現在可以在本機讀取事件，而不需要設定事件轉送。

除了收集和分析進出網域控制站的網路流量，ATA 可以使用 Windows 事件進一步加強偵測。 它會使用加強各種偵測的 NTLM 事件 4776，以及增強偵測機密群組修改的事件 4732、4733、4728、4729、4756 和 4757。 這可從您的 SIEM 接收，或藉由在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可提供 ATA 透過網域控制站網路流量無法取得的額外資訊。

#### <a name="siemsyslog"></a>SIEM/Syslog
為了讓 ATA 可以取用 Syslog 伺服器上的資料，您需要執行下列操作︰

-   將您的 ATA 閘道伺服器設定為接聽及接受從 SIEM/Syslog 伺服器轉送的事件。
> [!NOTE]
> ATA 只接聽 IPv4，而不會接聽 IPv6。 
-   將您的 SIEM/Syslog 伺服器設定為轉送特定事件至 ATA 閘道。

> [!IMPORTANT]
> -   請勿將所有 Syslog 資料都轉送給 ATA 閘道。
> -   ATA 支援來自 SIEM/Syslog 伺服器的 UDP 流量。

如需如何設定轉送特定事件到另一部伺服器的資訊，請參閱您的 SIEM/Syslog 伺服器產品的文件。 

> [!NOTE]
>如果您沒使用 SIEM/Syslog 伺服器，可將 Windows 網域控制站設定為轉送 Windows 事件識別碼 4776 以供 ATA 收集及分析。 Windows 事件識別碼 4776 提供 NTLM 驗證的相關資料。

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>將 ATA 閘道設定為接聽 SIEM 事件

1.  在 ATA 組態中，按一下 [資料來源] 下的 [SIEM]，開啟 [Syslog]，然後按一下 [儲存]。

    ![啟用 Syslog 接聽程式 UDP 映像](media/ATA-enable-siem-forward-events.png)

2.  將 SIEM 或 Syslog 伺服器設定為轉送 Windows 事件識別碼 4776 給其中一個 ATA 閘道的 IP 位址。 如需有關如何設定 SIEM 的詳細資訊，請參閱您的 SIEM 線上說明或每部 SIEM 伺服器的特定格式需求的技術支援選項。

ATA 支援下列格式的 SIEM 事件：  

#### <a name="rsa-security-analytics"></a>RSA 安全性分析
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog Header 是選擇性參數。

-   所有的欄位之間需以 "\n" 字元分隔。

-   欄位依序說明如下︰

    1.  RsaSA 常數 (必須出現)。

    2.  實際事件的時間戳記 (請確定它不是抵達 SIEM 傳送至 ATA 的時間戳記)。 精確度最好在毫秒以內，這非常重要。

    3.  Windows 事件識別碼

    4.  Windows 事件提供者名稱

    5.  Windows 事件記錄檔名稱

    6.  接收事件的電腦名稱 (在此案例中是 DC)

    7.  驗證的使用者名稱

    8.  來源主機名稱

    9. NTLM 的結果碼

-   順序很重要，而且訊息中不應包含任何其他東西。

#### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   必須符合通訊協定定義。

-   沒有 syslog 標頭。

-   標頭部分 (以管線符號分隔的部分) 必須存在 (如通訊協定中所述)。

-   事件的_延伸_部分必須有下列索引鍵︰

    -   externalId = Windows 事件識別碼

    -   rt = 實際事件的時間戳記 (請確定它不是抵達 SIEM 傳送給我們的時間戳記)。 精確度最好在毫秒以內，這非常重要。

    -   cat = Windows 事件記錄檔名稱

    -   shost = 來源主機名稱

    -   dhost = 接收事件的電腦 (在此案例中是 DC)

    -   duser = 驗證的使用者

-   _延伸_部分的順序不重要。

-   這兩個欄位必須是自訂索引鍵和 keyLable：

    -   “EventSource”

    -   “Reason or Error Code” = NTLM 的結果碼

#### <a name="splunk"></a>Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

電腦會嘗試驗證帳戶的認證。

驗證封裝：              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

登入帳戶：Administrator

來源工作站：       SIEM

錯誤碼：         0x0

-   Syslog Header 是選擇性參數。

-   所有欄位之間需以 “\r\n” 字元分隔。

-   欄位格式是「索引鍵=值」。

-   下列索引鍵必須存在而且有一個值︰

    -   EventCode = Windows 事件識別碼

    -   Logfile = Windows 事件記錄檔名稱

    -   SourceName = Windows 事件提供者名稱

    -   TimeGenerated = 實際事件的時間戳記 (請確定它不是抵達 SIEM 傳送至 ATA 的時間戳記)。 必須符合 yyyyMMddHHmmss.FFFFFF 的格式，精確度最好在毫秒以內，這非常重要。

    -   ComputerName = 來源主機名稱

    -   Message = 來自 Windows 事件的原始事件文字

-   Message 索引鍵和值必須是最後一個。

-   「索引鍵=值」對的順序不重要。

#### <a name="qradar"></a>QRadar
QRadar 可讓您透過代理程式收集事件。 如果使用代理程式收集資料，則會收集不含毫秒資料的時間格式。 因為 ATA 需要毫秒資料，所以必須將 QRadar 設定為使用無代理程式 Windows 事件收集。 如需詳細資訊，請參閱 [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol")。

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

所需欄位如下：

- 用於收集的代理程式類型
- Windows 事件記錄檔提供者名稱
- Windows 事件記錄檔來源
- DC 完整網域名稱
- Windows 事件識別碼

TimeGenerated 是實際事件的時間戳記 (請確定它不是抵達 SIEM 或傳送至 ATA 的時間戳記)。 必須符合 yyyyMMddHHmmss.FFFFFF 的格式，精確度最好在毫秒以內，這非常重要。

Message 是來自 Windows 事件的原始事件文字

確定「索引鍵=值」組之間有 \t。

>[!NOTE] 
> 不支援使用 WinCollect 進行 Windows 事件收集。


### <a name="configuring-vpn"></a>設定 VPN

ATA 會收集 VPN 資料，以協助分析電腦連線到網路的位置。

若要設定 VPN 資料，請移至 [組態] > [VPN]，然後輸入 VPN 的 **Radius 帳戶共用密碼**。

![設定 VPN](./media/vpn.png)

請參閱 VPN 文件以取得共用密碼。 支援的 VPN 廠商如下：

- Microsoft
- F5
- Check Point
- Cisco ASA



>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)
[步驟 7 »](install-ata-step7.md)



## <a name="related-videos"></a>相關影片
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

