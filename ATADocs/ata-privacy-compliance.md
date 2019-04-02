---
title: 進階威脅分析個人資料原則 | Microsoft Docs
description: 提供如何從 ATA 刪除私人資訊和個人資料的相關資訊連結。
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 46f38285f2822e80744d3aa89b6eb820dd660367
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638978"
---
# <a name="ata-data-security-and-privacy"></a>ATA 資料安全性和隱私權

適用對象：*Advanced Threat Analytics 1.9 版*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>搜尋與識別個人資料 

ATA 中與實體相關的所有資料皆衍生自 Active Directory (AD)，且會從此處複寫至 ATA。 搜尋個人資料時，您應考慮優先搜尋 AD。 

從 ATA 中心使用搜尋列，可檢視儲存在資料庫中的可識別個人資料。 使用者可搜尋特定使用者或裝置。 按一下實體就會開啟使用者或裝置設定檔頁面。 設定檔會提供您實體的完整詳細資料、歷程記錄以及衍生自 AD 的網路活動。 

## <a name="updating-personal-data"></a>更新個人資料 

ATA 中有關使用者和實體的個人資料會衍生自您組織 AD 的使用者物件。 因此，對 AD 使用者設定檔進行的任何變更都會在 ATA 中產生影響。 

## <a name="deleting-personal-data"></a>刪除個人資料 

雖然 ATA 中的資料會複寫且一律從 AD 更新，但在實體於 AD 內刪除時，會保留實體留在 ATA 中的資料以供安全性調查之用。 

若要永久從 ATA 資料庫刪除使用者相關資料，請遵循此程序： 

1. [下載](https://aka.ms/ata-gdpr-script) MongoDB 指令碼 (gdpr.js)。  

2. 將指令碼下載至 ATA 資料夾 (位於 `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB`)，並從 ATA 中心電腦執行下列命令： 

使用 ATA GDPR 資料庫指令碼來刪除實體與實體活動資料，如下節所述。

### <a name="delete-entities"></a>刪除實體

此動作會從 ATA 資料庫永久刪除實體。 若要執行此命令，請提供命令名稱 `deleteAccount`、`SamName` 和 `UpnName`，或是與您欲刪除之電腦或使用者名稱相關的 `GUID`。 例如： 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

執行此動作會從資料庫完全移除具有 UPN admin1@contoso.com 的實體，以及與該實體相關的所有活動與安全性警示。 

### <a name="delete-entity-activity-data"></a>刪除實體活動資料

此動作會從 ATA 資料庫永久刪除實體的活動資料。 所有實體都會保持原樣，但在指定時間範圍內與其相關的活動與安全性警示均會悉數刪除。 

若要執行此命令，請提供命令名稱 `deleteOldData`，以及您要在資料庫中保留的資料天數。 

例如： 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

此指令碼會從資料庫移除所有超過 30 天的實體活動與安全性警示。 您只會保留最後 30 天的資料。

## <a name="exporting-personal-data"></a>探索個人資料 

因為 ATA 中與實體相關的資料均衍生自 AD，所以該資料只有一部份儲存在 ATA 資料庫。 因此，您應從 AD 匯出與實體相關的資料。 

ATA 可讓您將所有安全性相關資訊匯出為 Excel，其中可能包含個人資料。 

 
## <a name="opt-out-of-system-generated-logs"></a>選擇退出系統產生記錄 

ATA 會收集各部署的匿名系統產生記錄，並透過 HTTPS 將此資料傳輸至 Microsoft 伺服器。 Microsoft 將使用此資料以協助改善未來的 ATA 版本。 

如需詳細資訊，請參閱[管理系統產生的記錄](manage-telemetry-settings.md)。

若要停用資料收集：

1. 登入 ATA 主控台，按一下工具列中的三個點，然後選取 [關於]。 
2. 取消選取**將使用資訊傳送給我們，以於未來協助改善客戶經驗**的核取方塊。 

## <a name="additional-resources"></a>其他資源

- 如需 ATA 信任與合規性的相關資訊，請參閱[服務信任入口網站](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)與 [Microsoft 365 Enterprise GDPR 合規性網站](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview)。
