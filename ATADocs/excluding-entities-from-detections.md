---
title: 在 Advanced Threat Analytics 中從偵測中排除實體 | Microsoft Doc
description: 說明如何停止 ATA 將特定實體活動視為可疑的活動
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21b1d8a4537bb77de120dac4b2f15bc785161749
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010256"
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="excluding-entities-from-detections"></a>從偵測中排除實體
本文說明如何排除實體以免觸發警示，以盡量減少良性的真肯定判斷，但能同時確保可攔截到真肯定判斷。 為了避免 ATA 針對來自特定使用者，屬於您平常企業營運一部份的活動發出不必要的警示，您可以將特定實體設為靜音或排除，以避免引發警示。

例如，如果您有執行 DNS 偵察的安全性掃描程式，或是在網域控制站遠端執行指令碼的系統管理員，而這些都是屬於組織中正常 IT 作業之一的許可活動。

若要在 ATA 中排除實體以避免引發警示：

您可以透過兩種方式排除實體，一是從可疑的活動本身，或從 [設定] 頁面上的 [排除項目] 索引標籤。

- **從可疑活動**：在可疑活動時間表中，當您收到有關允許執行特定活動 (且可能很頻繁) 之使用者、電腦或 IP 位址的活動警示，請以滑鼠右鍵按一下該實體上代表可疑活動之資料列結尾的三個點，並選取 [關閉並排除]。 <br></br>這會將該使用者、電腦或 IP 位址加入該可疑活動的排除清單中。 它也會關閉可疑活動，讓它不會再列於 [可疑的活動時間表] 中的 [開啟] 事件清單中。

    ![排除實體](./media/exclude-in-sa.png)

- **從 [設定] 頁面**：若要檢視或修改任何排除項目：在 [設定] 底下，按一下 [排除項目]，然後選擇可疑的活動，例如 [已公開敏感性帳戶認證]。

    ![排除設定](./media/exclusions-config-page.png)

若要從 [排除項目] 設定中移除實體：按一下實體名稱旁邊的減號，然後按一下頁面底部的 [儲存]。

建議您僅在取得該類型的警示，並判斷它們為良性肯定之後，才將排除項目新增至偵測中。 

> [!NOTE]
> 為了保護之故，並不是所有的偵測都可設定排除項目。 

某些偵測會提供秘訣，協助您決定所要排除的項目。 

每一個排除項目都取決於所在的環境。在某些環境中，您可以設定使用者；而在其他環境中，則可以設定電腦或 IP 位址。 

當您可以排除 IP 位址或電腦時，您只需要排除其中一個，而不需要同時提供兩者。

> [!NOTE]
> 只有 ATA 系統管理員才能修改設定頁面。


## <a name="see-also"></a>另請參閱
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [修改 ATA 組態](modifying-ata-center-configuration.md)
