---
title: "了解 Advanced Threat Analytics 主控台 | Microsoft Docs"
description: "描述如何登入 ATA 主控台和主控台的元件"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7067477066a2341fa15b2b0d283b2d7721239d5e
ms.sourcegitcommit: 42ce07e3207da10e8dd7585af0e34b51983c4998
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2017
---
適用於︰Advanced Threat Analytics 1.8 版



# <a name="working-with-the-ata-console"></a>使用 ATA 主控台

使用 ATA 主控台監視及回應 ATA 偵測到的可疑活動。

鍵入 ? 鍵將會提供 ATA 入口網站協助工具的鍵盤快速鍵。 

## <a name="enabling-access-to-the-ata-console"></a>啟用 ATA 主控台的存取權
若要成功登入 ATA 主控台，您必須以被指派適當 ATA 角色的使用者登入，才能存取 ATA 主控台。 如需 ATA 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 ATA 角色群組](ata-role-groups.md)。

## <a name="logging-into-the-ata-console"></a>登入 ATA 主控台

>[!NOTE]
 > 從 ATA 1.8 開始，將使用單一登入完成到 ATA 主控台的登入流程。

1. 在 ATA 中心伺服器中，按一下桌面上的 **Microsoft ATA 主控台**圖示，或開啟瀏覽器並瀏覽到 ATA 主控台。

    ![ATA 伺服器圖示](media/ata-server-icon.png)

 >[!NOTE]
 > 您也可以從 ATA 中心或 ATA 閘道開啟瀏覽器，然後瀏覽到您在為 ATA 主控台安裝 ATA 中心時設定的 IP 位址。    

2.  如果安裝 ATA 中心的電腦與您嘗試存取 ATA 主控台的電腦都已加入網域，ATA 支援與 Windows 驗證整合的單一登入 (如果您已登入電腦，ATA 會使用該權杖將您登入 ATA 主控台)。 您也可以使用智慧卡進行登入。 您在 ATA 中的權限會與您的[系統管理員角色](ata-role-groups.md)對應。

 > [!NOTE]
 > 請務必使用您的 ATA 系統管理員使用者名稱和密碼，登入您要存取 ATA 主控台的電腦。 或者，您可以使用不同的使用者身分執行瀏覽器，或登出 Windows 並使用 ATA 系統管理員使用者身分登入。 若要提示 ATA 主控台要求認證，請使用 IP 位址存取主控台，系統將提示您輸入認證。

3. 若要使用 SSO 進行登入，請確定 ATA 主控台網站已在您的瀏覽器中定義為近端內部網路網站，而且您使用簡短名稱或 localhost 進行存取。

> [!NOTE]
> 除了記錄每個可疑活動和健康狀態警示，您在 ATA 主控台中所做的每項設定變更也會記錄在 ATA 中心電腦的 Windows 事件記錄檔中，該記錄檔位於 [應用程式及服務記錄檔] 的 [Microsoft ATA] 下。 此外，也會記錄 ATA 主控台的每次登入。<br></br>  影響 ATA 閘道的設定也會記錄在 ATA 閘道電腦的 Windows 事件記錄檔中。 



## <a name="the-ata-console"></a>ATA 主控台

ATA 主控台可讓您依時間順序快速檢視所有可疑的活動。 不但讓您能夠深入了解任何活動，還能根據這些活動執行動作。 主控台也會顯示警示和通知，以反白顯示 ATA 網路相關問題或視為可疑的新活動。

以下是 ATA 主控台的重要元素。


### <a name="attack-time-line"></a>攻擊時間表

這是您登入 ATA 主控台時會前往的預設登陸頁面。 根據預設，所有開啟的可疑活動都會顯示在攻擊時間表上。 您可以篩選攻擊時間表，顯示所有、開啟、關閉或已解析的可疑活動。 您也可以查看指派給每個活動的嚴重性。

![ATA 攻擊時間表影像](media/ATA-Suspicious-Activity-Timeline.jpg)

如需詳細資訊，請參閱[處理可疑活動](working-with-suspicious-activities.md)。

### <a name="notification-bar"></a>通知列

偵測到新的可疑活動時，通知列會自動在右側開啟。 如果從上次登入之後有新的可疑活動，通知列會在您成功登入後開啟。 您可以隨時按一下右側箭號來存取通知列。

![ATA 通知列影像](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>篩選窗格

您可以根據狀態和嚴重性，篩選要顯示在攻擊時間表的可疑活動，或者要顯示在實體設定檔可疑活動索引標籤中的可疑活動。

### <a name="search-bar"></a>搜尋列

您可以在上層功能表找到搜尋列。 您可以搜尋 ATA 中的特定使用者、電腦或群組。 若要試試看，請開始輸入。

![ATA 主控台搜尋影像](media/ATA-console-search.png)

### <a name="health-center"></a>健全狀況中心

健康情況中心會在 ATA 部署未正常運作時向您提出警示。

![ATA 健全狀況中心影像](media/ATA-Health-Issue.jpg)

每當您的系統發生問題，例如連線錯誤或中斷與 ATA 閘道的連線，[健全狀況中心] 圖示會顯示一個紅點來告知您。 ![ATA 健全狀況中心有紅點的影像](media/ATA-Health-Center-Alert-red-dot.png)

健康情況中心警示可以關閉或解決，並且根據其嚴重性分類為 [高]、[中] 或 [低]。 如果您解除 ATA 服務偵測為仍在作用中的警示，它會自動移至開啟的警示清單。 如果系統偵測到已不再構成警示 (情況已修正)，它會自動移至已解除的清單。

### <a name="user-and-computer-profiles"></a>使用者和電腦設定檔

ATA 會為網路中每個使用者和電腦建置設定檔。 在使用者設定檔中，ATA 會顯示一般資訊，例如群組成員資格、最近的登入和最近存取的資源。 它也會提供使用者在其中透過 VPN 連線的位置清單。 如需 ATA 視為敏感性的群組成員資格清單，請參閱下文。

![使用者設定檔](media/user-profile.png)

在電腦設定檔中，ATA 會顯示一般資訊，例如最近的登入和最近存取的資源。

![電腦設定檔](media/computer-profile.png)

ATA 會在下列頁面上提供實體 (電腦、裝置、使用者) 的其他資訊︰[摘要]、[活動] 和 [可疑的活動]。

ATA 無法完全解析的設定檔將會利用旁邊的半實心圓形圖示來識別。


![ATA 無法解析的設定檔影像](media/ATA-Unresolved-Profile.jpg)

### <a name="sensitive-groups"></a>敏感性群組

ATA 將下列群組清單視為**敏感性**。 屬於這些群組的任何實體都視為具有敏感性：

- Enterprise Read-Only Domain Controllers 
- Domain Admins 
- 網域控制站 
- Schema Admins
- Enterprise Admins 
- Group Policy Creator Owners 
- Read-Only Domain Controllers 
- Administrators  
- Power Users  
- Account Operators  
- Server Operators   
- Print Operators
- Backup Operators
- Replicators 
- Remote Desktop Users 
- Network Configuration Operators 
- Incoming Forest Trust Builders 
- DNS Admins 


### <a name="mini-profile"></a>小型設定檔

在主控台中出現單一實體的任何位置，例如使用者或電腦，如果您將滑鼠停留在實體上，就會自動開啟小型設定檔，顯示下列資訊 (如果有的話)︰

![ATA 小型設定檔影像](media/ATA-mini-profile.jpg)

-   Name

-   圖片

-   電子郵件

-   電話

-   根據嚴重性分類的可疑活動數目



## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
