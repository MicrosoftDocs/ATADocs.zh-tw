---
title: ATA 1.8 版的新功能
description: 列出 ATA 1.8 版的新功能以及已知問題
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/03/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 6bacbf74ffc38809458cc2448c5162279ea89016
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913292"
---
# <a name="whats-new-in-ata-version-18"></a>ATA 1.8 版的新功能

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[從下載中心下載](https://www.microsoft.com/download/details.aspx?id=55536) \(英文\) 最新的 ATA 更新版本，或者從[評估中心](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)下載完整版本。

這些版本資訊提供此版 Advanced Threat Analytics 中更新、新功能、錯誤修正和已知問題的相關資訊。

## <a name="new--updated-detections"></a>新的和更新的偵測項目

- 不尋常的通訊協定實作已改進為能夠偵測 WannaCry 惡意程式碼。

- 新增！ **敏感性群組的異常修改**  
攻擊者會在權限提升階段期間，修改具有高權限的群組，以取得敏感性資源的存取權。 ATA 現在會偵測提高許可權的群組中是否有異常變更。
- 新增！ **可疑的驗證失敗** (行為暴力密碼破解)  
攻擊者嘗試對認證使用暴力密碼破解以入侵帳戶。 現在，ATA 在偵測到異常的驗證失敗行為時會引發警示。

- **遠端執行嘗試 - WMI exec**  
攻擊者可嘗試在網域控制站上從遠端執行程式碼，以控制您的網路。 ATA 已增強遠端執行偵測，包含 WMI 方法的偵測，以從遠端執行程式碼。

- 使用目錄服務查詢的偵察  
這項偵測已增強，可讓您針對單一敏感性實體攔截查詢，並減少在先前版本中產生的誤報數目。 如果您在 1.7 版中停用這項功能，安裝 1.8 版現在會自動將它啟用。

- Kerberos 黃金票證活動  
ATA 1.8 包含額外的技術來偵測黃金票證攻擊。
  - 現在，ATA 會偵測黃金票證存留間已過期的可疑活動。 如果 Kerberos 票證的使用超過允許的存留期，ATA 會偵測到可能已建立黃金票證的這項可疑活動。
- 下列偵測已增強以移除已知的誤判：
  - 權限提升偵測 (偽造 PAC)
  - 加密降級活動 (基本架構金鑰)
  - 不尋常的通訊協定實作
  - 信任中斷

## <a name="improved-triage-of-suspicious-activities"></a>改進可疑活動的分級

- 新增！ ATA 1.8 可讓您在分級程序期間，執行下列可疑活動動作：
  - **排除實體**使其未來不會引發可疑活動，以防止 ATA 在偵測到良性的真肯定時發出警示 (例如系統管理員執行遠端程式碼或偵測安全性掃描程式)。
  - **隱藏週期性**可疑活動使其不會發出警示。
  - 從攻擊時間表中**刪除可疑活動**。
- 追蹤可疑活動警示的程序現在更有效率。 可疑活動時間表已經過重新設計。 在 ATA 1.8 中，您只要在單一畫面上就能看到更多可疑的活動，並有更詳細的資訊可用於分級和調查用途。

## <a name="new-reports-to-help-you-investigate"></a>可協助您調查的新報表

- 新增！ 新增了**摘要報表**，可讓您查看 ATA 中所有摘要的資料，包括可疑活動、健康狀態問題等等。 您甚至可以定義週期性自動產生的自訂報表。
- 新增！ 新增了**敏感性群組報表**，可讓您查看特定期間內在敏感性群組中所做的全部變更。

## <a name="infrastructure-improvements"></a>基礎結構改進

- 已提升 ATA 中心效能。 在 ATA 1.8 中，ATA 中心每秒可以處理超過 1 百萬個封包。
- ATA 輕量型閘道現在可以在本機讀取事件，而不需要設定事件轉送。
- 您現在可以針對健康情況警示和可疑活動，另外設定電子郵件。

## <a name="security-improvements"></a>安全性改善

- 新增！ **單一登入進行 ATA 管理**。 ATA 支援與 Windows 驗證整合的單一登入 (如果您已登入電腦，ATA 會使用該權杖將您登入 ATA 主控台)。 您也可以使用智慧卡進行登入。 ATA 閘道和 ATA 輕量閘道的無訊息安裝腳本現在會使用登入的使用者內容，而不需要提供認證。
- 本機系統權限已從 ATA 閘道處理序中移除，因此您現在可以使用虛擬帳戶 (僅適用於獨立 ATA 閘道)、受管理的服務帳戶和群組受管理的服務帳戶，以執行 ATA 閘道處理序。
- 新增了 ATA 中心和閘道的稽核記錄檔，所有動作現在會記錄在 Windows 事件記錄檔中。
- 新增了對 ATA 中心 KSP 憑證的支援。

## <a name="additional-changes"></a>其他變更

- 新增附註的選項已從 [可疑活動] 移除
- 緩和可疑活動的建議已從可疑活動時間表移除。
- 開始使用 ATA 1.8 版。ATA 閘道與輕量型閘道會管理自己的憑證，且不需要系統管理員互動來管理。

## <a name="known-issues"></a>已知問題

> [!WARNING]
> 若要避免這些已知問題，請使用 1.8 更新 1 來更新或部署。

### <a name="ata-gateway-on-windows-server-core"></a>Windows Server Core 上的 ATA 閘道

**徵兆**：在具有 .Net Framework 4.7 的 Windows Server 2012R2 Core 上將 ATA 閘道版本升級至 1.8 可能失敗，並出現錯誤：Microsoft Advanced Threat Analytics 閘道已停止運作**。

![閘道核心錯誤](media/gateway-core-error.png)

在 Windows Server 2016 Core 上可能不會出現錯誤，但當您嘗試安裝時，處理序將會失敗，而且會在伺服器上的應用程式事件記錄檔中記錄事件 1000 和 1001 (處理序損毀)。

**描述**：.NET Framework 4.7 發生問題，導致使用 WPF 技術 (例如 ATA) 的應用程式無法載入。 如需詳細資訊，[請參閱 KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on)。

**因應措施**：將 .Net 4.7 解除安裝。[請參閱 KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) 以將 .NET 版本還原為 .NET 4.6.2，然後將 ATA 閘道版本更新至 1.8。 ATA 升級完成之後，您就可以重新安裝 .NET 4.7。  未來版本將會有更新以修正此問題。

### <a name="lightweight-gateway-event-log-permissions"></a>輕量型閘道事件記錄檔權限

**徵兆**：升級至 ATA 1.8 後，先前已授與權限以存取安全性事件記錄檔的應用程式或服務可能會喪失權限。

**描述**：為了讓您更輕鬆地部署 ATA，ATA 1.8 不需要 Windows 事件轉送設定就可直接存取安全性事件記錄檔。 同時，ATA 會作為低權限的本機服務執行，以維護更嚴格的安全性。 為了提供 ATA 讀取事件的存取權，ATA 服務會對自己授與安全性事件記錄檔的權限。 當發生這種情況時，可能會停用先前為其他服務設定的權限。

**因應措施**：執行下列 Windows PowerShell 指令碼。 這會從 ATA 移除登錄中未正確新增的權限，並透過其他 API 加以新增。 這可能會還原其他應用程式的權限。 如果未還原，則必須將其手動還原。 未來版本將會有更新以修正此問題。

```powershell
$ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
  try {
    $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
    $ATASddl = "O:BAG:SYD:" + $ATADaclEntry
    if($SecurityDescriptor.CustomSD -eq $ATASddl) {
      Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
    }
  }
  catch
  {
    # registry key does not exist
  }

$EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
$EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry
$EventLogConfiguration.SaveChanges()
```

### <a name="proxy-interference"></a>Proxy 干擾

**徵兆**：升級至 ATA 1.8 後，ATA 閘道服務可能會無法啟動。 在 ATA 錯誤記錄檔中，您可能會看到下列例外狀況：System.Net.Http.HttpRequestException: 傳送要求時發生錯誤。---> System.Net.WebException: 遠端伺服器傳回錯誤: (407) 要求 Proxy 驗證。**

**描述**：從 ATA 1.8 開始，ATA 閘道使用 HTTP 通訊協定與 ATA 中心進行通訊。 如果安裝了 ATA 閘道的電腦使用 Proxy 伺服器來連線到 ATA 中心，可能會中斷此通訊。

**因應措施**：在 ATA 閘道服務帳戶上停用 Proxy 伺服器。 未來版本將會有更新以修正此問題。

### <a name="report-settings-reset"></a>報表設定重設

**徵兆**：當您更新至 1.8 Update 1 時，會清除對已排程報表所做的任何設定。

**描述**：從 1.8 更新至 1.8 Update 1 會重設報表排程設定。

**因應措施**：更新至 1.8 Update 1 之前，請複製並重新輸入報表設定，這也可透過指令碼來完成。如需詳細資訊，請參閱[匯出和匯入 ATA 設定](ata-configuration-file.md)。

## <a name="see-also"></a>另請參閱

[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[將 ATA 更新至 1.8 版 - 移轉指南](ata-update-1.8-migration-guide.md)
