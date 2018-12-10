---
title: Azure ATP 已知問題 | Microsoft Docs
description: 說明 Azure ATP 目前已知問題
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1d478957b33e65e0016600826718ae6efd4e0e43
ms.sourcegitcommit: f4e1d3e28037afc7b9a22355808a04a8dc8b9605
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831437"
---
適用於：Azure 進階威脅防護

# <a name="azure-atp-known-issues"></a>Azure ATP 已知問題

Azure ATP 偶爾會有工程或功能上的限制，可能會限制或變更您組織使用 Azure ATP 服務的方式。 此處會說明沒有已知因應措施的已知問題限制，或是狀態為處理中但沒有具體更新時間表的工作。 

如需了解有已知因應措施的 Azure ATP 已知問題，請參閱[針對 Azure ATP 已知問題進行疑難排解](troubleshooting-atp-known-issues.md)。 若要查看您 Azure ATP 租用戶的狀態，請前往 [Azure ATP 健全狀況中心](atp-health-center.md)。 

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>超過 1000 名成員的 AD 群組，其詳細資料同步有限
> [!div class="mx-tableFixed"]  
|問題|狀態|
|----|----|
|Azure ATP 不支援在每個群組有超過 1000 名成員的 AD 群組中，進行實體詳細資料同步。 調查成員超過 1000 名之群組中的實體時，某些實體可能會無法同步或顯示詳細資料。|工程限制。 沒有任何已知的解決方式。|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>報表下載無法包含超過 100,000 個項目
> [!div class="mx-tableFixed"]  
|問題|狀態|
|----|----|
|Azure ATP 不支援下載每個報表包含超過 100,000 個項目的報表。 若報表包含的項目超過 100,000 個，報表會呈現為未完成。|工程限制。 沒有任何已知的解決方式。|

# <a name="closed"></a>關閉 

此群組的已知問題現在已關閉。 請檢查修正的版本號碼以取得參考。   
## <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>使用 Windows Server 2016 - v.2.57 (2018 年 12 月 2 日) 時，並未偵測到使用遠端 PowerShell 命令或指令碼的遠端程式碼執行嘗試
> [!div class="mx-tableFixed"]  
|問題|狀態|
|----|----|
|目前未在執行 Windows Server 2016 的感應器電腦上，偵測到遠端程式碼嘗試使用遠端 PowerShell 命令。 無法使用相關的偵測與結果警示。|工程小組目前正努力處理此問題，並新增 Windows Server 2016 支援。|

## <a name="see-also"></a>另請參閱

- [針對 Azure ATP 已知問題進行疑難排解](troubleshooting-atp-known-issues.md)
- [使用記錄檔針對 Azure ATP 進行疑難排解](troubleshooting-atp-using-logs.md)
- [Azure ATP 的新功能](atp-whats-new.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)