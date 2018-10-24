---
title: ATA SIEM 記錄檔參考 | Microsoft Docs
description: 提供從 ATA 傳送到您 SIEM 的可疑活動記錄檔範例。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e4dc613ded1234bad931a67af679bb067c2d7719
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134072"
---
*適用於：Advanced Threat Analytics 1.9 版*


# <a name="ata-siem-log-reference"></a>ATA SIEM 記錄檔參考

ATA 可以將可疑活動和監視警示事件轉送到您的 SIEM。 可疑活動事件採用 CEF 格式。 本參考文章提供傳送到您 SIEM 的可疑活動記錄檔範例。

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>CEF 格式的 ATA 可疑活動範例
下列欄位及其值會轉送到您的 SIEM：

-   start - 警示的開始時間
-   suser - 涉及此警示的帳戶 (通常應該是使用者帳戶)
-   shost - 此警示的來源電腦
-   outcome - 適用於指出該警示中執行活動成功/失敗的警示  
-   msg - 警示的描述
-   cnt - 適用於具有警示發生次數的警示 (例如猜過幾次密碼的暴力密碼破解)
-   app - 用於此警示的通訊協定
-   externalId - ATA 寫入對應至此警示之事件記錄檔的事件識別碼
-   cs#label 與 cs# - 這些是 CEF 允許使用的客戶字串，cs#label 是新欄位的名稱，而 cs# 是其值，例如：cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

在此範例中，cs1 是具有警示 URL 的欄位。

## <a name="sample-logs"></a>範例記錄檔

優先順序：3 = 低，5 = 中，10 = 高

### <a name="bruteforce--ldap"></a>暴力密碼破解 - LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     May  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|使用 LDAP 簡單繫結進行暴力密碼破解攻擊|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=有人嘗試從 CLIENT1 對 Darris Woods (軟體工程師) 使用 LDAP 通訊協定進行暴力密碼破解攻擊 (嘗試猜測 76 次)。 cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|使用 LDAP 簡單繫結進行暴力密碼破解攻擊|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=有人嘗試從 CLIENT1 對 Dino Hopkins (軟體工程師) 使用 LDAP 通訊協定進行暴力密碼破解攻擊 (嘗試猜測 3 次)。 cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|使用 LDAP 簡單繫結進行暴力密碼破解攻擊|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=有人嘗試從 CLIENT1 對 Dino Hopkins (軟體工程師) 使用 LDAP 通訊協定進行暴力密碼破解攻擊 (嘗試猜測 77 次) 並成功。 cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>暴力密碼破解
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|可疑的驗證失敗|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=可疑的驗證失敗指出從 CLIENT1 偵測到潛在暴力密碼破解攻擊。 externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>權限提升
#### <a name="silver"></a>Silver
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|使用偽造授權資料提升權限|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1 嘗試從 CLIENT2 使用偽造授權資料將權限提升至 HOST/client1。 externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Gold
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|使用偽造授權資料提升權限|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1 嘗試從 CLIENT1 使用偽造授權資料對 DC4 提升權限。 externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>黃金票證
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|加密降級活動|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=來自 CLIENT1 的 TGS_REQ 訊息之 TGT 欄位的加密方法已根據先前學到的行為降級。 這可能是 CLIENT1 上的黃金票證使用中的結果。 externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Honey Token 活動
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken 活動|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=privtriservice 執行了下列活動：\r\n從 DC1 使用 NTLM 對經由 DC1 的公司資源進行驗證。 externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>可疑的目錄服務複寫
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|惡意的目錄服務複寫|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg=user1 嘗試從 CLIENT1 對 DC1 提出惡意的複寫要求。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|惡意的資料保護私人資訊要求|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=來自 CLIENT1 的未知使用者嘗試從 DC1 擷取 DPAPI 網域備份金鑰並成功 4 次。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>大量物件刪除
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|大量物件刪除|5|start=2017-05-14T11:33:32.0000000Z msg=過去一段時間從網域 domain1.test.local 刪除了496 個物件 (AD 物件總數的 9.75%)。 cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>過度傳遞雜湊
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|加密降級活動|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=來自 CLIENT1 的 AS_REQ 訊息之 Encrypted_Timestamp 欄位的加密方法已根據先前學到的行為降級。 這可能是有人從 CLIENT1 使用過度傳遞雜湊竊取認證的結果。 externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>傳遞雜湊
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|使用傳遞雜湊攻擊竊取身分|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=有人從 user2 先前登入的其中一部電腦竊取 user2 的雜湊，並從 CLIENT1 使用。 externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>帳戶列舉
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|使用帳戶列舉探查|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=偵測到來自 CLIENT3 使用 Kerberos 通訊協定的可疑帳戶列舉活動。 攻擊者嘗試猜測帳戶名稱共 72 次，2 次猜測嘗試符合 Active Directory 中現有的帳戶名稱。 externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>DNS 探查
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|使用 DNS 探查|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=觀察到來自 CLIENT1 (非 DNS 伺服器) 對 DC1 的可疑 DNS 活動。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|使用 DNS 探查|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=觀察到來自 CLIENT1 (非 DNS 伺服器) 的可疑 DNS 活動。 此查詢是針對 contoso.com (Axfr 類型)。 回應是 NameError。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>SMB 工作階段列舉
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|使用 SMB 工作階段列舉探查|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=有人成功從 CLIENT1 對 DC1 執行 SMB 工作階段列舉嘗試，並公開 user1 (daf::1)。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>SAMR 列舉
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|使用目錄服務列舉的偵察|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=有人嘗試從 CLIENT1 對 DC1 使用 SAMR 通訊協定列舉下列目錄服務：\r\nuser1 成功列舉 domain1.test.local 中所有的群組 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>遠端執行
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|偵測到遠端執行嘗試|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Success msg=有人從 CLIENT1 在 DC1 上執行下列遠端執行嘗試：\r\n系統管理員成功從遠端建立 PSEXESVC。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>基本架構金鑰
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|加密降級活動|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=來自 CLIENT2 的 KRB_ERR 訊息之 ETYPE_INFO2 欄位的加密方法已根據先前學到的行為降級。 這可能是 DC3 上基本架構金鑰的結果。 externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|不尋常的通訊協定實作|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Success msg=系統管理員已成功從 CLIENT1 使用不尋常的通訊協定實作對 DC1 進行驗證。 這可能是用來執行傳遞雜湊和暴力密碼破解等攻擊之惡意工具的結果。 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="pass-the-ticket"></a>Pass the ticket
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|使用傳遞票證攻擊竊取身分|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=系統管理員的 Kerberos 票證已從 CLIENT2 竊取到 CLIENT1，並用來存取 krbtgt/DOMAIN1.TEST.LOCAL。 cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

### <a name="monitoring-alert"></a>監視警示
2018-01-30T10:42:09.102595+00:00 CENTER ATA 4932 CenterDatabaseDisconnectedMonito ï»¿CEF:0|Microsoft|ATA|1.8.6765.50002|CenterDatabaseDisconnectedMonitoringAlert|CenterDatabaseDisconnectedMonitoringAlert|10|externalId=1005 cs1Label=url cs1=https://center/monitoring msg=CENTER 中心所使用的資料庫已關閉。 最後偵測到的執行時間為 1/30/2018 10:39:39 AM UTC。

> [!NOTE]
> 所有監視警示皆已透過上述的相同範本傳送完成。



## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
