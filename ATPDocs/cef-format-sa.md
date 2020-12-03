---
title: 適用於身分識別的 Microsoft Defender SIEM 記錄參考
description: 提供從適用於身分識別的 Microsoft Defender 傳送到您 SIEM 的可疑活動記錄範例。
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: f5be050f11fc41e19c37410060acb825642369e3
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544108"
---
# <a name="product-long-siem-log-reference"></a>[!INCLUDE [Product long](includes/product-long.md)] SIEM 記錄參考

[!INCLUDE [Product short](includes/product-short.md)] 可以將安全性警示與健康情況警示事件轉送到您的 SIEM。 警示與事件使用 CEF 格式。 此參考文章提供傳送到您 SIEM 的記錄範例。

## <a name="sample-product-short-security-alerts-in-cef-format"></a>使用 CEF 格式的範例[!INCLUDE [Product short](includes/product-short.md)] 安全性警示

下列欄位及其值會轉送到您的 SIEM：

|詳細資料|說明|
|---------|---------------|
|start|警示開始的時間|
|suser|涉及警示的帳戶 (通常是使用者帳戶)|
|shost|涉及警示的帳戶 (通常是電腦帳戶)|
|outcome|若相關，則為警示中可疑活動的成功或失敗結果|
|msg|警示的描述|
|cnt|適用於具有活動發生次數的警示 (例如暴力密碼破解會有猜過密碼的次數)|
|app |用於此警示的通訊協定|
|externalId|[!INCLUDE [Product short](includes/product-short.md)] 寫入事件記錄檔的事件識別碼，其對應到每一種警示類型。 將警示轉送至 Microsoft Cloud App Security 時，此欄位會填入對應的 Cloud App Security 警示識別碼。|
|cs#label|CEF 允許的客戶字串，其中 cs#label 是新欄位的名稱 |
|cs#|CEF 允許的客戶字串，其中 cs# 是值。|

- 例如：`cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa`  
cs1 欄位是警示 URL。

- 例如：`cs2Label=trigger cs2=new`  
cs2 欄位可識別警示為新的或是已更新。

> [!NOTE]
> 若您計劃為[!INCLUDE [Product short](includes/product-short.md)] SIEM 記錄建立自動化或指令碼，建議您使用 **externalId** 欄位來識別警示類型，而非使用警示名稱。 警示名稱有時候可能會遭到修改，但每個警示的 **externalId** 永遠不會變。 如需外部識別碼的清單，請參閱[安全性警示名稱對應與唯一外部識別碼](suspicious-activity-guide.md#security-alert-name-mapping-and-unique-external-ids)。

## <a name="sample-logs"></a>範例記錄檔

此記錄範例符合 RFC 5424 的規範，但[!INCLUDE [Product short](includes/product-short.md)] 也支援 RFC 3164。

優先順序：

- 3=低
- 5=中
- 10=高

### <a name="account-enumeration-reconnaissance"></a>帳戶列舉偵察

02-21-2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|使用帳戶列舉偵察|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=觀察到來自 CLIENT1 使用 Kerberos 通訊協定的可疑帳戶列舉活動，且成功猜測 Lamon Maldonado (軟體工程師)。 externalId=2003 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="data-exfiltration-over-smb"></a>SMB 上的資料外流

12-19-2018 14:17:46 Auth.Error 127.0.0.1 1 2018-12-19T12:17:34.645993+00:00 DC1 CEF 3288 SmbDataExfiltrationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.60.0.0|SmbDataExfiltrationSecurityAlert|[預覽] 透過 SMB 的資料外流|10|start=2018-12-19T12:14:12.4932821Z app=Smb shost=CLIENT1 msg=Eugene Jenkins (軟體工程師) 在 DC2 上將可疑檔案複製到 CLIENT1。 externalId=2030 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new

### <a name="honeytoken-activity"></a>Honeytoken 活動

02-21-2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken 活動|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=下列活動的執行者為 honey:\r\n透過 DC1 登入至 CLIENT2。 externalId=2014 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="malicious-request-of-data-protection-api-master-key"></a>資料保護 API (DPAPI) 主要金鑰的惡意要求

10-29-2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|惡意資料保護私人資訊要求|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 由 CLIENT1 成功執行 1 次從 DC1 擷取 DPAPI 網域備份金鑰的嘗試。 externalId=2020 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="network-mapping-reconnaissance-dns"></a>網路對應偵察 (DNS)

10-29-2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.056894+00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|DnsReconnaissanceSecurityAlert|使用 DNS 偵察|5|start=2018-10-29T09:19:43.5033765Z app=Dns shost=CLIENT1 msg=觀察到來自 CLIENT1 (非 DNS 伺服器) 對 DC1 進行的可疑 DNS 活動。 externalId=2007 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/23937d33-ff71-484d-be0a-3c417fe573ce cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>使用目錄服務查詢探查

02-21-2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| 使用目錄服務列舉偵察 |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg=從 CLIENT1 針對 DC1嘗試執行下列使用 SAMR 通訊協定的目錄服務例舉: \r\nuser1 成功列舉 domain1.test.local 中的所有群組。 externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>遠端程式碼執行嘗試

10-29-2018 11:22:04 Auth.Warning 192.168.0.202 1 2018-10-29T09:22:00.100856+00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RemoteExecutionSecurityAlert|遠端程式碼執行嘗試|5|start=2018-10-29T09:19:45.0552367Z shost=CLIENT1 msg=已在 CLIENT 1 的 DC1 上執行下列遠端程式碼執行嘗試:\r\nuser1 已成功遠端排程一或多個工作。\r\nuser1 遠端排程一或多個工作失敗。\r\nuser1 已成功遠端執行一或多個 WMI 方法。 externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label=trigger cs2=new

### <a name="remote-code-execution-over-dns"></a>透過 DNS 執行遠端程式碼

1-17-2019 08:24:54 Auth.Warning 192.168.0.202 1 2019-01-17T08:24:54.100856+00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.63.0.0|DnsRemoteCodeExecutionSecurityAlert|[預覽] 透過 DNS 的遠端程式碼執行|5|start=2019-01-17T08:24:54.5293800Z app=Dns shost=CLIENT1 msg=動作項目嘗試透過 DNS 通訊協定從 DC1 的 CLIENT1 上遠端執行命令。 externalId=2036 cs1Label=url cs1=https\:////contoso-corp.atp.azure.com:13000/securityAlert/591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new

### <a name="security-principal-reconnaissance-ldap"></a>安全性主體偵察 (LDAP)

02-18-2019 16:48:08 Auth.Warning 127.0.0.1 1 2019-02-18T14:48:02.912264+00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity ï»¿0|Microsoft|Azure ATP|2.66.0.0|LdapSearchReconnaissanceSecurityAlert|[預覽] 使用 LDAP 查詢偵察|5|start=2019-02-18T14:46:29.4644276Z app=LdapSearch shost=CLIENT1 msg=CLIENT1 上的動作項目傳送可疑 LDAP 查詢到 DC1，在 2 個網域中搜尋 4 個類型的列舉與伺服器操作員 (成員可以管理網域伺服器) externalId=2038 cs1Label=url cs1=https\://contoso-corp.atp.azure..com:13000/securityAlert/81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-ldap"></a>可疑的暴力密碼破解攻擊 (LDAP)

02-21-2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|使用 LDAP 簡單繫結的暴力密碼破解攻擊|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=有使用 LDAP 通訊協定對來自 CLIENT1 的 Wofford Thurston (軟體工程師) 進行暴力密碼破解攻擊的嘗試 (100 次猜測嘗試)。 cnt=100 externalId=2004 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="suspected-brute-force-attack-kerberos-ntlm"></a>可疑的暴力密碼破解攻擊 (Kerberos NTLM)

10-29-2018 11:20:47 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:44.478827+00:00 DC3 CEF 3908 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|BruteForceSecurityAlert|可疑的驗證失敗|5|start=2018-10-29T09:19:44.9512286Z app=Kerberos shost=CLIENT1 msg=可疑的驗證失敗，表示從 CLIENT1 偵測到潛在的暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new

### <a name="suspected-dcsync-attack-replication-of-directory-services"></a>可疑的 DCSync 攻擊 (目錄服務的複寫)

02-21-2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|可疑服務建立|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 在 CLIENT1 上建立 MaliciousService 以執行潛在的惡意命令。 externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>可疑的黃金票證使用 (加密降級)

10-29-2018 11:25:07 Auth.Warning 192.168.0.202 1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|加密降級活動 (可能為黃金票證攻擊)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap 從 W10-000007-Lap 的 Kerberos 服務要求 (TGS_REQ) 中，使用了較弱的加密方法 (RC4) 來存取 host/domain1.test.local。 externalId=2009 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-non-existent-account"></a>可疑的黃金票證使用 (不存在的帳戶)

07-01-2018 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos 黃金票證 - 不存在的帳戶|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake，這不存在於 Active Directory 中，已使用 Kerberos 票證。 從 2 部電腦偵測到該票證存取 3 個資源。 這可能表示潛在的黃金票證攻擊。 externalId=2027 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-ticket-anomaly"></a>可疑的黃金票證使用 (票證異常)

1 2018-11-18T10:46:23.346946+00:00 MAXIMG-7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0|Microsoft|Azure ATP|2.56.0.0|GoldenTicketSizeAnomalySecurityAlert|[預覽] 可疑的黃金票證使用 (票證異常)|10|start=2018-11-18T10:44:12.9317797Z app=Kerberos shost=CLIENT2 suser=RFosdyke msg=Renzo Fosdyke (軟體工程師) 使用可疑的 Kerberos 票證從 CLIENT2 存取 ldap/domain1.test.local。 externalId=2032 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-time-anomaly"></a>可疑的黃金票證使用 (時間異常)

02-21-2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos 黃金票證活動|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Lanell Campos (軟體工程師) 的 Kerberos 票證有可疑的使用方式，表示偵測到潛在的黃金票證攻擊。 externalId=2022 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>可疑的黃金票證使用 (偽造的授權資料)

10-29-2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|使用偽造授權資料提升權限|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 無法從 CLIENT1 使用偽造授權資料，以針對 DC1 將權限提升至 host/domain1.test.local。 externalId=2013 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="suspected-identity-theft-pass-the-hash"></a>可疑的身分識別竊取 (雜湊傳遞)

02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|使用傳遞雜湊攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的雜湊在先前由 Eugene Jenkins (軟體工程師) 所登入並從 CLIENT1 所使用其中一部電腦中遭到竊取，。 externalId=2017 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="suspected-identity-theft-pass-the-ticket"></a>可疑的身分識別竊取 (票證傳遞)

02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|使用傳遞票證攻擊竊取身分|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (軟體工程師) 的 Kerberos 票證從 Admin-PC 被竊取至 Victom-PC，並用於存取 krbtgt/DOMAIN1.TEST.LOCAL。 externalId=2018 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="suspected-ntlm-authentication-tampering"></a>可疑的 NTLM 驗證竄改

07-17-2019 18:18:44 Auth.Warning 192.168.0.77 1 2019-07-09T15:18:30.967118+00:00 CENTER CEF 7144 AbnormalNtlmSigningSecurityAlert ï»¿0|Microsoft|Azure ATP|2.86.0.0|AbnormalNtlmSigningSecurityAlert|[預覽] 可疑的 NTLM 驗證竄改|5|start=2019-07-09T15:14:57.5280720Z app=Ntlm shost=CLIENT1 msg=CLIENT1 上有 2 個可疑的帳戶嘗試透過 NTLM 對 2 電腦進行驗證。 externalId=2039 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/d4ce6252-2c0f-47f6-a534-47ee8ad983be cs2Label=trigger cs2=new

### <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>可疑的 Overpass-the-Hash 攻擊 (加密降級)

02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 中 AS_REQ 訊息欄位的 Encrypted_Timestamp 加密方法已遭到降級。 這可能是有人從 CLIENT1 使用過度傳遞雜湊竊取認證的結果。 externalId=2008 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>可疑的萬能金鑰攻擊 (加密降級)

02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|加密降級活動|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=根據先前學習的行為，來自 CLIENT1 的 KRB_ERR 訊息中 ETYPE_INFO2 欄位的加密方法已遭到降級。 這可能是 DC1 上基本架構金鑰的結果。 externalId=2010 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="suspicious-authentication-failures"></a>可疑的驗證失敗

02-21-2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|可疑的驗證失敗|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=可疑的驗證失敗，表示從 CLIENT1 偵測到潛在的暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>透過 DNS 的可疑通訊

10-04-2018 14:49:38 Auth.Warning 192.168.0.202 1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|Azure ATP|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|透過 DNS 的可疑通訊|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=CLIENT1 已傳送可疑的 DNS 查詢，解析 suspiciousdomainname externalId=2031 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>可疑的網域控制站升級 (潛在的 DcShadow 攻擊)

07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **可疑的網域控制站升級 (潛在的 DcShadow 攻擊)** |10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1，這是 domain1.test.local 中的電腦，它已註冊為 DC1 上的網域控制站。 externalId=2028 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-additions-to-sensitive-groups"></a>敏感性群組的可疑新增項目

10-29-2018 11:21:03 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|敏性群組的可疑修改|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 非典型地修改了敏感性群組的成員資格。 externalId=2024 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>可疑的目錄服務複寫

02-21-2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|惡意的目錄服務複寫|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=user1 成功執行惡意的複寫要求 (從 CLIENT1 針對 DC1)。 outcome=Success externalId=2006 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>可疑的複寫要求 (潛在的 DcShadow 攻擊)

07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **可疑的複寫要求 (潛在的 DcShadow 攻擊)** |10|start=2018-07-12T08:17:55.3816102Z **app=複寫活動** shost=CLIENT1 msg=CLIENT1，這不是 domain1.test.local 中的有效網域控制站，已傳送變更到 DC1 上的目錄物件。 externalId=2029 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>可疑的服務建立

10-29-2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|可疑的服務建立|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 建立了 MaliciousService，以在 CLIENT1 上執行潛在的惡意命令。 externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>可疑 VPN 連線

07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|可疑的 VPN 連線|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 已從 3 個位置使用 3 部電腦連線到 VPN。 externalId=2025 cs1Label=url cs1=https\://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="suspected-wannacry-ransomware-attack"></a>可疑的 WannaCry 勒索軟體攻擊

02-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|可疑的 WannaCry 勒索軟體攻擊|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是用來執行 WannaCry 等攻擊的惡意工具結果。 externalId=2035 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-smb"></a>可疑的暴力密碼破解攻擊 (SMB)

002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|可疑的暴力密碼破解攻擊|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是用來執行 Hydra 等攻擊的惡意工具結果。 externalId=2033 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-use-of-metasploit-hacking-framework"></a>可疑的 Metasploit 入侵架構使用

002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|可疑的 Metasploit 攻擊|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是用來執行 Metasploit 等攻擊的惡意工具結果。 externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-overpass-the-hash-attack-kerberos"></a>可疑的 Overpass-the-Hash 攻擊 (Kerberos)

002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|可疑的 Overpass-the-Hash 攻擊|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是使用 Kerberos 通訊協定的惡意行為結果。 externalId=2002 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="user-and-ip-address-reconnaissance-smb"></a>使用者和 IP 位址偵察 (SMB)

002-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|使用 SMB 工作階段列舉偵察|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=從 CLIENT 2 針對 DC1 使用不尋常的通訊協定實作進行驗證嘗試。 可能是用來執行 Metasploit 等攻擊的惡意工具結果。 externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
