---
title: 更新 Azure ATP 感應器 | Microsoft Docs
description: 此描述如何在 Azure ATP 中更新感應器。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a24210415929b69152377d34aeec1bdc8906d08c
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744433"
---
適用於：Azure 進階威脅防護


# <a name="update-azure-atp-sensors"></a>更新 Azure ATP 感應器
請務必保持最新的 Azure 進階威脅防護，以啟用組織的最佳可能保護。

一個月會使用 Bug 修正、效能改善和新偵測來更新Azure ATP 服務數次。 這些更新偶而需要感應器的對應更新。 

如果您未更新感應器，則感應器可能無法與 Azure ATP 雲端服務通訊，這樣可能會導致服務效能欠佳。 

系統會使用強式的憑證式相互驗證，來進行感應器和 Azure 雲端服務之間的驗證。 

每個更新都會在所有支援的作業系統上測試和驗證，將對網路和作業的影響降至最低。

### <a name="azure-atp-sensor-update-types"></a>Azure ATP 感應器更新類型   

Azure ATP 感應器支援兩種更新：
- 次要版本更新： 
  - 經常 
  - 不需要 MSI 安裝，而且登錄未變更
  - Azure ATP 服務服務重新啟動
  - 不需要重新啟動網域控制站和伺服器

- 主要版本更新：
 - 罕見
 - 可能需要重新啟動網域控制站和伺服器
 - 包含重大變更 

> [!NOTE]
>- 您可以在設定頁面中控制感應器的自動重新啟動 (在主要更新中)。 
> - Azure ATP 感應器一律會保留至少 15% 可用的記憶體和 CPU。 如果服務使用太多記憶體，則 Azure ATP 感應器更新程式服務會自動重新啟動它。

## <a name="delayed-sensor-update"></a>延遲感應器更新
若要允許更逐步的更新程序，Azure ATP 可讓您將感應器設定為 [Delayed update] \(延遲更新\) 候選項目。 

更新 Azure ATP 雲端服務時，通常會自動更新感應器。 設定為 [Delayed update] \(延遲更新\) 的感應器，將會在初始雲端服務更新後的 24 小時更新。

這可讓您選取自動推出更新的特定感應器，以及延遲更新感應器的其餘部分，但只在您看到初始更新平順進行之後。

> [!NOTE]
> 如果發生錯誤，而且未更新感應器，則請開啟支援票證。 若要進一步強化 Proxy 以僅和您的執行個體通訊，請參閱 [Proxy 設定](configure-proxy.md)

將感應器設定為延遲更新：

1. 從 Azure ATP 入口網站中，按一下設定圖示，然後選取 [設定]。
2. 按一下 [更新] 索引標籤。
3. 在您想要延遲之每個感應器旁的資料表資料列中，將 [Delayed update] \(延遲更新\) 滑桿設定為 [開啟]。
4. 按一下 **[儲存]**。
 
## <a name="sensor-update-process"></a>感應器更新程序

Azure ATP 感應器每隔幾分鐘都會檢查是否有最新版本。 將 Azure ATP 雲端服務更新為較新版本之後，Azure ATP 感應器服務會啟動更新程序：

1. Azure ATP 雲端服務更新為最新版本。
2. Azure ATP 感應器更新程式服務會知道有已更新的版本。
3. 未設定為 [Delayed update] \(延遲更新\) 的感應器啟動更新程序：
  1. Azure ATP 感應器更新程式服務從雲端服務提取更新版本 (cab 檔案格式)。
  2. Azure ATP 感應器更新程式驗證檔案簽章。
  3. Azure ATP 感應器更新程式服務將 cab 檔案擷取至感應器安裝資料夾中的新資料夾。 預設會將它擷取至 *C:\Program Files\Azure Advanced Threat Protection Sensor\<版本號碼>*
  4. Azure ATP 感應器更新程式服務啟動 Azure ATP 感應器服務。
  5. Azure ATP 感應器服務指向從 cab 檔案擷取的新檔案。
  > [!NOTE]
  >感應器的次要更新不會安裝 MSI 或是變更任何登錄值或任何系統檔案。 即使是擱置重新啟動也不會影響感應器的更新。 
  6. 感應器會根據新更新的版本執行。
  7. 感應器收到 Azure 雲端服務的許可。 這可以在 [更新] 頁面中驗證。
  8. 下一個感應器啟動更新程序。 

4. 在更新 Azure ATP 雲端服務後的 24 小時，已選取 [Delayed update] \(延遲更新\) 的感應器會啟動更新程序。

![感應器更新](./media/sensor-update.png)


失敗時，如果感應器未完成更新程序，則會觸發相關的監視警示，並將其傳送為通知。

![感應器過期](./media/sensor-outdated.png)


## <a name="see-also"></a>另請參閱

- [設定事件轉寄](configure-event-forwarding.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)