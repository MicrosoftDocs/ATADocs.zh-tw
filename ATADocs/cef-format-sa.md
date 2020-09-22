---
title: ATA SIEM 記錄檔參考 | Microsoft Docs
description: 提供從 ATA 傳送到您 SIEM 的安全性警訊記錄檔樣本。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: d8e83ad51970e4add2e703182e9ad466f113a44e
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909724"
---
# <a name="ata-siem-log-reference"></a>ATA SIEM 記錄檔參考


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

ATA 可將安全性和健康情況警示事件轉送到您的 SIEM。 警示會以 CEF 格式轉送。 以下為會傳送至您 SIEM 的各類型安全性警訊記錄檔。

## <a name="sample-ata-security-alerts-in-cef-format"></a>使用 CEF 格式的樣本 ATA 安全性警示
下列欄位及其值會轉送到您的 SIEM：

- start - 警示開始的時間
- suser - 涉及警示的帳戶 (通常是使用者帳戶)
- shost - 警示的來源電腦
- outcome - 在警示中執行，且具有已定義活動成功或失敗的警示  
- msg - 警示描述
- 具有警示發生次數的警示 (例如暴力密碼破解會有猜過密碼的總數)
- app - 警示通訊協定
- externalId - ATA 寫入對應至此警示之事件記錄檔的事件識別碼*
- cs#label & cs# - 這些是 CEF 允許使用的客戶字串，cs#label 是新欄位的名稱，而 cs# 是其值，例如：cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

在此範例中，cs1 是具有警示 URL 的欄位。

*因為記錄檔名稱可能會有所變更，且不會有通知，所以若您根據記錄檔建立指令碼或自動化，請在使用記錄檔名稱的位置，使用各記錄檔的永久 externalID。 

|警示名稱|警示事件識別碼|
|---------|---------------|
|2001|基於異常行為懷疑身分遭竊|
|2002|不尋常的通訊協定實作|
|2003|使用帳戶列舉偵查|
|2004|使用 LDAP 簡單繫結的暴力密碼破解攻擊|
|2006|惡意的目錄服務複寫|
|2007|使用 DNS 探查|
|2008|加密降級活動|
|2009|加密降級活動 (可能為黃金票證)|
|2010|加密降級活動 (可能為 Overpass-the-Hash)|
|2011|加密降級活動 (可能為萬能金鑰)|
|2012|使用 SMB 工作階段列舉的偵察|
|2013|使用偽造授權資料提升權限|
|2014|Honeytoken 活動|
|2016|大量物件刪除|
|2017|使用傳遞雜湊攻擊竊取身分|
|2018|使用傳遞票證攻擊竊取身分|
|2019|偵測到遠端執行嘗試|
|2020|惡意的資料保護私人資訊要求|
|2021|使用目錄服務查詢的偵察|
|2022|Kerberos 黃金票證活動|
|2023|可疑的驗證失敗|
|2024|敏感性群組的異常修改|
|2026|可疑的服務建立|



## <a name="sample-logs"></a>範例記錄檔

優先順序：3 = 低，5 = 中，10 = 高

### <a name="abnormal-modification-of-sensitive-groups"></a>敏感性群組的異常修改
1 2018-12-12T16:53:22.925757+00:00 CENTER ATA 4688 AbnormalSensitiveGroupMembership CEF:0|Microsoft|ATA|1.9.0.0|AbnormalSensitiveGroupMembershipChangeSuspiciousActivity|敏感性群組的異常修改|5|start=2018-12-12T18:52:58.0000000Z app=GroupMembershipChangeEvent suser=krbtgt msg=krbtgt 具有非典型修改的敏感性群組成員。 externalId=2024 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113d028ca1ec1250ca0491

### <a name="brute-force-attack-using-ldap-simple-bind"></a>使用 LDAP 簡單繫結的暴力密碼破解攻擊
12-12-2018 19:52:18 驗證。警告 192.168.0.222 1 2018-12-12T17：52： 18.899690 + 00： 00 CENTER ATA 4688 LdapBruteForceSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |LdapBruteForceSuspiciousActivity |使用 LDAP 簡單系結的暴力密碼破解攻擊 | 5 | start = 2018-12-12T17：52： 10.2350665 Z app = Ldap msg = 10000 密碼猜測嘗試從 W2012R2-000000-SERVER-000000-伺服器的100帳戶進行。 成功猜測到了一個帳戶密碼。 externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>加密降級活動 (黃金票證)
12-12-2018 20:12:35 驗證。警告 192.168.0.222 1 2018-12-12T18：12： 35.105942 + 00： 00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |EncryptionDowngradeSuspiciousActivity |加密降級活動 | 5 | start = 2018-12-12T18：10： 35.0334169 Z app = Kerberos msg = w2012r2-000000-server 中來自訊息的 TGT TGS_REQ 欄位加密方法已根據先前學習的行為降級。 這可能是因正在於 W2012R2-000000-Server 上使用黃金票證所導致。 externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>加密降級活動 (Overpass-the-Hash)
12-12-2018 19:00:31 驗證。警告 192.168.0.222 1 2018-12-12T17：00： 31.963485 + 00： 00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |EncryptionDowngradeSuspiciousActivity |加密降級活動 | 5 | start = 2018-12-12T17：00： 31.2975188 Z app = Kerberos msg = W2012R2-000000-SERVER 中 AS_REQ message 的 Encrypted_Timestamp 欄位加密方法已根據先前學習的行為降級。 這可能為從 W2012R2-000000-Server 使用 Overpass-the-Hash 竊取認證所導致。 externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>加密降級活動 (基本架構金鑰)
12-12-2018 20:07:24 驗證。警告 192.168.0.222 1 2018-12-12T18：07： 24.065140 + 00： 00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |EncryptionDowngradeSuspiciousActivity |加密降級活動 | 5 | start = 2018-12-12T18：07： 24.0222746 Z app = Kerberos msg = W2012R2-000000-SERVER 中 KRB_ERR message 的 ETYPE_INFO2 欄位加密方法已根據先前學習的行為降級。 這可能是 DC1 上基本架構金鑰的結果。 externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Honeytoken 活動
12-12-2018 19:51:52 驗證。警告 192.168.0.222 1 2018-12-12T17：51： 52.659618 + 00： 00 CENTER ATA 4688 HoneytokenActivitySuspiciousActi ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |HoneytokenActivitySuspiciousActivity |Honeytoken activity | 5 | start = 2018-12-12T17：51： 52.5855994 Z app = Kerberos suser = USR78982 msg = USR78982 LAST78982： \r\nAuthenticated 在 DC1 上存取 CLIENT1 時，domain1 local\cifs： from 執行了下列活動。 externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>使用傳遞雜湊攻擊竊取身分
12-12-2018 19:56:02 驗證。錯誤 192.168.0.222 1 2018-12-12T17：56： 02.047236 + 00： 00 CENTER ATA 4688 PassTheHashSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |PassTheHashSuspiciousActivity |使用傳遞雜湊攻擊的身分識別遭竊 | 10 | start = 2018-12-12T17：54： 01.9582400 Z app = Ntlm suser = USR46829 LAST46829 msg = USR46829 LAST46829's Hash 從先前登入的其中一部電腦遭竊，USR46829 LAST46829，並從 W2012R2-000000-SERVER-000000-伺服器使用。 externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>使用傳遞票證攻擊竊取身分
12-12-2018 22:03:51 驗證。錯誤 192.168.0.222 1 2018-12-12T20：03： 51.643633 + 00： 00 CENTER ATA 4688 PassTheTicketSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |PassTheTicketSuspiciousActivity |使用傳遞票證攻擊的身分識別遭竊 | 10 | start = 2018-12-12T17：54： 12.9960662 Z app = Kerberos suser = Birdie Lamb msg = Birdie Lamb (軟體工程師) 的 Kerberos 票證已從 W2012R2-000000-SERVER-000106-伺服器遭竊至 W2012R2-000000-SERVER-000051-伺服器並用來存取 domain1。 local\host。 externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Kerberos 黃金票證活動
12-12-2018 19:53:26 驗證。錯誤 192.168.0.222 1 2018-12-12T17：53： 26.869091 + 00： 00 CENTER ATA 4688 GoldenTicketSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |GoldenTicketSuspiciousActivity |Kerberos 黃金票證活動 | 10 | start = 2018-12-13T06：51： 26.7290524 Z app = Kerberos suser = Sonja Chadsey msg = 可疑的 Sonja Chadsey (軟體工程師) 的 Kerberos 票證，表示偵測到潛在的黃金票證攻擊。 externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求
12-12-2018 20:03:49 驗證。錯誤 192.168.0.222 1 2018-12-12T18：03： 49.814620 + 00： 00 CENTER ATA 4688 RetrieveDataProtectionBackupKeyS ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |RetrieveDataProtectionBackupKeySuspiciousActivity |惡意的資料保護私人資訊要求 | 10 | start = 2018-12-12T17：58： 56.3537533 Z app = LsaRpc shost = W2012R2-000000-SERVER-000000-Server msg = 未知使用者執行1次成功從 W2012R2-000000-SERVER-000000-Server 嘗試從 DC1 取出 DPAPI 網域備份金鑰。 externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>惡意的目錄服務複寫
12-12-2018 19:56:49 驗證。錯誤 192.168.0.222 1 2018-12-12T17：56： 49.312648 + 00： 00 CENTER ATA 4688 DirectoryServicesReplicationSusp ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |DirectoryServicesReplicationSuspiciousActivity |惡意的目錄服務複寫 | 10 | start = 2018-12-12T17：52： 34.3287329 Z app = >ms-drsr shost = W2012R2-000000-SERVER-000000-Server msg = 惡意複寫要求已從 W2012R2-000000-SERVER-000000-Server 針對 DC1 成功執行。 outcome=Success externalId=2006 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>使用偽造授權資料提升權限
12-12-2018 19:51:15 驗證。錯誤 192.168.0.222 1 2018-12-12T17：51： 15.658608 + 00： 00 CENTER ATA 4688 ForgedPacSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |ForgedPacSuspiciousActivity |使用偽造的授權資料提升許可權 | 10 | start = 2018-12-12T17：51： 15.0261128 Z app = Kerberos suser = triservice msg = triservice 嘗試使用偽造的授權資料，從 W2012R2-000000-SERVER-000000 伺服器向 DC1 提升許可權。 externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>使用目錄服務查詢的偵察
12-12-2018 20:23:52 驗證。警告 192.168.0.222 1 2018-12-12T18：23： 52.155531 + 00： 00 CENTER ATA 4688 SamrReconnaissanceSuspiciousActi ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |SamrReconnaissanceSuspiciousActivity |使用目錄服務查詢的偵察 | 5 | start = 2018-12-12T18：04： 12.9868815 Z app = Samr shost = W2012R2-000000-SERVER-000000-Server msg = 使用 SAMR protocol 的下列目錄服務查詢嘗試從 W2012R2-000000-SERVER-000000-Server： \ r\nSuccessful 查詢關於傳入的樹系信任產生器 (此群組的成員可以在 domain1 中建立此樹系的連入單向信任。本機 externalId = 2021 cs1Label = url cs1 =) HTTPs \: //192.168.0.220/suspiciousActivity/5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>使用帳戶列舉偵查
1 2018-12-12T16:57:09.661680+00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi CEF:0|Microsoft|ATA|1.9.0.0|AccountEnumerationSuspiciousActivity|使用帳戶列舉的偵察|5|start=2018-12-12T16:57:09.1706828Z app=Kerberos shost=W2012R2-000000-Server msg=偵測到來自 W2012R2-000000-Server 使用 Kerberos 通訊協定的可疑帳戶列舉活動。 攻擊者嘗試猜測帳戶名稱共 100 次，1 次猜測嘗試符合 Active Directory 中現有的帳戶名稱。 externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>使用 DNS 探查
1 2018-12-12T16:57:20.743634+00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv CEF:0|Microsoft|ATA|1.9.0.0|DnsReconnaissanceSuspiciousActivity|使用 DNS 的偵察|5|start=2018-12-12T16:57:20.2556472Z app=Dns shost=W2012R2-000000-Server msg=觀察到來自 W2012R2-000000-Server (非 DNS 伺服器) 針對 DC1 的可疑 DNS 活動。 externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>使用 SMB 工作階段列舉的偵察
12-12-2018 19:50:51 驗證。警告 192.168.0.222 1 2018-12-12T17：50： 51.090247 + 00： 00 CENTER ATA 4688 EnumerateSessionsSuspiciousActiv ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |EnumerateSessionsSuspiciousActivity |使用 SMB 會話列舉的偵察 | 5 | start = 2018-12-12T17：00： 42.7234229 Z app = SrvSvc shost = W2012R2-000000-SERVER-000000-Server msg = SMB 會話列舉嘗試從 W2012R2-000000-SERVER-000000-Server 對 DC1 失敗。 未暴露任何帳戶。 externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>偵測到遠端執行嘗試
12-12-2018 19:58:45 驗證。警告 192.168.0.222 1 2018-12-12T17：58： 45.082799 + 00： 00 CENTER ATA 4688 RemoteExecutionSuspiciousActivit ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |RemoteExecutionSuspiciousActivity |偵測到遠端執行嘗試 | 5 | start = 2018-12-12T17：54： 23.9523766 Z shost = W2012R2-000000-SERVER-000000-Server msg = 在 DC1 上從 W2012R2-000000-SERVER-000000-Server： \ r\nFailed 對一或多個工作的遠端排程執行下列遠端執行嘗試。 externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作
1 2018-12-12T16:50:46.930234+00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalProtocolSuspiciousActivity|不尋常的通訊協定實作|5|start=2018-12-12T16:48:46.6480337Z app=Ntlm shost=W2012R2-000000-Server outcome=Success msg=triservice 使用不尋常的通訊協定實作成功從 W2012R2-000000-Server 對 DC1 進行驗證。 這可能是用來執行傳遞雜湊和暴力密碼破解等攻擊之惡意工具的結果。 externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>基於異常行為懷疑身分遭竊
1 2018-12-12T16:50:35.746877+00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalBehaviorSuspiciousActivity|根據異常行為懷疑竊取身分|5|start=2018-12-12T16:48:35.5501183Z app=Kerberos suser=USR45964 msg=USR45964 LAST45964 在執行活動時呈現異常行為，這些活動在過去一個月內都未出現，也不符合組織中其他帳戶的活動。 根據以下活動判斷異常行為：\r\n從 30 個異常的工作站執行互動式登入。\r\n要求存取 30 個異常的資源。 externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>可疑的驗證失敗
12-12-2018 19:50:34 驗證。警告 192.168.0.222 1 2018-12-12T17：04： 25.214067 + 00： 00 CENTER ATA 4688 BruteForceSuspiciousActivity ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |BruteForceSuspiciousActivity |可疑的驗證失敗 | 5 | start = 2018-12-12T17：03： 58.5892462 Z app = Kerberos shost = W2012R2-000000-SERVER-000106-Server msg = 可疑的驗證失敗，指出從 W2012R2-000000-SERVER-000106-伺服器偵測到潛在的暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>可疑的服務建立
12-12-2018 19:53:49 驗證。警告 192.168.0.222 1 2018-12-12T17：53： 49.913034 + 00： 00 CENTER ATA 4688 MaliciousServiceCreationSuspicio ‹的̈CEF： 0 |Microsoft |ATA | 1.9.0.0 |MaliciousServiceCreationSuspiciousActivity |可疑的服務建立 | 5 | start = 2018-12-12T19：53： 49.0000000 Z app = ServiceInstalledEvent shost = W2012R2-000000-SERVER-000000-Server msg = triservice 建立 FakeService，以便在 W2012R2-000000-SERVER-000000-Server 上執行可能的惡意命令。 externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="health-alerts"></a>健康狀態警示

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759+00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayDisconnectedMonitoringAlert|GatewayDisconnectedMonitoringAlert|5|externalId=1011 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=已經 5 分鐘沒有來自閘道中心的通訊。 上次通訊是在 2018 年 12 月 12 日下午 4:47:03 UTC。

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097+00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayStartFailureMonitoringAlert|GatewayStartFailureMonitoringAlert|5|externalId=1018 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=無法啟動 DC1 的閘道服務。 最後偵測到的執行時間為 2018年 12 月 12 日下午 3:04:12 UTC。

> [!NOTE]
> 所有健康情況警示都是使用與上述相同的範本來傳送。


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
