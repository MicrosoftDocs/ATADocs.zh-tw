---
title: Azure ATP 安全性警訊指南 | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0dd8d987472ef88108f2cb3541bd590d1a816726
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196645"
---
# <a name="azure-atp-security-alerts"></a>Azure ATP 安全性警示

Azure ATP 安全性警示會說明 Azure ATP 感應器在您網路上偵測到的可疑活動，以及涉及每項威脅的動作項目和電腦。   包含涉及使用者和電腦直接連結的警示辨識項清單，可協助您輕易且直接地進行調查。

Azure ATP 安全性警訊分為下列類別或階段，如同在典型網路攻擊終止鏈結中會看到的階段。 使用下列連結，深入了解設計來偵測每個攻擊的各階段警示，以及如何使用這些警示來協助保護您的網路：

  1. [偵察階段警示](atp-reconnaissance-alerts.md)
  2. [遭入侵的認證階段警示](atp-compromised-credentials-alerts.md)
  3. [橫向移動階段警示](atp-lateral-movement-alerts.md)
  4. [網域支配階段警示](atp-domain-dominance-alerts.md)
  5. [外流階段警示](atp-exfiltration-alerts.md)

若要深入了解所有 Azure ATP 安全性警示的結構和通用元件，請參閱[了解安全性警示](understanding-security-alerts.md)。

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>安全性警示名稱對應和唯一的外部識別碼

在 2.56 版中，所有現有的 Azure ATP 安全性警訊皆以更容易了解的名稱重新命名。 新舊名稱之間的對應和其相對應的唯一 externalId，皆如下表所列。 搭配指令碼或自動化使用時，Microsoft 建議使用警示外部識別碼來取代警示名稱，因為只有安全性警示外部識別碼具有永久性且不會變更。

> [!div class="mx-tableFixed"] 

|新安全性警訊名稱|舊安全性警訊名稱|唯一外部識別碼|嚴重性|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|---------|
|[帳戶列舉偵察](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|使用帳戶列舉偵查|2003|中型|探索|
|[透過 SMB 的資料外流](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| NA| 2030|高|外流，<br>橫向移動，<br>命令與控制|
|[Honeytoken 活動](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Honeytoken 活動|2014|中型|認證存取，<br> 探索|
|[資料保護 API 主要金鑰的惡意要求](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|惡意的資料保護私人資訊要求|2020|高|認證存取|
|[網路對應偵察 (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|使用 DNS 探查|2007|中型|探索|
|[遠端程式碼執行嘗試](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|遠端程式碼執行嘗試|2019|中型|執行，<br> 持續性，<br> 權限提升，<br> 防禦躲避，<br> 橫向移動|
|[透過 DNS 執行遠端程式碼](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|NA|2036|中型|權限提升，<br> 橫向移動|
|[安全性主體偵察 (LDAP) - 預覽](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview)|NA|2038|中型|認證存取|
|[可疑的暴力密碼破解攻擊 (Kerberos、NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|可疑的驗證失敗|2023|中型|認證存取|
|[可疑的暴力密碼破解攻擊 (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|使用 LDAP 簡單繫結的暴力密碼破解攻擊|2004|中型|認證存取|
|[可疑的暴力密碼破解攻擊 (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|不尋常的通訊協定實作 (可能使用 Hydra 等惡意工具)|2033|中型|橫向移動|
|[可疑的 DCShadow 攻擊 (網域控制站升階)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|可疑的網域控制站升級 (潛在的 DCShadow 攻擊)|2028|高|防禦躲避|
|[可疑的 DCShadow 攻擊 (網域控制站複寫要求)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|可疑的網域控制站複寫要求 (可能為 DCShadow 攻擊)|2029|高|防禦躲避|
|[可疑的 DCSync 攻擊 (目錄服務的複寫)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|惡意的目錄服務複寫|2006|高|持續性，<br> 認證存取|
|[可疑的黃金票證使用 (加密降級)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|加密降級活動 (可能為黃金票證攻擊)|2009|中型|權限提升，<br> 橫向移動，<br>持續性|
|[可疑的黃金票證使用 (偽造的授權資料)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|使用偽造授權資料提升權限|2013|高|權限提升，<br>橫向移動，<br>持續性|
|[可疑的黃金票證使用 (不存在的帳戶)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Kerberos 黃金票證 - 不存在的帳戶|2027|高|權限提升，<br> 橫向移動，<br>持續性|
|[可疑的黃金票證使用 (票證異常)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|NA|2032|高|權限提升，<br> 橫向移動，<br>持續性|
|[可疑的黃金票證使用 (時間異常)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Kerberos 黃金票證 - 時間異常|2022|高|權限提升，<br> 橫向移動，<br>持續性|
|[可疑的身分識別竊取 (雜湊傳遞)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|使用傳遞雜湊攻擊竊取身分|2017 年|高|橫向移動|
|[可疑的身分識別竊取 (票證傳遞)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|使用傳遞票證攻擊竊取身分|2018 年|高或中|橫向移動|
|[可疑的 Overpass-the-Hash 攻擊 (加密降級)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|加密降級活動 (可能為 Overpass-the-Hash 攻擊)|2008|中型|橫向移動|
|[可疑的 Overpass-the-Hash 攻擊 (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)|2002|中型|橫向移動|
|[可疑的萬能金鑰攻擊 (加密降級)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|加密降級活動 (可能為萬能金鑰攻擊)|2010|中型|橫向移動，<br> 持續性|
|[可疑的 Metasploit 入侵架構使用](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|不尋常的通訊協定實作 (可能使用 Metasploit 入侵工具)|2034|中型|橫向移動|
|[可疑的 NTLM 轉送攻擊 (Exchange 帳戶) - 預覽](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|NA|2037|中或低 (如果觀察到使用簽署的 NTLM v2 通訊協定)|權限提升， <br> 橫向移動|
|[可疑的 WannaCry 勒索軟體攻擊](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|不尋常的通訊協定實作 (可能為 WannaCry 勒索軟體攻擊)|2035|中型|橫向移動|
|[透過 DNS 的可疑通訊](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|透過 DNS 的可疑通訊|2031|中型|外流|
|[敏感性群組的可疑修改](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|敏感性群組的可疑修改|2024|中型|認證存取，<br>持續性|
|[可疑的服務建立](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|可疑的服務建立|2026|中型|執行，<br> 持續性，<br> 權限提升，<br> 防禦躲避，<br>橫向移動|
|[可疑的 VPN 連線](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|可疑 VPN 連線|2025|中型|持續性，<br>防禦躲避|
|[使用者和群組成員資格偵察 (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|使用目錄服務查詢探查|2021|中型|探索|
|[使用者和 IP 位址偵察 (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|使用 SMB 工作階段列舉探查|2012|中型|探索|
|

> [!NOTE]
> 若要停用任何安全性警示，請連絡支援人員。


## <a name="see-also"></a>另請參閱
- [使用安全性警訊](working-with-suspicious-activities.md)
- [了解安全性警訊](understanding-security-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
