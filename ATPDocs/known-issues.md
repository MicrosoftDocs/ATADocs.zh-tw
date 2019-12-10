---
title: Azure ATP 已知問題 | Microsoft Docs
description: 說明 Azure ATP 目前已知問題
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2bfa219334960300901ac47129800d52a80a69a
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65193526"
---
# <a name="azure-atp-known-issues"></a>Azure ATP 已知問題

Azure ATP 偶爾會有工程或功能上的限制，可能會限制或變更您組織使用 Azure ATP 服務的方式。 此處會說明沒有已知因應措施的已知問題限制，或是狀態為處理中但沒有具體更新時間表的工作。 

如需了解有已知因應措施的 Azure ATP 已知問題，請參閱[針對 Azure ATP 已知問題進行疑難排解](troubleshooting-atp-known-issues.md)。 若要查看您 Azure ATP 租用戶的狀態，請前往 [Azure ATP 健全狀況中心](atp-health-center.md)。 

## <a name="dns-reconnaissance-alert"></a>DNS 偵察警示
> [!div class="mx-tableFixed"] 

|問題|狀態|
|----|----|
*DNS 偵察*安全性警示問題會影響客戶，因為它會從單一機器發出重複的假警報 **DNS 偵察問題警示**。 若觀察到產生自單一機器的大量 **DNS 偵察警示**，在部署 2.67 並解決此問題之前關閉或刪除這些警示。 | 更新 2.67 可解決此問題。|

## <a name="suspected-brute-force-attack-ldap-security-alert-display"></a>顯示可疑的暴力密碼破解攻擊 (LDAP) 安全性警訊
> [!div class="mx-tableFixed"] 

|問題|狀態|
|----|----|
可疑的暴力密碼破解攻擊 (LDAP)  安全性警訊並不會總是如預期般顯示。 在某些情況下，警示描述會以錯誤的方式顯示。| 工程小組正在努力處理此問題。| 

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>超過 1000 名成員的 AD 群組，其詳細資料同步有限
> [!div class="mx-tableFixed"]  
> 
> |問題|狀態|
> |----|----|
> |Azure ATP 不支援在每個群組有超過 1000 名成員的 AD 群組中，進行實體詳細資料同步。 調查成員超過 1000 名之群組中的實體時，某些實體可能會無法同步或顯示詳細資料。|工程限制。 沒有任何已知的解決方式。|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>報表下載無法包含超過 100,000 個項目
> [!div class="mx-tableFixed"]  
> 
> |問題|狀態|
> |----|----|
> |Azure ATP 不支援下載每個報表包含超過 100,000 個項目的報表。 若報表包含的項目超過 100,000 個，報表會呈現為未完成。|工程限制。 沒有任何已知的解決方式。|

## <a name="closed-issues"></a>已關閉的問題

此群組的已知問題現在已關閉。 請檢查修正的版本號碼以取得參考。   
### <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>使用 Windows Server 2016 - v.2.57 (2018 年 12 月 2 日) 時，並未偵測到使用遠端 PowerShell 命令或指令碼的遠端程式碼執行嘗試
> [!div class="mx-tableFixed"]  
> 
> |問題|狀態|
> |----|----|
> |目前未在執行 Windows Server 2016 的感應器電腦上，偵測到遠端程式碼嘗試使用遠端 PowerShell 命令。 無法使用相關的偵測與結果警示。|工程小組目前正努力處理此問題，並新增 Windows Server 2016 支援。|

## <a name="see-also"></a>另請參閱

- [針對 Azure ATP 已知問題進行疑難排解](troubleshooting-atp-known-issues.md)
- [使用記錄檔針對 Azure ATP 進行疑難排解](troubleshooting-atp-using-logs.md)
- [Azure ATP 的新功能](atp-whats-new.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
