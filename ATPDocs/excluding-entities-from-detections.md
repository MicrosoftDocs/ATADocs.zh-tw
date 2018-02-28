---
title: "在 Azure 進階威脅防護中從偵測中排除實體 | Microsoft Doc"
description: "說明如何停止 Azure ATP 將特定實體活動視為可疑的活動"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護



# <a name="excluding-entities-from-detections"></a>從偵測中排除實體
本文說明如何排除實體以免觸發警示，以盡量減少良性的真肯定判斷，但能同時確保可攔截到真肯定判斷。 為了避免 Azure ATP 針對來自特定使用者，屬於您平常企業營運一部份的活動發出不必要的警示，您可以將特定實體設為靜音或排除，以避免引發警示。

例如，如果您有執行 DNS 偵察的安全性掃描程式，或是在網域控制站遠端執行指令碼的系統管理員，而這些都是屬於組織中正常 IT 作業之一的許可活動。 如需有關 Azure ATP 偵測協助您決定要排除哪些實體的詳細資訊，請參閱[可疑活動指南](suspicious-activity-guide.md)。

若要在 Azure ATP 中排除實體以避免引發警示：

您可以透過兩種方式排除實體，一是從可疑的活動本身，或從 [設定] 頁面上的 [排除項目] 索引標籤。

- **從可疑活動**：在可疑活動時間表中，當您收到有關允許執行特定活動 (且可能很頻繁) 之使用者、電腦或 IP 位址的活動警示，請以滑鼠右鍵按一下該實體上代表可疑活動之資料列結尾的三個點，並選取 [關閉並排除]。 <br></br>這會將該使用者、電腦或 IP 位址加入該可疑活動的排除清單中。 它也會關閉可疑活動，讓它不會再列於 [可疑的活動時間表] 中的 [開啟] 事件清單中。

    ![排除實體](./media/exclude-in-sa.png)

- **從 [設定] 頁面**：若要檢視或修改任何排除項目：在 [設定] 底下，按一下 [排除項目]，然後選擇可疑的活動，例如 [DNS 探查]。

    ![排除設定](./media/exclusions.png)

若要從 [排除項目] 設定中加入實體：輸入實體名稱，並按一下加號，然後按一下頁面底部的 [儲存]。

若要從 [排除項目] 設定中移除實體：按一下實體名稱旁邊的減號，然後按一下頁面底部的 [儲存]。

建議您僅在取得該類型的警示，並判斷它們為良性肯定之後，才將排除項目新增至偵測中。 

> [!NOTE]
> 為了保護之故，並不是所有的偵測都可設定排除項目。 

某些偵測會提供秘訣，協助您決定所要排除的項目。 

每一個排除項目都取決於所在的環境。在某些環境中，您可以設定使用者；而在其他環境中，則可以設定電腦或 IP 位址。 

當您可以排除 IP 位址或電腦時，您只需要排除其中一個，而不需要同時提供兩者。

> [!NOTE]
> 只有 Azure ATP 系統管理員才能修改設定頁面。


## <a name="see-also"></a>另請參閱

- [與 Windows Defender ATP 整合](integrate-wd-atp.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)