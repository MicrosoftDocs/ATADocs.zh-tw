---
title: "調查使用 DNS 探查 | Microsoft Docs"
description: "本文描述使用 DNS 探查，並提供 ATA 偵測到這類威脅時的調查指示。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 436b96f679836060cfaf40f6be3b92cf96dc0e04
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2017
---
適用於︰Advanced Threat Analytics 1.8 版

<a id="investigating-reconnaissance-using-dns" class="xliff"></a>

# 調查使用 DNS 探查

如果 ATA 在您的網路上偵測到**使用 DNS 探查**，就會向您提出警示，使用本文可協助您調查警示並了解如何修復問題。

<a id="what-is-reconnaissance-using-dns" class="xliff"></a>

## 什麼是使用 DNS 探查？

**使用 DNS 探查**警示指出有來自不尋常主機的可疑網域名稱系統 (DNS) 查詢，在您的內部網路上執行探查。

網域名稱系統 (DNS) 是實作為階層分散式資料庫的服務，提供主機名稱和網域名稱的解析。 DNS 資料庫中的名稱會形成階層式樹狀檢視結構，稱為網域命名空間。
對敵人而言，您的 DNS 包含對應內部網路的重要資訊，包括所有伺服器清單，通常也包括對應至其 IP 位址的所有用戶端清單。 此外，這項資訊之所以有價值，是因為它會列出在指定網路環境中通常是描述性的主機名稱。 藉由擷取這項資訊，敵人就可以在活動期間將火力集中在相關實體上。 [Nmap](https://nmap.org/)、[Fierce](https://github.com/mschwager/fierce) 及內建工具 (例如 [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx)) 等工具提供使用 DNS 探查的主機探索功能。
在內部主機中偵測到使用 DNS 查詢探查會造成問題，表示現有主機可能遭到入侵、可能有更廣泛的網路入侵，或可能有測試人員威脅。

<a id="dns-query-types" class="xliff"></a>

## DNS 查詢類型

DNS 通訊協定中有數種查詢類型。 ATA 會偵測 AXFR (傳輸) 要求，並在發現時建立警示。 這種類型的查詢應該只來自 DNS 伺服器。

<a id="discovering-the-attack" class="xliff"></a>

## 探索攻擊

當攻擊者嘗試執行使用 DNS 探查時，ATA 會偵測到此攻擊，並標示為中嚴重性。

![ATA 偵測到 DNS 探查](./media/dns-recon.png)
 
ATA 會顯示來源電腦的名稱，以及所執行之實際 DNS 查詢的其他詳細資料。 例如，可能有多個嘗試來自同一個主機。

<a id="investigating" class="xliff"></a>

## 調查

若要調查使用 DNS 探查，您必須先判斷查詢的原因。 這些原因可以識別為下列其中一個類別： 
-   真肯定：您的網路上有攻擊者或惡意程式碼。 可能是入侵周邊網路的攻擊者，或是測試人員威脅。
-   良性的真肯定：可能是滲透測試、事件處理小組活動、安全性掃描程式、新一代防火牆或執行獲批准活動的 IT 系統管理員所觸發的警示。
-   誤判：您可能會收到因設定錯誤而出現的警示，例如 ATA 閘道與您的 DNS 伺服器之間的連接埠 53 遭到封鎖 (或任何其他網路問題)。

下圖可協助您判斷應該採取的調查步驟：

![透過 ATA 解決 DNS 探查問題](./media/dns-recon-diagram.png)
 
1.  第一個步驟是識別產生警示的電腦，如下所述：
 
    ![在 ATA 中檢視 DNS 探查可疑活動](./media/dns-recon-2.png)
2.  識別這部電腦的正身。 它是工作站、伺服器、系統管理工作站、滲透測試站台，還是其他？
3.  如果電腦是 DNS 伺服器，而且具有要求區域次要複本的合法權限，則為誤判。 當您發現誤判時，請使用 [排除] 選項，如此一來在這部電腦上就不會再收到此特定警示。
4. 請確定 ATA 閘道與您的 DNS 伺服器之間已開啟連接埠 53。
4.  如果電腦用於系統管理工作或滲透測試，則為良性的真肯定，而且相關的電腦也可以設定為例外狀況。
5.  如果不是用於滲透測試，請檢查電腦是否正在執行安全性掃描程式或新一代防火牆，這會發出 AXFR 類型的 DNS 要求。
6.  最後，如果不符合上述任何一個準則，電腦可能遭到入侵，而必須接受完整調查。 
7.  如果查詢已隔離到特定電腦，而且經判斷不是良性，則應該採取下列步驟：
    1.  檢閱可用的記錄檔來源。 
    2.  執行主機型分析。 
    3.  如果活動不是來自可疑的使用者，則應該在電腦上執行鑑識調查分析，以判斷其是否已受到惡意程式碼的入侵。

<a id="post-investigation" class="xliff"></a>

## 調查後

用來入侵主機的惡意程式碼可能包含具有後門程式功能的特洛伊木馬病毒。 如果在遭入侵的主機中發現成功的橫向移動，修復動作應該延伸到這些主機 (包括變更主機上所使用的任何密碼和認證)，以及包含在橫向移動中的任何主機。 

如果在執行修復步驟之後無法確認受害主機沒有問題，或無法識別入侵的根本原因，Microsoft 會建議備份重要資料並重建主機電腦。 此外，請強化新的或重建的主機，再將其放回網路，以避免再次受到感染。 

Microsoft 建議您使用可透過 Microsoft 帳戶小組連絡的專業事件回應與復原小組，協助偵測攻擊者是否已在您網路中部署持續性方法。

<a id="mitigation" class="xliff"></a>

## 降低

您可以停用區域傳輸，或將區域傳輸僅限於指定的 IP 位址，來保護內部 DNS 伺服器，以防止發生使用 DNS 探查。 如需限制區域傳輸的其他資訊，請參閱 Windows Server Technet 文章：[Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (限制區域傳輸)。 您可以[使用 IPsec 保護區域傳輸](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx)，進一步鎖定限制的區域傳輸。 「修改區域傳輸」是檢查清單中的一項工作，應該加以解決才能[保護 DNS 伺服器免受內部和外部攻擊](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)。



<a id="see-also" class="xliff"></a>

## 另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
