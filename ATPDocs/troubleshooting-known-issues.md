---
title: 針對 Azure ATP 已知問題進行疑難排解
description: 描述如何針對 Azure ATP 的問題進行疑難排解。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/07/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4153df2c2811217fcff813b333bdaf13fbe46858
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828068"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>針對 Azure ATP 已知問題進行疑難排解

## <a name="sensor-failure-communication-error"></a>感應器失敗通訊錯誤

如果您收到以下感應器失敗錯誤：

System.Net.Http.HttpRequestException：傳送要求時發生錯誤。 ---> System.Net.WebException：無法連線至遠端伺服器 ---> System.Net.Sockets.SocketException：因為連線對象有一段時間並未正確回應，所以連線嘗試失敗；或是因為連線的主機無法回應，所以連線建立失敗...

**解決方法：**

請確保本機主機和 TCP 通訊埠 444 的通訊未受到封鎖。 若要深入了解 Azure ATP 必要條件，請參閱[連接埠](prerequisites.md#ports)。

## <a name="deployment-log-location"></a>部署記錄位置

針對安裝產品的使用者，Azure ATP 部署記錄位於 temp 目錄中。 在預設安裝位置中，其位於：C:\Users\Administrator\AppData\Local\Temp (或 %temp% 的上一層目錄)。 如需詳細資訊，請參閱[使用記錄檔針對 ATP 進行疑難排解](troubleshooting-using-logs.md)。

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxy 驗證問題顯示為授權錯誤

若您在感應器安裝期間收到下列錯誤：**感應器因授權問題而無法註冊**。

**部署記錄項目：**

[1C60:1AA8][2018-03-24T23:59:13]i000:2018-03-25 02:59:13.1237 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000:2018-03-25 02:59:56.4856 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000:2018-03-25 03:27:56.7399 針對 SensorBootstrapperApplication Engine.Quit 進行偵錯 [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500:正在關機，結束代碼:0x642

**原因：**

在某些情況下，透過 Proxy 進行通訊時，可能會在驗證期間以錯誤 401 或 403 回應 Azure ATP 感應器，而不是錯誤 407。 Azure ATP 感應器將錯誤 401 或 403 解譯為授權問題，而不是 Proxy 驗證問題。

**解決方法：**

請確定感應器可透過設定的 Proxy 瀏覽至 *.atp.azure.com，而無需進行驗證。 如需詳細資訊，請參閱[設定 Proxy 以進行通訊](configure-proxy.md)。

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Proxy 驗證問題顯示為連線錯誤

若您在感應器安裝期間收到下列錯誤：**感應器無法連線到服務。**

**原因：**

此問題可能是 Transparent Proxy 在伺服器核心上設定錯誤所導致，例如缺少 Azure ATP 所需的根憑證或根憑證不是最新版本。

**解決方法：**

執行下列 PowerShell Cmdlet，以確認伺服器核心上有 Azure ATP 服務受信任的根憑證存在。 以下範例使用 "DigiCert Baltimore Root" 與 "DigiCert Global Root"。

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"} | fl
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "df3c24f9bfd666761b268073fe06d1cc8d4f82a4"} | fl
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : DF3C24F9BFD666761B268073FE06D1CC8D4F82A4
FriendlyName : DigiCert Global Root G2
NotBefore    : 01/08/2013 15:00:00
NotAfter     : 15/01/2038 14:00:00
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

如果您沒有看到預期的輸出結果，請使用下列步驟：

1. 將 [Baltimore CyberTrust 根憑證](https://cacert.omniroot.com/bc2025.crt)與 [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) 下載到伺服器核心機器。
1. 執行下列 PowerShell Cmdlet 以安裝憑證。

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root
    ```

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>嘗試使用 Powershell 時發生的無訊息安裝錯誤

若您嘗試在無訊息感應器安裝期間使用 Powershell 並收到下列錯誤：

```powershell
"Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."
```

**原因：**

使用 Powershell 時無法包括安裝所需的 ./ 前置詞會導致此錯誤。

**解決方法：**

使用完整命令來成功安裝。

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Azure ATP 感應器 NIC 小組問題 <a name="nic-teaming"></a>

如果您嘗試在具備 NIC 小組介面卡的電腦上安裝 ATP 感應器，您將會接收到安裝錯誤。 如果您想要在使用 NIC 小組設定的電腦上安裝 ATP 感應器，請遵循這些指示：

1. 從 [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-0.9984.exe) 下載  Npcap 0.9984 版安裝程式。
    - 或者，向支援小組要求 Npcap 驅動程式 (支援無訊息安裝) 的 OEM 版本。
    - 如果 Npcap 的複本僅搭配 Azure ATP 安裝並使用，則不會計入五個複本、五部電腦或五個使用者授權的限制。 如需詳細資訊，請參閱 [NPCAP 授權](https://github.com/nmap/npcap/blob/master/LICENSE) \(英文\)。

如果您尚未在電腦上安裝感應器：

1. 如果您已安裝 WinPcap，請將它解除安裝。
1. 使用下列選項安裝 Npcap：loopback_support=no & winpcap_mode=yes。
    - 如果是使用 GUI 安裝程式，請取消選取 [回送支援]  並選取 [WinPcap]  模式。
1. 安裝感應器套件。

如果您已安裝感應器：

1. 將感應器解除安裝。
1. 將 WinPcap 解除安裝。
1. 使用下列選項安裝 Npcap：loopback_support=no & winpcap_mode=yes
    - 如果是使用 GUI 安裝程式，請取消選取 [回送支援]  並選取 [WinPcap]  模式。
1. 重新安裝感應器套件。

## <a name="multi-processor-group-mode"></a>多處理器群組模式

針對 Windows 作業系統 2008 R2 與 2012，多處理器群組模式中不支援 Azure ATP 感應器。

建議的可能因應措施：

- 如果超執行緒已開啟，請將它關閉。 這可能會減少足夠的邏輯核心數目，以避免需要在**多處理器群組**模式中執行。

- 如果您的電腦具有少於 64 個邏輯核心，而且是在 HP 主機上執行，您可以將 [NUMA 群組大小最佳化]  BIOS 設定從預設的[叢集]  變更為 [一般]  。

## <a name="microsoft-defender-atp-integration-issue"></a>Microsoft Defender ATP 整合問題

Azure 進階威脅防護可讓您將 Azure ATP 與 Microsoft Defender ATP 整合。 如需詳細資訊，請參閱[整合 Azure ATP 與 Microsoft Defender ATP](integrate-msde.md)。

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware 虛擬機器感應器問題

如果您在 VMware 虛擬機器上有 Azure ATP 感應器，則可能會收到健康情況警示「某些網路流量不會被分析」  。 當 VMware 中的設定不相符時，就可能會發生此狀況。

若要解決問題：

在虛擬機器的 NIC 設定中，將下列項目設定為 [已停用]  ：**IPv4 TSO 卸載**。

 ![VMware 感應器問題](media/vm-sensor-issue.png)

使用下列命令來檢查已啟用或停用大型傳送卸載 (LSO)：

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![檢查 LSO 狀態](media/missing-network-traffic-health-alert.png)

若已啟用 LSO，請使用下列命令來停用它：

`Disable-NetAdapterLso -Name {name of adapter}`

![停用 LSO 狀態](media/disable-lso-vmware.png)

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>感應器無法擷取群組受管理的服務帳戶 (gMSA) 認證

如果您收到下列健康情況警示：**目錄服務使用者認證不正確**

**感應器記錄項目：**

2020-02-17 14:01:36.5315 已啟動 ImpersonationManager CreateImpersonatorAsync 資訊 [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 已完成 ImpersonationManager CreateImpersonatorAsync 資訊 [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**感應器更新程式記錄項目：**

2020-02-17 14:02:19.6258 警告 無法擷取 GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA 密碼 [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**原因：**

感應器無法從 Azure ATP 入口網站擷取指定的 gMSA 帳戶。

**解決方法：**

請確定 gMSA 帳戶的認證正確，且感應器已獲授權可擷取帳戶的認證。 在已套用的原則中，您可能需要將 gMSA 帳戶新增至 **「以服務方式登入」** 使用者權利指派。

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>報表下載無法包含超過 300,000 個項目

Azure ATP 不支援下載每個報表包含超過 300,000 個項目的報表。 若報表包含的項目超過 300,000 個，報表會呈現為未完成。

**原因：**

這是工程限制。

**解決方法：**

沒有任何已知的解決方式。

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](prerequisites.md)
- [Azure ATP 容量規劃](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
