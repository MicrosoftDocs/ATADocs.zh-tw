---
title: 針對身分識別已知問題進行 Microsoft Defender 疑難排解
description: 說明如何針對身分識別的 Microsoft Defender 問題進行疑難排解。
ms.date: 02/04/2021
ms.topic: how-to
ms.openlocfilehash: be4aebf4ccbccece1348949cbe0acd19d803e163
ms.sourcegitcommit: 412420dd904690d855539a2589f9d5485e1f832e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/17/2021
ms.locfileid: "100569839"
---
# <a name="troubleshooting-microsoft-defender-for-identity-known-issues"></a>針對身分識別已知問題進行 Microsoft Defender 疑難排解

## <a name="sensor-failure-communication-error"></a>感應器失敗通訊錯誤

如果您收到以下感應器失敗錯誤：

System.Net.Http.HttpRequestException：傳送要求時發生錯誤。 ---> System.Net.WebException：無法連線至遠端伺服器 ---> System.Net.Sockets.SocketException：因為連線對象有一段時間並未正確回應，所以連線嘗試失敗；或是因為連線的主機無法回應，所以連線建立失敗...

**解決方法：**

請確保本機主機和 TCP 通訊埠 444 的通訊未受到封鎖。 若要深入瞭解 [!INCLUDE [Product long](includes/product-long.md)] 必要條件，請參閱 [埠](prerequisites.md#ports)。

## <a name="deployment-log-location"></a>部署記錄位置

[!INCLUDE [Product short](includes/product-short.md)]部署記錄檔位於安裝產品之使用者的臨時目錄中。 在預設安裝位置中，其位於：C:\Users\Administrator\AppData\Local\Temp (或 %temp% 的上一層目錄)。 如需詳細資訊，請參閱 [ [!INCLUDE [Product short](includes/product-short.md)] 使用記錄進行疑難排解](troubleshooting-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Proxy 驗證問題顯示為授權錯誤

若您在感應器安裝期間收到下列錯誤：**感應器因授權問題而無法註冊**。

**部署記錄項目：**

[1C60:1AA8][2018-03-24T23:59:13]i000:2018-03-25 02:59:13.1237 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000:2018-03-25 02:59:56.4856 已傳回 InteractiveDeploymentManager ValidateCreateSensorAsync 資訊 [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000:2018-03-25 03:27:56.7399 針對 SensorBootstrapperApplication Engine.Quit 進行偵錯 [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500:正在關機，結束代碼:0x642

**原因：**

在某些情況下，透過 proxy 進行通訊時，它可能會回應 [!INCLUDE [Product short](includes/product-short.md)] 感應器的錯誤401或403，而不是錯誤407。 [!INCLUDE [Product short](includes/product-short.md)]感應器會將錯誤401或403解釋為授權問題，而不是 proxy 驗證問題。

**解決方法：**

請確定感應器可透過設定的 Proxy 瀏覽至 *.atp.azure.com，而無需進行驗證。 如需詳細資訊，請參閱[設定 Proxy 以進行通訊](configure-proxy.md)。

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Proxy 驗證問題顯示為連線錯誤

若您在感應器安裝期間收到下列錯誤：**感應器無法連線到服務。**

**原因：**

問題可能是伺服器核心上的透明 proxy 設定錯誤所造成，例如所需的根憑證 [!INCLUDE [Product short](includes/product-short.md)] 不是目前或遺失。

**解決方法：**

執行下列 PowerShell Cmdlet，以確認 [!INCLUDE [Product short](includes/product-short.md)] 伺服器核心上存在服務受信任的根憑證。

在下列範例中，請針對所有客戶使用 "DigiCert 巴爾的摩 Root" 憑證。 此外，針對商業客戶使用「DigiCert 全域根目錄 G2」憑證，或針對美國政府 GCC High 客戶使用「DigiCert 全域根 CA」憑證（如指示）。

```powershell
# Certificate for all customers
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"} | fl

# Certificate for commercial customers
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "df3c24f9bfd666761b268073fe06d1cc8d4f82a4"} | fl

# Certificate for US Government GCC High customers
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "a8985d3a65e5e5c4b2d7d66d40c6dd2fb19c5436"} | fl
```

所有客戶的憑證輸出：

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

商業客戶的憑證輸出憑證：

```Output
Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : DF3C24F9BFD666761B268073FE06D1CC8D4F82A4
FriendlyName : DigiCert Global Root G2
NotBefore    : 01/08/2013 15:00:00
NotAfter     : 15/01/2038 14:00:00
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

美國政府的憑證輸出 GCC High 客戶：

```Output
Subject      : CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : A8985D3A65E5E5C4B2D7D66D40C6DD2FB19C5436
FriendlyName : DigiCert
NotBefore    : 11/9/2006 4:00:00 PM
NotAfter     : 11/9/2031 4:00:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

如果您沒有看到預期的輸出結果，請使用下列步驟：

1. 將下列憑證下載到 Server Core 電腦。 針對所有客戶，下載 [巴爾的摩 CyberTrust 跟](https://cacert.omniroot.com/bc2025.crt) 證書。

    此外：

    - 針對商業客戶，下載 [DigiCert Global 根目錄 G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) 憑證
    - 針對美國政府 GCC High 客戶，下載 [DigiCert Global 根 CA](https://cacerts.digicert.com/DigiCertGlobalRootCA.crt) 憑證

1. 執行下列 PowerShell Cmdlet 以安裝憑證。

    ```powershell
    # For all customers, install certificate
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root

    # For commercial customers, install certificate
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root

    # For US Government GCC High customers, install certificate
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootCA.crt" -CertStoreLocation Cert:\LocalMachine\Root
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

<a name="nic-teaming"></a>

## <a name="defender-for-identity-sensor-nic-teaming-issue"></a>適用于身分識別感應器 NIC 小組問題的 Defender

如果您嘗試在設定了 [!INCLUDE [Product short](includes/product-short.md)] NIC 小組介面卡的電腦上安裝感應器，則會收到安裝錯誤。 如果您想要 [!INCLUDE [Product short](includes/product-short.md)] 在使用 NIC 小組設定的電腦上安裝感應器，請遵循下列指示：

1. 從下載 Npcap 1.0 版安裝程式  [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-1.00.exe) 。
    - 或者，向支援小組要求 Npcap 驅動程式 (支援無訊息安裝) 的 OEM 版本。
    - Npcap 的複本不會計入五個複本、五部電腦或五個使用者授許可權制（如果其已安裝且單獨搭配使用） [!INCLUDE [Product short](includes/product-short.md)] 。 如需詳細資訊，請參閱 [NPCAP 授權](https://github.com/nmap/npcap/blob/master/LICENSE) \(英文\)。

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

針對 Windows 作業系統 2008 R2 與 2012，多處理器群組模式中不支援 [!INCLUDE [Product short](includes/product-short.md)] 感應器。

建議的可能因應措施：

- 如果超執行緒已開啟，請將它關閉。 這可能會減少足夠的邏輯核心數目，以避免需要在 **多處理器群組** 模式中執行。

- 如果您的電腦具有少於 64 個邏輯核心，而且是在 HP 主機上執行，您可以將 [NUMA 群組大小最佳化]  BIOS 設定從預設的[叢集]  變更為 [一般]  。

## <a name="microsoft-defender-for-endpoint-integration-issue"></a>Microsoft Defender 的端點整合問題

[!INCLUDE [Product short](includes/product-short.md)] 可讓您 [!INCLUDE [Product short](includes/product-short.md)] 與 Microsoft Defender For Endpoint 整合。 如需詳細資訊，請參閱 [ [!INCLUDE [Product short](includes/product-short.md)] 與 Microsoft Defender For Endpoint 整合](integrate-mde.md) 。

## <a name="vmware-virtual-machine-sensor-issue"></a>VMware 虛擬機器感應器問題

如果您 [!INCLUDE [Product short](includes/product-short.md)] 在 VMware 虛擬機器上有感應器，您可能會收到健康情況警示， **表示某些網路流量未進行分析**。 當 VMware 中的設定不相符時，就可能會發生此狀況。

若要解決問題：

在虛擬機器的 NIC 設定中，將下列內容設定為 [ **停用** ]： [ **IPv4 TSO** 卸載]。

![VMware 感應器問題](media/vm-sensor-issue.png)

使用下列命令來檢查已啟用或停用大型傳送卸載 (LSO)：

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![檢查 LSO 狀態](media/missing-network-traffic-health-alert.png)

若已啟用 LSO，請使用下列命令來停用它：

`Disable-NetAdapterLso -Name {name of adapter}`

![停用 LSO 狀態](media/disable-lso-vmware.png)

> [!NOTE]
>
> - 您可能需要重新開機電腦，這些變更才會生效。
> - 這些步驟會根據您的 VMWare 版本而有所不同。 如需有關如何針對您的 VMWare 版本停用 LSO/TSO 的詳細資訊，請參閱 VMWare 檔。

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>感應器無法擷取群組受管理的服務帳戶 (gMSA) 認證

如果您收到下列健康情況警示：**目錄服務使用者認證不正確**

**感應器記錄項目：**

2020-02-17 14:01:36.5315 已啟動 ImpersonationManager CreateImpersonatorAsync 資訊 [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 已完成 ImpersonationManager CreateImpersonatorAsync 資訊 [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**感應器更新程式記錄項目：**

2020-02-17 14:02:19.6258 警告 無法擷取 GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA 密碼 [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**原因：**

感應器無法從入口網站取出指定的 gMSA 帳戶 [!INCLUDE [Product short](includes/product-short.md)] 。

**解決方法：**

請確定 gMSA 帳戶的認證正確，且感應器已獲授權可擷取帳戶的認證。 雖然不 [!INCLUDE [Product short](includes/product-short.md)]  需要 gMSA 帳戶的 [ **以服務方式登** 入] 許可權，但此問題通常是藉由將許可權新增至帳戶來解決。

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>報表下載無法包含超過 300,000 個項目

[!INCLUDE [Product short](includes/product-short.md)] 不支援每份報表包含300000個以上專案的報表下載。 若報表包含的項目超過 300,000 個，報表會呈現為未完成。

**原因：**

這是工程限制。

**解決方法：**

沒有任何已知的解決方式。

## <a name="sensor-fails-to-enumerate-event-logs"></a>感應器無法列舉事件記錄檔

如果您在主控台中看到有限的數目或缺少安全性事件警示或邏輯活動， [!INCLUDE [Product short](includes/product-short.md)] 但未觸發健康情況警示。 

**感應器記錄項目：**

EventLogException EventLogException：：控制碼在 void EventLogException 時無效。. 擲回 (int errorCode) 的物件系統上。 NativeWrapper. EvtGetEventInfo (EventLogHandle 控制碼，EvtEventPropertyId enumType) ，于字串 System.Diagnostics.Eventing.Reader.EventLogRecord.get_ContainerLog 中 () 

**原因：**

任意存取控制清單會限制本地服務帳戶存取所需的事件記錄檔。

**解決方法：**

確定任意存取控制清單包含下列專案：

`(A;;0x1;;;S-1-5-80-818380073-2995186456-1411405591-3990468014-3617507088)`

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
