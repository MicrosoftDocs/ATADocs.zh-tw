---
title: 在 Azure 進階威脅防護中從偵測中排除實體
description: 說明如何停止 Azure ATP 將特定實體活動視為可疑的活動
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 11/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bc777fde6cdf12abb45b9608091166e3cf03ee2c
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80669575"
---
# <a name="excluding-entities-from-detections"></a>從偵測中排除實體
本文說明如何從觸發警示中排除實體。 排除某些實體可減少良性確判，同時確保您能攔截到確判。 為了避免讓 Azure ATP 在平常企業營運時，從特定使用者發出不必要的警示，您可設為靜音或排除對特定實體發出警示。 此外，預設會排除某些常用實體。 

例如，如果您有執行 DNS 偵察的安全性掃描器，或是在網域控制站上遠端執行指令碼的系統管理員，這些都屬於組織中正常 IT 作業中的許可活動，可以排除。 如需各 Azure ATP 偵測的詳細資訊，以協助您決定要排除的實體，請參閱[安全性警訊指南](suspicious-activity-guide.md)。

## <a name="entities-excluded-by-default-from-raising-alerts"></a>預設會排除而不引發警示的實體
 對於像是**經由 DNS 進行的可疑通訊**等特定警示，Azure ATP 會依據客戶意見反應及研究，新增自動排除的網域項目。 
 
![經由 DNS 進行的可疑通訊自動排除項目](./media/dns-auto-exclusions.png) 

## <a name="exclude-entities-from-raising-alerts"></a>排除而不引發警示的實體

有兩種方式可手動排除實體，一種是直接透過安全性警訊，一種是透過 [設定] 頁面上的 [排除項目] 索引標籤。 

- **透過安全性警訊**：在活動時間軸中，當您收到**允許**頻繁執行特定活動之使用者、電腦或 IP 位址的活動警示時，請執行下列步驟：
  - 在該列末端的三個點上按一下按右鍵，開啟該實體的安全性警訊，並選取 [關閉並排除]  。 如此會將使用者、電腦或 IP 位址，新增到該安全性警訊的排除項目清單中。 如此會關閉安全性警訊，且警示將不會繼續列於**警示時間軸**中的**未結案**事件清單。

    ![排除實體](./media/exclude-in-sa.png)

- **從 [設定] 頁面**：若要檢閱或修改任何排除項目：請在 [設定]  下，按一下 [排除項目]  ，然後選取要套用排除的安全性警訊，例如 **DNS 偵查**。

    ![排除設定](./media/exclusions.png)

若要從 [排除項目]  設定中新增實體：請輸入實體名稱，並按一下加號，然後按一下頁面底部的 [儲存]  。

若要從 [排除項目]  設定中移除實體：請按一下實體名稱旁的減號，然後按一下頁面底部的 [儲存]  。

建議您只有在取得該特定類型的警示，*且*判斷它們為良性確判之後，才將排除項目新增至偵測中。 

> [!NOTE]
> 為了保護之故，並不是所有的偵測都可設定排除項目。 

某些偵測會提供秘訣，協助您決定所要排除的項目。 

每一個排除項目都取決於所在的環境。在某些環境中，您可以設定使用者；而在其他環境中，則可以設定電腦或 IP 位址。 

當您可以排除 IP 位址或電腦時，您只需要排除其中一個，而不需要同時提供兩者。

> [!NOTE]
> 只有 Azure ATP 系統管理員才可修改設定頁面。


## <a name="see-also"></a>另請參閱

- [Azure ATP 安全性警訊指南](suspicious-activity-guide.md)
- [與 Microsoft Defender ATP 整合](integrate-wd-atp.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
