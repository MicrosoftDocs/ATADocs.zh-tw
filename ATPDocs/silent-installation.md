---
title: 以無訊息模式安裝 Azure 進階威脅防護
description: 說明如何以無訊息模式安裝 Azure ATP。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39437a0397c4d4c0a0238b0e7895c7ee8d15a510
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912495"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Azure ATP 切換參數與無訊息安裝

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

此文章提供 Azure ATP 切換參數與無訊息安裝的指導方針與指示。

## <a name="prerequisites"></a>先決條件

Azure ATP 必須安裝 Microsoft .NET Framework 4.7 或更新版本。

當您安裝 Azure ATP 時，若尚未安裝 .Net Framework 4.7 或更新版本，就會在部署 Azure ATP 時自動安裝 .Net Framework 4.7。

> [!NOTE]
> .Net Framework 4.7 的安裝可能需要重新啟動伺服器。 在網域控制站上安裝 Azure ATP 感應器時，請考慮為網域控制站排程維護視窗。

使用 Azure ATP 無訊息安裝時，安裝程式是設定為在安裝結束時自動重新啟動伺服器 (如有必要)。 請務必只在維護時段執行無訊息安裝。 因為 Windows Installer 的某個錯誤 (Bug)，*norestart* 旗標無法可靠地用來確定伺服器不會重新啟動。

若要追蹤您的部署進度，請監視位於 `%AppData%\Local\Temp` 中的 Azure ATP 安裝程式記錄檔。

## <a name="azure-atp-sensor-silent-installation"></a>Azure ATP 感應器無訊息安裝

> [!NOTE]
> 使用 System Center Configuration Manager 或其他軟體部署系統，以無訊息模式部署 Azure ATP 感應器時，建議建立兩個部署套件：</br>- Net Framework 4.7 或更新版本 (可能需要重新啟動網域控制站)</br>- Azure ATP 感應器。 </br>讓 Azure ATP 感應器套件相依於 .Net Framework 套件的部署。 </br>取得 [.Net Framework 4.7 離線部署套件](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows)。

使用下列命令執行 Azure ATP 感應器的完整無訊息解除安裝：

**cmd.exe syntax**：

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**Powershell 語法**：

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> 使用 Powershell 語法時，省略 **./** 前置詞會導致發生防止無訊息安裝的錯誤。

> [!NOTE]
> 從 Azure ATP 入口網站的 [設定] 區段、[感應器] 頁面，複製存取金鑰。

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|

**安裝參數**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |InstallationPath|InstallationPath=""|否|設定 AATP 感應器二進位檔案的安裝路徑。 預設路徑：%programfiles%\Azure Advanced Threat Protection sensor
> |AccessKey|AccessKey="\*\*"|是|設定用來向 Azure ATP 執行個體註冊 Azure ATP 感應器的存取金鑰。|

**範例**：

使用下列命令以無訊息模式安裝 Azure ATP 感應器：

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="
```

## <a name="proxy-authentication"></a>Proxy 驗證

請使用下列命令來完成 Proxy 驗證：

**語法**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|否|指定 Azure ATP 感應器的 ProxyUrl 和連接埠號碼。|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|否|如果您的 Proxy 服務需要驗證，請以 DOMAIN\user 格式提供使用者名稱。|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|否|指定 Proxy 使用者名稱的密碼。 \* 認證會經過加密，並由 Azure ATP 感應器儲存在本機。|

## <a name="update-the-azure-atp-sensor"></a>更新 Azure ATP 感應器

使用下列命令以無訊息模式更新 Azure ATP 感應器：

**語法**：

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|是|執行安裝程式，但不顯示任何 UI 和提示。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|是|指定 .Net Framework 安裝的參數。 必須設定，才能強制執行 .Net Framework 的無訊息安裝。|

**範例**：

以無訊息模式更新 Azure ATP 感應器：

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-azure-atp-sensor-silently"></a>以無訊息模式將 Azure ATP 感應器解除安裝

使用下列命令執行 Azure ATP 感應器的無訊息解除安裝：

**語法**：

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**安裝選項**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息解除安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|是|執行解除安裝程式，但不顯示任何 UI 和提示。|
> |解除安裝|/uninstall|是|從伺服器中執行 Azure ATP 感應器的無訊息解除安裝。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|

**範例**：

以無訊息模式將 Azure ATP 感應器從伺服器解除安裝：

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](prerequisites.md)
- [安裝 Azure ATP 感應器](install-step4.md)
- [設定 Azure ATP 感應器](install-step5.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)