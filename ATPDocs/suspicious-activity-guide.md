---
title: 適用於身分識別的 Microsoft Defender 安全性警示指南
description: 此文章提供適用於身分識別的 Microsoft Defender 所發出的安全性警示清單。
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: b6870f7c02dcd9497c08f8ebba33fde967092a4c
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542187"
---
# <a name="product-long-security-alerts"></a>[!INCLUDE [Product long](includes/product-long.md)] 安全性警示

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

[!INCLUDE [Product long](includes/product-long.md)] 安全性警示會說明[!INCLUDE [Product short](includes/product-short.md)] 感應器在您網路上偵測到的可疑活動，以及涉及每個威脅的執行者與電腦。 包含涉及使用者和電腦直接連結的警示辨識項清單，可協助您輕易且直接地進行調查。

[!INCLUDE [Product short](includes/product-short.md)] 安全性警示分為下列類別或階段，如同在典型網路攻擊狙殺鏈中會看到的階段。 使用下列連結，深入了解設計來偵測每個攻擊的各階段警示，以及如何使用這些警示來協助保護您的網路：

1. [偵察階段警示](reconnaissance-alerts.md)
1. [遭入侵的認證階段警示](compromised-credentials-alerts.md)
1. [橫向移動階段警示](lateral-movement-alerts.md)
1. [網域支配階段警示](domain-dominance-alerts.md)
1. [外流階段警示](exfiltration-alerts.md)

若要深入了解所有[!INCLUDE [Product short](includes/product-short.md)] 安全性警示的結構與通用元件，請參閱[了解安全性警示](understanding-security-alerts.md)。

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>安全性警示名稱對應和唯一的外部識別碼

下表列出警示名稱，以及其對應的唯一外部識別碼與其 Microsoft Cloud App Security 警示識別碼。 搭配指令碼或自動化使用時，Microsoft 建議使用警示外部識別碼來取代警示名稱，因為只有安全性警示外部識別碼具有永久性且不會變更。

### <a name="external-ids"></a>[外部識別碼](#tab/external)

> [!div class="mx-tdBreakAll"]
> |安全性警訊名稱|唯一外部識別碼|嚴重性|MITRE ATT&CK Matrix&trade;|
> |---|---|---|---|
> |[帳戶列舉偵察](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|中型|探索|
> |[Active Directory 屬性偵察 (LDAP)](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210)|2210|中型|探索|
> |[透過 SMB 的資料外流](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|高|外流，<br>橫向移動，<br>命令與控制|
> |[Honeytoken 活動](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|中型|認證存取，<br>探索|
> |[資料保護 API 主要金鑰的惡意要求](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|高|認證存取|
> |[網路對應偵察 (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|中型|探索|
> |[遠端程式碼執行嘗試](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|中型|執行，<br>持續性，<br>權限提升，<br>防禦躲避，<br>橫向移動|
> |[透過 DNS 執行遠端程式碼](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|中型|權限提升，<br>橫向移動|
> |[安全性主體偵察 (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|中型|認證存取|
> |[可疑的暴力密碼破解攻擊 (Kerberos、NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|中型|認證存取|
> |[可疑的暴力密碼破解攻擊 (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|中型|認證存取|
> |[可疑的暴力密碼破解攻擊 (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|中型|橫向移動|
> |[可疑的 DCShadow 攻擊 (網域控制站升級)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|高|防禦躲避|
> |[可疑的 DCShadow 攻擊 (網域控制站複寫要求)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|高|防禦躲避|
> |[可疑的 DCSync 攻擊 (目錄服務的複寫)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|高|持續性，<br>認證存取|
> |[可疑的黃金票證使用 (加密降級)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|中型|權限提升，<br>橫向移動，<br>持續性|
> |[可疑的黃金票證使用 (偽造的授權資料)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|高|權限提升，<br>橫向移動，<br>持續性|
> |[可疑的黃金票證使用 (不存在的帳戶)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|高|權限提升，<br>橫向移動，<br>持續性|
> |[可疑的黃金票證使用 (票證異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|高|權限提升，<br>橫向移動，<br>持續性|
> |[可疑的黃金票證使用方式 (使用 RBCD 的票證異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040)|2040|高|持續性|
> |[可疑的黃金票證使用 (時間異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|高|權限提升，<br>橫向移動，<br>持續性|
> |[可疑的身分識別竊取 (雜湊傳遞)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|高|橫向移動|
> |[可疑的身分識別竊取 (票證傳遞)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|高或中|橫向移動|
> |[可疑的 Kerberos SPN 公開 (外部識別碼 2410)](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)|2410|高|認證存取|
> |[可疑的 Netlogon 權限提升嘗試 (CVE-2020-1472 惡意探索)](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411)|2411|高|權限升級|
> |[可疑的 NTLM 驗證竄改](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|中型|權限提升， <br>橫向移動|
> |[可疑的 NTLM 轉送攻擊](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|中或低 (如果觀察到使用簽署的 NTLM v2 通訊協定)|權限提升， <br>橫向移動|
> |[可疑的 Overpass-the-Hash 攻擊 (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|中型|橫向移動|
> |[可疑的流氓 Kerberos 憑證使用方式](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047)|2047|高|橫向移動|
> |[可疑的基本結構金鑰攻擊 (加密降級)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|中型|橫向移動，<br>持續性|
> |[可疑的 SMB 封包操作 (CVE-2020-0796 惡意探索) - (預覽)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|2406|高|橫向移動|
> |[可疑的 Metasploit 入侵架構使用](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|中型|橫向移動|
> |[可疑的 WannaCry 勒索軟體攻擊](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|中型|橫向移動|
> |[敏感性群組的可疑新增項目](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|中型|認證存取，<br>持續性|
> |[透過 DNS 的可疑通訊](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|中型|外流|
> |[可疑的服務建立](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|中型|執行，<br>持續性，<br>權限提升，<br>防禦躲避，<br>橫向移動|
> |[可疑的 VPN 連線](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|中型|持續性，<br>防禦躲避|
> |[使用者與群組成員資格偵察 (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|中型|探索|
> |[使用者和 IP 位址偵察 (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|中型|探索|

### <a name="cloud-app-security-ids"></a>[Cloud App Security 識別碼](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |安全性警訊名稱|Cloud App Security 警示識別碼|
> |---|---|
> |[帳戶列舉偵察](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Active Directory 屬性偵察 (LDAP)](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210)|ALERT_EXTERNAL_AATP_LDAP_SENSITIVE_ATTRIBUTE_RECONNAISSANCE_SECURITY_ALERT|
> |[透過 SMB 的資料外流](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Honeytoken 活動](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[資料保護 API 主要金鑰的惡意要求](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[網路對應偵察 (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[遠端程式碼執行嘗試](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[透過 DNS 執行遠端程式碼](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[安全性主體偵察 (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[可疑的暴力密碼破解攻擊 (Kerberos、NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_BRUTE_FORCE_SECURITY_ALERT|
> |[可疑的暴力密碼破解攻擊 (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[可疑的暴力密碼破解攻擊 (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[可疑的 DCShadow 攻擊 (網域控制站升級)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[可疑的 DCShadow 攻擊 (網域控制站複寫要求)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_REPLICATION_SECURITY_ALERT|
> |[可疑的 DCSync 攻擊 (目錄服務的複寫)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[可疑的黃金票證使用 (加密降級)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[可疑的黃金票證使用 (偽造的授權資料)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[可疑的黃金票證使用 (不存在的帳戶)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[可疑的黃金票證使用 (票證異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[可疑的黃金票證使用方式 (使用 RBCD 的票證異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040)|ALERT_EXTERNAL_AATP_RESOURCE_BASED_CONSTRAINED_DELEGATION_GOLDEN_TICKET_SECURITY_ALERT|
> |[可疑的黃金票證使用 (時間異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[可疑的身分識別竊取 (雜湊傳遞)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[可疑的身分識別竊取 (票證傳遞)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[可疑的 Kerberos SPN 公開 (外部識別碼 2410)](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)|ALERT_EXTERNAL_AATP_KERBEROASTING_SECURITY_ALERT|
> |[可疑的 Netlogon 權限提升嘗試 (CVE-2020-1472 惡意探索)](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411)|ALERT_EXTERNAL_AATP_NETLOGON_BYPASS_SECURITY_ALERT|
> |[可疑的 NTLM 驗證竄改](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[可疑的 NTLM 轉送攻擊](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[可疑的 Overpass-the-Hash 攻擊 (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[可疑的流氓 Kerberos 憑證使用方式](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047)|ALERT_EXTERNAL_AATP_ROGUE_CERTIFICATE_USAGE_SECURITY_ALERT|
> |[可疑的基本結構金鑰攻擊 (加密降級)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[可疑的 SMB 封包操作 (CVE-2020-0796 惡意探索) - (預覽)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|ALERT_EXTERNAL_AATP_SMB_GHOST_SECURITY_ALERT|
> |[可疑的 Metasploit 入侵架構使用](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[可疑的 WannaCry 勒索軟體攻擊](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[敏感性群組的可疑新增項目](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[透過 DNS 的可疑通訊](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[可疑的服務建立](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[可疑的 VPN 連線](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[使用者與群組成員資格偵察 (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[使用者和 IP 位址偵察 (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

<!-- FROM TOP TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Medium|Lateral movement|-->
<!-- FROM BOTTOM TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|-->

---

> [!NOTE]
> 若要停用任何安全性警示，請連絡支援人員。

## <a name="see-also"></a>另請參閱

- [使用安全性警訊](working-with-suspicious-activities.md)
- [了解安全性警訊](understanding-security-alerts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
