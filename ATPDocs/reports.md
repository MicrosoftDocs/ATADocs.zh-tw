---
title: 使用適用於身分識別的 Microsoft Defender 報告
description: 描述如何在適用於身分識別的 Microsoft Defender 中產生報告以監視您的網路。
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 1d09bd832167d960323ed0422a7858e9e512c4e1
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533455"
---
# <a name="microsoft-defender-for-identity-reports"></a>適用于身分識別報告的 Microsoft Defender

[!INCLUDE [Product long](includes/product-long.md)] 入口網站中的 [[!INCLUDE [Product short](includes/product-short.md)] 報告] 區段可讓您排程或立即產生並下載報告，為您提供系統與實體狀態資訊。 您可使用報告功能建立系統健全狀況、安全性警訊，以及在環境中偵測到之潛在橫向移動路徑的報告。

若要存取報表頁面，請按一下功能表列中的報表圖示：![報表圖示](media/report-icon.png)。
可用的報表包括：

- **摘要報表**：摘要報表提供系統中的狀態儀表板。 您可以檢視三個索引標籤：[摘要] 列出在您網路上偵測到的問題，[Open suspicious activities] \(開啟可疑活動\) 列出您應該處理的可疑活動，而 [Open health issues] \(開啟健康狀態問題\) 列出您應該處理的[!INCLUDE [Product short](includes/product-short.md)] 健康狀態問題。 列出的可疑活動和健康狀態問題會依類型細分。

- **敏感性群組的修改**：此報表會列出對敏感性群組 (例如系統管理員，或手動標記的帳戶或群組) 所做的每次修改。 若您使用[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器接收有關您敏感性群組的完整報告，必須先確定[事件會從您的網域控制站轉送至獨立感應器](configure-event-forwarding.md)。

- **密碼以純文字格式公開**：部分服務使用不安全的 LDAP 通訊協定，以純文字傳送帳戶認證。 即使是敏感性帳戶也可能會發生此情況。 監視網路流量的攻擊者可能會惡意攔截並重複使用這些認證。 此報告會列出[!INCLUDE [Product short](includes/product-short.md)] 偵測到以純文字傳送的所有來源電腦與帳戶密碼。

- **敏感性帳戶的橫向移動路徑**：此報告會列出透過橫向移動路徑公開的敏感性帳戶。 如需詳細資訊，請參閱[橫向移動路徑](use-case-lateral-movement-path.md)。 此報告會收集在您選取的報告期間中，偵測到的潛在橫向移動路徑。

產生報表的方式有兩種：依需求，或排程報表定期傳送到您的電子郵件。

若要依需求產生報表：

1. 在[!INCLUDE [Product short](includes/product-short.md)] 入口網站功能表列中，按一下功能表列中的報表圖示：![報表圖示](media/report-icon.png)。

1. 在您選取的報告類型下，設定 [開始] 與 [結束] 日期，然後按一下 [下載]。
 ![顯示報表下載的螢幕擷取畫面](media/reports.png)

若要設定排程的報表：

1. 在 [報告] 頁面中，按一下 [設定排程報告]，或在[!INCLUDE [Product short](includes/product-short.md)] 入口網站設定頁面中，按一下 [通知與報告] 下的 [排程報告]。

    ![排程報表](media/sched-reports.png)

    > [!NOTE]
    > 根據預設，每日報表會在午夜 (UTC) 過後不久傳送。 透過使用時間選取範圍選項，挑選您自己的時間。

1. 按一下您所選報告類型旁的 [排程]，以設定報告的傳遞頻率及電子郵件地址。 您選取的報告頻率會決定包含在報告中的資訊。 若要新增電子郵件地址，請按一下電子郵件地址欄位旁的加號，然後輸入地址並按一下 [儲存]。

    ![排程報表頻率和電子郵件](media/sched-report1.png)

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
