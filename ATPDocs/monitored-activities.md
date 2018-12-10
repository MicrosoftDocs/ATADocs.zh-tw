---
title: 受 Azure ATP 監視的網域活動 |Microsoft Docs
description: 描述 Azure 進階威脅防護監視的每一種活動類型
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 37d1a032-65e7-4a89-be0b-c3f9cc2bacdb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: afcad5dccda979bed54e7808bddb3c4190f5c3a8
ms.sourcegitcommit: bdf5dc203ecec3e7542f2ed08852afeff4f20dcd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2018
ms.locfileid: "52950334"
---
適用於：Azure 進階威脅防護



# <a name="azure-atp-monitored-activities"></a>受 Azure ATP 監視的活動

Azure 進階威脅防護會監視您組織 Active Directory 產生的資訊、網路活動及事件活動，來偵測可疑活動。 受監視的活動資訊可讓 Azure ATP 協助您判斷每個潛在威脅的有效性，並正確分與回應。 

在有效威脅或**確判**的情況下，Azure ATP 可讓您探索每個事件的缺口範圍；調查涉及的實體有哪些，以及判斷如何予以補救。

受 Azure ATP 監視的資訊會以活動形式呈現。 Azure ATP 目前支援監視下列活動類型：

> [!NOTE] 
> - 本文與所有 Azure ATP 感應器類型皆有關。
>- 受 Azure ATP 監視的活動會同時出現在使用者和電腦設定檔頁面上。 
 

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>受監視使用者活動：使用者帳戶 AD 屬性變更

|受監視的活動|說明|
|---------------------|------------------|
|使用者電子郵件已變更|使用者電子郵件屬性已變更。|
|使用者管理員已變更|使用者的管理員屬性已變更。|
|使用者電話號碼已變更|使用者的電話號碼屬性已變更。|
|使用者標題已變更 |使用者的標題屬性已變更。|
|帳戶限制委派狀態已變更 |帳戶狀態目前為啟用或停用委派。|
|帳戶限制委派 Spn 已變更 | 限制委派會限制指定伺服器可以代表使用者執行的目標服務。|
|帳戶停用已變更 |指出帳戶為停用或啟用。|
|帳戶過期|帳戶過期的日期。|
|帳戶過期時間已變更 |帳戶過期日期的變更。|
|帳戶鎖定已變更|帳戶過期日期的變更。|
|帳戶密碼已變更|使用者已變更密碼。|
|帳戶密碼已過期 |使用者的密碼已過期。|
|密碼永久有效已變更 |使用者的密碼已變更為永久有效。|
|不需帳戶密碼已變更 |使用者帳戶已變更，允許使用空白密碼登入。|
|需要帳戶智慧卡已變更  |帳戶已變更為要求使用者以智慧卡登入裝置。|
|帳戶支援的加密類型已變更 |Kerberos 支援的加密類型已變更 (類型：Des、AES 129、AES 256)|
|群組成員資格已變更  |使用者已由另一名使用者，或自行新增到群組或從中移除。|
|帳戶 Upn 名稱已變更  |使用者的主體名稱已變更。|

## <a name="monitored-user-activities-ad-security-principal-operations"></a>受監視使用者活動：AD 安全性主體作業

|受監視的活動|說明|
|---------------------|------------------|
|安全性主體已建立 |帳戶已建立 (使用者及電腦)。|
|安全性主體刪除已變更  |帳戶已刪除/還原 (使用者及電腦)。|
|安全性主體顯示名稱已變更   |帳戶顯示名稱已從 X 變更為 Y。|
|安全性主體名稱已變更  |帳戶名稱屬性已變更。|
|安全性主體路徑已變更  |帳戶辨別名稱已從 X 變更為 Y。|
|安全性主體 Sam 名稱已變更 |SAM 名稱已變更 (SAM 是登入名稱，用來支援執行較舊版作業系統的用戶端和伺服器)。|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>受監視使用者活動：以網域控制站為基礎的使用者作業

|受監視的活動|說明|
|---------------------|------------------|
|目錄服務複寫  |使用者嘗試複寫目錄服務。|
|DNS 查詢  |使用者對網域控制站執行了 AXFR 查詢。|
|Wmi 執行  |使用者嘗試遠端執行 WMI 方法。|
|服務建立   |使用者嘗試在遠端對遠端電腦建立特定服務。|
|SMB 工作階段列舉   |使用者嘗試列舉網域控制站上已開啟 SMB 工作階段的所有使用者。|
|SMB 檔案複製| 使用 SMB 的使用者複製檔案|
|工作排程  |使用者嘗試在遠端對遠端電腦排程 X 工作。|
|SAMR 查詢   |使用者執行了 SAMR 查詢。|
|私人資料擷取  |使用者嘗試/成功使用 LSARPC 通訊協定查詢私人資料。|




## <a name="monitored-user-activities-login-operations"></a>受監視使用者活動：登入作業

|登入類型|受監視的活動|說明|
|---------------------|---------------------|------------------|
|登入類型 2|認證驗證  |使用 NTLM 和 Kerberos 驗證方法的網域帳戶驗證事件。|
|登入類型 2|互動式登入  |使用者透過輸入使用者名稱及密碼 (驗證方法 Kerberos) 取得了網路存取權。|
|登入類型 2|VPN 連線   |使用者已透過 VPN 連線 - 使用 RADIUS 通訊協定進行驗證。|
|登入類型 3|資源存取  |使用者使用 Kerberos 驗證存取了資源。|
|登入類型 8|LDAP 純文字  |使用者搭配純文字密碼 (簡單驗證) 使用 LDAP 進行了驗證。|
|登入類型 10|遠端桌面 |使用者使用 Kerberos 驗證，對遠端電腦執行了 RDP 工作階段。|
| --- |失敗的登入 |網域帳戶的驗證嘗試失敗 (透過 NTLM 和 Kerberos)，原因如下：帳戶已停用/過期/鎖定/使用未受信任的憑證，或登入時數無效/舊密碼/密碼已過期/密碼錯誤。|


## <a name="monitored-machine-activities-machine-account"></a>受監視電腦活動：電腦帳戶

|受監視的活動|說明|
|---------------------|------------------|
|電腦作業系統已變更|電腦 OS 的變更。


## <a name="see-also"></a>另請參閱
- [管理安全性警訊](working-with-suspicious-activities.md)
- [安全性警訊指南](suspicious-activity-guide.md)
- [調查實體](investigate-entity.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
