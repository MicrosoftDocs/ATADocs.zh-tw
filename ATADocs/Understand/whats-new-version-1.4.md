---
title: "Advanced Threat Analytics 1.4 版的新功能 | Microsoft Docs"
description: "列出 ATA 1.4 版的新功能以及已知問題"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3884e7d40a598aed292cc492bfa1bd5a5e360990
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
# <a name="what39s-new-in-ata-version-14"></a>ATA 1.4 版的新功能
這些版本資訊提供 Advanced Threat Analytics 1.4 版中已知問題的相關資訊。

## <a name="whats-new-in-this-version"></a>此版本有什麼新功能？

-   支援 Windows 事件轉送 (WEF) 將事件直接從網域控制站傳送至 ATA 閘道。

-   藉由結合 DPI (深度封包檢查) 和 Windows 事件記錄檔來增強公司資源上的傳遞雜湊偵測。

-   增強未加入網域裝置與非 Windows 裝置的偵測與可見度支援。

-   支援每個 ATA 閘道更多流量的效能改善。

-   支援每個 ATA 中心更多 ATA 閘道的效能改善。

-   新增自動名稱解析程序，符合電腦名稱和 IP 位址 – 此唯一功能可在調查程序中節省寶貴的時間，並提供有力的證據給安全性分析師

-   收集使用者的輸入以自動微調偵測程序的改良功能。

-   NAT 裝置的自動偵測。

-   無法連線到網域控制站時進行的自動容錯移轉。

-   系統健全狀況監視和通知現在提供部署的整體健全狀況狀態，以及組態與連線能力的相關特定問題。

-   實體運作所在站台和位置的可見度。

-   多重網域支援。

-   單一標籤網域 (SLD) 的支援。

-   支援修改 IP 位址與 ATA 閘道和 ATA 中心的憑證。

-   協助改善客戶體驗的遙測。

## <a name="known-issues"></a>已知問題
下列已知問題存在於此版本中。

### <a name="network-capture-software"></a>網路擷取軟體
在 ATA 閘道上，您可以安裝的唯一支援網路擷取軟體是 [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) (Microsoft 網路監視器 3.4)。 請勿安裝 Microsoft Message Analyzer 或其他任何網路擷取軟體。 安裝其他軟體將會造成 ATA 閘道停止正常運作。

### <a name="installation-from-zip-file"></a>從 Zip 檔案安裝
安裝 ATA 閘道時，請務必從 zip 檔案解壓縮檔案至本機目錄，並從該處安裝。 請勿直接從 zip 檔案內部安裝 ATA 閘道，否則安裝將會失敗。

### <a name="uninstalling-previous-versions-of-ata"></a>解除安裝舊版的 ATA
如果您已安裝舊版 ATA，包含公開預覽或私人預覽版本，您必須在安裝此版本 ATA 之前先解除安裝 ATA 中心與 ATA 閘道。

您也必須刪除資料庫檔案和記錄檔。 舊版 ATA 的資料庫與 GA 版的 ATA 不相容。

當您嘗試解除安裝 ATA 中心或 ATA 閘道時，如果開啟了 ATA 安裝，而不是解除安裝，您必須新增下列登錄機碼，然後再次解除安裝 ATA。

**ATA 中心**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   利用 `C:\Program Files\Microsoft Advanced Threat Analytics\Center` 的值新增名為 `InstallationPath` 的字串值。 這是預設安裝資料夾。 如果您已變更安裝資料夾，請輸入安裝 ATA 所在的路徑。

    ![ATA 中心安裝路徑的登錄編輯程式](media/ATA-uninstall-center-bug.jpg)

**ATA 閘道**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   利用 `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway` 的值新增名為 `InstallationPath` 的字串值。 這是預設安裝資料夾。  如果您已變更安裝資料夾，請輸入安裝 ATA 所在的路徑。

    ![ATA 閘道安裝路徑的登錄編輯程式](media/ATA-GW-uninstall-bug.jpg)

解除安裝之後，請刪除 ATA 中心和 ATA 閘道上的安裝資料夾。  如果您在不同的資料夾中安裝資料庫，請刪除 ATA 中心上的資料庫資料夾。

### <a name="health-alert---disconnected-ata-gateway"></a>健全狀況警示 - 已中斷 ATA 閘道的連線
如果您多個 ATA 閘道，並已中斷 ATA 閘道警示的連線，只會在其中一個警示中自動進行解除，其他警示維持開啟狀態。 您必須手動確認 ATA 閘道已啟動，且服務正在執行，並手動解除警示。

### <a name="kb-on-virtualization-host"></a>虛擬化主機上的 KB
請勿在虛擬化主機上安裝 KB 3047154。 這可能會導致連接埠鏡像無法正常運作。

## <a name="see-also"></a>另請參閱

[將 ATA 更新至 1.6 版 - 移轉指南](ata-update-1.6-migration-guide.md)

[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)