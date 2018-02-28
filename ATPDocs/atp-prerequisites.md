---
title: "Azure 進階威脅防護必要條件 | Microsoft Docs"
description: "描述在環境中成功部署 Azure ATP 的需求"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 819eeb73c57e7b1de5e7e5e837aa2d6db2e0848d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護



# <a name="azure-atp-prerequisites"></a>Azure ATP 必要條件
本文描述在您的環境中成功部署 Azure ATP 的需求。

>[!NOTE]
> 如需如何規劃資源和容量的相關資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。


Azure ATP 是以 Azure ATP 雲端服務組成，其包含工作區管理入口網站及工作區入口網站、Azure ATP 獨立感應器及/或 Azure ATP 感應器。 如需 Azure ATP 元件的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

每個 Azure ATP 工作區皆支援 Active Directory 樹系邊界，且支援 Windows 2003 和更新版本的樹系功能等級 (FFL)。 針對搭配多個樹系的部署，每個樹系皆需要個別的 Azure ATP 工作區。


[開始之前](#before-you-start)︰本節列出在開始 Azure ATP 安裝之前您應該收集的資訊以及您應該具備的帳戶和網路實體。

[Azure ATP 工作區管理入口網站](#azure-atp-workspace-management-portal-and-workspace-portal-requirements)：此節說明工作區管理入口網站瀏覽器的需求。

[Azure ATP 工作區入口網站](#azure-atp-workspace-management-portal-and-workspace-portal-requirements)：此節說明執行 Azure ATP 工作區入口網站的瀏覽器需求。

[Azure ATP 獨立感應器](#azure-atp-sensor-requirements)：此節列出 Azure ATP 獨立感應器的硬體及軟體需求，以及需在 Azure ATP 獨立感應器伺服器上進行的設定。

[Azure ATP 感應器](#azure-atp-lightweight-sensor-requirements)：此節列出 Azure ATP 感應器的硬體及軟體需求。

![Azure ATP 架構圖表](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>開始之前
本節列出在開始 Azure ATP 安裝之前您應該收集的資訊以及您應該具備的帳戶和網路實體。


-   針對監視網域中的所有物件具有讀取存取權的**內部部署** Azure AD 使用者帳戶和密碼。

    > [!NOTE]
    > 如果您已經在網域中設定不同組織單位 (OU) 的自訂 ACL，請確定選取的使用者具有讀取這些 OU 的權限。

-   如果您在 Azure ATP 獨立感應器上執行 Wireshark，在停止 Wireshark 擷取後，將需要重新啟動 Azure 進階威脅防護感應器服務。 否則，感應器會停止擷取流量。

- 如果您嘗試在具備 NIC 小組介面卡的電腦上安裝 ATP 感應器，您將會接收到安裝錯誤。 如果您想要在具備 NIC 小組的電腦上安裝 ATP 感應器，請連絡您的 Azure ATP 支援代表。

-    建議︰使用者應該擁有「刪除的物件」容器的唯讀權限。 這可讓 Azure ATP 偵測網域中對物件進行大量刪除的動作。 如需設定「已刪除物件」容器的唯讀權限相關資訊，請參閱[檢視或設定目錄物件的權限](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) \(英文\) 文章中的＜變更刪除的物件容器的權限＞。

-   選擇性︰沒有任何網路活動之使用者的使用者帳戶。 此帳戶設定為 Azure ATP Honeytoken 使用者。 如需詳細資訊，請參閱[設定排除項目和 Honeytoken 使用者](install-atp-step7.md)。

-   選擇性：部署獨立感應器時，您必須將 Windows 事件 4776、4732、4733、4728、4729、4756、4757 及 7045 轉寄給 ATP，以進一步針對機密群組、Honeytoke 偵測及惡意服務建立，強化 Azure ATP Pass-the-Hash、Brute Force 及 Modification。 在 Azure ATP 感應器中，會自動接收這些事件。 在 Azure ATP 獨立感應器中，這些事件可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉寄來接收。 所收集的事件可提供 Azure ATP 透過網域控制站網路流量無法取得的額外資訊。


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Azure ATP 工作區管理入口網站及工作區入口網站需求
對 Azure ATP 工作區入口網站及 Azure ATP 工作區管理入口網站的存取是透過瀏覽器，並支援下列瀏覽器及設定：
-   Microsoft Edge
-   Internet Explorer 第 10 版及更新版本
-   Google Chrome 4.0 和更新版本
-   螢幕解析度最低需求為 1700 像素
-   防火牆/Proxy 開啟 - 若要與 Azure ATP 雲端服務通訊，您必須在防火牆/Proxy 中開啟：*.atp.azure.com 連接埠 443。 

## <a name="azure-atp-standalone-sensor-requirements"></a>Azure ATP 獨立感應器需求
本節列出 Azure ATP 獨立感應器的需求。
### <a name="general"></a>一般
Azure ATP 獨立感應器可安裝在執行 Windows Server 2012 R2 或 Windows Server 2016 (包括 Server Core) 的伺服器上。
Azure ATP 獨立感應器可以安裝在屬於網域或工作群組之成員的伺服器上。
Azure ATP 獨立感應器可以用來監視具 Windows Server 2003 或更新版本之網域功能等級的網域控制站。

若要讓網域控制站與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。


如需使用虛擬機器與 Azure ATP 獨立感應器的相關資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。

> [!NOTE]
> 至少需要 5 GB 的空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格
為了達到最佳效能，將 Azure ATP 獨立感應器的 [電源選項] 設定為 [高效能]。<br>
Azure ATP 獨立感應器可以支援監視多個網域控制站，依進出網域控制站的網路傳輸量而定。

>[!NOTE] 
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 獨立感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。


### <a name="network-adapters"></a>網路介面卡
Azure ATP 獨立感應器需要至少一個管理介面卡和至少一個擷取介面卡︰

-   **管理介面卡** - 用於您公司網路上的通訊。 此介面卡應進行下列設定：

    -   包含預設感應器的靜態 IP 位址

    -   慣用和替代的 DNS 伺服器

    -   **此連線的 DNS 尾碼**應該是受監視之每個網域的網域 DNS 名稱。

        ![在進階 TCP/IP 設定中設定 DNS 尾碼](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > 如果 Azure ATP 獨立感應器是網域的成員，這可能會自動設定。

-   **擷取介面卡** - 用來擷取進出網域控制站的流量。

    > [!IMPORTANT]
    > -   設定擷取介面卡的連接埠鏡像做為網域控制站網路流量的目的地。 如需詳細資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。 一般而言，設定通訊埠鏡像必須與網路或虛擬化團隊合作。
    > -   為您的環境設定靜態、無法經路由傳送的 IP 位址，沒有預設感應器也沒有 DNS 伺服器位址。 例如，1.1.1.1/32。 這會確保擷取網路介面卡可以擷取最大的流量，而且管理網路介面卡會用於傳送和接收必要的網路流量。

### <a name="ports"></a>連接埠
下表列出 Azure ATP 獨立感應器在管理介面卡上至少需要設定的連接埠：

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP 和 UDP|389|網域控制站|輸出|
|安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
|LDAP 至通用類別|TCP|3268|網域控制站|輸出|
|LDAPS 至通用類別|TCP|3269|網域控制站|輸出|
|SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
|Kerberos|TCP 和 UDP|88|網域控制站|輸出|
|Netlogon (SMB、CIFS、SAM-R)|TCP 和 UDP|445|網域控制站|輸出|
|Windows Time|UDP|123|網域控制站|輸出|
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|透過 RPC 的 NTLM|TCP|135|網路上的所有裝置|輸出|
|NetBIOS|UDP|137|網路上的所有裝置|輸出|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDDP|1813|RADIUS|輸入|

> [!NOTE]
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-atp-step8-samr.md)。
> - 下列連接埠需要為 Azure ATP 獨立感應器在網路上的裝置上針對傳入開啟：
>   -   透過 RPC 的 NTLM (TCP 連接埠 135) (針對解析目的)
>   -   NetBIOS (UDP 連接埠 137) (針對解析目的)
>   -   SAM-R 查詢 (TCP/UDP 連接埠 445) (針對偵測目的)


## <a name="azure-atp-sensor-requirements"></a>Azure ATP 感應器需求
本節列出 Azure ATP 感應器的需求。
### <a name="general"></a>一般
Azure ATP 感應器可在執行 Windows Server 2008 R2 SP1 (不含 Server Core)、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 (包含 Core 但不含 Nano) 的網域控制站上安裝。

網域控制站可以是唯讀網域控制站 (RODC)。

若要讓網域控制站與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

於安裝期間會安裝 .Net Framework 4.7，並可能會導致網域控制站重新開機。


> [!NOTE]
> 至少需要 5 GB 的空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

Azure ATP 感應器在網域控制站上需要安裝至少兩個核心和 6 GB 的 RAM。
為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項] 設定為 [高效能]。
Azure ATP 感應器可以部署在各種負載和大小的網域控制站上，依進出網域控制站的網路流量，以及安裝在該網域控制站上的資源數量而定。

>[!NOTE] 
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

Azure ATP 感應器可為所有網域控制站的網路介面卡監視其上的本機流量。 <br>
部署後，如果您想要修改監視的網路介面卡，則可以使用 Azure ATP 工作區入口網站。

執行 Windows 2008 R2 且啟用 Broadcom 網路介面卡小組的網域控制站不支援感應器。

### <a name="ports"></a>連接埠
下表列出 Azure ATP 感應器至少需要的連接埠：

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|透過 RPC 的 NTLM|TCP|135|網路上的所有裝置|輸出|
|Netlogon (SMB、CIFS、SAM-R)|TCP/UDP|445|網域控制站|輸出|
|NetBIOS|UDP|137|網路上的所有裝置|輸出|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDDP|1813|RADIUS|輸入|

> [!NOTE]
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。
> - 下列連接埠需要為 Azure ATP 感應器在網路上的裝置上針對傳入開啟：
>   -   透過 RPC 的 NTLM (TCP 連接埠 135) (針對解析目的)
>   -   NetBIOS (UDP 連接埠 137) (針對解析目的)
>   -   SAM-R 查詢 (TCP/UDP 連接埠 445) (針對偵測目的)





## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 架構](atp-architecture.md)
- [安裝 ATP](install-atp-step1.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)

