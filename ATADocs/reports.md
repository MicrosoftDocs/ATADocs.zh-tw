---
title: 使用 ATA 報表 | Microsoft Docs
description: 描述如何在 ATA 中產生報表以監視您的網路。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eaa579a6b82bab27bba0ddb79b39f06bd495debc
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133220"
---
*適用於：Advanced Threat Analytics 1.9 版*


# <a name="ata-reports"></a>ATA 報表

主控台中的 ATA 報表區段可讓您產生報表，以提供系統狀態資訊，除了系統健康狀態，還報告您環境中偵測到的可疑活動。

若要存取報表頁面，請按一下功能表列中的報表圖示：![報表圖示](./media/ata-report-icon.png)。
可用的報表包括： 

- **摘要報表**：摘要報表提供系統中的狀態儀表板。 您可以檢視三個索引標籤：[摘要] 列出您網路上偵測到的問題，[Open suspicious activities (開啟可疑活動)] 列出您應該處理的可疑活動，而 [Open health issues (開啟健康狀態問題)] 列出您應該處理的 ATA 系統健康狀態問題。 列出的可疑活動和健康狀態問題會依類型細分。 

- **敏感性群組的修改**：此報表會列出對敏感性群組 (例如系統管理員) 進行的每次修改。

- **密碼以純文字格式公開**：部分服務使用不安全的 LDAP 通訊協定，以純文字傳送帳戶認證。 即使是敏感性帳戶也可能會發生此情況。 監視網路流量的攻擊者可能會惡意攔截並重複使用這些認證。 此報表會列出所有來源電腦，以及 ATA 所偵測到以純文字傳送的帳戶密碼。 

- **機密帳戶的橫向移動路徑**：此報表會列出透過橫向移動路徑公開的機密帳戶。 如需詳細資訊，請參閱[橫向移動路徑](use-case-lateral-movement-path.md)

產生報表的方式有兩種：依需求，或排程報表定期傳送到您的電子郵件。

若要依需求產生報表：

1. 在 ATA 主控台功能表列中，按一下功能表列中的報表圖示： ![報表圖示](./media/ata-report-icon.png)。

2. 在您的已選取報表類型下，設定**開始**與**結束**日期，並按一下 [下載]。 
 ![報表](./media/reports.png)

若要設定排程的報表：
 
1. 在 [報表] 頁面中，按一下 [Set scheduled reports (設定排程的報表)]，或在 ATA 主控台的 [設定] 頁面中，按一下 [Notifications and Reports (通知與報表)] 下的 [排程的報表]。

   ![排程報表](./media/ata-sched-reports.png)

  > [!NOTE]
  > 每日報表是設計為在午夜 (UTC) 過後不久傳送。

2. 按一下已選取報表類型旁的 [排程]，以設定傳送報表的頻率和電子郵件地址，按一下電子郵件地址旁的加號予以新增，然後按一下 [儲存]。

   ![排程報表頻率和電子郵件](./media/sched-report1.png)


> [!NOTE]
> 排程的報表會以電子郵件形式傳送，您必須已在 [設定] 下設定電子郵件伺服器，然後在 [通知與報表] 下選取 [郵件伺服器]，才能傳送這些報表。


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
