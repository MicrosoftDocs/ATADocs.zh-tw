---
title: 在 Advanced 威脅分析中驗證埠鏡像
description: 描述如何驗證已正確設定連接埠鏡像
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 78f8f287721af62e2d7992b48ebb5f91421cd571
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956307"
---
# <a name="validate-port-mirroring"></a>驗證連接埠鏡像

*適用於：Advanced Threat Analytics 1.9 版*

> [!NOTE]
> 本文只有在部署 ATA 閘道 (而非 ATA 輕量型閘道) 時才適用。 若要判斷是否需要使用 ATA 閘道，請參閱[為您的部署選擇正確閘道](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment)。

下列步驟會引導您逐步完成驗證已正確設定連接埠鏡像的程序。 若要讓 ATA 正常運作，ATA 閘道必須能夠看到網域控制站之間的流量。 ATA 使用的主要資料來源是對進出網域控制站的網路流量的深度封包檢查。 若要讓 ATA 查看網路流量，必須設定連接埠鏡像。 連接埠鏡像會將流量從一個連接埠 (來源連接埠) 複製到另一個連接埠 (目的地連接埠)。

## <a name="validate-port-mirroring-using-a-windows-powershell-script"></a>使用 Windows PowerShell 指令碼驗證連接埠鏡像

1. 將此指令碼的文字儲存為名為 *ATAdiag.ps1* 的檔案。
1. 在您想要驗證的 ATA 閘道上執行這個指令碼。
此指令碼會產生從 ATA 閘道到網域控制站的 ICMP 流量，並在網域控制站上的擷取 NIC 尋找該流量。
如果 ATA 閘道發現 ICMP 流量的目的地 IP 位址，與您在 ATA 主控台中輸入的 DC IP 位址相同，則會將連接埠鏡像視為已設定。

如何執行此指令碼的範例：

```powershell
# ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

# Set variables
$ErrorActionPreference = "stop"
$starttime = get-date
$byteIn = new-object byte[] 4
$byteOut = new-object byte[] 4
$byteData = new-object byte[] 4096  # size of data

$byteIn[0] = 1  # for promiscuous mode
$byteIn[1-3] = 0
$byteOut[0-3] = 0

# Convert network data to host format
function NetworkToHostUInt16 ($value)
{
    [Array]::Reverse($value)
    [BitConverter]::ToUInt16($value,0)
}
function NetworkToHostUInt32 ($value)
{
    [Array]::Reverse($value)
    [BitConverter]::ToUInt32($value,0)
}
function ByteToString ($value)
{
    $AsciiEncoding = new-object system.text.asciiencoding
    $AsciiEncoding.GetString($value)
}

Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
Write-Host ""
Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

# Initialize a first ping connection
Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
Write-Host ""
Write-Host "Press any key to continue..." -ForegroundColor Red
[void][System.Console]::ReadKey($true)
Write-Host ""
Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow

# Open a socket
$socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)

# Include the IP header
$socket.setsocketoption("IP","HeaderIncluded",$true)
$socket.ReceiveBufferSize = 10000
$ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
$socket.bind($ipendpoint)

# Enable promiscuous mode
[void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)

# Initialize test variables
$tests = 0
$TestResult = "Noise"
$OneSuccess = 0

while ($tests -le $PingCount)
{
    if (!$socket.Available)  # see if any packets are in the queue
    {
        start-sleep -milliseconds 500
        continue
    }

    # Capture traffic
    $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)

    # Decode the header so we can read ICMP
    $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
    $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)

    # Set IP version & header length
    $VersionAndHeaderLength = $BinaryReader.ReadByte()

    # TOS
    $TypeOfService= $BinaryReader.ReadByte()

    # More values, and the Protocol Number for ICMP traffic
    # Convert network format of big-endian to host format of little-endian
    $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $TTL = $BinaryReader.ReadByte()
    $ProtocolNumber = $BinaryReader.ReadByte()
    $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())

    # The source and destination IP addresses
    $SourceIPAddress = $BinaryReader.ReadUInt32()
    $DestinationIPAddress = $BinaryReader.ReadUInt32()

    # The source and destimation ports
    $sourcePort = [uint16]0
    $destPort = [uint16]0

    # Close the stream reader
    $BinaryReader.Close()
    $memorystream.Close()

    # Cast DCIP into an IPaddress type
    $DCIPP = [ipaddress] $DCIP
    $DestinationIPAddressP = [ipaddress] $DestinationIPAddress

    #Ping the DC at the end after starting the capture
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null

    # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console
    # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured

    if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP?
    {
        $TestResult = "Port Spanning success!"
        $OneSuccess = 1
    } else {
        $TestResult = "Noise"
    }

    # Put source, destination, test result in Powershell object
    new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
    #Count tests
    $tests ++
}

if ($OneSuccess -eq 1)
{
    Write-Host "Port Spanning Success!" -ForegroundColor Green
    Write-Host ""
    Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
    Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
} else {
    Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
}

Write-Host ""
Write-Host "Press any key to continue..." -ForegroundColor Red
[void][System.Console]::ReadKey($true)
```

## <a name="validate-port-mirroring-using-net-mon"></a>使用 Net Mon 驗證連接埠鏡像
1. 在您想要驗證的 ATA 閘道上安裝 [Microsoft 網路監視器 3.4](https://www.microsoft.com/download/details.aspx?id=4865) 。

    > [!IMPORTANT]
    > 請勿在 ATA 閘道上安裝 Microsoft Message Analyzer 或其他流量擷取軟體。

1. 開啟網路監視器並建立新的 [擷取] 索引標籤。

    1. 只選取 [擷取]  網路介面卡或連接到設定為連接埠鏡像目的地的交換器連接埠之網路介面卡。

    1. 確定已啟用 P-Mode

    1. 按一下 [新增擷取]  。

        ![建立新的擷取索引標籤影像](media/ATA-Port-Mirroring-Capture.jpg)

1. 在 [顯示篩選器] 視窗中，輸入下列篩選：**KerberosV5 OR LDAP**，然後按一下 [套用]  。

    ![套用 KerberosV5 或 LDAP 篩選影像](media/ATA-Port-Mirroring-filter-settings.jpg)

1. 按一下 [啟動]  ，啟動擷取工作階段。 如果您看不到網域控制站之間的流量，請檢閱您的連接埠鏡像組態。

    ![啟動擷取工作階段影像](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > 請務必確定您可以看到網域控制站之間的流量。

1. 如果您只看到一個方向的流量，您應該和網路或虛擬化小組合作，以協助疑難排解您的連接埠鏡像組態。

## <a name="see-also"></a>另請參閱

- [設定連接埠鏡像](configure-port-mirroring.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
