---
title: "ATA 1.8 版的新功能 | Microsoft Docs"
description: "列出 ATA 1.8 版的新功能以及已知問題"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 6850c5e8e264a9610e377a9ab4aadca338971ee1
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# ATA 1.8 版的新功能
<a id="whats-new-in-ata-version-18" class="xliff"></a>

[從下載中心下載](https://www.microsoft.com/download/details.aspx?id=55536) \(英文\) 最新的 ATA 更新版本，或者從[評估中心](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)下載完整版本。

這些版本資訊提供此版 Advanced Threat Analytics 中更新、新功能、錯誤修正和已知問題的相關資訊。



## 新的和更新的偵測項目
<a id="new--updated-detections" class="xliff"></a>

- 不尋常的通訊協定實作已改進為能夠偵測 WannaCry 惡意程式碼。

- 新增！ **敏感性群組的異常修改**：攻擊者會在權限提升階段期間，修改具有高權限的群組，以取得敏感性資源的存取權。 ATA 現在會偵測已提升權限之群組中有異常變更的情況。
- 新增！ **可疑的驗證失敗** (行為暴力密碼破解)：攻擊者嘗試對認證使用暴力密碼破解以入侵帳戶。 現在，ATA 在偵測到異常的驗證失敗行為時會引發警示。   

- **遠端執行嘗試 - WMI exec**：攻擊者可嘗試在網域控制站上從遠端執行程式碼，以控制您的網路。 ATA 已增強遠端執行偵測，包含 WMI 方法的偵測，以從遠端執行程式碼。

- 使用目錄服務查詢探查：此偵測已增強為能夠攔截對單一敏感性實體的查詢，並減少上一版所產生的誤判數目。 如果您在 1.7 版中停用這項功能，安裝 1.8 版現在會自動將它啟用。

- Kerberos 黃金票證活動：ATA 1.8 包含可偵測黃金票證攻擊的其他技術。
    - 現在，ATA 會偵測黃金票證存留間已過期的可疑活動。 如果 Kerberos 票證的使用超過允許的存留期，ATA 會偵測到可能已建立黃金票證的這項可疑活動。
- 下列偵測已增強以移除已知的誤判：  
    - 權限提升偵測 (偽造 PAC) 
    - 加密降級活動 (基本架構金鑰)
    - 不尋常的通訊協定實作
    - 信任中斷

## 改進可疑活動的分級
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   新增！ ATA 1.8 可讓您在分級程序期間，執行下列可疑活動動作： 
    - **排除實體**使其未來不會引發可疑活動，以防止 ATA 在偵測到良性的真肯定時發出警示 (例如系統管理員執行遠端程式碼或偵測安全性掃描程式)。
    - **隱藏週期性**可疑活動使其不會發出警示。
    - 從攻擊時間表中**刪除可疑活動**。
-   追蹤可疑活動警示的程序現在更有效率。 可疑活動時間表已經過重新設計。 在 ATA 1.8 中，您將能夠在單一畫面上顯示更多可疑活動資訊，其中包含用於分級和調查的更佳資訊。 

## 可協助您調查的新報表
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   新增！ 新增了**摘要報表**，可讓您查看 ATA 中所有摘要的資料，包括可疑活動、健康狀態問題等等。 您甚至可以定義週期性自動產生的自訂報表。
-   新增！ 新增了**敏感性群組報表**，可讓您查看特定期間內在敏感性群組中所做的全部變更。


## 基礎結構改進
<a id="infrastructure-improvements" class="xliff"></a>

-   已提升 ATA 中心效能。 在 ATA 1.8 中，ATA 中心每秒可以處理超過 1 百萬個封包。
-   ATA 輕量型閘道現在可以在本機讀取事件，而不需要設定事件轉送。
-   您現在可以為監視警示和可疑活動分別設定電子郵件。

## 安全性改善
<a id="security-improvements" class="xliff"></a>

-   新增！ **單一登入進行 ATA 管理**。 ATA 支援與 Windows 驗證整合的單一登入 (如果您已登入電腦，ATA 會使用該權杖將您登入 ATA 主控台)。 您也可以使用智慧卡進行登入。 ATA 閘道和 ATA 輕量型閘道的無訊息安裝指令碼現在使用登入的使用者內容，而不需要提供認證。
-   本機系統權限已從 ATA 閘道處理序中移除，因此您現在可以使用虛擬帳戶 (僅適用於獨立 ATA 閘道)、受管理的服務帳戶和群組受管理的服務帳戶，以執行 ATA 閘道處理序。   
-   新增了 ATA 中心和閘道的稽核記錄檔，所有動作現在會記錄在 Windows 事件記錄檔中。
-   新增了對 ATA 中心 KSP 憑證的支援。




## 另請參閱
<a id="see-also" class="xliff"></a>
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[將 ATA 更新至 1.8 版 - 移轉指南](ata-update-1.8-migration-guide.md)

