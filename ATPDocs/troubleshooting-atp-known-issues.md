---
title: 針對 Azure ATP 已知問題進行疑難排解 | Microsoft Docs
description: 描述如何針對 Azure ATP 的問題進行疑難排解。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2112e9fea1f316ff12d87b3a477b78bff4457a5f
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
適用於：Azure 進階威脅防護


# <a name="troubleshooting-azure-atp-known-issues"></a>針對 Azure ATP 已知問題進行疑難排解 


## <a name="deployment-log-location"></a>部署記錄位置
 
對於安裝產品的使用者，Azure ATP 部署記錄位於暫存記錄中。 在預設安裝位置中，其位於︰C:\Users\Administrator\AppData\Local\Temp (或 %temp% 上方的一個目錄)。

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Azure ATP 感應器 NIC 小組問題

如果您嘗試在具備 NIC 小組介面卡的電腦上安裝 ATP 感應器，您將會接收到安裝錯誤。 如果您想要在使用 NIC 小組設定的電腦上安裝 ATP 感應器，請遵循這些指示：

如果尚未安裝感應器：

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

## <a name="windows-defender-atp-integration-issue"></a>Windows Defender ATP 整合問題

Azure 進階威脅防護可讓您將 Azure ATP 與 Windows Defender ATP 整合。 目前，只有 Windows Defender ATP 私人預覽客戶才能進行整合。 

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware 虛擬機器感應器問題

如果您在 VMware 虛擬機器上有 Azure ATP 感應器，則可能會收到監視警示「某些網路流量不會被分析」。 當 VMware 中的設定不相符時，就會發生此狀況。

若要解決此問題：

在虛擬機器的 NIC 設定中將以下設定設為 **0** 或 [停用]：TsoEnable、LargeSendOffload、TSO Offload、Giant TSO Offload。
> [!NOTE]
> 針對 Azure ATP 感應器，您只需要停用 NIC 設定底下的 [IPv4 TSO Offload]。

 ![VMware 感應器問題](./media/vm-sensor-issue.png)

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)