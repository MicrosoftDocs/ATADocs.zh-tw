---
title: Azure ATP SIEM 記錄檔參考 | Microsoft Docs
description: 提供從 Azure ATP 傳送到您 SIEM 的可疑活動記錄檔範例。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 4d1a4d24e2102a019b9df627f2d00c1df981c3ae
ms.sourcegitcommit: 4d8e7c690453d9b78e6e597c3f8562250d335ba5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2018
ms.locfileid: "52177380"
---
適用於：Azure 進階威脅防護


# <a name="azure-atp-siem-log-reference"></a>Azure ATP SIEM 記錄檔參考

Azure ATP 可以將安全性警示與監視警示事件轉送到您的 SIEM。 警示與事件使用 CEF 格式。 此參考文章提供傳送到您 SIEM 的記錄範例。

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>範例 Azure ATP 安全性警示使用 CEF 格式
下列欄位及其值會轉送到您的 SIEM：

|詳細資料|說明|
|---------|---------------|
|start|警示的開始時間|
|suser|涉及警示的帳戶 (通常是使用者帳戶)|
|shost|涉及警示的帳戶 (通常是使用者帳戶)|
|outcome|若相關，則為警示中可疑活動的成功或失敗結果|
|msg|警示的描述|
|cnt|適用於具有活動發生次數的警示 (例如暴力密碼破解會有猜過密碼的次數)|
|app |用於此警示的通訊協定|
|externalId|Azure ATP 寫入事件記錄檔的事件類型識別碼，對應到每一種警示類型|
|cs#label|CEF 允許的客戶字串，其中 cs#label 是新欄位的名稱 |
|cs#|CEF 允許的客戶字串，其中 cs# 是值。|
|
- 例如：cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> cs1 欄位是警示 URL。 

- 例如：cs2Label=trigger cs2=new
<br> cs2 欄位可識別警示為新的或是已更新。


> [!NOTE]
> 若您計劃為 Azure ATP SIEM 記錄檔建立自動化或指令碼，建議您使用 **externalId** 欄位來識別警示類型，而非使用警示名稱。 警示名稱有時候可能會遭到修改，但每個警示的 **externalId** 永遠不會變。  

## <a name="azure-atp-security-alert-unique-externalids"></a>Azure ATP 安全性警訊唯一的 externalId

|安全性警訊名稱|唯一的 externalId|
|---------|---------|
|使用 LDAP 簡單繫結的暴力密碼破解攻擊|2004|
|加密降級活動 - 萬能金鑰|2011|
|加密降級活動 (可能為 Overpass-the-Hash 攻擊)|2008|
|加密降級活動 (可能為黃金票證攻擊)|2009|
|加密降級活動 (可能為萬能金鑰攻擊)|2010|
|Honeytoken 活動|2014|
|使用傳遞雜湊攻擊竊取身分|2017 年|
|使用傳遞票證攻擊竊取身分|2018 年|
|Kerberos 黃金票證 - 時間異常|2022|
|Kerberos 黃金票證 - 不存在的帳戶|2027|
|惡意的資料保護私人資訊要求|2020|
|惡意的目錄服務複寫|2006|
|使用偽造授權資料提升權限|2013|
|使用帳戶列舉偵查|2003|
|使用 DNS 探查|2007|
|使用 SMB 工作階段列舉探查|2012|
|使用目錄服務查詢探查|2021|
|遠端程式碼執行嘗試|2019|
|可疑的驗證失敗|2023|
|可疑的網域控制站複寫要求 (可能為 DCShadow 攻擊)|2029|
|可疑的網域控制站升級 (潛在的 DCShadow 攻擊)|2028|
|透過 DNS 的可疑通訊|2031|
|敏感性群組的可疑修改|2024|
|可疑的服務建立|2026|
|可疑 VPN 連線|2025|
|不尋常的通訊協定實作 (可能為 WannaCry 勒索軟體攻擊)*|2002|
|不尋常的通訊協定實作 (可能使用 Hydra 等惡意工具)*|2002|
|不尋常的通訊協定實作 (可能使用 Metasploit 入侵工具)*|2002|
|不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)*|2002|
|*不尋常的通訊協定實作*警示目前正共用 externalId。 各類型警示的 externalId，在未來的版本中將會變更為唯一的 externalId|****|

## <a name="sample-logs"></a>範例記錄檔

記錄檔範例符合 RFC 5242 的規範，但 Azure ATP 也支援 RFC 3164。

優先順序：

- 3=低
- 5=中
- 10=高

### <a name="brute-force-attack-using-ldap-simple-bind"></a>使用 LDAP 簡單繫結的暴力密碼破解攻擊
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|使用 LDAP 簡單繫結的暴力密碼破解攻擊|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=有使用 LDAP 通訊協定對來自 CLIENT1 的 Wofford Thurston (軟體工程師) 進行暴力密碼破解攻擊的嘗試 (100 次猜測嘗試)。 cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="encryption-downgrade-activity---golden-ticket"></a>加密降級活動 - 黃金票證
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|加密降級活動 (可能為黃金票證攻擊)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap 從 W10-000007-Lap 的 Kerberos 服務要求 (TGS_REQ) 中，使用了較弱的加密方法 (RC4)，存取 host/domain1.test.local。 externalId=2009 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity----skeleton-key"></a>加密降級活動 - 萬能金鑰
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 的 KRB_ERR 訊息之 ETYPE_INFO2 欄位的加密方法已遭到降級。 這可能是 DC1 上基本架構金鑰的結果。 externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="encryption-downgrade-activity---overpass-the-hash"></a>加密降級活動 - Overpass-the-Hash
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 的 AS_REQ 訊息欄位之 Encrypted_Timestamp 的加密方法已遭到降級。 這可能是有人從 CLIENT1 使用過度傳遞雜湊竊取認證的結果。 externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="honeytoken-activity"></a>Honeytoken 活動
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken 活動|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=下列活動的執行者為 honey:\r\n透過 DC1 登入至 CLIENT2。 externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="identity-theft-using-pass-the-hash"></a>使用雜湊傳遞的身分識別竊取
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|使用傳遞雜湊攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的雜湊從先前由 Eugene Jenkins (軟體工程師) 登入的其中一部電腦遭到竊取，並從 CLIENT1 使用。 externalId=2017 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="identity-theft-using-pass-the-ticket-attack"></a>使用傳遞票證攻擊竊取身分
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|使用傳遞票證攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的 Kerberos 票證從 Admin-PC 被竊取至 Victom-PC，並用於存取 krbtgt/DOMAIN1.TEST.LOCAL。 externalId=2018 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="kerberos-golden-ticket"></a>Kerberos 黃金票證 (Golden Ticket) 
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos 黃金票證活動|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Lanell Campos (軟體工程師) 的 Kerberos 票證有可疑的使用方式，表示偵測到潛在的黃金票證攻擊。 externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="kerberos-golden-ticket-non-existent-account"></a>Kerberos 黃金票證不存在的帳戶
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos 黃金票證 - 不存在的帳戶|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake，這不存在於 Active Directory 中，已使用 Kerberos 票證。 從 2 部電腦偵測到該票證存取 3 個資源。 這可能表示潛在的黃金票證攻擊。 externalId=2027 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|惡意資料保護私人資訊要求|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 由 CLIENT1 成功執行 1 次從 DC1 擷取 DPAPI 網域備份金鑰的嘗試。 externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="malicious-replication-of-directory-services"></a>惡意的目錄服務複寫 
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|可疑服務建立|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 在 CLIENT1 上建立 MaliciousService 以執行潛在的惡意命令。 externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="privilege-escalation-using-forged-authorization-data"></a>使用偽造授權資料提升權限
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|使用偽造授權資料提升權限|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 無法從 CLIENT1 使用偽造授權資料，針對 DC1 將權限提升至 host/domain1.test.local。 externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-account-enumeration"></a>使用帳戶列舉偵查
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|使用帳戶列舉探查|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=觀察到來自 CLIENT1 使用 Kerberos 通訊協定的可疑帳戶列舉活動，且成功猜中 Lamon Maldonado (軟體工程師)。 externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>使用目錄服務查詢探查 
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| 使用目錄服務列舉探查 |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg=從 CLIENT1 針對 DC1嘗試執行下列使用 SAMR 通訊協定的目錄服務例舉: \r\nuser1 成功列舉 domain1.test.local 中的所有群組。 externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="reconnaissance-using-dns"></a>使用 DNS 探查
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|使用 DNS 探查|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=觀察到來自 CLIENT1 (其並非 DNS 伺服器) 的可疑 DNS 活動。 此查詢是針對示範查詢 (類型 Axfr)。 回應是 NoError。 externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c cs2Label=trigger cs2=update

### <a name="reconnaissance-using-smb-session-enumeration"></a>使用 SMB 工作階段列舉探查
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.962930+00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EnumerateSessionsSecurityAlert|使用 SMB 工作階段列舉探查|5|start=2018-02-21T14:19:03.2071170Z app=SrvSvc shost=CLIENT1 msg=user1 成功執行 SMB 工作階段列舉嘗試 (從 CLIENT1 針對 DC1)，並公開 Eugene Jenkins (user2-computer)。 externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>遠端程式碼執行嘗試
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|RemoteExecutionSecurityAlert|偵測到遠端執行嘗試|5|start=2018-02-21T14:19:41.9912772Z app=Wmi shost=CLIENT1 suser=user1 outcome=Success msg=從 CLIENT1 於 DC1 上嘗試執行下列遠端執行 :\r\nuser1 成功遠端執行一或多個 WMI 方法。 externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="suspicious-authentication-failures"></a>可疑的驗證失敗
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|可疑的驗證失敗|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=可疑的驗證失敗，表示從 CLIENT1 偵測到潛在的暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>透過 DNS 的可疑通訊
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|通過 DNS 的可疑通訊|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 傳送了解析 suspiciousdomainname externalId=2031 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new 的可疑 DNS 查詢

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>可疑的網域控制站升級 (潛在的 DcShadow 攻擊)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **可疑的網域控制站升級 (潛在的 DcShadow 攻擊)**|10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1，這是 domain1.test.local 中的電腦，它已註冊為 DC1 上的網域控制站。 externalId=2028 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-modification-of-sensitive-groups"></a>敏感性群組的可疑修改
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|敏感群組的可疑修改|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 非典型地修改了敏感群組的成員資格。 externalId=2024 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>可疑的目錄服務複寫
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|惡意的目錄服務複寫|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=user1 成功執行惡意的複寫要求 (從 CLIENT1 針對 DC1)。 outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>可疑的複寫要求 (潛在的 DcShadow 攻擊)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **可疑的複寫要求 (潛在的 DcShadow 攻擊)**|10|start=2018-07-12T08:17:55.3816102Z **app=複寫活動** shost=CLIENT1 msg=CLIENT1，這不是 domain1.test.local 中的有效網域控制站，已傳送變更到 DC1 上的目錄物件。 externalId=2029 cs1Label=url cs1=https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>可疑的服務建立 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|建立可疑的服務|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 建立了 MaliciousService，以在 CLIENT1 上執行潛在的惡意命令。 externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>可疑 VPN 連線
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|可疑 VPN 連線|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 已從 3 個位置使用 3 部電腦連線到 VPN。     externalId=2025 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation---potential-use-of-malicious-tools-such-a-hydra"></a>不尋常的通訊協定實作 - (可能使用 Hydra 等惡意工具)
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|不尋常的通訊協定實作|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是用來執行雜湊傳遞和暴力密碼破解等攻擊的惡意工具結果。 externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="unusual-protocol-implementation--potential-use-of-malicious-tools-such-a-metasploit"></a>不尋常的通訊協定實作 - (可能使用 Metasploit 等惡意工具)
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.460233+00:00 DC3 CEF 3908 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalProtocolSecurityAlert|不尋常的通訊協定實行 (可能使用 Metasploit 入侵工具)|5|start=2018-10-29T09:19:46.6092465Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT2 嘗試使用不尋常的通訊協定實作，針對 DC1 進行驗證。 externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/573f10a1-6f8a-44b1-a5b1-212d40996363 cs2Label=trigger cs2=new

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
