---
title: "在 Advanced Threat Analytics 中設定事件收集 | Microsoft Docs"
description: "描述使用 ATA 設定事件收集的選項"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f807b428dfcc12a15b814106cc190f2a72fa4254
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*適用於︰Advanced Threat Analytics 1.6 和 1.7 版*



# <a name="configure-event-collection"></a>設定事件收集
若要增強偵測功能，ATA 需要識別碼為 4776 的 Windows 事件記錄檔。 將這項資訊轉送至 ATA 閘道的方法有兩個：設定 ATA 閘道接聽 SIEM 事件，或[設定 Windows 事件轉送](#configuring-windows-event-forwarding)。

## <a name="event-collection"></a>事件收集
除了收集和分析進出網域控制站的網路流量，ATA 可以使用 Windows 事件 4776 來進一步加強 ATA 的傳遞雜湊偵測。 這可從您的 SIEM 接收，或藉由在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可提供 ATA 透過網域控制站網路流量無法取得的額外資訊。

### <a name="siemsyslog"></a>SIEM/Syslog
為了讓 ATA 可以取用 Syslog 伺服器上的資料，您需要執行下列操作︰

-   將您的 ATA 閘道伺服器設定為接聽及接受從 SIEM/Syslog 伺服器轉送的事件。
> [!NOTE]
> ATA 只接聽 IPv4，而不會接聽 IPv6。 
-   將您的 SIEM/Syslog 伺服器設定為轉送特定事件至 ATA 閘道。

> [!IMPORTANT]
> -   請勿將所有 Syslog 資料都轉送給 ATA 閘道。
> -   ATA 支援來自 SIEM/Syslog 伺服器的 UDP 流量。

如需如何設定轉送特定事件到另一部伺服器的資訊，請參閱您的 SIEM/Syslog 伺服器產品的文件。 

### <a name="windows-event-forwarding"></a>Windows 事件轉送
如果您沒使用 SIEM/Syslog 伺服器，可將 Windows 網域控制站設定為轉送 Windows 事件識別碼 4776 以供 ATA 收集及分析。 Windows 事件識別碼 4776 提供 NTLM 驗證的相關資料。

## <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>將 ATA 閘道設定為接聽 SIEM 事件

1.  在 ATA 設定中，在 [事件] 索引標籤下啟用 **Syslog**，然後按 [儲存]。

    ![啟用 Syslog 接聽程式 UDP 映像](media/ATA-enable-siem-forward-events.png)

2.  將 SIEM 或 Syslog 伺服器設定為轉送 Windows 事件識別碼 4776 給其中一個 ATA 閘道的 IP 位址。 如需有關如何設定 SIEM 的詳細資訊，請參閱您的 SIEM 線上說明或每部 SIEM 伺服器的特定格式需求的技術支援選項。

### <a name="siem-support"></a>SIEM 支援
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

## <a name="configuring-windows-event-forwarding"></a>設定 Windows 事件轉送

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>具連接埠鏡像之 ATA 閘道的 WEF 設定

設定從網域控制站鏡像連接埠到 ATA 閘道之後，請依照下面的指示使用來源起始組態來設定 Windows 事件轉送。 這是一個設定 Windows 事件轉送的方法。 

**步驟 1︰新增網路服務帳戶到網域 Event Log Readers 群組。** 

在此案例中，我們假設 ATA 閘道是網域的成員。

1.    開啟「Active Directory 使用者和電腦」，瀏覽至 [BuiltIn] 資料夾，然後按兩下 [Event Log Readers] 群組。 
2.    選取 [成員]。
4.    如果未列出 [Network Service]，請按一下 [新增]，在 [輸入要選取的物件名稱] 欄位中輸入 **Network Service**。 然後按一下 [檢查名稱]，再按兩次 [確定]。 

請注意，在將 [網路服務] 新增到 [Event Log Readers] 群組後，您必須重新啟動網域控制站，變更才會生效。

**步驟 2︰在網域控制站上建立原則以設定 [設定目標訂閱管理員] 設定。** 
> [!Note] 
> 您可以建立這些設定的群組原則，並將群組原則套用到 ATA 閘道監視的每個網域控制站。 下面的步驟修改網域控制站的本機原則。     

1.    在每個網域控制站上執行下列命令︰*winrm quickconfig*
2.  在命令提示字元中輸入 *gpedit.msc*
3.    展開 [電腦設定] > [系統管理範本] > [Windows 元件] > [事件轉送]

 ![本機原則群組編輯器影像](media/wef 1 local group policy editor.png)

4.    按兩下 [設定目標訂閱管理員]。
   
    1.    選取 [啟用]。
    2.    在 [選項] 下，按一下 [顯示]。
    3.    在 [SubscriptionManagers] 下，輸入下列值，然後按一下 [確定]：    *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (例如：Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![設定目標訂閱影像](media/wef 2 config target sub manager.png)
   
    5.    按一下 [ **確定**]。
    6.    在提升權限的命令提示字元中，輸入 *gpupdate /force*。 

**步驟 3：在 ATA 閘道上執行下列步驟** 

1.    開啟提升權限的命令提示字元，輸入 *wecutil qc*
2.    開啟 [事件檢視器]。 
3.    以滑鼠右鍵按一下 [訂閱]，然後選取 [建立訂閱]。 

   1.    為訂閱輸入名稱和描述。 
   2.    對於 [目的記錄檔]確認已選取 [轉送的事件]。 對於要讀取事件的 ATA，目的記錄檔必須是 [轉送的事件]。 
   3.    選取 [來源電腦起始]，按一下 [選取電腦群組]。
        1.    按一下 [加入網域電腦]。
        2.    在 [輸入要選取的物件名稱] 欄位中輸入網域控制站的名稱。 然後按一下 [檢查名稱]，再按一下 [確定]。 
       
        ![事件檢視器影像](media/wef3 event viewer.png)
   
        
        3.    按一下 [ **確定**]。
   4.    按一下 [選取事件]。

        1. 按一下 [依記錄]，然後選取 [安全性]。
        2. 在 [包含/排除事件識別碼] 欄位中輸入 **4776**，然後按一下 [確定]。 

 ![查詢篩選影像](media/wef 4 query filter.png)

   5.    以滑鼠右鍵按一下建立的訂閱，然後選取 [執行階段狀態]，查看是否有任何問題及其狀態。 
   6.    稍候幾分鐘之後，請查看事件 4776 出現在 ATA 閘道上 [轉送的事件] 中。


### <a name="wef-configuration-for-the-ata-lightweight-gateway"></a>ATA 輕量型閘道的 WEF 設定
當您在網域控制站上安裝 ATA 輕量型閘道時，可以設定網域控制站將事件轉送給自己。 執行下列步驟來設定使用 ATA 輕量型閘道時的 Windows 事件轉送。 這是一個設定 Windows 事件轉送的方法。  

**步驟 1︰新增網路服務帳戶到網域 Event Log Readers 群組** 

1.    開啟「Active Directory 使用者和電腦」，瀏覽至 [BuiltIn] 資料夾，然後按兩下 [Event Log Readers] 群組。 
2.    選取 [成員]。
3.    如果未列出 [Network Service]，請按一下 [新增]，在 [輸入要選取的物件名稱] 欄位中輸入 **Network Service**。 然後按一下 [檢查名稱]，再按兩次 [確定]。 

**步驟 2︰安裝 ATA 輕量型閘道之後在網域控制站上執行下列步驟** 

1.    開啟提升權限的命令提示字元，輸入 *winrm quickconfig* 和 *wecutil qc* 
2.    開啟 [事件檢視器]。 
3.    以滑鼠右鍵按一下 [訂閱]，然後選取 [建立訂閱]。 

   1.    為訂閱輸入名稱和描述。 
   2.    對於 [目的記錄檔]確認已選取 [轉送的事件]。 對於要讀取事件的 ATA，目的記錄檔必須是 [轉送的事件]。

        1.    選取 [收集器起始]，按一下 [選取電腦]。 然後按一下 [加入網域電腦]。
        2.    在 [輸入要選取的物件名稱] 中輸入網域控制站的名稱。 然後按一下 [檢查名稱]，再按一下 [確定]。

            ![訂閱屬性影像](media/wef 5 sub properties computers.png)

        3.    按一下 [ **確定**]。
   3.    按一下 [選取事件]。

        1.    按一下 [依記錄]，然後選取 [安全性]。
        2.    在 [包含/排除事件識別碼] 中輸入 *4776*，然後按一下 [確定]。 

![查詢篩選影像](media/wef 4 query filter.png)


  4.    以滑鼠右鍵按一下建立的訂閱，然後選取 [執行階段狀態]，查看是否有任何問題及其狀態。 

> [!Note] 
> 您可能需要重新啟動網域控制站，設定才會生效。 

稍候幾分鐘之後，請查看事件 4776 出現在 ATA 閘道上 [轉送的事件] 中。



如需詳細資訊，請參閱[設定電腦轉送及收集事件](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>另請參閱
- [安裝 ATA](install-ata-step1.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
