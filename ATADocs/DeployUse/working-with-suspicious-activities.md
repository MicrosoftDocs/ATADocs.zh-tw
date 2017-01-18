---
title: "處理可疑活動 | Microsoft Docs"
description: "描述如何檢閱 ATA 所識別的可疑活動"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 29a8b5b76b4b435157f0907f0dc98731dacbc53a


---

適用於︰Advanced Threat Analytics 1.7 版



# <a name="working-with-suspicious-activities"></a>處理可疑活動
本主題說明如何使用 Advanced Threat Analytics 的基本概念。

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>在攻擊時間表上檢閱可疑活動
登入 ATA 主控台之後，您會自動進入開啟的**可疑活動時間表**。 可疑活動會依時間順序列出，最新的可疑活動位於時間表頂端。
每個可疑活動都有下列資訊︰

-   涉及的實體，包括使用者、電腦、伺服器、網域控制站以及資源。

-   可疑活動的時間和時間範圍。

-   可疑活動的嚴重性，高級、中級或低級。

-   狀態︰開啟、已解析或關閉。

-   能力

    -   透過電子郵件與組織中的其他人員分享可疑的活動。

    -   將可疑活動匯出至 Excel。

    -   新增可疑活動的注意事項。

    -   提供可疑活動的輸入。

-   提供如何回應可疑活動的建議。

> [!NOTE]
> -   當滑鼠停留在使用者或電腦上時，會顯示實體小型設定檔，提供實體的其他相關資訊，並包含實體連結的可疑活動數目。
> -   如果您按一下實體，它會帶您到使用者或電腦的實體設定檔。

![ATA 可疑活動時間表影像](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>篩選可疑活動清單
篩選可疑活動清單：

1.  在畫面左側的 [篩選依據] 窗格中，選取下列其中一個項目︰[所有]、[開啟的]、[已解析] 或 [已關閉]。

2.  若要進一步篩選清單，請選取 [高級]、[中級] 或 [低級]。

**可疑活動嚴重性**

-   **低**

    表示可能會導致攻擊的可疑活動，這些攻擊專為惡意使用者或軟體設計來存取組織的資料。

-   **中**

    表示可能會讓特定身分識別處於更嚴重攻擊之風險中的可疑活動，這些攻擊可能會導致身分識別盜用或特殊權限的提升

-   **高**

    表示可能會導致身分識別盜用、權限提升或其他高影響攻擊的可疑活動

**可疑活動狀態**

-   **開啟**

    所有新的可疑活動都出現此清單中

-   **已解決**

    用於追蹤您已識別、研究與修正以緩解的可疑活動。

    > [!NOTE]
    > 如果在短時間內偵測到相同的活動，ATA 可能會重新開啟已經解析的活動。

-   **已關閉**

    您以手動方式關閉的活動。 如果 ATA 偵測到類似的可疑活動，將會建立新的偵測。

## <a name="provide-input-on-a-suspicious-activity"></a>提供可疑活動的輸入
若要啟用 ATA 來了解您與您的網路，某些可疑活動 (DNS 探查、Pass the Ticket、SMB 工作階段列舉、異常行為和遠端執行) 會要求您的輸入，以加強接下來的可疑活動偵測。

1.  對於可讓您提供輸入的可疑活動，會自動開啟輸入問題。 系統會要求您回答網路上活動的相關問題，以及是否將其視為可疑。 在下列範例中，系統會詢問您是否允許從特定電腦執行掃描工具。

    ![ATA 提供可疑活動輸入影像](media/ATA-Input.JPG)

2.  如果您回答「否」，此活動會視為可疑，ATA 從這台電腦遇到此活動的任何時候，您都會收到警示。

3.  不過，如果您回答「是」，可能會關閉可疑活動，來自此電腦的此類型未來活動可能不會產生可疑活動，或者會產生自動關閉的活動。

4.  如果您不知道，您可以按一下 [取消]。

## <a name="change-the-status-of-a-suspicious-activity"></a>變更可疑活動的狀態
您可以按一下可疑活動的目前狀態，然後選取下列 [開啟]、[已解析] 或 [已關閉] 其中一項來變更可疑活動的狀態。

## <a name="see-also"></a>另請參閱
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [使用 ATA 偵測設定](working-with-detection-settings.md)
- [修改 ATA 組態](modifying-ata-configuration.md)



<!--HONumber=Jan17_HO1-->


