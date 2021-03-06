---
title: 適用於身分識別的 Microsoft Defender 安全性警示實驗室教學課程概觀
description: 此教學課程概觀描述用來模擬威脅以供 適用於身分識別的 Defender 偵測之適用於身分識別的 Microsoft Defender 安全性警示實驗室的四個部分。
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 61602a6bb7d3037d2278c2f492395ed058e8910b
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533557"
---
# <a name="tutorial-overview-microsoft-defender-for-identity-security-alert-lab"></a>教學課程總覽：適用于身分識別安全性警示實驗室的 Microsoft Defender

[!INCLUDE [Product long](includes/product-long.md)] 安全性警示實驗室教學課程的目的是要說明 **[!INCLUDE [Product short](includes/product-short.md)]** 對網路可疑活動與潛在攻擊的識別及偵測功能。 這個四部分的教學課程說明如何安裝及設定工作環境，以針對[!INCLUDE [Product short](includes/product-short.md)] 的一些「離散」偵測進行測試。 此實驗室將焦點放在[!INCLUDE [Product short](includes/product-short.md)] 的「特徵」型功能上。 此實驗室並不包括進階機器學習及使用者或實體型的行為偵測，因為這些偵測需要一個最多有 30 天真實網路流量的學習期間。

## <a name="lab-setup"></a>實驗室設定

這個四部分系列中的第一個教學課程會逐步引導您建立一個實驗室來測試[!INCLUDE [Product short](includes/product-short.md)] 的離散偵測。 此教學課程包括有關設定實驗室及完成其劇本所需的機器、使用者和工具的資訊。 這些指示假設您已熟悉為實驗室用途及其他管理工作，設定域控制站和工作站。 您的實驗室與建議的實驗室設定越相似，就越容易依照[!INCLUDE [Product short](includes/product-short.md)] 測試程序進行操作。 當您的實驗室設定完成時，請使 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示劇本來進行測試。

> [!div class="nextstepaction"]
> [設定 ATP 安全性警示實驗室](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>偵察劇本

這個四部分系列中的第二個教學課程是一個偵察劇本。 偵察活動可讓攻擊者取得對您環境的徹底了解和完整對應，以供稍後使用。 此劇本使用來自常見、可公開取得之入侵與攻擊工具的範例，示範[!INCLUDE [Product short](includes/product-short.md)] 對來自潛在攻擊之可疑活動的一些識別及偵測功能。

> [!div class="nextstepaction"]
> [偵察劇本](playbook-reconnaissance.md)

## <a name="lateral-movement-playbook"></a>橫向移動劇本

橫向移動劇本是四部分教學課程系列中的第三個。 橫向移動是由嘗試支配網域的攻擊者所進行的。 當您執行此劇本時，將會從您在實驗室中進行的模擬橫向移動，了解[!INCLUDE [Product short](includes/product-short.md)] 的橫向移動路徑威脅偵測與安全性警示服務。  

> [!div class="nextstepaction"]
> [橫向移動劇本](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>網域支配劇本

四部分系列中的最後一個教學課程是網域支配劇本。 在網域支配階段，攻擊者已經取得合法認證來存取您的網域控制站，並會嘗試達到持續性的網域支配。 您將模擬一些常見的網域支配方法，以了解[!INCLUDE [Product short](includes/product-short.md)] 以網域支配為焦點的威脅偵測與安全性警示服務。

> [!div class="nextstepaction"]
> [網域支配劇本](playbook-domain-dominance.md)


## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
