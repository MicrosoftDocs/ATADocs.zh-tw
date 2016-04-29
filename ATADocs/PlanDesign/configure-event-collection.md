---
# required metadata

title: 設定事件收集 | Microsoft Advanced Threat Analytics
description: 描述使用 ATA 設定事件收集的選項
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定事件收集
若要增強 ATA 對傳遞雜湊攻擊的偵測，ATA 需要識別碼為 4776 的 Windows 事件記錄檔。 將這項資訊轉送至 ATA 閘道的方法有兩個：設定 ATA 閘道接聽 SIEM 事件，或[設定 Windows 事件轉送](#configuring-windows-event-forwarding)。

## 事件收集
除了收集和分析進出網域控制站的網路流量，ATA 可以使用 Windows 事件 4776 來進一步加強 ATA 的傳遞雜湊偵測。 這可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送。 所收集的事件可提供 ATA 透過網域控制站網路流量無法取得的額外資訊。

### SIEM/Syslog
為了讓 ATA 可以取用 Syslog 伺服器上的資料，您需要執行下列操作︰

-   將您的其中一個 ATA 閘道伺服器設定為接聽及接受從 SIEM/Sylog 伺服器轉送的事件。

-   將您的 SIEM/Syslog 伺服器設定為轉送特定事件至 ATA 閘道。

> [!IMPORTANT]
> -   請勿將所有 Syslog 資料都轉送給 ATA 閘道。
> -   ATA 支援來自 SIEM/Syslog 伺服器的 UDP 流量。

如需如何設定轉送特定事件到另一部伺服器的資訊，請參閱您的 SIEM/Syslog 伺服器產品的文件。 如需轉送事件到 ATA 的詳細資訊，請參閱[設定事件收集](configure-event-collection.md)。

### Windows 事件轉送
如果您沒使用 SIEM/Syslog 伺服器，可將 Windows 網域控制站設定為轉送 Windows 事件識別碼 4776 以供 ATA 收集及分析。 Windows 事件識別碼 4776 提供 NTLM 驗證的相關資料。

## 將 ATA 閘道設定為接聽 SIEM 事件

1.  在 ATA 閘道的設定中，啟用 **Syslog 接聽程式 UDP**。

    設定接聽的 IP 位址，如下圖。 預設的連接埠為 514。

    ![啟用 Syslog 接聽程式 UDP 映像](media/ATA-enable-siem-forward-events.png)

2.  將 SIEM 或 Syslog 伺服器設定為轉送 Windows 事件識別碼 4776 給上圖中選取的 IP 位址。 如需有關如何設定 SIEM 的詳細資訊，請參閱您的 SIEM 線上說明或每部 SIEM 伺服器的特定格式需求的技術支援選項。

### SIEM 支援
ATA 支援下列格式的 SIEM 事件：

#### RSA 安全性分析
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

#### HP Arcsight
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

#### Splunk
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

## 設定 Windows 事件轉送
如果您沒使用 SIEM 伺服器，可將您的網域控制站設定為直接轉送 Windows 事件識別碼 4776 至您的 ATA 閘道之一。

1.  使用具有系統管理員權限的網域帳戶登入所有網域控制站和 ATA 閘道機器。
2. 請確定您連線的所有網域控制站和 ATA 閘道已加入相同網域。
3.  在每個網域控制站上，在提高權限的命令提示字元中輸入：
```
winrm quickconfig
```
4.  在 ATA 閘道上，在提高權限的命令提示字元中輸入：
```
wecutil qc
```
5.  在每個網域控制站上，在 [Active Directory Users and Computers]**** 中瀏覽至 [Builtin]**** 資料夾，按兩下 [Event Log Readers]**** 群組。
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)
以滑鼠右鍵按一下它，並選取 [內容]****。 在 [成員]**** 索引標籤上，新增每個 ATA 閘道的電腦帳戶。
![wef_ad event log reader popup](media/wef_ad-event-log-reader-popup.png)
6.  在 ATA 閘道上，開啟 [事件檢視器]，以滑鼠右鍵按一下 [訂閱]****，然後選取 [建立訂閱]****。  

    a.  在 [訂閱類型和來源電腦]**** 下，按一下 [選取電腦]**** 並加入網域控制站然後測試連線。
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b。  在 [要收集的事件]**** 下，按一下 [選取事件]****。 選取 [依記錄]****，向下捲動以選取 [安全性]****。 然後，在 [包含/排除事件識別碼]**** 中輸入 **4776**。
    ![wef_4776](media/wef_4776.png)

    c. 在 [變更使用者帳戶或設定進階設定]**** 下，按一下 [進階]****。
        將 [通訊協定]**** 設定為 **HTTP**，[連接埠]**** 設定為 **5985**。
    ![wef_http](media/wef_http.png)

 7. [選擇性] 如果您想要較短的輪詢間隔，在 ATA 閘道上，設定訂閱的活動訊號為 5 秒，就能加快輪詢速率。

```
wecutil ss <CollectionName>/cm:custom
wecutil ss <CollectionName> /hi:5000
```

8. 在 ATA 閘道的設定頁面上，啟用 [Windows 事件轉送收集]****。

    > [!NOTE]
    > 當您啟用此設定，ATA 閘道會尋找已從網域控制站轉送給它的 Windows 事件的轉送事件記錄檔。

如需詳細資訊，請參閱[設定電腦轉送及收集事件](https://technet.microsoft.com/en-us/library/cc748890)。

## 另請參閱
- [安裝 ATA](/advanced-threat-analytics/DeployUse/install-ata)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


