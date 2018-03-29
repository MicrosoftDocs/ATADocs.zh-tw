---
title: Azure ATP SIEM 記錄檔參考 | Microsoft Docs
description: 提供從 Azure ATP 傳送到您 SIEM 的可疑活動記錄檔範例。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/28/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0a632473490d157e2b85a30bdb82947982da9551
ms.sourcegitcommit: 7c9fe4eb781bec71129310a6e0c5e76b022a0213
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
適用於：Azure 進階威脅防護


# <a name="azure-atp-siem-log-reference"></a>Azure ATP SIEM 記錄檔參考

Azure ATP 可以將可疑活動和監視警示事件轉寄到您的 SIEM。 可疑活動事件採用 CEF 格式。 本參考文章提供傳送到您 SIEM 的可疑活動記錄檔範例。

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>CEF 格式的 Azure ATP 可疑活動範例
下列欄位及其值會轉送到您的 SIEM：

-   start - 警示的開始時間
-   suser - 涉及此警示的帳戶 (通常應該是使用者帳戶)
-   shost - 此警示的來源電腦
-   outcome - 適用於指出該警示中執行活動成功/失敗的警示  
-   msg - 警示的描述
-   cnt - 適用於具有警示發生次數的警示 (例如猜過幾次密碼的暴力密碼破解)
-   app - 用於此警示的通訊協定
-   externalId - Azure ATP 寫入對應至此警示之事件記錄檔的事件識別碼
-   cs#label 與 cs# - 這些是 CEF 允許使用的客戶字串，cs#label 是新欄位的名稱，而 cs# 是其值，例如：cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

在此範例中，cs1 是具有警示 URL 的欄位。

## <a name="sample-logs"></a>範例記錄檔

下列記錄檔範例符合 RFC 5242 的規範，但 Azure ATP 也支援 RFC 3164 規範。

優先順序：

- 3=低
- 5=中
- 10=高

### <a name="bruteforce--ldap"></a>暴力密碼破解 - LDAP
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|使用 LDAP 簡單繫結的暴力密碼破解攻擊|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=有使用 LDAP 通訊協定對來自 CLIENT1 的 Wofford Thurston (軟體工程師) 進行暴力密碼破解攻擊的嘗試 (100 次猜測嘗試)。 cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>暴力密碼破解
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|可疑的驗證失敗|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=可疑的驗證失敗，表示從 CLIENT1 偵測到潛在的暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>權限提升
#### <a name="silver"></a>Silver
02-21-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:15.186167+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|使用偽造授權資料提升權限|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=user1 嘗試從 CLIENT1 使用偽造授權資料將權限提升至 host/domain1.test.local。 externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Gold
02-21-2018  16:19:20    Auth.Error  192.168.0.220   1 2018-02-21T14:19:14.358037+00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|ForgedPacSecurityAlert|使用偽造授權資料提升權限|10|start=2018-02-21T14:19:02.8595383Z app=Kerberos suser=user1 msg=user1 無法從 CLIENT1 使用偽造授權資料針對 DC1 將權限提升至 host/domain1.test.local。 externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>黃金票證
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos 黃金票證活動|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Lanell Campos (軟體工程師) 的 Kerberos 票證有可疑的使用方式，表示偵測到潛在的黃金票證攻擊。 externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="honey-token-activity"></a>Honey Token 活動
02-21-2018  16:20:36    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken 活動|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=下列活動的執行者為 honey:\r\n透過 DC1 登入至 CLIENT2。 externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>可疑的目錄服務複寫
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|惡意的目錄服務複寫|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=user1 成功執行惡意的複寫要求 (從 CLIENT1 針對 DC1)。 outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求
02-21-2018  16:22:08    Auth.Error  192.168.0.220   1 2018-02-21T14:21:54.080266+00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RetrieveDataProtectionBackupKeySecurityAlert|惡意的資料保護私人資訊要求|10|start=2018-02-21T14:19:41.8382786Z app=LsaRpc shost=CLIENT1 msg=user1 從 CLIENT 1 成功執行 1 次嘗試從 DC1 擷取 DPAPI 網域備份金鑰。 externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>過度傳遞雜湊
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 的 AS_REQ 訊息欄位之 Encrypted_Timestamp 的加密方法已遭到降級。 這可能是有人從 CLIENT1 使用過度傳遞雜湊竊取認證的結果。 externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>傳遞雜湊
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|使用傳遞雜湊攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的雜湊從先前由 Eugene Jenkins (軟體工程師) 登入的其中一部電腦遭到竊取，並從 CLIENT1 使用。 externalId=2017 cs1Label=url cs1=https://test-syslog.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>帳戶列舉
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|使用帳戶列舉探查|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=觀察到來自 CLIENT1 使用 Kerberos 通訊協定的可疑帳戶列舉活動，且成功猜中 Lamon Maldonado (軟體工程師)。 externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>DNS 探查
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|使用 DNS 探查|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=觀察到來自 CLIENT1 (其並非 DNS 伺服器) 的可疑 DNS 活動。 此查詢是針對示範查詢 (類型 Axfr)。 回應是 NoError。 externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>SMB 工作階段列舉
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|使用 SMB 工作階段列舉探查|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=user1 成功執行 SMB 工作階段列舉嘗試 (從 CLIENT1 針對 DC1)，並公開 Eugene Jenkins (user2-computer)。 externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>SAM-R 列舉
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| 使用目錄服務列舉探查 |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg=從 CLIENT1 針對 DC1嘗試執行下列使用 SAMR 通訊協定的目錄服務例舉: \r\nuser1 成功列舉 domain1.test.local 中的所有群組。 externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>遠端執行
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|偵測到遠端執行嘗試|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=從 CLIENT1 於 DC1 上嘗試執行下列遠端執行 :\r\nuser1 成功遠端執行一或多個 WMI 方法。 externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>基本架構金鑰
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 的 KRB_ERR 訊息之 ETYPE_INFO2 欄位的加密方法已遭到降級。 這可能是 DC1 上基本架構金鑰的結果。 externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|不尋常的通訊協定實作|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 這可能是用來執行傳遞雜湊和暴力密碼破解等攻擊之惡意工具的結果。 externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>惡意的服務建立
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|可疑服務建立|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 在 CLIENT1 上建立 MaliciousService 以執行潛在的惡意命令。 externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass the ticket

02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|使用傳遞票證攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的 Kerberos 票證從 Admin-PC 被竊取至 Victom-PC，並用於存取 krbtgt/DOMAIN1.TEST.LOCAL。 externalId=2017 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd


## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)