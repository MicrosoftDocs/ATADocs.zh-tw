---
title: 在 Advanced Threat Analytics 中設定 Windows 事件轉送 | Microsoft Docs
description: 描述使用 ATA 設定 Windows 事件轉送的選項
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 825185a2aaf792e6b9c1fe58e022174c2f98bb0c
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196821"
---
# <a name="configuring-windows-event-forwarding"></a>設定 Windows 事件轉送

*適用於：Advanced Threat Analytics 1.9 版*

> [!NOTE]
> 針對 ATA 1.8 版及更新版本，ATA 輕量型閘道不再需要事件收集設定。 ATA 輕量型閘道現在會本機讀取事件，而不需要設定事件轉送。

為增強偵測功能，ATA 需要下列 Windows 事件：4776、4732、4733、4728、4729、4756、4757、7045。 這些事件可透過 ATA 輕量型閘道自動讀取；如果未部署 ATA 輕量型閘道，則可以透過下列兩個方式之一轉送至 ATA 閘道：藉由將 ATA 閘道設定為接聽 SIEM 事件，或藉由設定 Windows 事件轉送。

> [!NOTE]
> 如果您使用 Server Core，則 [wecuti](https://docs.microsoft.com/windows-server/administration/windows-commands/wecutil) 可用於建立和管理從遠端電腦機轉送之事件的訂用帳戶。

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>具連接埠鏡像之 ATA 閘道的 WEF 設定

在設定從網域控制站到 ATA 閘道之間的連接埠鏡像後，請使用下列指示以使用來源起始設定來設定 Windows 事件轉送。 這是一個設定 Windows 事件轉送的方法。 

**步驟 1︰新增網路服務帳戶到網域 Event Log Readers 群組。** 

在此案例中，假設 ATA 閘道是網域的成員。

1.  開啟 [Active Directory 使用者和電腦]，瀏覽至 **BuiltIn** 資料夾，然後按兩下 [Event Log Readers]。 
2.  選取 [成員]。
3.  如果未列出 [Network Service]，請按一下 [新增]，在 [輸入要選取的物件名稱] 欄位中輸入 **Network Service**。 然後按一下 [檢查名稱]，再按兩次 [確定]。 

在將 [網路服務] 新增到 [Event Log Readers] 群組後，請重新啟動網域控制站，變更才會生效。

**步驟 2︰在網域控制站上建立原則以設定 [設定目標訂閱管理員] 設定。** 
> [!Note] 
> 您可以建立這些設定的群組原則，並將群組原則套用到 ATA 閘道監視的每個網域控制站。 下面的步驟修改網域控制站的本機原則。     

1. 在每個網域控制站上執行下列命令︰*winrm quickconfig*
2. 在命令提示字元中輸入 *gpedit.msc*
3. 展開 [電腦設定] > [系統管理範本] > [Windows 元件] > [事件轉送]

   ![本機原則群組編輯器影像](media/wef%201%20local%20group%20policy%20editor.png)

4. 按兩下 [設定目標訂閱管理員]。
   
   1.  選取 [已啟用]。
   2.  在 [選項] 下，按一下 [顯示]。

   3.  在 [SubscriptionManagers] 下，輸入下列值，然後按一下 [確定]：*Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* 
      
        *(例如: Server=`http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)*
      
        ![設定目標訂閱影像](media/wef%202%20config%20target%20sub%20manager.png)
      
   4.  按一下 [ **確定**]。
   5.  在提升權限的命令提示字元中，輸入 *gpupdate /force*。 

**步驟 3：在 ATA 閘道上執行下列步驟** 

1.  開啟提升權限的命令提示字元，輸入 *wecutil qc*
2.  開啟 [事件檢視器]。 
3.  以滑鼠右鍵按一下 [訂閱]，然後選取 [建立訂閱]。 

    1.  為訂閱輸入名稱和描述。 
    2.  針對 [目的地記錄檔]，請確認已選取 [轉送的事件]。 對於要讀取事件的 ATA，目的記錄檔必須是 [轉送的事件]。 
    3.  選取 [來源電腦起始]，按一下 [選取電腦群組]。
        1.  按一下 [加入網域電腦]。
        2.  在 [輸入要選取的物件名稱] 欄位中輸入網域控制站的名稱。 然後按一下 [檢查名稱]，再按一下 [確定]。  
          ![事件檢視器影像](media/wef3%20event%20viewer.png)  
        3.  按一下 [ **確定**]。
    4.  按一下 [選取事件]。
        1. 按一下 [依記錄]，然後選取 [安全性]。
        2. 在 [Includes/Excludes Event ID (包含/排除事件識別碼)] 欄位中鍵入事件編號，然後按一下 [確定]。 例如，鍵入 4776，如下範例所示。

        ![查詢篩選影像](media/wef%204%20query%20filter.png)

    5.  以滑鼠右鍵按一下建立的訂閱，然後選取 [執行階段狀態]，以查看該狀態是否有任何問題。 
    6.  幾分鐘後，請檢查您設定要轉送的事件是否出現在 ATA 閘道上 [轉送的事件] 中。


如需詳細資訊，請參閱[設定電腦以轉送和收集事件](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>另請參閱
- [安裝 ATA](install-ata-step1.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
