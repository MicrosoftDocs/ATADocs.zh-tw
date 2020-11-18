---
title: 以無訊息方式安裝 Microsoft Defender 身分識別
description: 這會說明如何以無訊息方式安裝 Microsoft Defender for Identity。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d87aa443bad2731ee3e5ff226930980ac52c79d7
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846709"
---
# <a name="product-long-switches-and-silent-installation"></a>[!INCLUDE [Product long](includes/product-long.md)] 切換和無訊息安裝

本文提供 [!INCLUDE [Product long](includes/product-long.md)] 切換開關和無訊息安裝的指導方針和指示。

## <a name="prerequisites"></a>先決條件

[!INCLUDE [Product short](includes/product-short.md)] 需要安裝 Microsoft .NET Framework 4.7 或更新版本。

當您安裝時 [!INCLUDE [Product short](includes/product-short.md)] ， [!INCLUDE [Product short](includes/product-short.md)] 如果尚未安裝 .net framework 4.7 或更新版本，則 .net framework 4.7 會自動安裝為部署的一部分。

> [!NOTE]
> .Net Framework 4.7 的安裝可能需要重新啟動伺服器。 在 [!INCLUDE [Product short](includes/product-short.md)] 網域控制站上安裝感應器時，請考慮為網域控制站排程維護時段。

使用 [!INCLUDE [Product short](includes/product-short.md)] 無訊息安裝時，安裝程式會設定為在安裝 (結束時自動重新開機伺服器（如有必要）) 。 請務必只在維護時段執行無訊息安裝。 因為 Windows Installer 的某個錯誤 (Bug)，*norestart* 旗標無法可靠地用來確定伺服器不會重新啟動。

若要追蹤您的部署進度，請監視 [!INCLUDE [Product short](includes/product-short.md)] 位於中的安裝程式記錄檔 `%AppData%\Local\Temp` 。

## <a name="product-short-sensor-silent-installation"></a>[!INCLUDE [Product short](includes/product-short.md)] 感應器無訊息安裝

> [!NOTE]
> 透過 [!INCLUDE [Product short](includes/product-short.md)] System Center Configuration Manager 或其他軟體部署系統以無訊息方式部署感應器時，建議您建立兩個部署套件：</br>- Net Framework 4.7 或更新版本 (可能需要重新啟動網域控制站)</br>- [!INCLUDE [Product short](includes/product-short.md)] 感應器。 </br>讓 [!INCLUDE [Product short](includes/product-short.md)] 感應器套件相依于 .Net Framework 套件部署的部署。 </br>取得 [.Net Framework 4.7 離線部署套件](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows)。

使用下列命令來執行感應器的完全無訊息安裝 [!INCLUDE [Product short](includes/product-short.md)] ：

**cmd.exe syntax**：

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**Powershell 語法**：

```powershell
.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> 使用 Powershell 語法時，省略 **./** 前置詞會導致發生防止無訊息安裝的錯誤。

> [!NOTE]
> 從 [!INCLUDE [Product short](includes/product-short.md)] 入口網站設定區段 [**感應器**] 頁面複製存取金鑰。 **Configuration**

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
> |InstallationPath|InstallationPath=""|否|設定感應器二進位檔安裝的路徑 [!INCLUDE [Product short](includes/product-short.md)] 。 預設路徑：%programfiles%\Azure Advanced Threat Protection sensor
> |AccessKey|AccessKey="\*\*"|是|設定用來向實例註冊感應器的存取金鑰 [!INCLUDE [Product short](includes/product-short.md)] [!INCLUDE [Product short](includes/product-short.md)] 。|

**範例**：

使用下列命令以無訊息模式安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器：

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
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|否|為[!INCLUDE [Product short](includes/product-short.md)] 感應器指定 ProxyUrl 與連接埠號碼。|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|否|如果您的 Proxy 服務需要驗證，請以 DOMAIN\user 格式提供使用者名稱。|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|否|指定 Proxy 使用者名稱的密碼。 \* 認證會經過加密，並由[!INCLUDE [Product short](includes/product-short.md)] 感應器儲存在本機。|

## <a name="update-the-product-short-sensor"></a>更新 [!INCLUDE [Product short](includes/product-short.md)] 感應器

使用下列命令以無訊息方式更新 [!INCLUDE [Product short](includes/product-short.md)] 感應器：

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

若要以無訊息方式更新 [!INCLUDE [Product short](includes/product-short.md)] 感應器：

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-product-short-sensor-silently"></a>以無訊息方式卸載 [!INCLUDE [Product short](includes/product-short.md)] 感應器

使用下列命令來執行感應器的無訊息卸載 [!INCLUDE [Product short](includes/product-short.md)] ：

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
> |解除安裝|/uninstall|是|從伺服器執行無訊息的 [!INCLUDE [Product short](includes/product-short.md)] 感應器卸載。|
> |[說明]|/help|否|提供說明和快速參考。 顯示安裝程式命令的正確用法，包括所有選項和行為清單。|

**範例**：

若要從伺服器以無訊息方式卸載 [!INCLUDE [Product short](includes/product-short.md)] 感應器：

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器](install-step4.md)
- [設定 [!INCLUDE [Product short](includes/product-short.md)] 感應器](install-step5.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
