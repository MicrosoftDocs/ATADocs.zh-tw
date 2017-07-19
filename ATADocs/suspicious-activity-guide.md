---
title: "ATA 可疑活動指南 | Microsoft Docs"
description: "本文提供 ATA 可能偵測到的可疑活動清單及修復步驟。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8a230f47f0bf0e886ba46c964e2c2121e9ee44a4
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2017
---
適用於︰Advanced Threat Analytics 1.8 版


# <a name="introduction"></a>簡介

ATA 提供下列進階攻擊各階段的偵測︰探查、認證入侵、橫向移動、權限提升、網域支配等等。

ATA 目前對狙殺鏈中提供偵測的階段會在下面的影像中反白顯示。

![ATA 著重在攻擊狙殺鏈中的橫向活動](media/attack-kill-chain-small.jpg)

本文提供每個階段中每個可疑活動的詳細資料。


## <a name="reconnaissance-using-account-enumeration"></a>使用帳戶列舉偵查

| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 帳戶列舉攻擊是一種攻擊手法，攻擊者可利用此手法來猜測不同的帳戶名稱，並使用 Kerberos 驗證嘗試來探索使用者是否存在於網路。 成功猜對的帳戶可能會用於後續攻擊步驟。 | 檢查有問題的電腦，並嘗試判斷是否有合理的原因導致啟動這麼多的 Kerberos 驗證程序。 這些是嘗試且無法得知多個帳戶的程序，因為使用者不存在 (Client_Principal_Unknown 錯誤)，而且至少一個存取嘗試成功。 <br></br>**例外：**此偵測需要尋找多個不存在的帳戶，並嘗試從單一電腦進行驗證。 如果使用者手動鍵入使用者名稱或網域時出錯，此驗證嘗試會視為登入不存在帳戶的嘗試。 需要許多使用者登入的終端機伺服器可能會合理擁有大量錯誤的登入嘗試。 |調查負責產生這些要求的處理序。  如需根據來源連接埠識別處理序的說明，請參閱 [Have you ever wanted to see which Windows process sends a certain packet out to network?](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/) (是否曾經想查看哪個 Windows 處理序將特定封包送出到網路？)|中型|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>使用目錄服務列舉探查 (SAM-R)

| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 目錄服務探查是一種攻擊手法，攻擊者可利用此手法來對應目錄結構，並鎖定特殊權限帳戶以在稍後用於攻擊步驟。 安全性帳戶管理員遠端 (SAM-R) 通訊協定是用來查詢目錄的其中一種方法。 | 了解為何有問題的電腦正在執行安全性帳戶管理員 - 遠端 (MS-SAMR)。 其執行方式異常，可能正在查詢敏感性實體。 <br></br>**例外：**此偵測需要分析提出 SAM-R 查詢之使用者的正常行為，並在觀察到異常查詢時向您發出警示。 敏感性使用者若登入非其所有的電腦，可能會觸發 SAM-R 查詢並偵測為異常，即使它屬於正常工作處理序的一部分亦然。 IT 小組的成員通常可能會發生此情況。 如果標記為可疑但是正常使用的結果，可能是因為 ATA 先前未觀察到的行為所致。 | 在此情況下，建議針對每個 Active Directory 樹系，延長學習期間並改善 ATA 在網域中的涵蓋範圍。<br></br>[下載並執行 “SAMRi10” 工具](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b)。 ATA 小組已發行 SAMRi10，可強化環境對 SAM-R 查詢的防禦。 | 中型|

## <a name="reconnaissance-using-dns"></a>使用 DNS 探查


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 您的 DNS 伺服器包含您網路中所有電腦、IP 位址和服務的對應。 攻擊者會使用這項資訊來對應您的網路結構，並鎖定感興趣的電腦以在稍後用於攻擊步驟。 | 了解為何有問題的電腦正在執行完整傳輸區域 (AXFR) 查詢來取得 DNS 網域中所有的記錄。 <br></br>**例外：**此偵測會識別發出 DNS 區域傳輸要求的非 DNS 伺服器。 有數個已知會發出這類要求到 DNS 伺服器的安全性掃描程式解決方案。 <br></br>另請確認 ATA 能夠從 ATA 閘道透過連接埠 53 與 DNS 伺服器通訊，以避免發生誤判的情況。| 仔細選擇哪些主機可以提出要求，以限制區域傳輸。 如需詳細資訊，請參閱[保護 DNS 的安全](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx)和[檢查清單：保護 DNS 伺服器的安全](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)。 |中型|

## <a name="reconnaissance-using-smb-session-enumeration"></a>使用 SMB 工作階段列舉探查


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 伺服器訊息區 (SMB) 列舉可讓攻擊者取得您網路中的使用者最近登入之來源 IP 位址的相關資訊。 一旦攻擊者擁有這項資訊，他們就可以使用這項資訊來鎖定特定帳戶，並在網路中橫向移動。 | 了解為何有問題的電腦正在執行 SMB 工作階段列舉。<br></br>**例外：**此偵測需要假設 SMB 工作階段列舉在企業網路中的使用不合法，但某些安全性掃描程式解決方案 (例如 Websense) 發出這類要求。 | [使用 net cease 工具來強化您的環境](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) | 中型   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>暴力密碼破解 (LDAP、Kerberos、NTLM)


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 在暴力密碼破解攻擊中，攻擊者會嘗試許多密碼，並希望最後能夠猜對。 攻擊者會有系統地檢查所有可能的密碼 (或一組大量的可能密碼)，直到找到正確的密碼為止。 攻擊者猜對密碼之後，就可以像是使用者一樣登入網路。 目前，ATA 支援使用 Kerberos 或 NTLM 通訊協定的水平 (多個帳戶) 暴力密碼破解攻擊，以及使用 LDAP 簡單繫結的水平和垂直 (單一帳戶、多個密碼嘗試) 攻擊。 | 了解為何有問題的電腦可能無法驗證多個使用者帳戶 (這些使用者的驗證嘗試次數大致上相同)，或為何單一使用者有大量驗證失敗。 <br></br>**例外：**此偵測需要分析向不同資源進行驗證之帳戶的正常行為，並在觀察到異常模式時觸發警示。 此模式在自動驗證的指令碼中很常見，但可能使用過期的認證 (亦即不正確的密碼或使用者名稱)。 | 複雜且很長的密碼提供必要的第一層安全性，以防止暴力密碼破解攻擊。 | 中型   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>以純文字驗證公開的敏感性帳戶，以及服務以純文字驗證公開帳戶


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 電腦上的某些服務以純文字傳送帳戶認證，即使是敏感性帳戶亦然。 監視您流量的攻擊者可能會惡意攔截並保留這些認證。 敏感性帳戶的任何純文字密碼將會觸發警示。 | 找到有問題的電腦，並了解其為何使用 LDAP 簡單繫結。 | 確認來源電腦上的設定，並確定未使用 LDAP 簡單繫結。 改用 LDAP SAL 或 LDAPS，而不要使用 LDAP 簡單繫結。 請遵循安全性分層架構 (Security Tiered Framework) 並限制跨層存取，以避免提升權限。 | 服務公開為「低」；敏感性帳戶為「中」 |

## <a name="honey-token-account-suspicious-activities"></a>Honey Token 帳戶可疑活動


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| Honey Token 帳戶是假帳戶，可設定來設置陷阱、識別和追蹤網路中與這些帳戶相關的惡意活動。 這些是您網路上未使用且休眠的帳戶，如果有來自 Honey Token 帳戶的可疑活動，可能表示惡意使用者正在嘗試使用這個帳戶。 | 了解為何 Honey Token 帳戶正在從這部電腦進行驗證。 | 在 ATA 設定檔頁面中瀏覽您環境的其他敏感性 (特殊權限) 帳戶，看看是否有潛在可疑的活動。 | 中型   |

## <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 攻擊者可以使用工具，透過特定方式實作 SMB/Kerberos 通訊協定，以取得您網路上的功能。 這表示用於過度傳遞雜湊或暴力密碼破解攻擊的惡意技術。 | 了解為何有問題的電腦以不尋常的方式使用驗證通訊協定或 SMB。 <br></br>**例外：**在很罕見的情況下，如果使用了以非標準方式實作通訊協定的合法工具，就可能會觸發此偵測。 某些滲透測試應用程式已知會這樣做。 | 擷取網路流量，並識別哪個處理序產生不尋常通訊協定實作的流量。<br></br>若要判斷這是否為 WannaCry 攻擊，請執行下列動作：<br></br> 1. 下載可疑活動的 Excel 匯出。<br></br>
2.  開啟 [網路活動] 索引標籤，然後移至 [Json] 欄位以複製相關的 Smb1SessionSetup 與 Ntlm JSON<br></br>
3.  如果 Smb1SessionSetup.OperatingSystem 是 "Windows 2000 2195" 且 Smb1SessionSetup.IsEmbeddedNtlm 是 "true"，以及如果 Ntlm.SourceAccountId 是 "null"，則這是 WannaCry。
| 中   |

## <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| Windows 的幾個元件使用資料保護 API (DPAPI) 來安全地儲存密碼、加密金鑰和其他敏感性資料。 網域控制站會保留備份的主要金鑰，該金鑰可用來解密已加入網域的 Windows 電腦使用 DPAPI 加密的所有密碼。 攻擊者可以使用 DPAPI 網域備份的主要金鑰，來解密所有已加入網域之電腦上的所有密碼 (瀏覽器密碼、加密的檔案等)。 | 了解為何電腦使用此未記載的 API 呼叫要求將主要金鑰用於 DPAPI。 | 如需 DPAPI 的詳細資訊，請參閱 [Windows Data Protection](https://msdn.microsoft.com/library/ms995355.aspx) (Windows 資料保護)。 | 高     |

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>基於異常行為懷疑身分遭竊


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 建立行為模型之後 (需要持續 3 週至少 50 個使用中帳戶才能建立行為模型)，任何異常行為將會觸發警示。 不符合為特定使用者帳戶建立之模型的行為可能指出身分遭竊。 | 了解為何有問題的使用者可能有不同行為。 <br></br>**例外：**如果 ATA 只涵蓋一部分 (並非所有網域控制站都會路由傳送到 ATA 閘道)，則只能了解特定使用者的部分活動。 如果過了 3 週後，ATA 突然開始涵蓋您所有的流量，使用者的完整活動可能會導致觸發警示。 | 確定在您所有的網域控制站上部署 ATA。 <br></br>1.確認使用者是否在組織中有新職位。<br></br>2.確認使用者是否為零工。<br></br>3.確認使用者是否剛從長假返回工作。| 所有使用者為「中」，敏感性使用者為「高」 |


## <a name="pass-the-ticket"></a>Pass the ticket


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 傳遞票證攻擊是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取 Kerberos 票證，並藉由模擬網路上的實體來使用它存取另一部電腦。 | 此偵測需要在兩部 (或多部) 不同的電腦上使用相同的 Kerberos 票證。 在某些情況下，如果您的 IP 位址快速變更，ATA 可能無法判斷是相同電腦或不同電腦使用不同的 IP 位址。 這是 DHCP 集區 (VPN、WiFi 等) 和共用 IP 集區 (NAT 裝置) 過小的常見問題。 | 請遵循安全性分層架構 (Security Tiered Framework) 並限制跨層存取，以避免提升權限。 | 高     |

## <a name="pass-the-hash"></a>Pass the hash


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 在傳遞雜湊攻擊中，攻擊者會使用使用者密碼的基礎 NTLM 雜湊 (而不是一般情況下的相關聯純文字密碼)，向遠端伺服器或服務進行驗證。 | 檢查帳戶是否在出現此警示前後執行任何異常活動。 | 實作[傳遞雜湊](http://aka.ms/PtH)中所述的建議。 請遵循安全性分層架構 (Security Tiered Framework) 並限制跨層存取，以避免提升權限。 | 高|

## <a name="over-pass-the-hash"></a>過度傳遞雜湊


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 過度傳遞雜湊攻擊會惡意探索 Kerberos 驗證通訊協定中的實作弱點，其中 NTLM 雜湊可用來建立 Kerberos 票證，讓攻擊者在沒有使用者密碼的情況下向網路中的服務進行驗證。 | 加密降級：了解為何有問題的帳戶可能在了解如何使用 AES 之後，在 Kerberos 中使用 RC4。 <br></br>**例外：**此偵測需要分析用於網域的加密方法，並在觀察到異常和較弱的方法時向您發出警示。 在某些情況下，會使用較弱的加密方法，而且 ATA 會偵測為異常，不過它可能屬於正常工作處理序的一部分 (但很罕見)。 當 ATA 先前未觀察到這類行為時，就會發生此情況。 改善 ATA 在網域中的涵蓋範圍將有所幫助。 | 實作[傳遞雜湊](http://aka.ms/PtH)中所述的建議。 請遵循安全性分層架構 (Security Tiered Framework) 並限制跨層存取，以避免提升權限。 | 高     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>使用偽造授權資料提升權限 (MS14-068 破解 (偽造 PAC) / MS11-013 破解 (Silver PAC))


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 舊版 Windows Server 中的已知弱點可讓攻擊者操作專用權屬性憑證 (PAC)，這是 Kerberos 票證中包含使用者授權資料 (在 Active Directory 中為群組成員資格) 的欄位，會授與攻擊者更多權限。 | 檢查受影響的電腦上是否正在執行可能使用 PAC 以外授權方法的特殊服務。 <br></br>**例外：**在某些特定情況下，資源會實作自己的授權機制，而可能在 ATA 中觸發警示。 | 確定具有 Windows Server 2012 R2 以前作業系統的所有網域控制站與 [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) 一起安裝，而且 2012 R2 以前的所有成員伺服器和網域控制站已更新 KB2496930。 如需詳細資訊，請參閱 [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) 和[偽造 PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)。 | 高     |

## <a name="abnormal-sensitive-group-modification"></a>敏感性群組的異常修改


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 舊版 Windows Server 中的已知弱點可讓攻擊者操作專用權屬性憑證 (PAC)，這是 Kerberos 票證中包含使用者授權資料 (在 Active Directory 中為群組成員資格) 的欄位，會授與攻擊者更多權限。 | 驗證群組變更合法。 <br></br>**例外：**此偵測需要分析修改敏感性群組之使用者的正常行為，並在觀察到異常變更時向您發出警示。 當 ATA 先前未觀察到這類行為時，合法變更可能會觸發警示。 延長學習期間並改善 ATA 在網域中的涵蓋範圍將有所幫助。 | 確定縮小授權修改敏感性群組的人員群組。 盡可能使用 Just-In-Time 權限。 | 中型   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>加密降級 - 基本架構金鑰惡意程式碼


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 基本架構金鑰是在網域控制站上執行的惡意程式碼，允許在不知道帳戶密碼的情況下，使用任何帳戶向網域進行驗證。 此惡意程式碼通常會使用較弱的加密演算法，來加密網域控制站上的使用者密碼。 | 加密降級：了解為何有問題的帳戶可能在了解如何使用 AES 之後，在 Kerberos 中使用 RC4。 <br></br>**例外：**此偵測需要分析用於網域的加密方法。 在某些情況下，會使用較弱的加密方法，而且 ATA 會偵測為異常，不過它屬於正常工作處理序的一部分 (但很罕見)。 | 您可以使用 [ATA 小組所撰寫的掃描程式](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73)，來檢查基本架構金鑰是否影響您的網域控制站。 | 高 |

## <a name="golden-ticket"></a>黃金票證


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 如果攻擊者具有網域管理員權限，就可以建立 Kerberos 票證授權票證 (TGT)，以提供授權給網路中所有的資源，並將票證到期時間設定為其選擇的任何時間。 這可讓攻擊者取得網路中的持續性。 | 加密降級：了解為何有問題的帳戶可能在了解如何使用 AES 之後，在 Kerberos 中使用 RC4。 <br></br>**例外：**此偵測需要分析用於網域的加密方法，並在觀察到異常和較弱的方法時傳送警示。 在某些情況下，會使用較弱的加密方法，而且 ATA 會偵測為異常，即使它屬於正常工作處理序的一部分亦然 (但很罕見)。 當 ATA 先前未觀察到這類行為時，就會發生此情況。 確定 ATA 完整涵蓋您的網域。 | 請透過下列方式，盡可能保護主要金鑰 Kerberos 票證授權票證 (KRBTGT) 的安全：<br></br>1.實體安全性<br></br>2.虛擬機器的實體安全性<br></br>3.執行網域控制站強化<br></br>4.本機安全性授權 (LSA) 隔離/Credential Guard<br></br>如果偵測到黃金票證，則需要進行更深入的調查，以評估是否需要復原戰術。<br></br>根據 Microsoft 部落格 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 上的指引，使用 [Reset the krbtgt account password/keys](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 krbtgt 帳戶密碼/金鑰) 工具，定期變更 Kerberos 票證授權票證 (KRBTGT) 兩次。 <br></br>實作這些[傳遞雜湊建議](http://aka.ms/PtH)。 | 中型   |



## <a name="remote-execution"></a>遠端執行


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 盜用系統管理員認證的攻擊者可能會在您的網域控制站上執行遠端命令。 這可用於取得持續性、收集資訊、發動拒絕服務 (DOS) 的攻擊或任何其他原因。 | 了解有問題的帳戶是否可以對您的網域控制站執行此遠端執行。 <br></br>**例外：**有時在網域控制上執行命令的合法使用者可能會觸發此警示，不過它屬於正常系統管理程序的一部分。 對網域控制站執行系統管理工作的 IT 小組成員或服務帳戶最常發生此情況。 | 限制從非 0 層電腦遠端存取網域控制站。 刪除任何可疑、過時且不需要的檔案和資料夾。 實作強式使用者帳戶控制 (UAC) 原則。 實作 [PAW](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access) 只允許強化的電腦連線到系統管理員的網域控制站。 | 低      |

## <a name="malicious-replication-requests"></a>惡意的複寫要求


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與網域或樹系中儲存相同資料複本的所有其他網域控制站同步處理。 取得適當權限之後，攻擊者就可以像是網域控制站一樣起始複寫要求，如此可讓攻擊者擷取儲存在 Active Directory 中的資料，包括密碼雜湊。 | 了解為何電腦可能使用網域控制站複寫 API。 此偵測需要使用目錄樹系設定分割的 ATA 了解電腦是否為網域控制站。 <br></br>**例外：**Azure AD 目錄同步可能會導致觸發此警示。 | 驗證下列權限：-   複寫目錄變更 <br></br>-   全部複寫目錄變更<br></br>如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](https://technet.microsoft.com/library/hh296982.aspx)<br></br>您可以利用[AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 PowerShell 指令碼，以判斷誰在網域中具有這些權限。 | 中型   |



## <a name="broken-trust-between-domain-and-computers"></a>網域與電腦之間的信任中斷


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 信任中斷表示 Active Directory 安全性需求可能無效。 這通常會視為基準安全性與合規性失敗，而且是攻擊者容易攻擊的目標。 如果在 24 小時內從電腦帳戶看到超過 5 次連續 Kerberos 驗證失敗，就會在 ATA 中觸發警示。 由於電腦未與網域控制站通訊，因此 (1) 它沒有更新的群組原則，而且 (2) 登入受到快取認證的限制。 | 檢查事件記錄檔，確定電腦與網域的信任關係狀況良好。 | 視需要將電腦加回網域，或重設電腦的密碼。 | 低      |

## <a name="massive-object-deletion"></a>大量物件刪除


| 說明|調查|建議|嚴重性|
|------|----|------|----------|
| 當刪除的帳戶超過所有帳戶的 5% 時，ATA 就會引發此警示。 這需要已刪除項目容器的讀取權限。 | 了解為何突然刪除您所有帳戶的 5%。 | 移除可刪除 Active Directory 中帳戶之使用者的權限。 如需詳細資訊，請參閱 [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (檢視或設定目錄物件的權限)。 | 低 |

## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [調查偽造的 PAC 攻擊](use-case-forged-pac.md)
- [針對 ATA 已知錯誤進行疑難排解](troubleshooting-ata-known-errors.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
