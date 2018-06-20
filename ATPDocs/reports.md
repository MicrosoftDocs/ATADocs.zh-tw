---
title: 使用 Azure ATP 報表 | Microsoft Docs
description: 描述如何在 Azure ATP 中產生報表以監視您的網路。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8d9c7f9208ce76e6c2ca915729b9c64f769ae7bd
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202284"
---
適用於：Azure 進階威脅防護


# <a name="azure-atp-reports"></a>Azure ATP 報表

工作區入口網站中的 Azure ATP 報表區段可讓您產生報表，以提供系統狀態資訊，除了系統健康狀態，還報告您環境中偵測到的可疑活動。


若要存取報表頁面，請按一下功能表列中的報表圖示：![報表圖示](./media/atp-report-icon.png)。
可用的報表包括： 

- **摘要報表**：摘要報表提供系統中的狀態儀表板。 您可以檢視三個索引標籤：[摘要] 列出您網路上偵測到的問題，[Open suspicious activities (開啟可疑活動)] 列出您應該處理的可疑活動，而 [Open health issues (開啟健康狀態問題)] 列出您應該處理的 Azure ATP 系統健康狀態問題。 列出的可疑活動和健康狀態問題會依類型細分。 

- **機密群組的修改**：此報表會列出對敏感性群組 (例如系統管理員，或手動標記的帳戶或群組) 所做的每次修改。 如果您使用 Azure ATP 獨立感應器接收有關您機密群組的完整報表，則必須先確定[事件從您的網域控制站轉寄至獨立感應器](configure-event-forwarding.md)。 

- **密碼以純文字格式公開**：部分服務使用不安全的 LDAP 通訊協定，以純文字傳送帳戶認證。 即使是敏感性帳戶也可能會發生此情況。 監視網路流量的攻擊者可能會惡意攔截並重複使用這些認證。 此報表會列出所有來源電腦以及 Azure ATP 偵測到以純文字傳送之帳戶密碼。 

- **機密帳戶的橫向移動路徑**：此報表會列出透過橫向移動路徑公開的機密帳戶。 如需詳細資訊，請參閱[橫向移動路徑](use-case-lateral-movement-path.md)。 相對於工作區入口網站中顯示的資訊 (僅表示兩天)，此報表會收集過去的 60 天內建立的路徑。

產生報表的方式有兩種：依需求，或排程報表定期傳送到您的電子郵件。

若要依需求產生報表：

1. 在 Azure ATP 工作區入口網站功能表列中，按一下功能表列中的 [報表] 圖示： ![報表圖示](./media/atp-report-icon.png)。

2. 在您的已選取報表類型下，設定**開始**與**結束**日期，並按一下 [下載]。 
 ![報表](./media/reports.png)

若要設定排程的報表：
 
1. 在 [報表] 頁面中，按一下 [Set scheduled reports (設定排程的報表)]，或在 Azure ATP 工作區入口網站的 [設定] 頁面中，按一下 [Notifications and Reports (通知與報表)] 下的 [排程的報表]。

   ![排程報表](./media/atp-sched-reports.png)
 
 > [!NOTE]
 > 每日報表是設計為在午夜 (UTC) 過後不久傳送。

2. 按一下已選取報表類型旁的 [排程]，以設定傳送報表的頻率和電子郵件地址，按一下電子郵件地址旁的加號予以新增，然後按一下 [儲存]。

   ![排程報表頻率和電子郵件](./media/sched-report1.png)


## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)