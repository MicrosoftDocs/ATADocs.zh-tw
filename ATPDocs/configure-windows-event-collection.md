---
title: 在 Azure 進階威脅防護中設定 Windows 事件收集 | Microsoft Docs
description: 在安裝 ATP 的這個步驟中，您要設定 Windows 事件收集。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 54a1d8311c0c0a717ad5a205248d366c65fc010a
ms.sourcegitcommit: c625acd3e44a3ba9619638f84264b3b271383e3a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/25/2020
ms.locfileid: "77590517"
---
# <a name="configure-windows-event-collection"></a>設定 Windows 事件集合

為增強威脅偵測功能，Azure 進階威脅防護 (Azure ATP) 需要下列 Windows 事件：4776、4732、4733、4728、4729、4756、4757、7045 與 8004。 Azure ATP 感應器可以自動讀取這些事件。如果沒有部署 Azure ATP 感應器，則有兩種方法可以將它們轉送到 Azure ATP 獨立感應器：一種是[將 Azure ATP 獨立感應器設定](configure-event-forwarding.md)為接聽 SIEM 事件，另一種是[設定 Windows 事件轉送](configure-event-forwarding.md)。

> [!NOTE]
>
> - Azure ATP 獨立感應器無法支援所有資料來源類型，因而會導致遺漏偵測。 若要完整涵蓋您的環境，建議您部署 Azure ATP 感應器。
> - 在設定事件收集之前，請務必檢閱並驗證您的[稽核原則](atp-advanced-audit-policy.md)，以確保網域控制站已正確設定為可記錄必要的事件。

除了收集和分析進出網域控制站的網路流量之外，Azure ATP 可以使用 Windows 事件來進一步加強偵測。 Azure ATP 會針對 NTLM 使用能增強各種偵測的 Windows 事件 4776 與 8004，並使用事件 4732、4733、4728、4729、4756、4757、7045 與 8004 以增強機密群組修改與服務建立的偵測。 這些可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送。 所收集的事件可提供 Azure ATP 透過網域控制站網路流量無法取得的額外資訊。

> [!NOTE]
> 要 收集 Windows 事件 8004 的網域群組原則應該**只**套用到網域控制站。

## <a name="ntlm-authentication-using-windows-event-8004"></a>使用 Windows 事件 8004 的 NTLM 驗證

設定 Windows 事件 8004 收集：

1. 瀏覽至：電腦設定\原則\Windows 設定\安全性設定\本機原則\安全性選項
2. 設定或建立**網域群組原則**，以套用到每個網域中的網域控制站，如下所示：
   - 網路安全性:限制 NTLM:限制 NTLM: 送往遠端伺服器的連出 NTLM 流量 = **全部稽核**
   - 網路安全性:限制 NTLM:限制 NTLM: 稽核這個網域的 NTLM 驗證 = **全部啟用**
   - 網路安全性:限制 NTLM:限制 NTLM: 稽核連入 NTLM 流量 = **啟用所有帳戶的稽核**

當 Windows 事件 8004 由 Azure ATP 感應器剖析時，會使用伺服器存取的資料加強 Azure ATP NTLM 驗證活動。

## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP SIEM 記錄檔參考](cef-format-sa.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
