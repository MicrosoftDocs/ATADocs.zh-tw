---
title: Azure 進階威脅防護實用資源清單 | Microsoft Docs
description: 本文提供 Azure ATP 實用資源清單
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 56b74b2e02fcab2b7584afbabd5d4384f066261c
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166373"
---
適用於：Azure 進階威脅防護



# <a name="azure-atp-readiness-guide"></a>Azure ATP 整備指南

此文章為您提供的整備藍圖，其中包含協助您開始使用「Azure 進階威脅防護」的資源清單。 

## <a name="understanding-azure-atp"></a>了解 Azure ATP

Azure 進階威脅防護 (ATP) 為雲端服務，可識別並保護您的企業免於多種進階目標式網路攻擊與內部威脅。 您可以利用下列資源深入了解 Azure ATP： 
- [Azure ATP 概觀](what-is-atp.md)
- [Azure ATP 簡介影片 - 完整版](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>部署決定

Azure ATP 是由位於 Azure 中的雲端服務以及可安裝在網域控制站上的整合式感應器或專用伺服器上的獨立感應器所組成。 在您啟動並執行 Azure ATP 之前，請務必選擇最適合您部署與需求的感應器類型。 Azure ATP 整合式感應提供加強的安全性、較低的營運成本與較簡單的部署方式。 Azure ATP 獨立感應器要求實體硬體、額外的設定步驟與較高的營運成本。 <br>若您使用實體伺服器，容量規劃非常重要。 為您的感應器配置空間時，可從調整大小工具取得協助： 
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) - 調整大小的工具會自動收集 Azure ATP 監視器的流量多寡。 其會自動為感應器提供支援能力以及資源建議。 
- [ATA 容量規劃指南](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>部署 Azure ATP

這些資源可協助您安裝 Azure ATP、連線至 Active Directory、下載感應器套件、設定事件收集，也可與您的 VPN 整合，及設定 honeytoken 帳戶和排除項目。 
- [Azure ATP (屬於 EMS E5)](http://aka.ms/aatptrial) 有效試用期為 90 天。
- [部署指南](install-atp-step1.md)遵循下列步驟在您的環境中部署 Azure ATP。
- [整合 Azure ATP 與 Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Azure ATP 設定

Azure ATP 中的必要基本設定是在建立工作區時設定的。 但您仍可進行一些額外設定來微調 Azure ATP，更正確地在您的環境中進行偵測，例如 SIEM 整合與稽核設定。 

- [Azure ATP 一般文件](what-is-atp.md)
- [稽核設定](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – 在 ATP 部署前後，稽核網域控制站的健康情況。 

## <a name="work-with-azure-atp"></a>使用 Azure ATP

Azure ATP 開始運作之後，檢視在 Azure ATP 入口網站活動時間表中偵測到的可疑活動。 活動時間表是登入 Azure ATP 入口網站之後的預設登陸頁面。 根據預設，所有開啟的可疑活動都會顯示在攻擊時間表上。 您也可以查看指派給每個活動的嚴重性。 透過向下切入實體 (電腦、裝置、使用者) 來開啟其提供詳細資訊的設定檔頁面，以調查每個可疑活動。 以下資源有助於您處理 Azure ATP 的可疑活動： 

- [Azure ATP 可疑活動指南](suspicious-activity-guide.md)了解使用 Azure ATP 偵測進行分級及採取下一個步驟。
- [將群組標記為機密](sensitive-accounts.md)掌握機密安全性群組的認證暴露。

## <a name="security-best-practices"></a>安全性最佳做法

- [Azure ATP 常見問題集](atp-technical-faq.md) - 本文提供有關 Azure ATP 的常見問題清單，並提供深入解析和答案。 

## <a name="community-resources"></a>社群資源

部落格：[Azure ATP 部落格](https://aka.ms/aatpblog)

公用社群：[Azure ATP 技術社群](https://aka.ms/AatpCom)

私人社群：[Azure ATP Yammer 群組](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9：[Microsoft 安全性 Channel 9 頁面](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>另請參閱

- [使用機密帳戶](sensitive-accounts.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)