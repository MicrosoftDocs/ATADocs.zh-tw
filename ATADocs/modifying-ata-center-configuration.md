---
title: 變更 Advanced Threat Analytics ATA 中心設定
description: 描述如何變更您 ATA 中心的 IP 位址、連接埠、主控台 URL 或憑證。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 498eea7cfe1393bd0b616fc5cfbb11bd18334f8f
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414007"
---
# <a name="modifying-the-ata-center-configuration"></a>修改 ATA 中心設定



適用於：*Advanced Threat Analytics 1.9 版*

初始部署後，請小心修改 ATA Center。 更新主控台 URL 和憑證時，請使用下列程序。

## <a name="the-ata-console-url"></a>ATA 主控台 URL

在下列情況下將使用 URL：

-   這是 ATA 閘道用來與 ATA 中心通訊的 URL。

- 安裝 ATA 閘道 – 安裝 ATA 閘道時，它會在 ATA 中心自行登錄。 此登錄程序透過連接至 ATA 主控台來完成。 如果您輸入 FQDN 做為 ATA 主控台 URL，請確定 ATA 閘道可將 FQDN 解析為 ATA 主控台所繫結的 IP 位址。

-   警示 – 當 ATA 送出 SIEM 或電子郵件警示，它會包含可疑活動的連結。 連結的主機部分是 ATA 主控台的 URL 設定。

-   如果是安裝來自內部憑證授權單位 (CA) 的憑證，請讓 URL 符合憑證中的主體名稱。 這樣可避免使用者在連線到 ATA 主控台時收到警告訊息。

-   使用 FQDN 做為 ATA 主控台 URL 時，可讓您修改 ATA 主控台所使用的 IP 位址，而不會中斷先前的警示，或需要重新下載 ATA 閘道套件。 您只需要使用新的 IP 位址來更新 DNS。

1. 確認您使用的新 URL 會解析為 ATA 主控台的 IP 位址。

2. 在 ATA 設定中，於 [中心]  下輸入新的 URL。 此時 ATA 中心服務仍然使用原始 URL。 

   ![變更 ATA 組態](media/change-center-config.png)

   > [!NOTE]
   > 如果輸入了自訂的 IP 位址，除非在 ATA 中心上安裝此 IP 位址，否則將無法按一下 [啟動]  。
    
3. 等候 ATA 閘道進行同步。現在，這些閘道會有兩個可能的 URL 可存取 ATA 主控台。 只要 ATA 閘道可以使用原始 URL 來連線，就不會嘗試使用新 URL。

4. 在所有 ATA 閘道皆已使用更新的設定同步後，請在 [中心設定] 頁面中按一下 [啟動]  按鈕來啟動新的 URL。 當您啟動新 URL 時，ATA 閘道就會使用新的 URL 來存取 ATA 中心。 ATA 閘道連線到 ATA 中心服務之後，將會提取最新的設定，並將僅有 ATA 主控台的新 URL。 

   ![啟動憑證](media/center-activation.png)

> [!NOTE]
> -   在啟動新的 URL 時，如果 ATA 閘道離線，且從未取得更新的設定，請在 ATA 閘道上手動更新設定 JSON 檔案。
> -   啟動新的 URL 之後，如果需要部署新的 ATA 閘道，您需要再次下載 ATA 閘道安裝套件。


## <a name="the-ata-center-certificate"></a>ATA 中心憑證

> [!WARNING]
> - 不支援更新現有憑證的程序。 更新憑證的唯一方法是建立新憑證，然後設定 ATA 使用新憑證。


按照此程序來取代憑證：

1. 在目前的憑證到期之前，建立新的憑證並確認將新憑證安裝在 ATA 中心伺服器上。 <br></br>建議您從內部憑證授權單位選擇憑證，但也可以建立新的自我簽署憑證。 如需詳細資訊，請參閱 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate) \(英文\)。

2. 在 ATA 設定中，於 [中心]  下選取新建立的憑證。 此時 ATA 中心服務仍然繫結至原始憑證。 

   ![變更 ATA 組態](media/change-center-config.png)

3. 等候 ATA 閘道進行同步。現在，這些閘道會有兩個可能的憑證，可進行相互驗證。 只要 ATA 閘道可以使用原始憑證來連線，就不會嘗試使用新憑證。

4. 更新的設定在所有 ATA 閘道同步之後，便可啟動 ATA 中心服務所繫結的新憑證。 啟動新憑證時，ATA 中心服務會繫結到新憑證。 ATA 閘道現在會使用新的憑證向 ATA 中心驗證。 ATA 閘道連線到 ATA 中心服務之後，將會提取最新的設定，並將僅有 ATA 中心的新憑證。 

> [!NOTE]
> -   在啟動新的憑證時，如果 ATA 閘道離線，且從未取得更新的設定，請在 ATA 閘道上手動更新設定 JSON 檔案。
> -   您使用的憑證必須受 ATA 閘道所信任。
> -   憑證也用於 ATA 主控台，所以應該符合 ATA 主控台位址，以避免瀏覽器警告。
> -   如果您需要在啟用新的憑證後部署新的 ATA 閘道，則需要再次下載 ATA 閘道安裝套件。



 
## <a name="see-also"></a>另請參閱
- [使用 ATA 主控台](working-with-ata-console.md)
- [查看 ATA 論壇！](https://aka.ms/ata-forum)
