---
# required metadata

title: 安裝 ATA - 步驟 2 | Microsoft Advanced Threat Analytics
description: 安裝 ATA 的步驟 2 協助您設定 ATA 中心伺服器網域連線設定
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安裝 ATA - 步驟 2

>[!div class="step-by-step"] [« 步驟 1](install-ata-step1.md)
[步驟 3 »](install-ata-step3.md)

## 步驟 2： 進行 ATA 閘道一般設定
[一般] 設定索引標籤中的設定適用於 ATA 中心管理的所有 ATA 閘道。

若要進行一般 ATA 閘道設定，請執行下列作業：

1.  開啟 ATA 主控台並登入。 如需指示，請參閱[使用 ATA 主控台](working-with-ata-console.md)。

2.  按一下設定圖示，然後選取 [設定]。

    ![ATA 閘道組態設定](media/ATA-config-icon.JPG)

3.  在 [一般] 索引標籤的 [ATA 閘道] 下輸入下列資訊，然後按一下 [儲存]。

    |欄位|註解|
    |---------|------------|
    |**使用者名稱** (必填)|輸入唯讀使用者名稱，例如︰**user1**。|
    |**密碼** (必填)|輸入唯讀使用者的密碼，例如︰**Pencil1**。 **注意︰**請確定此密碼是否正確。 如果您儲存的密碼錯誤，ATA 服務會停止在 ATA 閘道伺服器上執行。|
    |**網域** (必填)|輸入唯讀使用者的網域，例如︰**contoso.com**。 **注意︰**您務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶是在 corp.contoso.com 網域中，您需要輸入 `corp.contoso.com`，而非 contoso.com|
    |自動更新所有 ATA 閘道 |如果您啟用此設定，在未來版本中，當您更新 ATA 中心時，所有 ATA 閘道都會自動更新。|

    ![ATA 網域連線設定影像](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"] [« 步驟 1](install-ata-step1.md)
[步驟 3 »](install-ata-step3.md)


## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO3-->


