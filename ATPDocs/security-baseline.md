---
title: 適用于 Microsoft Defender 身分識別的 Azure 安全性基準
description: 適用于身分識別安全性基準的 Microsoft Defender 提供程式指引和資源，可讓您執行 Azure 安全性基準測試中所指定的安全性建議。
author: msmbaldwin
ms.service: microsoft-defender-for-identity
ms.topic: conceptual
ms.date: 12/03/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 37d46cd2a7810193990cc3143e69c9ea83c6afe2
ms.sourcegitcommit: 69339ed7712657427ee40af8cc3ac41e11ed2dd2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2020
ms.locfileid: "96597946"
---
# <a name="azure-security-baseline-for-microsoft-defender-for-identity"></a>適用于 Microsoft Defender 身分識別的 Azure 安全性基準

此安全性基準會將來自 [Azure 安全性基準測試版本 2.0](https://docs.microsoft.com/azure/security/benchmarks/overview) 的指引套用至 Microsoft Defender 以進行身分識別。 Azure 安全性基準提供如何在 Azure 上保護雲端解決方案的建議。 內容會依 Azure 安全性基準測試所定義的 **安全性控制** ，以及適用于 Microsoft Defender 身分識別的相關指引來分組。 未排除適用于 Microsoft Defender for Identity 的 **控制項**。

若要查看 Microsoft Defender for Identity 如何完全對應至 Azure 安全性基準測試，請參閱 [完整的 Microsoft defender 身分識別安全性基準對應](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines)檔案。

## <a name="network-security"></a>網路安全性

如需詳細資訊，請參閱 [Azure 安全性效能評定：網路安全性](/azure/security/benchmarks/security-controls-v2-network-security)。

### <a name="ns-6-simplify-network-security-rules"></a>NS-6：簡化網路安全性規則

**指導** 方針：使用 Azure 虛擬網路服務標籤來定義網路安全性群組的網路存取控制，或針對您的 Defender 針對身分識別資源設定的 Azure 防火牆。 建立安全性規則時，您可以使用服務標籤取代特定的 IP 位址。 藉由指定服務標記名稱 (例如：「>azureadvancedthreatprotection」 ) 在規則的適當來源或目的地欄位中，您可以允許或拒絕對應服務的流量。 Microsoft 會管理服務標籤包含的位址前置詞，並隨著位址變更自動更新服務標籤。

- [在 proxy 伺服器中啟用身分識別服務 Url 的 Defender 存取](https://docs.microsoft.com/defender-for-identity/configure-proxy#enable-access-to--service-urls-in-the-proxy-server)

- [瞭解和使用服務標記](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

## <a name="identity-management"></a>身分識別管理

如需詳細資訊，請參閱 [Azure 安全性效能評定：身分識別管理](/azure/security/benchmarks/security-controls-v2-identity-management)。

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1：將 Azure Active Directory 標準化為中央身分識別與驗證系統

**指導** 方針：適用于身分識別的 Defender 使用 Azure Active Directory (Azure AD) 作為預設身分識別和存取管理服務。 您應該將 Azure AD 標準化，以管理組織的身分識別和存取管理：

- Microsoft 雲端資源，例如 Azure 入口網站、Azure 儲存體、Azure 虛擬機器 (Linux 和 Windows) 、Azure Key Vault、PaaS 和 SaaS 應用程式。
- 您的組織資源，例如 Azure 上的應用程式或您的公司網路資源。

保護 Azure AD 在組織的雲端安全性實務中，應具有較高的優先順序。 Azure AD 提供身分識別安全分數，協助您評定相對於 Microsoft 最佳做法建議的身分識別安全性狀態。 請使用此分數來測量設定符合最佳做法建議的程度，並改善您的安全性狀態。

注意： Azure AD 支援外部身分識別，讓沒有 Microsoft 帳戶的使用者可以使用其外部身分識別登入其應用程式和資源。

- [Azure Active Directory 中的租用](https://docs.microsoft.com/azure/active-directory/develop/single-and-multi-tenant-apps) 

- [如何建立及設定 Azure AD 執行個體](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant) 

- [使用應用程式的外部識別提供者](https://docs.microsoft.com/azure/active-directory/b2b/identity-providers) (機器翻譯) 

- [Azure Active Directory 中的身分識別安全分數為何](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4：針對所有以 Azure Active Directory 為基礎的存取，使用增強式驗證控制項

**指引**：適用于身分識別的 Defender 使用 Azure Active Directory，透過多重要素驗證和強式無密碼方法來支援增強式驗證控制項。

- 多重要素驗證-啟用 Azure AD 多重要素驗證，並遵循 Azure 資訊安全中心身分識別和存取管理建議，以取得多重要素驗證設定中的一些最佳作法。 您可以根據登入條件和風險因素，對所有、選取的使用者或依使用者的層級強制執行多重要素驗證。
- 無密碼 authentication-有三個可用的無密碼 authentication 選項： Windows Hello 企業版、Microsoft Authenticator 應用程式和內部部署驗證方法（例如智慧卡）。

針對系統管理員和特殊許可權的使用者，請確定已使用強式驗證方法的最高層級，接著向其他使用者推出適當的增強式驗證原則。

- [如何在 Azure 中啟用多重要素驗證](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted) 

- [Azure Active Directory 的無密碼驗證選項簡介](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-passwordless) 

- [Azure AD 預設密碼原則](https://docs.microsoft.com/azure/active-directory/authentication/concept-sspr-policy#password-policies-that-only-apply-to-cloud-user-accounts) 

- [使用 Azure AD 密碼保護排除不正確的密碼](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad)

**Azure 資訊安全中心監視**：是

**責任**：客戶

## <a name="privileged-access"></a>特殊權限存取

如需詳細資訊，請參閱 [Azure 安全性效能評定：特殊權限存取](/azure/security/benchmarks/security-controls-v2-privileged-access)。

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1：保護及限制高權限使用者

**指導** 方針： Defender for Identity 具有下列高許可權帳戶：全域管理員

安全性系統管理員

限制高許可權帳戶或角色的數目，並在提高許可權的層級保護這些帳戶，因為具有此許可權的使用者可以直接或間接讀取和修改 Azure 環境中的每個資源。

您可以啟用對 Azure 資源的即時 (JIT) 特殊許可權存取，以及使用 Azure AD) PIM Azure AD Privileged Identity Management () 的 Azure Active Directory (。 JIT 只有在使用者需要時，才會授與暫時性權限以執行特殊權限的工作。 當您的 Azure AD 組織中有可疑或不安全的活動時，PIM 也會產生安全性警示。
- [適用于身分識別角色群組的 Microsoft Defender](https://docs.microsoft.com/defender-for-identity/role-groups)

- [Azure AD 中的系統管理員角色權限](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) 

- [使用 Azure Privileged Identity Management 安全性警示](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [在 Azure AD 中保護混合式部署和雲端部署的特殊權限存取](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Azure 資訊安全中心監視**：是

**責任**：客戶

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2：限制對業務關鍵系統的系統管理存取

**指導** 方針：適用于身分識別的 Defender 使用 azure 角色型存取控制 (azure RBAC) 藉由限制哪些帳戶被授與存取權給他們所在的訂用帳戶和管理群組，來隔離對商務關鍵性系統的存取。

確定您也會限制對管理、身分識別和安全性系統的存取權，這些系統具有您商務關鍵性存取權的系統管理存取權，例如 Active Directory 網網域控制站 (Dc) 、安全性工具和系統管理工具，以及安裝在商務關鍵性系統上的代理程式。 入侵這些管理和安全性系統的攻擊者，可以立即 weaponize 它們來入侵商務關鍵資產。

所有類型的存取控制都應符合您的企業分割策略，以確保存取控制的一致性。

- [適用于身分識別角色群組的 Microsoft Defender](https://docs.microsoft.com/defender-for-identity/role-groups)

- [Azure 元件和參考模型](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) 

- [管理群組存取](https://docs.microsoft.com/azure/governance/management-groups/overview#management-group-access) 

- [Azure 訂用帳戶管理員](https://docs.microsoft.com/azure/cost-management-billing/manage/add-change-subscription-administrator)

**Azure 資訊安全中心監視**：是

**責任**：客戶

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3：定期檢閱及協調使用者存取

**指導** 方針：適用于身分識別的 Defender 會使用 Azure Active Directory 帳戶來管理其資源、定期審核使用者帳戶和存取指派，以確保帳戶及其存取權都有效。 您可以使用 Azure AD 存取評論來查看群組成員資格、企業應用程式的存取權，以及角色指派。 Azure AD 報告可以提供記錄以協助探索過時的帳戶。 您也可以使用 Azure AD Privileged Identity Management 建立存取權審核報表工作流程，以加速審核程式。

此外，Azure Privileged Identity Management 也可以設定為在建立過多的系統管理員帳戶時發出警示，以及識別已過時或設定不正確的系統管理員帳戶。

注意：某些 Azure 服務支援不是透過 Azure AD 管理的本機使用者和角色。 您將需要分開管理這些使用者。

- [在 Privileged Identity Management (PIM) 中建立 Azure 資源角色的存取權審核 ](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [如何使用 Azure AD 身分識別和存取權檢閱](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overvie)

**Azure 資訊安全中心監視**：是

**責任**：客戶

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6：使用特殊權限存取工作站

**指引**：安全、隔離的工作站對於敏感性角色 (例如系統管理員、開發人員及重要服務操作員) 的安全性來說至關重要。 使用高度安全的使用者工作站及/或 Azure 防禦來進行系統管理工作。 使用 Azure Active Directory、Microsoft Defender for Endpoint 及/或 Microsoft Intune 來部署安全且受管理的使用者工作站以進行系統管理工作。 受保護的工作站可以集中管理以施行安全設定，包括增強式驗證、軟體和硬體基準、受限的邏輯和網路存取。

- [瞭解特殊許可權的存取工作站](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-managed-workstation) 
- [部署特殊權限存取工作站](https://docs.microsoft.com/azure/active-directory/devices/howto-azure-managed-workstation) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

## <a name="data-protection"></a>資料保護

如需詳細資訊，請參閱 [Azure 安全性效能評定：資料保護](/azure/security/benchmarks/security-controls-v2-data-protection)。

### <a name="dp-2-protect-sensitive-data"></a>DP-2：保護敏感性資料

**指導** 方針： Defender for Identity 藉由使用 Azure Active Directory (Azure AD) 角色來限制存取，以保護敏感性資料。

為確保存取控制的一致性，所有類型的存取控制都應與您的企業分割策略相符。 企業分割策略也應由機密或業務關鍵資料和系統的位置來通知。

針對 Microsoft 管理的基礎平台，Microsoft 會將所有客戶內容視為敏感性資訊，並防範客戶資料外洩和暴露。 為了確保 Azure 中的客戶資料保持安全，Microsoft 會實行預設的資料保護控制項和功能。
- [Azure AD 可存取 Cloud App Security 的角色](https://docs.microsoft.com/cloud-app-security/manage-admins)

- [Azure 角色型存取控制 (RBAC) ](https://docs.microsoft.com/azure/role-based-access-control/overview) 

- [瞭解 Azure 中的客戶資料保護](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

## <a name="asset-management"></a>資產管理

如需詳細資訊，請參閱 [Azure 安全性效能評定：資產管理](/azure/security/benchmarks/security-controls-v2-asset-management)。

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1：確保安全性小組能夠看到資產的風險

**指引**：確保安全性小組會獲得 Azure 租用戶和訂用帳戶中的「安全性讀取者」權限，而能夠使用 Azure 資訊安全中心來監視安全性風險。 

根據安全性小組責任的結構，監視安全性風險可能是中央安全性小組或本地小組的責任。 然而，安全性見解和風險務必要在組織內部集中彙總。 

「安全性讀取者」權限可以廣泛套用至整個租用戶 (根管理群組)，或將範圍限定於管理群組或特定訂用帳戶。 

注意：若要取得工作負載和服務的可見度，可能需要其他權限。 

- [安全性讀取者角色概觀](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader)

- [Azure 管理群組概觀](https://docs.microsoft.com/azure/governance/management-groups/overview)

**Azure 資訊安全中心監視**：目前無法使用

**責任**：客戶

## <a name="logging-and-threat-detection"></a>記錄與威脅偵測

如需詳細資訊，請參閱 [Azure 安全性效能評定：記錄與威脅偵測](/azure/security/benchmarks/security-controls-v2-logging-threat-protection)。

### <a name="lt-1-enable-threat-detection-for-azure-resources"></a>LT-1：啟用 Azure 資源的威脅偵測

**指導** 方針： Defender for Identity 可在偵測到可疑的活動時通知您，方法是透過提名感應器將安全性和健康狀態警示傳送至您的 Syslog 伺服器。
將任何來自 Defender for Identity 的記錄轉送到您的 SIEM，可用來設定自訂威脅偵測。 確定您正在監視不同類型的 Azure 資產，以找出潛在的威脅和異常。 專注于取得高品質的警示，以減少因分析師排序的誤報。 警示可能源自于記錄資料、代理程式或其他資料。

- [如何與 Syslog 整合](https://docs.microsoft.com/defender-for-identity/setting-syslog)
- [建立自訂分析規則來偵測威脅](https://docs.microsoft.com/azure/sentinel/tutorial-detect-threats-custom) 

- [使用 Azure Sentinel 的網路威脅情報](https://docs.microsoft.com/azure/architecture/example-scenario/data/sentinel-threat-intelligence)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2：啟用 Azure 身分識別與存取權管理的威脅偵測

**指導** 方針： Azure Active Directory (Azure AD) 提供下列使用者記錄，可在 Azure AD 報告中查看，或與 Azure 監視器、Azure Sentinel 或其他 SIEM/監視工具整合，以取得更精密的監視和分析使用案例：

- 登入 – 登入報告會提供受控應用程式和使用者登入活動的使用情況相關資訊。

- 稽核記錄 - 可針對各種功能在 Azure AD 內進行的所有變更，提供記錄追蹤功能。 Audit 記錄檔的範例包括對 Azure AD 內的任何資源所做的變更，例如新增或移除使用者、應用程式、群組、角色和原則。

- 有風險的登入 - 有風險的登入表示非使用者帳戶合法擁有者的某人嘗試登入。

- 標幟為有風險的使用者 - 有風險的使用者表示可能被盜用的使用者帳戶。

Azure 資訊安全中心也可能會對某些可疑活動發出警示，例如在訂用帳戶中有過多的失敗驗證嘗試次數、已淘汰的帳戶。 除了基本的安全性檢查監視以外，Azure 資訊安全中心的威脅防護模組也可以從個別的 Azure 計算資源 (虛擬機器、容器、App Service)、資料資源 (SQL DB 和儲存體) 與 Azure 服務層收集更深入的安全性警示。 這項功能可讓您查看個別資源內的帳戶異常。

- [Azure Active Directory 中的稽核活動報表](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [啟用 Azure Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection) 
- [Azure 資訊安全中心內的威脅防護](https://docs.microsoft.com/azure/security-center/threat-protection)

**Azure 資訊安全中心監視**：是

**責任**：客戶

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5：將安全性記錄的管理與分析集中

**指導** 方針：確定您要將 Azure 活動記錄整合到您的集中記錄。 透過 Azure 監視器內嵌記錄，以匯總端點裝置、網路資源和其他安全性系統所產生的安全性資料。 在 Azure 監視器中，請使用 Log Analytics 工作區來查詢和執行分析，並使用 Azure 儲存體帳戶來長期和封存儲存體。

此外，請啟用資料並將其上架至 Azure Sentinel 或協力廠商 SIEM。

許多組織選擇使用 Azure Sentinel 「經常性存取」資料，而這些資料經常使用，並 Azure 儲存體使用較不常使用的「冷」資料。

適用于身分識別的 Defender 可將所有安全性相關記錄轉送到您的 SIEM，以進行集中式管理。

- [如何使用 Azure 監視器收集平臺記錄和計量](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings) 
- [如何使 Azure Sentinel 上線](https://docs.microsoft.com/azure/sentinel/quickstart-onboard) 

- [整合 Defender for Identity 與 Syslog](https://docs.microsoft.com/defender-for-identity/setting-syslog)

**Azure 資訊安全中心監視**：是

**責任**：客戶

## <a name="incident-response"></a>事件回應

如需詳細資訊，請參閱 [Azure 安全性效能評定：事件回應](/azure/security/benchmarks/security-controls-v2-incident-response)。

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1：準備 – 更新 Azure 的事件回應流程

**指引**：確定您的組織具有回應安全性事件的流程、已更新 Azure 的這些處理序，而且會定期執行以確保就緒。

- [在企業環境中實作安全性](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud) (機器翻譯)

- [事件回應參考指南](https://docs.microsoft.com/microsoft-365/downloads/IR-Reference-Guide.pdf) (英文)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2：準備 – 設定事件通知

**指引**：在 Azure 資訊安全中心中設定安全性事件連絡人資訊。 當 Microsoft 安全回應中心 (MSRC) 發現您的資料已遭非法或未經授權的合作對象存取時，Microsoft 會使用此連絡人資訊來與您連絡。 您也可以選擇根據您的事件回應需求，在不同的 Azure 服務中自訂事件警示和通知。 

- [如何設定 Azure 資訊安全中心的安全性連絡人](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Azure 資訊安全中心監視**：是

**責任**：客戶

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3：偵測與分析 – 根據高品質警示建立事件

**指引**：確定您具有建立高品質警示並測量警示品質的流程。 這可讓您從過去的事件吸取教訓，並為分析師設定警示優先順序，這樣他們就不會浪費時間在誤報上。 

您可以根據過去事件的經驗、已驗證的社區來源，以及設計成透過融合和相互關聯不同信號來源以產生和清除警示的工具，來建置高品質警示。 

Azure 資訊安全中心 (ASC) 可在許多 Azure 資產之間提供高品質的警示。 您可以使用 ASC 資料連接器將警示串流至 Azure Sentinel。 Azure Sentinel 可讓您建立進階警示規則，以自動產生事件供調查之用。 

使用匯出功能匯出 Azure 資訊安全中心警示和建議，以利找出 Azure 資源的風險。 以手動或持續不斷的方式匯出警示和建議。

- [如何設定匯出](https://docs.microsoft.com/azure/security-center/continuous-export)

- [如何將警示串流至 Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Azure 資訊安全中心監視**：目前無法使用

**責任**：客戶

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4：偵測和分析 – 調查事件

**指引**：確定分析師在調查潛在的事件時可查詢和使用各種資料來源，以全面觀照發生的狀況。 您應收集各種記錄，以追蹤整個攻擊鏈中潛在攻擊者的活動，而避免產生盲點。  您也應確實獲取深入解析和知識，以供其他分析師和未來的歷程記錄參考使用。  

用於調查的資料來源包括已從範圍內服務和執行中的系統收集的集中式記錄來源，但也可以包含：

- 網路資料 – 使用網路安全性群組的流量記錄、Azure 網路監看員和 Azure 監視器，擷取網路流量記錄和其他分析資訊。 

- 執行中系統的快照集： 

    - 使用 Azure 虛擬機器的快照集功能，建立執行中系統磁碟的快照集。 

    - 使用作業系統的原生記憶體傾印功能，建立執行中系統記憶體的快照集。

    - 使用 Azure 服務的快照集功能或軟體本身的功能，建立執行中系統的快照集。

Azure Sentinel 可讓您對絕大多數的記錄來源進行廣泛的資料分析，並提供案例管理入口網站來管理事件的完整生命週期。 調查期間的情報資訊可以與事件相關聯，以供追蹤和報告之用。 

- [為 Windows 機器的磁碟建立快照集](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [為 Linux 機器的磁碟建立快照集](https://docs.microsoft.com/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Microsoft Azure 支援診斷資訊和記憶體傾印收集](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [使用 Azure Sentinel 調查事件](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5：偵測與分析 – 設定事件的優先順序

**指引**：根據警示嚴重性和資產敏感度，為分析師提供應優先關注哪些事件的內容。 

Azure 資訊安全中心會指派每個警示的嚴重性，以協助您設定應優先調查哪些警示。 嚴重性是以「資訊安全中心」在「尋找」或用來發出警示的分析，以及導致警示的活動背後有惡意意圖的信賴等級為基礎。

此外，請使用標籤來標示資源，並建立命名系統以識別及分類 Azure 資源，尤其是處理敏感資料的資源。  您需負責根據發生事件的 Azure 資源和環境的重要性，設定警示的補救優先順序。

- [Azure 資訊安全中心的安全性警示](https://docs.microsoft.com/azure/security-center/security-center-alerts-overview)

- [使用標記來組織 Azure 資源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Azure 資訊安全中心監視**：目前無法使用

**責任**：客戶

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6：圍堵、根除及復原 – 將事件處理自動化

**指引**：將手動重複的工作自動化，以縮短回應時間並降低分析師的負擔。 手動工作需要較長的時間來執行、使每個事件變慢，並減少分析師可以處理的事件數目。 手動工作也會使分析師更加疲勞，而增加人為錯誤導致延遲的風險，並降低分析師有效專注處理複雜工作的能力。 請使用 Azure 資訊安全中心和 Azure Sentinel 中的工作流程自動化功能來自動觸發動作，或執行劇本以回應傳入的安全性警示。 劇本會採取動作，例如傳送通知、停用帳戶，以及隔離有問題的網路。 

- [在資訊安全中心設定工作流程自動化](https://docs.microsoft.com/azure/security-center/workflow-automation)

- [在 Azure 資訊安全中心設定自動化威脅回應](https://docs.microsoft.com/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [在 Azure Sentinel 中設定自動化威脅回應](https://docs.microsoft.com/azure/sentinel/tutorial-respond-threats-playbook)

**Azure 資訊安全中心監視**：目前無法使用

**責任**：客戶

## <a name="posture-and-vulnerability-management"></a>狀況和弱點管理

如需詳細資訊，請參閱 [Azure 安全性效能評定：狀況和弱點管理](/azure/security/benchmarks/security-controls-v2-vulnerability-management)。

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8：執行一般攻擊模擬

**指引**：如有需要，請對您的 Azure 資源執行滲透測試或紅隊活動，並確保補救所有重要的安全性結果。
請遵循 Microsoft 雲端滲透測試參與規則，以確保您的滲透測試不會違反 Microsoft 原則。 針對 Microsoft 管理的雲端基礎結構、服務和應用程式，使用 Microsoft 對於紅隊和即時網站滲透測試的策略和執行方法。

- [Azure 中的滲透測試](https://docs.microsoft.com/azure/security/fundamentals/pen-testing) (機器翻譯)

- [滲透測試運作規則](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Microsoft Cloud Red Teaming](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure 資訊安全中心監視**：不適用

**責任**：共用

## <a name="governance-and-strategy"></a>控管與策略

如需詳細資訊，請參閱 [Azure 安全性效能評定：治理和策略](/azure/security/benchmarks/security-controls-v2-governance-strategy)。

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1：定義資產管理和資料保護策略 

**指引**：務必記載並傳達明確的策略，以持續監視及保護系統和資料。 請優先探索、評估、保護及監視業務關鍵資料和系統。 

此策略應該包含下列項目的已記載指引、原則和標準： 

-   符合商業風險的資料分類標準

-   安全性組織對風險和資產清查的可見度 

-   安全性組織核准 Azure 服務以供使用的程序 

-   資產在其生命週期中的安全性

-   符合組織資料分類的必要存取控制策略

-   使用 Azure 原生和協力廠商資料保護功能

-   傳輸中和待用使用案例的資料加密需求

-   適當的密碼編譯標準

如需詳細資訊，請參閱下列參考資料：
- [Azure 安全性架構建議 - 儲存體、資料和加密](https://docs.microsoft.com/azure/architecture/framework/security/storage-data-encryption?toc=/security/compass/toc.json&amp;bc=/security/compass/breadcrumb/toc.json) (機器翻譯)

- [Azure 安全性基礎觀念 - Azure 資料安全性、加密和儲存體](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview) (機器翻譯)

- [雲端採用架構 - Azure 資料安全性和加密最佳做法](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices?toc=/azure/cloud-adoption-framework/toc.json&amp;bc=/azure/cloud-adoption-framework/_bread/toc.json) (機器翻譯)

- [Azure 安全性效能評定 - 資產管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Azure 安全性效能評定 - 資料保護](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2：定義企業分割策略 

**指引**：使用身分識別、網路、應用程式、訂用帳戶、管理群組和其他控制項的組合，建立企業範圍的策略來分割對產的存取。

審慎權衡安全性區隔的需求，以及需要與彼此通訊並存取資料的啟用每日作業需求。

請確定跨控制項類型（包括網路安全性、身分識別和存取模型、應用程式許可權/存取模型，以及人力流程式控制件）一致地實行分割策略。

- [Azure 中的分割策略指引 (影片)](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) (機器翻譯)

- [Azure 中的分割策略指引 (文件)](https://docs.microsoft.com/security/compass/governance#enterprise-segmentation-strategy) (機器翻譯)

- [使用企業分割策略來調整網路分割](https://docs.microsoft.com/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3：定義安全性狀態管理策略

**指引**：持續測量並降低個別資產及其裝載環境的風險。 設定高價值資產的優先順序以及高度公開的攻擊面，例如已發佈的應用程式、網路輸入和輸出點、使用者和系統管理員端點等等。

- [Azure 安全性效能評定 - 狀態和弱點管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4：協調組織角色、責任及權責

**指引**：務必為安全性組織中的角色和責任記載並傳達清楚的策略。 優先為安全性決策提供清楚的權責、讓每個人熟知共同責任模型，並讓技術團隊熟知保護雲端的技術。

- [Azure 安全性最佳做法 1 – 人員：讓小組熟知雲端安全性旅程](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey) (機器翻譯)

- [Azure 安全性最佳做法 2 - 人員：讓小組熟知雲端安全性技術](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology) (機器翻譯)

- [Azure 安全性最佳做法 3 - 流程：指派雲端安全性決策的權責](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-5-define-network-security-strategy"></a>GS-5：定義網路安全性策略

**指引**：建立 Azure 網路安全性方法，作為組織整體安全性存取控制策略的一部分。  

此策略應該包含下列項目的已記載指引、原則和標準： 

-   集中式網路管理和安全性責任

-   與企業分割策略一致的虛擬網路分割模型

-   不同威脅和攻擊案例的補救策略

-   網際網路邊緣和輸入與輸出策略

-   混合式雲端和內部部署互連能力策略

-   最新的網路安全性成品 (例如網路圖、參考網路架構)

如需詳細資訊，請參閱下列參考資料：
- [Azure 安全性最佳做法 11 - 架構。單一整合的安全性策略](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy) (機器翻譯)

- [Azure 安全性效能評定 - 網路安全性](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Azure 網路安全性概觀](https://docs.microsoft.com/azure/security/fundamentals/network-overview)

- [企業網路架構策略](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/architecture) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6：定義身分識別和特殊權限存取策略

**指引**：建立 Azure 身分識別和特殊權限存取方法，作為組織整體安全性存取控制策略的一部分。  

此策略應該包含下列項目的已記載指引、原則和標準： 

-   集中式身分識別和驗證系統，以及其與其他內部和外部身分識別系統的互連能力

-   不同使用案例和條件中的增強式驗證方法

-   高權限使用者的保護

-   異常使用者活動監視和處理  

-   使用者身分識別、存取權檢閱與核對流程

如需詳細資訊，請參閱下列參考資料：

- [Azure 安全性效能評定 - 身分識別管理](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Azure 安全性效能評定 - 特殊權限存取](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Azure 安全性最佳做法 11 - 架構。單一整合的安全性策略](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy) (機器翻譯)

- [Azure 身分識別管理安全性概觀](https://docs.microsoft.com/azure/security/fundamentals/identity-management-overview)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7：定義記錄和威脅回應策略

**指引**：建立記錄和威脅回應策略，以快速偵測威脅並進行補救，同時符合合規性需求。 優先為分析師提供高品質警示和順暢體驗，讓他們能夠專注處理威脅，而非整合和手動步驟。 

此策略應該包含下列項目的已記載指引、原則和標準： 

-   安全性作業 (SecOps) 組織的角色和責任 

-   妥善定義且與 NIST 或其他產業架構一致的事件回應流程 

-   記錄擷取和保留，以支援威脅偵測、事件回應及合規性需求

-   使用 SIEM、原生 Azure 功能及其他來源，集中顯示及相互關聯威脅的相關資訊 

-   與客戶、供應商和相關公開合作對象之間的溝通和通知計畫

-   使用 Azure 原生和協力廠商平台進行事件處理，例如記錄和威脅偵測、鑑定，以及攻擊補救和根除

-   處理事件和事件後活動的流程，例如吸取的經驗和證據保留

如需詳細資訊，請參閱下列參考資料：

- [Azure 安全性效能評定 - 記錄與威脅偵測](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Azure 安全性效能評定 - 事件回應](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Azure 安全性最佳做法 4 - 流程。更新雲端的事件回應流程](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud) (機器翻譯)

- [Azure 採用架構、記錄與報告決策指南](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Azure 企業規模、管理與監視](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring) (機器翻譯)

**Azure 資訊安全中心監視**：不適用

**責任**：客戶

## <a name="next-steps"></a>後續步驟

- 請參閱 [Azure 安全性效能評定 V2 概觀](/azure/security/benchmarks/overview)
- 深入了解 [Azure 資訊安全性基準](/azure/security/benchmarks/security-baselines-overview)
