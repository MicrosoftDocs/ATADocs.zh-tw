---
title: 適用於身分識別的 Microsoft Defender 所監視的網域活動
description: 描述由適用於身分識別的 Microsoft Defender 所監視的每個活動類型
ms.date: 12/24/2020
ms.topic: conceptual
ms.openlocfilehash: 5ca3a3681eb15b1b2a8935942daaf7a39f9c15c3
ms.sourcegitcommit: 78fb0cead845c7098c780f4daa624a741e350ec2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/24/2020
ms.locfileid: "97763620"
---
# <a name="product-long-monitored-activities"></a>[!INCLUDE [Product long](includes/product-long.md)] 所監視的活動

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

[!INCLUDE [Product long](includes/product-long.md)] 會監視從您組織的 Active Directory 產生的資訊、網路活動與事件活動，來偵測可疑活動。 監視的活動資訊可讓[!INCLUDE [Product short](includes/product-short.md)] 協助您判斷每個潛在威脅的有效性，並正確進行分級與回應。

在確實為有效威脅 (或 **確判為真**) 的情況下，[!INCLUDE [Product short](includes/product-short.md)] 可讓您探索每個事件的缺口範圍、調查涉及的實體有哪些，以及判斷如何予以補救。

由[!INCLUDE [Product short](includes/product-short.md)] 所監視的資訊會以活動的形式呈現。 [!INCLUDE [Product short](includes/product-short.md)] 目前支援監視下列活動類型：

> [!NOTE]
>
> - 此文章與所有[!INCLUDE [Product short](includes/product-short.md)] 感應器類型皆相關。
> - [!INCLUDE [Product short](includes/product-short.md)] 所監視的活動會同時出現在使用者與電腦設定檔頁面上。
> - 您也可以在 [Cloud App Security](https://portal.cloudappsecurity.com/) 與 Microsoft 365 Defender 的[進階搜捕](https://security.microsoft.com/advanced-hunting)頁面找到[!INCLUDE [Product short](includes/product-short.md)] 監視的活動。

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>受監視的使用者活動：使用者帳戶 AD 屬性變更

|受監視的活動|說明|
|---------------------|------------------|
|帳戶限制委派狀態已變更|帳戶狀態目前為啟用或停用委派。|
|帳戶限制委派 SPN 已變更|限制委派會限制指定伺服器可以代表使用者執行的目標服務。|
|帳戶停用已變更|指出帳戶為停用或啟用。|
|帳戶過期|帳戶過期的日期。|
|帳戶過期時間已變更|帳戶過期日期的變更。|
|帳戶鎖定已變更|帳戶過期日期的變更。|
|帳戶密碼已變更|使用者已變更密碼。|
|帳戶密碼已過期|使用者的密碼已過期。|
|密碼永久有效已變更|使用者的密碼已變更為永久有效。|
|不需帳戶密碼已變更|使用者帳戶已變更，允許使用空白密碼登入。|
|需要帳戶智慧卡已變更|帳戶已變更為要求使用者以智慧卡登入裝置。|
|帳戶支援的加密類型已變更|Kerberos 支援的加密類型已變更 (類型：Des、AES 129、AES 256)|
|帳戶 UPN 名稱已變更|使用者的主體名稱已變更。|
|群組成員資格已變更|使用者已由另一名使用者，或自行新增到群組或從中移除。|
|使用者電子郵件已變更|使用者電子郵件屬性已變更。|
|使用者管理員已變更|使用者的管理員屬性已變更。|
|使用者電話號碼已變更|使用者的電話號碼屬性已變更。|
|使用者標題已變更|使用者的標題屬性已變更。|

<!-- Rollback
|SID-History Changed|Account's SID-History attribute was changed.|
-->

## <a name="monitored-user-activities-ad-security-principal-operations"></a>受監視的使用者活動：AD 安全性主體作業

|受監視的活動|說明|
|---------------------|------------------|
|安全性主體已建立|帳戶已建立 (使用者及電腦)。|
|安全性主體刪除已變更|帳戶已刪除/還原 (使用者及電腦)。|
|安全性主體顯示名稱已變更|帳戶顯示名稱已從 X 變更為 Y。|
|安全性主體名稱已變更|帳戶名稱屬性已變更。|
|安全性主體路徑已變更|帳戶辨別名稱已從 X 變更為 Y。|
|安全性主體 Sam 名稱已變更|SAM 名稱已變更 (SAM 是登入名稱，用來支援執行較舊版作業系統的用戶端和伺服器)。|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>受監視的使用者活動：以網域控制站為基礎的使用者作業

|受監視的活動|說明|
|---------------------|------------------|
|目錄服務複寫|使用者嘗試複寫目錄服務。|
|DNS 查詢|對網域控制站執行的查詢使用者類型 (**AXFR**、**TXT**、**MX**、**NS**、**SRV**、**ANY**、**DNSKEY**)。|
|私人資料擷取|使用者嘗試/成功使用 LSARPC 通訊協定查詢私人資料。|
|服務建立|使用者嘗試在遠端對遠端電腦建立特定服務。|
|SMB 工作階段列舉|使用者嘗試列舉網域控制站上已開啟 SMB 工作階段的所有使用者。|
|SMB 檔案複製|使用 SMB 的使用者複製檔案|
|SAMR 查詢|使用者執行了 SAMR 查詢。|
|工作排程|使用者嘗試在遠端對遠端電腦排程 X 工作。|
|Wmi 執行|使用者嘗試遠端執行 WMI 方法。|

## <a name="monitored-user-activities-login-operations"></a>受監視的使用者活動：登入作業

|登入類型|受監視的活動|說明|
|---------------------|---------------------|------------------|
|登入類型 2|認證驗證|使用 NTLM 和 Kerberos 驗證方法的網域帳戶驗證事件。|
|登入類型 2|互動式登入|使用者透過輸入使用者名稱與密碼 (驗證方法 Kerberos 或 NTLM) 取得了網路存取權。|
|登入類型 2|使用憑證的互動式登入|使用者使用憑證取得了網路存取權。|
|登入類型 2|VPN 連線|使用者已透過 VPN 連線 - 使用 RADIUS 通訊協定進行驗證。|
|登入類型 3|資源存取|使用者使用 Kerberos 或 NTLM 驗證存取了資源。|
|登入類型 3|委派資源存取|使用者使用 Kerberos 委派存取了資源。|
|登入類型 8|LDAP 純文字|使用者搭配純文字密碼 (簡單驗證) 使用 LDAP 進行了驗證。|
|登入類型 10|遠端桌面|使用者使用 Kerberos 驗證，對遠端電腦執行了 RDP 工作階段。|
|---|失敗的登入|網域帳戶的驗證嘗試失敗 (透過 NTLM 和 Kerberos)，原因如下：帳戶已停用/過期/鎖定/使用未受信任的憑證，或登入時數無效/舊密碼/密碼已過期/密碼錯誤。|
|---|使用憑證的失敗登入|網域帳戶的驗證嘗試失敗 (透過 Kerberos)，原因如下：帳戶已停用/過期/鎖定/使用未受信任的憑證，或登入時數無效/舊密碼/密碼已過期/密碼錯誤。|

## <a name="monitored-machine-activities-machine-account"></a>受監視的虛擬機器活動：電腦帳戶

|受監視的活動|說明|
|---------------------|------------------|
|電腦作業系統已變更|電腦 OS 的變更。

## <a name="see-also"></a>另請參閱

- [管理安全性警訊](working-with-suspicious-activities.md)
- [安全性警訊指南](suspicious-activity-guide.md)
- [調查實體](investigate-entity.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
