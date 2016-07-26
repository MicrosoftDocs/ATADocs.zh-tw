---
title: "變更 ATA 設定 - IIS 憑證 | Microsoft ATA"
description: "描述如何變更 IIS 為 ATA 中心所使用的憑證。"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 6516500f3134228cc92e269ef5ea8bfe4faa19d9


---

# 變更 ATA 設定 - IIS 憑證

>[!div class="step-by-step"]
[« ATA 主控台 IP 位址](modifying-ata-config-consoleip.md)
[網域連線密碼 »](modifying-ata-config-dcpassword.md)

## 建立 IIS 憑證
在主控台中，您可以選取和變更 ATA 中心服務的憑證，但您無法變更 IIS 所使用的憑證。

若要變更這些設定，請使用下列程序：

> [!NOTE]
> 修改 IIS 憑證後，您應該於安裝新的 ATA 閘道前下載 ATA 閘道安裝套件。

如果您需要修改 IIS 為 ATA 中心所使用的憑證，請從 ATA 中心伺服器依照下列步驟。

1.  ATA 中心伺服器上安裝新的憑證。

2.  開啟 Internet Information Services (IIS) 管理員.A。

3.  展開伺服器名稱，然後展開 [網站]。

4.  選取 Microsoft ATA 主控台的站台，在 [動作] 窗格中按一下 [繫結]。

    ![ATA 主控台繫結動作](media/ATA-console-change-IP-bindings.jpg)

5.  選取 [HTTPS] 並按一下 [編輯]。

6.  在 [SSL 憑證]下，選取新的憑證。

7.  安裝新的 ATA 閘道前，請先下載 ATA 閘道安裝套件。

>[!div class="step-by-step"]
[« ATA 主控台 IP 位址](modifying-ata-config-consoleip.md)
[網域連線密碼 »](modifying-ata-config-dcpassword.md)

## 另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [安裝 ATA](install-ata.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


