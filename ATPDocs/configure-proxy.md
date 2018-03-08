---
title: "設定您的 Proxy 或防火牆，以啟用與感應器的 Azure ATP 通訊 | Microsoft Docs"
description: "描述如何設定防火牆或 Proxy，以允許 Azure ATP 雲端服務和 Azure ATP 感應器之間的通訊"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f077bbd9990affbb6c552c5ad8875fdfebbd70f2
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
適用於：Azure 進階威脅防護



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>設定您的 Proxy 以允許 Azure ATP 感應器與 Azure ATP 雲端服務之間的通訊

若要讓網域控制站與雲端服務通訊，您必須在防火牆或 Proxy 中開啟：*.atp.azure.com 連接埠 443。 設定必須是在電腦層級 (=電腦帳戶) 而不是在使用者帳戶層級。 您可以使用下列步驟測試您的組態：
 
1.  確認**目前使用者**可使用 IE 瀏覽 DC 的下列 URL 來存取處理器端點：https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (適用於美國)，您應該會收到錯誤 503：

 ![服務無法使用](./media/service-unavailable.png)
 
2.  如果您沒有收到錯誤 503，請檢閱 Proxy 設定並再試一次。

3.  如果 Proxy 設定適用於 **CURRENT_USER** (也就是您有看到 503 錯誤)，則請以提升權限的命令提示字元執行下列命令，查看 WinInet Proxy 設定是否已針對 **LOCAL_SYSTEM** 帳戶 (由感應器更新程式服務使用) 啟用：
 
    reg compare "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" /v DefaultConnectionSettings

如果您收到「錯誤: 系統找不到指定的登錄機碼或值。」 這表示在 **LOCAL_SYSTEM** 層級沒有設定任何 Proxy
 
 ![Proxy 本機系統錯誤](./media/proxy-local-system-error.png)

如果結果為「比較的結果: 不同」，則表示已針對 **LOCAL_SYSTEM** 設定 Proxy，但它與 **CURRENT_USER** 不相同：
 
  ![Proxy 比較的結果](./media/proxy-result-compared.png)

5.  如果 **LOCAL_SYSTEM** 沒有正確的 Proxy 設定 (未設定或是與 **CURRENT_USER** 不同)，則您可能需要從 **CURRENT_USER** 將 Proxy 設定複製到 **LOCAL_SYSTEM**。 請確定在您修改登錄機碼之前，先將它備份：

 Current user key: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings” Local system key: HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings”

 
6.  針對 **Local_Service** 帳戶完成步驟 4 和 5，它與 **Local_System** 相同，但應該是 S-1-5-19 而非 S-1-5-18。



## <a name="see-also"></a>另請參閱
- [設定事件轉寄](configure-event-forwarding.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)