---
title: ATA 1.7 版的新功能
description: 列出 ATA 1.7 版的新功能以及已知問題
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 14fd7b13b61005ef215c6ba80920572ebcdf0b64
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774701"
---
# <a name="whats-new-in-ata-version-17"></a>ATA 1.7 版的新功能
這些版本資訊提供此版 Advanced Threat Analytics 中已知問題的相關資訊。

## <a name="whats-new-in-the-ata-17-update"></a>什麼是 ATA 1.7 更新的新功能？
ATA 1.7 的更新提供下列各方面的改良︰

-   新的和更新的偵測項目

-   角色型存取控制

-   支援 Windows Server 2016 和 Windows Server 2016 Core

-   使用者體驗改善

-   次要變更


### <a name="new--updated-detections"></a>新的和更新的偵測項目


- **使用目錄服務列舉探查** 在探查階段中，攻擊者會使用不同的方法收集網路中實體的相關資訊。 使用 SAM-R 通訊協定的目錄服務列舉可讓攻擊者取得網域中的使用者和群組清單，了解不同實體之間的互動。 

- **傳遞雜湊的增強功能** 為了增強對傳遞雜湊的偵測，我們加入了其他行為模型來驗證實體的模式。 這些模型可讓 ATA 建立實體行為與可疑 NTLM 驗證的相互關聯，並區分真正的傳遞雜湊攻擊與正面案例的假警報行為。

- **傳遞票證的增強功能** 若要成功偵測一般的進階攻擊和傳遞票證，IP 位址與電腦帳戶之間的相互關聯必須是正確的。 這在 IP 位址因設計而快速變更的環境中 (例如 Wi-Fi 網路和共用相同主機的多個虛擬機器) 是一項挑戰。 為了克服這項挑戰並提升傳遞票證偵測的準確度，我們大幅改進了 ATA 的網路名稱解析 (NNR) 機制以減少假警報。

- **異常行為的增強功能** 在 ATA 1.7 中增加了 NTLM 驗證資料做為偵測異常行為的資料來源，提供的演算法能更廣泛涵蓋網路中的實體行為。 

- **不尋常的通訊協定實作增強功能** ATA 現在會偵測 Kerberos 通訊協定中不尋常的通訊協定實作，以及 NTLM 通訊協定中其他的異常。 具體來說，Kerberos 這些新的異常常用於越過雜湊攻擊。


### <a name="infrastructure"></a>基礎結構

- **角色型存取控制** 角色型存取控制 (RBAC) 功能。 ATA 1.7 包含三個角色︰ATA 管理員、ATA 分析員和 ATA 執行者。

- **支援 Windows Server 2016 和 Windows Server Core** ATA 1.7 支援在執行 Windows Server 2008 R2 SP1 (不含 Server Core)、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 (包含 Core 但不含 Nano) 的網域控制站上部署輕量型閘道。 此外，此版本支援 Windows Server 2016 的 ATA 中心與 ATA 閘道兩個元件。

### <a name="user-experience"></a>使用者體驗
- **設定體驗** 我們在此版本中重新設計了 ATA 設定體驗，讓您能獲得更好的使用者體驗，也對有多個 ATA 閘道的環境有更好的支援。 此版本也引進 ATA 閘道更新頁面，可以更簡單、更好管理各種不同閘道的自動更新。

## <a name="known-issues"></a>已知問題
下列已知問題存在於此版本中。

### <a name="gateway-automatic-update-may-fail"></a>閘道自動更新可能會失敗
**徵兆︰** 在 WAN 連結慢速的環境中，ATA 閘道更新可能會達到更新的逾時 (100 秒) 而無法順利完成。
在 ATA 主控台中，ATA 閘道將會有很長一段時間處於「正在更新 (正在下載套件)」狀態，然後最後失敗。
**因應措施︰** 若要解決此問題，請從 ATA 主控台下載最新的 ATA 閘道套件，以手動方式更新 ATA 閘道。

> [!IMPORTANT]
>  不支援為 ATA 所使用的憑證自動更新憑證。 使用這些憑證可能會在自動更新憑證時導致 ATA 停止運作。 

### <a name="no-browser-support-for-jis-encoding"></a>針對 JIS 編碼無瀏覽器支援
**徵兆：** ATA 主控台在使用 JIS 編碼的瀏覽器上可能不會如預期般運作 **因應措施：** 將瀏覽器的編碼變更為 Unicode UTF-8。
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>使用 VMware 時的「已丟棄連接埠鏡像流量」

在 VMware 上使用輕量閘道時的「已丟棄連接埠鏡像流量」警示。

若在 VMware 虛擬機器上使用網域控制站，可能會收到有關於**已丟棄連接埠鏡像流量**的警示。 當 VMware 中的組態不相符時，即可能會發生此情況。 若要避免這些警示，可檢查是否已將虛擬機器中的下列設定設為 [0] 或 [已停用]：  

- TsoEnable
- LargeSendOffload(IPv4)
- IPv4 TSO Offload

此外也請考慮停用 [IPv4 Giant TSO Offload]。 如需詳細資訊，請參閱 VMware 文件。

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>自動閘道更新在更新為 1.7 update 1 時失敗

從 ATA 1.7 更新為 ATA 1.7 update 1 時，自動 ATA 閘道更新處理序和使用閘道套件的閘道手動更新可能都沒有如預期運作。
如果 ATA 中心使用的憑證在更新 ATA 前經過變更，即可能發生此問題。
若要驗證此問題，請檢閱 ATA 閘道的 **Microsoft.Tri.Gateway.Updater.log**，並尋找下列例外狀況：**System.Net.Http.HttpRequestException: 傳送要求時發生錯誤。---> System.Net.WebException: 基礎連線已關閉: 傳送時發生未預期的錯誤。---> System.IdentityModel.Tokens.SecurityTokenValidationException: 無法驗證憑證指紋**

![ATA 更新閘道錯誤](media/17update_gatewaybug.png)

為解決此問題，請在變更憑證後，從提升權限的命令提示字元瀏覽至下列位置：**%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**，然後執行以下項目：

1. Mongo.exe ATA (ATA 必須大寫) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})

### <a name="export-suspicious-activity-details-to-excel-may-fail"></a>將可疑活動詳細資料匯出至 Excel 可能失敗
嘗試將可疑活動詳細資料匯出至 Excel 檔案時，作業可能會因下列錯誤而失敗：*Error [BsonClassMapSerializer`1] System.FormatException: 將類別 Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity 的 Activity 屬性還原序列化時發生錯誤: Element 'ResourceIdentifier' 不符合類別 Microsoft.Tri.Common.Data.EventActivities.NtlmEvent 的任何欄位或屬性。---> System.FormatException: 項目 'ResourceIdentifier' 不符合類別 Microsoft.Tri.Common.Data.EventActivities.NtlmEvent 的任何欄位或屬性。*

若要解決此問題，請從提升權限的命令提示字元瀏覽至下列位置：**%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**，然後執行以下命令：
1.  `Mongo.exe ATA` (ATA 必須是大寫)
2.  `db.SuspiciousActivityActivity.update({ "Activity._t": "NtlmEvent" },{$unset: {"Activity.ResourceIdentifier": ""}}, {multi: true});`

## <a name="minor-changes"></a>次要變更

- ATA 現在針對 ATA 主控台是使用 OWIN 而不是 IIS。
- 如果 ATA 中心服務已關閉，您將無法存取 ATA 主控台。
- 由於 ATA NNR 中的變更，已不再需要短期的租用子網路。

## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[將 ATA 更新為 1.7 版 - 移轉指南](ata-update-1.7-migration-guide.md)

