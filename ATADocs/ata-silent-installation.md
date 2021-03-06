---
title: 以無訊息方式安裝 Advanced 威脅分析
description: 本文說明如何以無訊息方式安裝 ATA。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/20/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 55c12920020a0cbcda0b38e7b9d0cae083423a4e
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690970"
---
# <a name="ata-silent-installation"></a>ATA 無訊息安裝

[!INCLUDE [Banner for top of topics](includes/banner.md)]

本文提供以無訊息方式安裝 ATA 的指示。

## <a name="prerequisites"></a>先決條件

ATA 1.9 版需要安裝 Microsoft .NET Framework 4.6.1。

當您安裝或更新 ATA 時，.Net Framework 4.6.1 會隨著 Microsoft ATA 部署自動安裝。

> [!Note]
> .Net framework 4.6.1 安裝可能需要重新啟動伺服器。 在網域控制站上安裝 ATA 閘道時，請考慮為這些網域控制站排定維護期間。 使用 ATA 無訊息安裝方法時，安裝程式會設定為在安裝結束時自動重新啟動伺服器安裝 (如有必要)。 由於 Windows Installer 的某個錯誤，norestart 旗標無法可靠地用來確定伺服器不會重新啟動，因此請務必只在維護期間執行無訊息安裝。

若要追蹤部署的進度，請監視位於 **%AppData%\Local\Temp** 的 ATA 安裝程式記錄檔。

## <a name="install-the-ata-center"></a>安裝 ATA 中心

使用下列命令安裝 ATA 中心：

**語法**：

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CertificateThumbprint="<CertThumbprint>"]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|
> |LicenseAccepted|--LicenseAccepted|是|指出已閱讀並核准授權。 無訊息安裝時必須設定。|

**安裝參數**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
>|InstallationPath|InstallationPath="<InstallPath>"|否|設定 ATA 二進位檔案的安裝路徑。 預設路徑︰C:\Program Files\Microsoft Advanced Threat Analytics\Center|
>|DatabaseDataPath|DatabaseDataPath= "<DBPath>"|否|設定 ATA 資料庫的資料夾路徑。 預設路徑︰C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
>|CenterCertificateThumbprint|CenterCertificateThumbprint="<CertThumbprint>"|否|設定 ATA 中心的憑證指紋。 此憑證可用來保護 ata 閘道與 ATA 中心的通訊，以及驗證 ATA 主控台網站的身分識別。 如果未設定，安裝會產生自我簽署憑證。|

**範例**：

若要使用預設安裝路徑和使用者定義憑證指紋來安裝 ATA 中心：

```dos
"Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
```

## <a name="update-the-ata-center"></a>更新 ATA 中心

使用下列命令更新 ATA 中心：

**語法**：

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|

更新 ATA 時，安裝程式會自動偵測 ATA 是否已安裝在伺服器上，而不需要使用更新安裝選項。

**範例**：

以無訊息方式更新 ATA 中心。 在大型環境中，ATA 中心更新可能需要一些時間才能完成。 監視 ATA 記錄檔以追蹤更新的進度。

```dos
"Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-center-silently"></a>以無訊息方式將 ATA 中心解除安裝

使用下列命令執行 ATA 中心的無訊息解除安裝：

**語法**：

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Uninstall] [/Help] [--DeleteExistingDatabaseData]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息解除安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行解除安裝程式，但不顯示任何 UI 和提示。|
> |解除安裝|/uninstall|是|從伺服器執行 ATA 中心的無訊息解除安裝。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|

**安裝參數**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息解除安裝而言是否為必要？|說明|
> |---|---|---|---|
> |DeleteExistingDatabaseData|DeleteExistingDatabaseData|否|刪除現有資料庫中的所有檔案。|

**範例**：

若要從伺服器以無訊息方式解除安裝 ATA 中心，並移除所有現有的資料庫資料：

```dos
"Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData
```

## <a name="ata-gateway-silent-installation"></a>ATA 閘道無訊息安裝

> [!NOTE]
> 使用 System Center Configuration Manager 或其他軟體部署系統，以無訊息方式部署 ATA 輕量型閘道時，建議建立兩個部署套件：</br>- Net Framework 4.6.1，包括重新啟動網域控制站</br>- ATA 閘道。 </br>讓 ATA 閘道套件相依於 .Net Framework 套件的部署。 </br>取得 [.Net Framework 4.6.1 離線部署套件](https://www.microsoft.com/download/details.aspx?id=49982)。

使用下列命令以無訊息方式安裝 ATA 閘道：

**語法**：

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"] [ConsoleAccountName="<AccountName>"] [ConsoleAccountPassword="<AccountPassword>"]
```

> [!NOTE]
> 如果您想要在已加入網域的電腦上工作，並已使用 ATA 系統管理員使用者名稱和密碼登入，則不需要在這裡提供您的認證。

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|

**安裝參數**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
>|InstallationPath|InstallationPath="<InstallPath>"|否|設定 ATA 二進位檔案的安裝路徑。 預設路徑︰C:\Program Files\Microsoft Advanced Threat Analytics\Center
>|ConsoleAccountName|ConsoleAccountName="<AccountName>"|是|為用來向 ATA 中心註冊 ATA 閘道的使用者帳戶 (user@domain.com) 設定名稱。|
>|ConsoleAccountPassword|ConsoleAccountPassword="<AccountPassword>"|是|為用來向 ATA 中心註冊 ATA 閘道的使用者帳戶 (user@domain.com) 設定密碼。|

**範例**：

若要以無訊息方式安裝 ATA 閘道，請使用您的 ATA 系統管理員認證登入已加入網域的電腦，以便您不需要在安裝期間指定認證。 否則，請使用指定的認證向 ATA 中心註冊：

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
```

## <a name="update-the-ata-gateway"></a>更新 ATA 閘道

使用下列命令以無訊息方式更新 ATA 閘道：

**語法**：

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|

**範例**：

若要以無訊息方式更新 ATA 閘道：

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-gateway-silently"></a>以無訊息方式將 ATA 閘道解除安裝

使用下列命令執行 ATA 閘道的無訊息解除安裝：

**語法**：

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息解除安裝而言是否為必要？|說明|
> |---|---|---|---|
> |Quiet|/quiet|是|執行解除安裝程式，但不顯示任何 UI 和提示。|
> |解除安裝|/uninstall|是|從伺服器執行 ATA 閘道的無訊息解除安裝。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|

**範例**：

若要從伺服器以無訊息方式將 ATA 閘道解除安裝：

```dos
"Microsoft ATA Gateway Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
