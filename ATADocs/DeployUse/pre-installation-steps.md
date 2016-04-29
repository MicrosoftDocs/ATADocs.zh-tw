---
# required metadata

title: 安裝前的步驟 | Microsoft Advanced Threat Analytics
description: 描述在環境中成功部署 ATA 的需求
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 12bbdcc0-9ac2-4bad-8f26-06ee498351fa

# optional metadata

ROBOTS: noindex,nofollow
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安裝前的步驟
本文描述在您的環境中成功部署 ATA 的條件需求。

ATA 是由 ATA 中心與 ATA 閘道這兩個元件組成。 如需 ATA 元件的詳細資訊，請參閱 [ATA 架構](/advanced=threat-analytics/understand/ata-architecture)。

[開始之前](#before-you-start)︰本節列出在開始 ATA 安裝之前您應該收集的資訊以及您應該具備的帳戶和網路實體。

[ATA 中心](#ata-center-requirements)︰本節列出 ATA 中心的硬體軟體需求，以及您需要在 ATA 中心伺服器上做的設定。

[ATA 閘道](#ata-gateway-requirements)︰本節列出 ATA 閘道的硬體軟體需求，以及您需要在 ATA 閘道伺服器上做的設定。

[ATA 主控台](#ata-console)︰本節列出執行 ATA 主控台的瀏覽器需求。

![ATA 架構圖](media/ATA-architecture-topology.jpg)

## 開始之前
本節列出在開始 ATA 安裝之前您應該收集的資訊以及您應該具備的帳戶和網路實體。

-   在 Windows Server 2008 或更新版本執行的**網域控制站**。

-   在即將監視的網域中，具有**所有物件**讀取存取權的**使用者帳戶和密碼**。

    > [!NOTE]
    > 如果您已經在網域中設定不同組織單位 (OU) 的自訂 ACL，請確定選取的使用者具有讀取這些 OU 的權限。

    選擇性︰使用者應該擁有「刪除的物件」容器的唯讀權限。 這可讓 ATA 偵測網域中的大量刪除物件。 如需設定刪除的物件容器的唯讀權限相關資訊，請參閱[檢視或設定目錄物件的權限](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx)主題中的**變更刪除的物件容器的權限**。

-   選擇性︰沒有任何網路活動之使用者的使用者帳戶。 此帳戶將會設定為 ATA Honeytoken 使用者。 若要設定 Honeytoken 使用者，您需要使用者帳戶的 SID，而不是使用者名稱。

-   選擇性︰除了收集和分析進出網域控制站的網路流量，ATA 可以使用 Windows 事件 4776 來進一步加強 ATA 的傳遞雜湊偵測。 這可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送。 所收集的事件可提供 ATA 透過網域控制站網路流量無法取得的額外資訊。

-   有一份 VPN 和 Wi-Fi 上使用的所有子網路清單可能有幫助，它們會在極短的時間內 (幾秒或幾分鐘) 重新指派裝置之間的 IP 位址。  您會想要找出這些短期租用子網路，讓 ATA 可以減少其快取存留期以配合裝置之間的快速重新指派。 請參閱[安裝 ATA](/advanced-threat-analytics/deployuse/install-ata)了解短期租用子網路的組態。

## ATA 中心需求
本節列出 ATA 中心的需求。

ATA 中心可安裝在執行 Windows Server 2012 R2 的伺服器上。 執行 Windows Update，確定已安裝所有重要的更新。
 您要監視的網域控制站數目以及每個網域控制站的負載，決定了硬體的需求。

也可將 ATA 中心安裝為虛擬機器。 如需詳細資訊，請參閱[設定連接埠鏡像](/advanced-threat-analytics/PlanDesign/configure-port-mirroring)。

如果將 ATA 中心當做虛擬機器執行，請在建立新檢查點之前先關閉伺服器，以避免潛在的資料庫損毀。

> [!NOTE]
> ATA 中心可以安裝在屬於網域或工作群組的成員伺服器上。

**最低需求**

-   CPU - 8 核心

-   記憶體 - 48 GB

-   儲存體 - 每月 1000 GB，用於監視 2 個輕度載入的網域控制站

ATA 中心最少需要 21 天的資料來進行使用者行為分析。 如需硬體需求的詳細資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/plandesign/ata-capacity-planning)。

> [!NOTE]
> 如果您想要在包含一些 VM 的實驗室中安裝 ATA，建議您至少配備 2 核心、4 GB RAM 和 100 GB 的儲存體，方便您與不支援生產環境部署的 ATA 主控台互動。

### 時間同步
ATA 中心伺服器、ATA 閘道伺服器和網域控制站必須時間同步相差在 5 分鐘內。

### BIOS 設定
ATA 資料庫需要您**停用** BIOS 中的非統一記憶體存取 (NUMA)。 您的系統中 NUMA 可能叫做節點交錯，在此情況下您必須**啟用**節點交錯。 如需詳細資訊，請參閱您的 BIOS 文件。

### 網路介面卡
需求：

-   一個網路介面卡

-   兩個 IP 位址

ATA 中心和 ATA 閘道之間的通訊是在連接埠 443 上使用 SSL 加密。 此外，ATA 主控台在 IIS 上執行，並在連接埠 443 上使用 SSL 保護。 建議使用**兩個 IP 位址**。 ATA 中心服務會將連接埠 443 繫結到第一個 IP 位址，IIS 會將連接埠 443 繫結到第二個 IP 位址。

> [!NOTE]
> 可以單一 IP 位址使用兩個不同的連接埠，但建議使用兩個 IP 位址。

### 連接埠
下表列出 ATA 中心正常運作最少要開啟的連接埠。

在這張表中，IP 位址 1 繫結至 ATA 中心服務，IP 位址 2 繫結至 ATA 主控台的 IIS 服務。

|通訊協定|傳輸|Port|去/從|方向|IP 位址|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (ATA 通訊)|TCP|443 或可設定|ATA 閘道|輸入|IP 位址 1|
|**HTTP**|TCP|80|公司網路|輸入|IP 位址 2|
|**HTTPS**|TCP|443|公司網路和 ATA 閘道|輸入|IP 位址 2|
|**SMTP** (選擇性)|TCP|25|SMTP 伺服器|輸出|IP 位址 2|
|**SMTPS** (選擇性)|TCP|465|SMTP 伺服器|輸出|IP 位址 2|
|**Syslog** (選擇性)|TCP|514|Syslog 伺服器|輸出|IP 位址 2|

### 憑證
請確定 ATA 閘道可以存取您的 CRL 發佈點。 如果 ATA 閘道沒有網際網路存取權，請遵循[手動匯入 CRL 的程序](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx)，小心安裝整個鏈結的所有 CRL 發佈點。

為了簡化 ATA 中心的安裝，您可以在 ATA 中心安裝期間安裝自我簽署的憑證。 部署後，可將自我簽署的憑證取代為由內部憑證授權單位發出、ATA 閘道將會使用的憑證。

> [!NOTE]
> 自我簽署憑證應該只在實驗室部署中使用。

ATA 中心需要下列服務的憑證︰

-   Internet Information Services (IIS) – Web 伺服器憑證

-   ATA Center 服務 – 伺服器驗證憑證

> [!NOTE]
> 如果您要從其他電腦存取 ATA 主控台，請確定這些電腦會信任 IIS 使用的憑證，否則在進入登入頁面之前就會出現警告頁面，指出網站的安全性憑證有問題。

## ATA 閘道需求
ATA 閘道可安裝在執行 Windows Server 2012 R2 的伺服器上。

執行 Windows Update，確定已安裝所有**重要**的更新。
安裝 ATA 閘道前，請確定已安裝下列更新︰[KB2919355](https://support.microsoft.com/en-us/kb/2919355/)。

您可以執行下列 Windows PowerShell Cmdlet 來確認安裝與否：`[Get-HotFix -Id kb2919355]`。

> [!NOTE]
> -   ATA 閘道可以安裝在屬於網域或工作群組的成員伺服器上。
> -   ATA 閘道不能安裝在網域控制站上。

如需使用虛擬機器與 ATA 閘道的詳細資訊，請參閱[設定連接埠鏡像](/ATA/plandesign/configure-port-mirroring.html)。

> [!NOTE]
> 如果將 ATA 閘道當做虛擬機器執行，請在建立新檢查點之前先關閉伺服器，以避免潛在的資料庫損毀。

ATA 閘道可以支援監視多個網域控制站，依進出網域控制站的網路傳輸量而定。

**最低需求：**

-   CPU - 4 核心

-   記憶體 - 8 GB

-   儲存體 - OS 夠用 + 10GB 用於 ATA + 損毀傾印 = 至少 100 GB

如需詳細資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/plandesign/ata-capacity-planning)。

### 電源設定
為了達到最佳效能，將 ATA 閘道的 [電源選項]**** 設定為 [高效能]****。

### 時間同步
ATA 中心伺服器和 ATA 閘道伺服器必須時間同步相差在 5 分鐘內。

此外，ATA 閘道伺服器和它連線的網域控制站必須時間同步在 5 分鐘內。

### 網路介面卡
ATA 閘道需要至少一個管理介面卡和至少一個擷取介面卡︰

-   **管理介面卡** - 將會用於您的公司網路上的通訊。 此介面卡應設定以下項目：

    -   靜態 IP 位址，包含預設閘道

    -   慣用和替代的 DNS 伺服器

    -   **此連線的 DNS 尾碼**應該是受監視之每個網域的網域 DNS 名稱。

        ![](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > 如果 ATA 閘道是網域的成員，這會自動設定。

-   **擷取介面卡** - 將用來擷取進出網域控制站的流量。

    > [!IMPORTANT]
    > -   設定擷取介面卡的連接埠鏡像做為網域控制站網路流量的目的地。 如需詳細資訊，請參閱[設定連接埠鏡像](/ATA/PlanDesign/configure-port-mirroring.html)。 一般而言，設定連接埠鏡像必須與網路或虛擬化團隊合作。
    > -   為您的環境設定靜態、無法經路由傳送的 IP 位址，沒有預設閘道也沒有 DNS 伺服器位址。 例如，1.1.1.1/32。 這可確保擷取網路介面卡可以擷取最大量的流量，且管理網路介面卡會用來傳送和接收必要的網路流量。

### 連接埠
下表列出在管理介面上設定 ATA 閘道最少需要的連接埠。

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP 和 UDP|389|網域控制站|輸出|
|安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
|LDAP 至通用類別|TCP|3268|網域控制站|輸出|
|LDAPS 至通用類別|TCP|3269|網域控制站|輸出|
|Kerberos|TCP 和 UDP|88|網域控制站|輸出|
|Netlogon|TCP 和 UDP|445|網域控制站|輸出|
|Windows Time|UDP|123|網域控制站|輸出|
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|透過 RPC 的 NTLM|TCP|135|網路上的所有裝置|輸出|
|NetBIOS|UDP|137|網路上的所有裝置|輸出|
|SSL|TCP|443 或如中心服務所設定|ATA 中心：<br /><br />- 中心服務 IP 位址<br />- IIS IP 位址|輸出|
|Syslog (選擇性)|UDP|514|SIEM 伺服器|輸入|

> [!NOTE]
> 隨著 ATA 閘道完成解析程序的一部分，在 ATA 閘道網路中的裝置上，下列連接埠必須開啟輸入。
>
> -   透過 RPC 的 NTLM
> -   NetBIOS

### 憑證
為了簡化 ATA 中心的安裝，您可以在 ATA 中心安裝期間安裝自我簽署的憑證。 部署後，可將自我簽署的憑證取代為由內部憑證授權單位發出、ATA 閘道將會使用的憑證。

> [!NOTE]
> 自我簽署憑證應該只在實驗室部署中使用。

支援**伺服器驗證**的憑證必須安裝在本機電腦存放區中 ATA 閘道的電腦存放區。 此憑證必須受到 ATA 中心的信任。

## ATA 主控台
ATA 主控台的存取是透過瀏覽器，支援下列瀏覽器︰

-   Internet Explorer 第 10 版及更新版本

-   Google Chrome 第 40 版及更新版本

-   螢幕解析度最低需求為 1700 像素

## 另請參閱
[ATA 架構](/advanced-threat-analytics/understand/ata-architecture)
 [安裝 ATA](/advanced-threat-analytics/deployuse/install-ata)
 [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


