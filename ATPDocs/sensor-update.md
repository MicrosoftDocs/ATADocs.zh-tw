---
title: 更新適用於身分識別的 Microsoft Defender
description: 描述如何更新及延遲適用於身分識別的 Microsoft Defender 中的感應器更新。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d65de1862d97a1d8dbb84fdc84252851fbe44d63
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846777"
---
# <a name="update-product-long-sensors"></a>更新[!INCLUDE [Product long](includes/product-long.md)] 感應器

將您的[!INCLUDE [Product long](includes/product-long.md)] 感應器維持在最新狀態，為您的組織提供盡可能完善的保護。

[!INCLUDE [Product long](includes/product-long.md)] 服務一個月通常會更新幾次，以提供新偵測、功能與效能改進。 這些更新通常包括與感應器對應的次要更新。 [!INCLUDE [Product short](includes/product-short.md)] 感應器與對應的更新永遠不會有您網域控制站的寫入權限。 感應器更新套件只會控制[!INCLUDE [Product short](includes/product-short.md)] 感應器與感應器偵測功能。

## <a name="product-short-sensor-update-types"></a>[!INCLUDE [Product short](includes/product-short.md)] 感應器更新類型

[!INCLUDE [Product short](includes/product-short.md)] 感應器支援兩種更新：

- 次要版本更新：
  - 經常
  - 不需要 MSI 安裝，而且不會變更登錄
  - 已重新啟動：[!INCLUDE [Product short](includes/product-short.md)] 感應器服務
  - 未重新啟動：網域控制站服務與伺服器 OS

- 主要版本更新：
  - 罕見
  - 包含重大變更
  - 已重新啟動：[!INCLUDE [Product short](includes/product-short.md)] 感應器服務
  - 可能需要重新啟動：網域控制站服務與伺服器 OS

> [!NOTE]
>
> - 在[!INCLUDE [Product short](includes/product-short.md)] 入口網站設定頁面中，控制自動感應器重新啟動 (針對 **主要** 更新)。
> - [!INCLUDE [Product short](includes/product-short.md)] 感應器在安裝所在的網域控制站上一律會保留至少 15% 的可用記憶體與可用 CPU。 如果[!INCLUDE [Product short](includes/product-short.md)] 服務耗用太多記憶體，服務會自動停止並由[!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務重新啟動。

## <a name="delayed-sensor-update"></a>延遲感應器更新

由於目前[!INCLUDE [Product short](includes/product-short.md)] 開發及推出更新的速度都很快，您可以定義感應器的子集群組當作延遲更新通道，以提供漸進式的感應器更新程序。 [!INCLUDE [Product short](includes/product-short.md)] 可讓您選擇更新感應器的方式，並將每個感應器設定為 **延遲更新** 候選項目。

每當[!INCLUDE [Product short](includes/product-short.md)] 服務更新時，沒有選取為要延遲更新的感應器就會自動更新。 設定為 **延遲更新** 的感應器會在每個服務更新正式推出後，延遲 72 小時進行更新。

**延遲更新** 選項可讓您選取特定感應器作為自動更新通道，它們會在更新推出時自動更新，而您的其他感應器可以設定成延遲更新，讓您有時間確認自動更新的感應器都更新成功。

> [!NOTE]
> 如果發生錯誤，而且未更新感應器，則請開啟支援票證。 若要進一步強化 Proxy 以僅和您的執行個體通訊，請參閱 [Proxy 設定](configure-proxy.md)。
系統會使用強式的憑證式相互驗證，來進行感應器和 Azure 雲端服務之間的驗證。

每個更新都會在所有支援的作業系統上測試和驗證，將對網路和作業的影響降至最低。

將感應器設定為延遲更新：

1. 從[!INCLUDE [Product short](includes/product-short.md)] 入口網站，按一下設定圖示，然後選取 [設定]。
1. 按一下 [更新] 索引標籤。
1. 在您想要延遲之每個感應器旁的資料表資料列中，將 [Delayed update] \(延遲更新\) 滑桿設定為 [開啟]。
1. 按一下 **[儲存]** 。

## <a name="sensor-update-process"></a>感應器更新程序

[!INCLUDE [Product short](includes/product-short.md)] 感應器每隔幾分鐘就會檢查是否有最新版本。 將[!INCLUDE [Product short](includes/product-short.md)] 雲端服務更新為較新版本之後，[!INCLUDE [Product short](includes/product-short.md)] 感應器服務會開始進行更新程序：

1. [!INCLUDE [Product short](includes/product-short.md)] 雲端服務更新為最新版本。
1. [!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務會知道有已更新的版本。
1. 不是設定成 **延遲更新** 的感應器會逐一更新：
    1. [!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務從雲端服務提取已更新的版本 (cab 檔案格式)。
    1. [!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式驗證檔案簽章。
    1. [!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務將 cab 檔案解縮至感應器安裝資料夾中的新資料夾。 根據預設，會將其解壓縮至 *C:\Program Files\Azure Advanced Threat Protection Sensor\<version number>*
    1. [!INCLUDE [Product short](includes/product-short.md)] 感應器服務指向從 cab 檔案解壓縮的新檔案。
    1. [!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務啟動 [!INCLUDE [Product short](includes/product-short.md)] 感應器服務。
        > [!NOTE]
        > 次要感應器更新不會安裝 MSI，也不會變更登錄值或任何系統檔案。 即使有擱置的重新啟動也不影響感應器更新。
    1. 感應器會根據新的已更新版本執行。
    1. 感應器收到 Azure 雲端服務的許可。 您可以在 [更新] 頁面中確認感應器狀態。
    1. 下一個感應器啟動更新程序。

1. [!INCLUDE [Product short](includes/product-short.md)] 雲端服務更新過後 72 小時，選取為要 **延遲更新** 的感應器會按照自動更新之感應器的相同更新程序來更新。

![感應器更新](media/sensor-update.png)

系統會針對無法完成更新程序的任何感應器觸發相關健康情況警示，並以通知傳送。

![感應器更新失敗](media/sensor-outdated.png)

## <a name="see-also"></a>另請參閱

- [設定事件轉寄](configure-event-forwarding.md)
- [[!INCLUDE [Product short](includes/product-short.md)]先決條件](prerequisites.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
