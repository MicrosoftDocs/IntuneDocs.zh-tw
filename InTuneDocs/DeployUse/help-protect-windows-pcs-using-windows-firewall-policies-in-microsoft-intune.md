---
# required metadata

title: Windows 電腦的防火牆原則 | Microsoft Intune
description:
keywords:
author: robstackmsft
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 9549c072-ac3d-4d14-a931-a2eda8846217

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 在 Microsoft Intune 中使用 Windows 防火牆原則協助保護 Windows 電腦
Microsoft Intune 使用一些方法來協助您保護使用 Intune 用戶端所管理的 Windows 電腦安全，其中包括使用可讓您在電腦上進行 Windows 防火牆設定的原則。

如果您尚未在電腦上安裝 Intune Windows 電腦用戶端，請參閱[使用 Microsoft Intune 安裝 Windows 電腦用戶端](install-the-windows-pc-client-with-microsoft-intune.md)

使用以下各節中的資訊可協助您設定、部署及監視 Windows 電腦上的 Windows 防火牆原則。

## 使用 Intune 原則管理 Windows 防火牆
Windows 防火牆原則可讓您建立及部署在受管理電腦上控制 Windows 防火牆的設定。 您不能管理 Windows 防火牆的自訂例外，且這些設定不會影響協力廠商防火牆。

> [!NOTE]
> 如果設定以 Microsoft Intune 原則及群組原則管理同一台電腦的相同設定，群組原則設定會覆寫 Microsoft Intune 原則設定。 如需如何避免 Intune 原則與群組原則產生衝突的詳細資訊，請參閱[解決 GPO 和 Microsoft Intune 原則衝突](resolve-gpo-and-microsoft-intune-policy-conflicts.md)
>
> 如果您想要將 Windows 防火牆設定部署到執行 Windows Vista 的電腦，則必須先在這些電腦上安裝 [Hotfix KB971800](http://support2.microsoft.com/kb/971800) 。

> 若要使用 Intune 管理 Windows 防火牆，您要管理的電腦上必須啟用下列兩項服務：
>
> -   Windows 防火牆
> -   IPsec 原則代理

## 設定 Windows 防火牆原則

1.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [原則] &gt; [新增原則]

2.  設定並部署 Windows 防火牆設定 原則。 您可以使用建議的設定或自訂設定。 如需如何建立和部署原則的詳細資訊，請參閱[使用 Microsoft Intune 電腦用戶端的一般 Windows 電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)

    下節列出您可以在原則中設定的值，以及在不自訂原則的情況下將使用的預設值。

部署 Windows 防火牆原則之後，即可在 [原則] 工作區的 [所有原則] 頁面上檢視其狀態。

## Windows 防火牆的原則設定

### 開啟 Windows 防火牆

這些原則設定可在連線到網域 (例如，在工作場所中)、私人 (信任) 網路 (例如家用網路) 或不受信任的公用網路 (例如咖啡廳) 的受管理電腦上啟用 Windows 防火牆。 所有這些設定的預設值都是 [是] (最安全的值)。 



### 阻擋所有連入連線，包括允許之程式清單中的連線

這些原則設定會設定在受管理電腦連線到網域 (例如，在工作場所中)、私人 (信任) 網路 (例如家用網路) 或不受信任的公用網路 (例如咖啡廳) 時，Windows 防火牆會封鎖連入網路流量。 所有這些設定的預設值都是 [是] (最安全的值)。 

> 如果您環境中所包含的受管理電腦，執行未安裝 Service Pack 的 Windows Vista ，則您必須安裝與 Microsoft 知識庫 [文章編號 971800](http://go.microsoft.com/fwlink/?LinkId=188405) 相關聯的更新，或者停用部署至那些電腦之原則中的 [阻擋所有連入連線]  原則設定。

### 當 Windows 防火牆阻擋新程式時通知使用者

這些原則設定會設定在受管理電腦連線到網域 (例如，在工作場所中)、私人 (信任) 網路 (例如家用網路) 或不受信任的公用網路 (例如咖啡廳) 時， Windows 防火牆是否通知電腦使用者。 所有這些設定的預設值都是 [是]。


### 預先定義的例外

設定上面的基本值之後，即可設定例外狀況，允許特定網路流量通過防火牆，而不管上面所設定的值為何。 根據預設，不會設定這些設定。

|設定名稱|詳細資料|
|------------------|--------------------|
|**BranchCache - 內容擷取**<br>(Windows 7 或更新版本)|可讓 BranchCache 用戶端使用 HTTP 在分散模式下互相擷取內容，並在託管快取模式下從託管快取擷取內容。 這項設定使用 HTTP。|
|**BranchCache - 託管快取用戶端**<br>(Windows 7 或更新版本)|可讓 BranchCache 用戶端使用託管快取。 這項設定使用 HTTPS。|
|**BranchCache - 託管快取伺服器**|可讓 BranchCache 用戶端使用託管快取與其他用戶端通訊。 這項設定使用 HTTPS。|
|**BranchCache - 同儕節點探索**<br>(Windows 7 或更新版本)|可讓 BranchCache 用戶端使用 WS 探索通訊協定，查詢本機子網路上的內容可用性。|
|**BITS 對等快取**|可讓用戶端使用背景智慧型傳送服務 (BITS)，在相同子網路中的用戶端上尋找及共用儲存在 BITS 快取的檔案。 這項設定使用 WSDAPI 和 RPC。|
|**連線到網路投影機**|可讓使用者透過有線或無線網路，連線到投影機來投影簡報。 這項設定使用 WSDAPI。|
|**核心網路功能**|可讓用戶端使用 IPv4 和 IPv6 連線到網路資源。|
|**分散式交易協調器**|可讓電腦協調更新受交易保護之資源 (例如資料庫、訊息佇列和檔案系統) 的交易。|
|**檔案及印表機共用**|可讓使用者與網路上的其他使用者共用本機檔案和印表機。 這項設定使用 NetBIOS、LLMNR、SMB 和 RPC。|
|**HomeGroup**<br>(Windows 7 或更新版本)|可讓受管理電腦加入 HomeGroup 網路。|
|**iSCSI 服務**|可讓受管理電腦連線到 iSCSI 伺服器和裝置。|
|**金鑰管理服務**|可讓您計算企業環境中電腦的授權相容。|
|**Media Center Extender**|可讓 Media Center Extender 與執行 Windows Media Center 的電腦通訊。 這項設定使用 SSDP 和 qWave。|
|**Netlogon 服務**|設定網域用戶端和網域控制站之間的安全性通道，以驗證使用者和服務。 這項設定使用 RPC。|
|**網路探索**|可讓電腦探索其他裝置，並被網路上的其他裝置探索。 這項設定使用功能探索裝載與發佈服務，以及 SSDP、NetBIOS、LLMNR 和 UPnP 網路通訊協定。|
|**效能記錄檔及警示**|可讓您從遠端管理效能記錄檔及警示服務。 這項設定使用 RPC。|
|**遠端系統管理**|可允許對電腦進行遠端系統管理。|
|**遠端協助**|可讓受管理電腦的使用者要求網路上的其他使用者提供遠端協助。 這項設定使用 SSDP、PNRP、Teredo 和 UPnP 網路通訊協定。|
|**遠端桌面**|可讓電腦使用遠端桌面來存取其他電腦。|
|**遠端事件記錄檔管理**|可讓您從遠端檢視及管理用戶端事件記錄檔。 這項設定使用具名管道和 RPC。|
|**遠端排程工作管理**|可允許對工作排定服務進行遠端管理。 這項設定使用 RPC。|
|**遠端服務管理**|可允許對用戶端上的本機服務進行遠端管理。 這項設定使用具名管道和 RPC。|
|**遠端磁碟區管理**|可允許進行遠端軟體和硬體磁碟區管理。 這項設定使用 RPC。|
|**路由及遠端存取**|可允許傳入 VPN 和遠端存取連線連到電腦。|
|**安全通訊端通道通訊協定**|可允許使用安全通訊端通道通訊協定 (SSTP) 連到受管理電腦的傳入 VPN 連線。 這項設定使用 HTTPS。|
|**SNMP 陷阱**|可讓受管理電腦接收 SNMP 陷阱服務流量。|
|**UPnP 架構**|在電腦上設定 UPnP 架構服務，讓電腦可探索並使用經過 UPnP 認證的裝置。|
|**Windows 共用檢視電腦名稱登錄服務**|可讓電腦透過對等名稱解析通訊協定尋找其他電腦並與之通訊。 這項設定使用 SSDP 和 PNRP。|
|**Windows Media Player**|可讓使用者透過 UDP 接收串流媒體。|
|**Windows Media Player 網路共用服務**|可讓使用者透過網路共用媒體。 這項設定使用 SSDP、qWave 和 UPnP 網路通訊協定。|
|**Windows Media Player 網路共用服務 (網際網路)**<br>(Windows 7 或更新版本)|可讓使用者透過網際網路共用家用媒體。|
|**Windows 會議空間**|可讓使用者透過網路執行協同作業，以共用文件、程式或其桌面。 這項設定使用 DFSR 和 P2P。|
|**Windows Peer to Peer Collaboration Foundation**|設定各種點對點程式和技術，以允許其連線。 這項設定使用 SSDP 和 PNRP。|
|**Windows 遠端管理 (相容性)**|可允許使用 WS-Management (Web 服務通訊協定，用於作業系統和裝置的遠端管理) 對受管理電腦進行遠端管理。|
|**Windows 遠端管理**<br>(Windows 8 或更新版本)|可允許使用 WS-Management (Web 服務通訊協定，用於作業系統和裝置的遠端管理) 對受管理電腦進行遠端管理。|
|**Windows Virtual PC**<br>(Windows 7 或更新版本)|可讓虛擬機器與其他電腦通訊。|
|**無線可攜式裝置**|可允許使用媒體傳輸通訊協定 (MTP)，將媒體從支援網路存取的相機或媒體裝置傳送到受管理電腦。 這項設定使用 SSDP 和 UPnP 網路通訊協定。|

### 請參閱
[保護 Windows 電腦的原則](policies-to-protect-windows-pcs-in-microsoft-intune.md)


<!--HONumber=May16_HO2-->

