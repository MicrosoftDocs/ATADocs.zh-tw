---
title: "使用效能計數器為 ATA 疑難排解 | Microsoft ATA"
description: "描述如何使用效能計數器疑難排解 ATA 相關問題"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/21/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 21f28848dd22cfbcbb4b4871300621203b445fb4
ms.openlocfilehash: a6113c106653039ca3b4337d9250d9b9baca4611


---

*適用於︰Advanced Threat Analytics 1.7 版*



# 使用效能計數器疑難排解 ATA
ATA 效能計數器提供每個 ATA 元件執行程度的見解。 ATA 中的元件會循序處理資料，因此當發生問題時，會導致元件中某處的流量部分中斷。 若要修正此問題，您必須找出發生問題的元件，並在連鎖的源頭修正問題。 使用在效能計數器中找到的資料，來了解每個元件的運作情況。
請參閱 [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)以了解內部 ATA 元件的流程。

**ATA 元件程序**：

1.  當元件達到其大小上限時，它會封鎖先前的元件且不會傳送多個實體給它。

2.  然後，先前的元件最終將會開始增加**其**本身的大小，直到它封鎖先前的元件且不會傳送多個實體。

3.  這會在傳回 NetworkListener 元件時發生，此元件將會在無法再轉送實體時捨棄流量。


## ATA 閘道效能計數器

在本節中，ATA 閘道的每個參考也都適用於 ATA 輕量型閘道。

您可以新增 ATA 閘道的效能計數器來觀察 ATA 閘道的即時效能狀態。
您可藉由開啟「效能監視器」並新增 ATA 閘道的所有計數器來完成此動作。 效能計數器物件的名稱是：「Microsoft ATA 閘道」。

以下是要注意的主要 ATA 閘道計數器清單︰

|計數器|說明|閾值|疑難排解|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF Parser Messages/Sec|每秒由 ATA 閘道處理的流量。|沒有閾值|協助您了解 ATA 閘道正在剖析的流量。|
|NetworkListener PEF Dropped Events/Sec|每秒由 ATA 閘道減少的流量。|此數字應保持為零 (可接受極少數的短時間減少高載)。|檢查是否有任何元件達到其大小上限，並且封鎖 NetworkListener 所有的先前元件。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|ATA GW Counter/NetworkListener ETW Dropped Events/Sec|每秒由 ATA 閘道減少的流量。|此數字應保持為零 (可接受極少數的短時間減少高載)。|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|ATA GW Counter/NetworkActivityTranslator Message Data # Block Size|為轉譯成網路活動 (NA) 而加入佇列的流量。|應小於上限 -1 (預設上限︰100,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|ATA GW Counter/EntityResolver Activity Block Size|做為解決方法而加入佇列的網路活動 (NA) 數量。|應小於上限 -1 (預設上限︰10,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|ATA GW Counter/EntitySender Entity Batch Block Size|要傳送給 ATA 中心而加入佇列的網路活動 (NA) 數量。|應小於上限 -1 (預設上限︰1,000,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|ATA GW Counter/EntitySender Batch Send Time|傳送最後一個批次所花的時間。|大部分時候應小於 1000 毫秒|檢查 ATA 閘道和 ATA 中心之間是否有任何網路問題。|

> [!NOTE]
> -   時間計數器以毫秒為單位。
> -   有時候使用「報告」圖形類型監視計數器的完整清單會更方便 (範例︰所有計數器的即時監視)

## ATA 輕量型閘道效能計數器
效能計數器可用於輕量型閘道中的配額管理，確保 ATA 不會耗盡安裝所在的網域控制站太多的資源。
若要測量 ATA 在輕量型閘道上強制執行的資源限制，請新增下列計數器︰

開啟「效能監視器」並新增 ATA 閘道的所有計數器。 效能計數器物件的名稱是：「Microsoft ATA 閘道器」和「Microsoft ATA 閘道更新程式」。


|計數器|說明|閾值|疑難排解|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max %|輕量型閘道處理序可使用的 CPU 時間最大量 (以百分比表示)。 |沒有閾值。 | 這是為了保護網域控制站資源不被 ATA 輕量型閘道用完所做的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對執行網域控制站的伺服器加入更多資源。|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|輕量型閘道處理序可使用的認可記憶體最大量 (以位元組表示)。|沒有閾值。 | 這是為了保護網域控制站資源不被 ATA 輕量型閘道用完所做的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對執行網域控制站的伺服器加入更多資源。| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size|輕量型閘道處理序可使用的實體記憶體最大量 (以位元組表示)。|沒有閾值。 | 這是為了保護網域控制站資源不被 ATA 輕量型閘道用完所做的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對執行網域控制站的伺服器加入更多資源。|



若要查看您實際的耗用量，請參閱下列計數器︰



|計數器|說明|閾值|疑難排解|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.Gateway)\%Processor Time|輕量型閘道處理序實際正在使用的 CPU 時間量 (以百分比表示)。 |沒有閾值。 | 比較此計數器的結果與 GatewayUpdaterResourceManager CPU Time Max % 中找到的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對輕量型閘道提供更多資源。|
|Process(Microsoft.Tri.Gateway)\Private Bytes|輕量型閘道處理序實際正在使用的認可記憶體量 (以位元組表示)。|沒有閾值。 | 比較此計數器的結果與 GatewayUpdaterResourceManager Commit Memory Max Size 中找到的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對輕量型閘道提供更多資源。| 
|Process(Microsoft.Tri.Gateway)\Working Set|輕量型閘道處理序實際正在使用的實體記憶體量 (以位元組表示)。|沒有閾值。 |比較此計數器的結果與 GatewayUpdaterResourceManager Working Set Limit Size 中找到的限制。 如果您看到處理序經常在經過一段時間之後達到最大的限制 (處理序達到限制時，就會開始捨棄流量)，表示您需要對輕量型閘道提供更多資源。|

## ATA 中心效能計數器
您可以新增 ATA 中心的效能計數器來觀察 ATA 中心的即時效能狀態。

您可藉由開啟「效能監視器」並新增 ATA 中心的所有計數器來完成此動作。 效能計數器物件的名稱是：「Microsoft ATA 中心」。

以下是要注意的主要 ATA 中心計數器清單︰

|計數器|說明|閾值|疑難排解|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver Entity Batch Block Size|ATA 中心加入佇列的實體批次數目。|應小於上限 -1 (預設上限︰10,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。  請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size|要處理而加入佇列的網路活動 (NA) 數目。|應小於上限 -1 (預設上限︰50,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|Microsoft ATA Center\EntityProfiler Network Activity Block Size|要分析而加入佇列的網路活動 (NA) 數目。|應小於上限 -1 (預設上限︰10,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|
|Microsoft ATA Center\CenterDatabase &#42; Block Size|要寫入資料庫而加入佇列的特定類型網路活動數目。|應小於上限 -1 (預設上限︰50,000)|檢查是否有任何元件達到其大小上限，並且封鎖先前的元件直到 NetworkListener。 請參閱上方的 **ATA 元件程序**。<br /><br />檢查 CPU 或記憶體確定沒有問題。|


> [!NOTE]
> -   時間計數器以毫秒為單位
> -   有時候使用「報告」的圖形類型監視計數器的完整清單會更方便 (範例︰所有計數器的即時監視)。

## 作業系統計數器
以下是要注意的主要作業系統計數器清單︰

|計數器|說明|閾值|疑難排解|
|-----------|---------------|-------------|-------------------|
|Processor(_Total)\% Processor Time|處理器花費在執行非閒置執行緒的經過時間百分比。|平均小於 80%|檢查是否有花費的處理器時間遠超過預期的特定程序。<br /><br />新增更多處理器。<br /><br />減少每部伺服器的流量。<br /><br />"Processor(_Total)\% Processor Time" 計數器在虛擬伺服器上可能會較不精確，在此情況下，要測量處理器電源不足，更精確的方式是透過 "System\Processor Queue Length" 計數器。|
|System\Context Switches/sec|所有處理器從一個執行緒切換到另一個執行緒的組合速率。|小於 5000&#42; 個核心 (實體核心)|檢查是否有花費的處理器時間遠超過預期的特定程序。<br /><br />新增更多處理器。<br /><br />減少每部伺服器的流量。<br /><br />"Processor(_Total)\% Processor Time" 計數器在虛擬伺服器上可能會較不精確，在此情況下，要測量處理器電源不足，更精確的方式是透過 "System\Processor Queue Length" 計數器。|
|System\Processor Queue Length|準備好執行，且正等候排程的執行緒數目。|小於 5&#42; 個核心 (實體核心)|檢查是否有花費的處理器時間遠超過預期的特定程序。<br /><br />新增更多處理器。<br /><br />減少每部伺服器的流量。<br /><br />"Processor(_Total)\% Processor Time" 計數器在虛擬伺服器上可能會較不精確，在此情況下，要測量處理器電源不足，更精確的方式是透過 "System\Processor Queue Length" 計數器。|
|Memory\Available MBytes|可供配置的實體記憶體 (RAM) 數量。|應大於 512|檢查是否有花費的實體記憶體遠超過預期的特定程序。<br /><br />減少實體記憶體數量。<br /><br />減少每部伺服器的流量。|
|LogicalDisk(&#42;)\Avg. 的集合規則|從磁碟讀取資料的平均延遲 (您應該選擇資料庫磁碟機做為執行個體)。|應小於 10 毫秒|檢查是否有特定程序，其利用的資料庫磁碟機超過預期。<br /><br />如果此磁碟機可以提供目前的工作負載，同時具有小於 10 毫秒的延遲，請洽詢儲存體小組/廠商。 使用磁碟使用計數器可判斷目前的工作負載。|
|LogicalDisk(&#42;)\Avg. 的集合規則|將資料寫入磁碟的平均延遲 (您應該選擇資料庫磁碟機做為執行個體)。|應小於 10 毫秒|檢查是否有特定程序，其利用的資料庫磁碟機超過預期。<br /><br />如果此磁碟機可以提供目前的工作負載，同時具有小於 10 毫秒的延遲，請洽詢儲存體小組/廠商。 使用磁碟使用計數器可判斷目前的工作負載。|
|\LogicalDisk(&#42;)\Disk Reads/sec|執行讀取作業至磁碟的速率。|沒有閾值|磁碟使用計數器可在疑難排解儲存體延遲時新增見解。|
|\LogicalDisk(&#42;)\Disk Read Bytes/sec|每秒從磁碟讀取的位元組數目。|沒有閾值|磁碟使用計數器可在疑難排解儲存體延遲時新增見解。|
|\LogicalDisk&#42;\Disk Writes/sec|執行寫入作業至磁碟的速率。|沒有閾值|磁碟使用計數器 (可在疑難排解儲存體延遲時新增見解)|
|\LogicalDisk(&#42;)\Disk Write Bytes/sec|每秒寫入磁碟的位元組數目。|沒有閾值|磁碟使用計數器可在疑難排解儲存體延遲時新增見解。|

## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


