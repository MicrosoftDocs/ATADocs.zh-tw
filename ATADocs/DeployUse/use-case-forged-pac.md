---
title: "調查偽造的 PAC 攻擊 | Microsoft Docs"
description: "本文說明偽造的 PAC 攻擊，並提供網路上偵測到這類威脅時的調查指示。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 437f387815fbbfbe261a192764a428e0d285ef32
ms.sourcegitcommit: 97aced94f47cf3c1b473d25b77d10a300c3f517e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2017
---
適用於︰Advanced Threat Analytics 1.7 版

# <a name="investigating-forged-pac-attacks"></a>調查偽造的 PAC 攻擊

Microsoft 不斷提升安全性偵測功能，並能夠向安全性分析師提供近乎即時的可採取行動情報。 Microsoft Advanced Threat Analytics (ATA) 有助於引導此項變更。 如果 ATA 在您的網路上偵測到偽造的 PAC 可疑活動，就會向您提出警示，本文會協助您了解並調查。

## <a name="what-is-a-privileged-access-certificate-pac"></a>什麼是特殊權限存取憑證 (PAC)？

權限屬性憑證 (PAC) 是 Kerberos 票證中的資料結構，此種票證掌握授權資訊，包括群組成員資格、安全性識別碼以及使用者設定檔資訊。 在 Active Directory 網域中，這可將網域控制站 (DC) 提供的授權資料傳遞給其他成員伺服器和工作站，用於驗證和授權。 除了成員資格資訊外，PAC 還包含額外的認證資訊、設定檔和原則資訊，以及支援的安全性中繼資料。 

驗證通訊協定 (驗證身分識別的通訊協定) 使用 PAC 資料結構傳輸授權資訊，以控制資源存取。

### <a name="pac-validation"></a>PAC 驗證

PAC 驗證是一種安全性功能，可以防止攻擊者以攔截式攻擊方式來未經授權而存取系統或其資源，尤其是在使用模擬使用者的應用程式中。 模擬牽涉到信任的身分識別，例如被授與提高權限可存取資源和執行工作的服務帳戶。 PAC 驗證可在使用模擬的 Kerberos 驗證設定中強化更安全的授權環境。 [PAC 驗證](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/)可確保使用者出示的確實是 Kerberos 票證授與的授權資料，而且票證權限未經修改。

進行 PAC 驗證時，伺服器會編碼包含 PAC 簽章類型和長度的要求訊息，並將其傳送到 DC。 DC 會解碼要求，並擷取伺服器總和檢查碼和 KDC 總和檢查碼值。 如果總和檢查碼驗證成功，DC 就會將成功代碼傳回伺服器。 不成功則傳回指出 PAC 已遭變更的代碼。 

Kerberos PAC 內容會簽署兩次︰ 
- 一次使用 KDC 的主要金鑰，防止惡意的伺服器端服務變更授權資料。
- 一次使用目的地資源伺服器帳戶的主要金鑰，防止使用者修改 PAC 內容以及新增自己的授權資料。

### <a name="pac-vulnerability"></a>PAC 弱點
資訊安全佈告欄 [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) 和 [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) 解決的 Kerberos KDC 弱點，可能會讓攻擊者操縱有效 Kerberos 票證中的 PAC 欄位，獲得額外的權限。

## <a name="forged-pac-attack"></a>偽造的 PAC 攻擊

偽造的 PAC 攻擊是攻擊者試圖利用這些弱點，提高其在您 Active Directory 樹系或網域中的權限。 若要發動此攻擊，攻擊者必須︰
-    具有網域使用者的認證。
-    具有可針對遭入侵網域認證進行驗證之網域控制站的網路連線。
-    使用正確的工具。 Python Kerberos 入侵套件 (PyKEK) 是已知的 PAC 偽造工具。

如果攻擊者擁有必要認證和連線能力，他們就可以修改或偽造現有的 Kerberos 使用者登入權杖 (TGT) 的特殊權限存取憑證 (PAC)。 攻擊者會變更群組成員資格宣告，以包含較高權限的群組 (例如，「網域系統管理員」或「企業系統管理員」)。 然後，攻擊者再將修改的 PAC 併入 Kerberos 票證中。 使用此 Kerberos 票證向未修補的網域控制站 (DC) 要求服務票證，提高攻擊者在網域和授權的權限，以執行他們本來不能執行的動作。 攻擊者會出示已修改的使用者登入權杖 (TGT)，要求資源的存取權杖 (TGS) 以存取網域中的任何資源。 這表示攻擊者可以偽裝成 Active Directory 中任何使用者的授權資料 (PAC)，略過所有限制存取網路的已設定資源 ACL。

## <a name="discovering-the-attack"></a>探索攻擊
當攻擊者嘗試提高其權限時，ATA 會偵測並將它標示為高嚴重性警示。

![偽造的 PAC 可疑活動](./media/forged-pac.png)

無論偽造的 PAC 成功與否，ATA 都會在可疑的活動警示中指出。 成功和失敗的警示都應該調查，因為嘗試失敗仍表示攻擊者在您的環境中出現過。

## <a name="investigating"></a>調查
收到 ATA 中偽造的 PAC 警示後，您需要判斷該做些什麼來緩和攻擊。 若要這樣做，您必須先將警示分類為下列其中一項︰ 
-    真肯定︰ATA 偵測到惡意的動作
-    誤判︰假警示 – 偽造的 PAC 攻擊並未真的發生 (這是 ATA 誤判為偽造的 PAC 攻擊事件)
-    良性真肯定︰ATA 偵測到確有其事但非惡意的動作，例如滲透測試。

下圖可協助您判斷應該採取哪些步驟︰

![偽造的 PAC 圖表](./media/forged-pac-diagram.png)

1. 首先檢查 ATA 攻擊時間軸中的警示，查看偽造的授權攻擊為成功、失敗或嘗試 (嘗試的攻擊也是失敗的攻擊)。 成功和失敗的攻擊都會造成「真肯定」，但在環境中會顯示不同的嚴重性。
 
 ![偽造的 PAC 可疑活動](./media/forged-pac-sa.png)


2.    偵測到的偽造的 PAC 攻擊如果成功︰
    -    如果發出警示的 DC 已正確修補過，則為誤判。 在此情況下，您應該關閉警示，傳送電子郵件到 ATAEval@microsoft.com 以通知 ATA 小組，協助我們持續改善偵測。 
    -    如果警示中的 DC 未經正確修補︰
        -    如果警示中列出的服務沒有自己的授權機制，這就是「真肯定」，您應該執行組織的事件回應 (IR) 程序。 
        -    如果警示中列出的服務有內部授權機制要求授權資料，可能會誤判為偽造的 PAC。 

3.    偵測到的攻擊如果失敗︰
    -    如果作業系統或應用程式已知要修改 PAC，則可能是「良性真肯定」，您應該和應用程式或作業系統的擁有者一起修正這個問題。

    -    如果作業系統或應用程式並未要修改 PAC︰ 

        -    如果列出的服務沒有自己的授權服務，這就是「真肯定」，您應該執行組織的事件回應 (IR) 程序。 即使攻擊者未成功提高其在網域中的權限，您可以假設您的網路中有攻擊者，而且您希望盡快找到他們，以免他們發動其他已知的進階持續性攻擊，以提高其權限。 
        -    如果警示中列出的服務有自己的授權機制要求授權資料，可能會誤判為偽造的 PAC。


Microsoft 建議您使用可透過 Microsoft 帳戶小組連絡的專業事件回應與復原小組，協助偵測攻擊者是否已在您網路中部署持續性方法。 這些方法可以透過使用惡意軟體以及身分識別缺口，例如遭竊的認證和黃金票證來發動攻擊。


## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [修改 ATA 組態](modifying-ata-configuration.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
