---
title: 針對 Azure ATP 已知問題進行疑難排解 | Microsoft Docs
description: 描述如何針對 Azure ATP 的問題進行疑難排解。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b78b7f39b7d5c94e2709e080677344919dd422cf
ms.sourcegitcommit: 2aab3c4244db694616ec02a9b8ae2e266d6fdddc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69629316"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>針對 Azure ATP 已知問題進行疑難排解 


## <a name="deployment-log-location"></a>部署記錄位置
 
針對安裝產品的使用者，Azure ATP 部署記錄位於 temp 目錄中。 在預設安裝位置中，其位於：C:\Users\Administrator\AppData\Local\Temp (或 %temp% 的上一層目錄)。 如需詳細資訊，請參閱[使用記錄檔針對 ATP 進行疑難排解](troubleshooting-atp-using-logs.md)。

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxy 驗證問題顯示為授權錯誤

若您在感應器安裝期間收到下列錯誤：**感應器因授權問題而無法註冊**。

部署記錄項目: [1C60:1AA8][2018-03-24T23:59:13]i000:2018-03-25 02:59:13.1237 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000:2018-03-25 02:59:56.4856 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000:2018-03-25 03:27:56.7399 針對 SensorBootstrapperApplication Engine.Quit 進行偵錯 [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500:正在關機，結束代碼:0x642


**原因：**

在某些情況下，透過 Proxy 進行通訊時，可能會在驗證期間以錯誤 401 或 403 回應 Azure ATP 感應器，而不是錯誤 407。 Azure ATP 感應器將錯誤 401 或 403 解譯為授權問題，而不是 Proxy 驗證問題。 

**解決方法：**

請確定感應器可透過設定的 Proxy 瀏覽至 *.atp.azure.com，而無需進行驗證。 如需詳細資訊，請參閱[設定 Proxy 以進行通訊](configure-proxy.md)。




## Azure ATP 感應器 NIC 小組問題 <a name="nic-teaming"></a>

如果您嘗試在具備 NIC 小組介面卡的電腦上安裝 ATP 感應器，您將會接收到安裝錯誤。 如果您想要在使用 NIC 小組設定的電腦上安裝 ATP 感應器，請遵循這些指示：

如果您尚未在電腦上安裝感應器：

1.  從 [https://nmap.org/npcap/](https://nmap.org/npcap/) 下載 Npcap。
2.  如果您已安裝 WinPcap，請將它解除安裝。
3.  使用下列選項安裝 Npcap：loopback_support=no & winpcap_mode=yes
4.  安裝感應器套件。

如果您已安裝感應器：

1.  從 [https://nmap.org/npcap/](https://nmap.org/npcap/) 下載 Npcap。
2.  將感應器解除安裝。
3.  將 WinPcap 解除安裝。
4.  使用下列選項安裝 Npcap：loopback_support=no & winpcap_mode=yes
5.  重新安裝感應器套件。

## <a name="multi-processor-group-mode"></a>多處理器群組模式 
針對 Windows 作業系統 2008 R2 與 2012，多處理器群組模式中不支援 Azure ATP 感應器。

建議的可能因應措施：
- 如果超執行緒已開啟，請將它關閉。 這可能會減少足夠的邏輯核心數目，以避免需要在**多處理器群組**模式中執行。 

- 如果您的電腦具有少於 64 個邏輯核心，而且是在 HP 主機上執行，您可以將 [NUMA 群組大小最佳化]  BIOS 設定從預設的[叢集]  變更為 [一般]  。 

## <a name="windows-defender-atp-integration-issue"></a>Windows Defender ATP 整合問題

Azure 進階威脅防護可讓您將 Azure ATP 與 Windows Defender ATP 整合。 如需詳細資訊，請參閱[整合 Azure ATP 與 Windows Defender ATP](integrate-wd-atp.md)。 

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware 虛擬機器感應器問題

如果您在 VMware 虛擬機器上有 Azure ATP 感應器，則可能會收到監視警示「某些網路流量不會被分析」  。 當 VMware 中的設定不相符時，就會發生此狀況。

若要解決此問題：

在虛擬機器的 NIC 設定中，將下列設定設為 [0]  或 [停用]  ：TsoEnable、LargeSendOffload、TSO Offload、Giant TSO Offload。
> [!NOTE]
> 針對 Azure ATP 感應器，您只需要停用 NIC 設定底下的 [IPv4 TSO Offload]  。

 ![VMware 感應器問題](./media/vm-sensor-issue.png)

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
