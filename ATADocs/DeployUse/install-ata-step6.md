---
# required metadata

title: 安裝 ATA | Microsoft Advanced Threat Analytics
description: 在安裝 ATA 的最後一個步驟裡，您可以設定短期租用子網路和 Honeytoken 使用者。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安裝 ATA - 步驟 6

>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)

## 步驟 6： 設定短期租用子網路和 Honeytoken 使用者
短期租用子網路是 IP 位址指派變更非常快速的子網路，通常在幾秒或幾分鐘內就會變更。 例如，用於您 Vpn 和 Wi-fi IP 位址的 IP 位址。 若要輸入您組織中使用的短期租用子網路清單，請遵循下列步驟︰

1.  從 ATA 閘道電腦上的 ATA 主控台，按一下設定圖示，然後選取 [設定].

    ![ATA 組態設定](media/ATA-config-icon.JPG)

2.  在 [偵測] 下方，輸入下列短期租用子網路的項目。 輸入使用斜線標記法格式的短期租用子網路，例如︰`192.168.0.0/24` 並按一下加號。

3.  如是 Honeytoken 帳戶 SID，請輸入沒有任何網路活動的使用者帳戶 SID，並按一下加號。 例如： `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > 若要尋找使用者的 SID，請在 ATA 主控台中搜尋使用者，然後按一下 [帳戶資訊] 索引標籤。 

4.  設定排除項目︰您可以設定要從特定可疑活動中排除的 IP 位址。 如需詳細資訊，請參閱[使用 ATA 偵測設定](working-with-detection-settings.md)。

5.  按一下 [儲存].

![儲存變更](media/ATA-VPN-Subnets.JPG)

恭喜，您已成功部署 Microsoft Advanced Threat Analytics！

檢查受攻擊的時間線以便檢視偵測到的可疑活動，並搜尋使用者或電腦並檢視其設定檔。

ATA 將立即開始掃描是否有可疑的活動。 某些活動 (例如某些可疑行為的活動) 會等到 ATA 有時間建立行為設定檔之後 (至少三週) 才可以使用。


>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)


## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


