---
title: "針對存取管理的 Advanced Threat Analytics 角色群組 |Microsoft Docs"
description: "逐步引導您使用 ATA 角色群組。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/30/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6243c03af9e40b8774b2ce7089a47e54569ba45e
ms.sourcegitcommit: cb2a4df6805d41bf030d3439ef87281fc6acc98f
translationtype: HT
---
適用於︰Advanced Threat Analytics 1.7 版




# <a name="ata-role-groups"></a>ATA 角色群組

角色群組可以進行 ATA 的存取管理。 使用角色群組可以隔離安全性小組內的責任，並授與使用者執行工作所需的存取權。 本文說明存取管理和 ATA 角色授權，以及協助您在 ATA 中準備和執行角色群組。

> [!NOTE]
> ATA 中心上的所有本機系統管理員都會自動成為 Microsoft Advanced Threat Analytics 系統管理員。

## <a name="types-of-ata-role-groups"></a>ATA 角色群組的類型 

ATA 引進了 3 種類型的角色群組︰ATA 管理員、ATA 使用者以及 ATA 檢視者。 下表描述 ATA 中每個角色可用的存取類型。 視您指派何種角色而定，ATA 中的各種畫面與功能表選項將無法使用，如下所示︰

|活動 |Microsoft Advanced Threat Analytics 管理員|Microsoft Advanced Threat Analytics 使用者|Microsoft Advanced Threat Analytics 檢視者|
|----|----|----|----|
|登入|可用|可用|可用|
|提供可疑活動的輸入|可用|可用|無法使用|
|變更可疑活動的狀態|可用|可用|無法使用|
|透過電子郵件/取得連結共用/匯出可疑的活動|可用|可用|無法使用|
|新增/編輯可疑活動的附註|可用|可用|無法使用|
|變更監視警示的狀態|可用|可用|無法使用|
|更新 ATA 設定|可用|無法使用|無法使用|
|閘道 - 新增|可用|無法使用|無法使用|
|閘道 - 刪除 |可用|無法使用|無法使用|
|監視的 DC - 新增 |可用|無法使用|無法使用|
|監視的 DC - 刪除|可用|無法使用|無法使用|
|檢視警示及可疑的活動|可用|可用|可用|


當使用者嘗試存取不適用於其角色群組的頁面時，他們會被重新導向至 ATA 未授權的頁面。 

## <a name="add--remove-users---ata-role-groups"></a>新增 \ 移除使用者 - ATA 角色群組 

ATA 使用本機的 Windows 群組做為角色群組的基礎。 ATA 中心伺服器上的角色群組必須接受管理。
若要新增或移除使用者，請使用 [本機使用者和群組] MMC (Lusrmgr.msc)。 您可以在加入網域的電腦上新增網域帳戶以及本機帳戶。 
