---
title: "使用用戶端軟體管理電腦"
description: "安裝 Intune 用戶端軟體管理 Windows 電腦。"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 03/28/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 3b8d22fe-c318-4796-b760-44f1ccf34312
ms.reviewer: owenyen
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: e217648c744d76d4cde6b8927137cd569b8d0a2e
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2017
---
# <a name="manage-windows-pcs-as-computers-via-intune-software-client"></a>透過 Intune 軟體用戶端將 Windows 電腦做為電腦管理

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Intune 為管理行動裝置的組織提供全面的解決方案。 Intune 可以使用 Windows 10 作業系統內建的現代裝置管理功能，將 Windows 電腦做為行動裝置管理。 為了符合貴組織的管理需求，Intune 也可以使用 Intune 軟體用戶端將 Windows 電腦做為電腦管理。 此管理方法使用舊版 Windows 作業系統中的傳統電腦管理功能。

Intune 軟體用戶端最適合執行舊版作業系統 (例如無法做為行動裝置管理的 Windows 7) 的 Windows 電腦。 Intune 軟體用戶端使用群組原則之類的管理功能從雲端管理電腦。

Intune 使用軟體用戶端最多可支援將 7,000 部 Windows 電腦做為電腦管理。 如果是更大型的部署，可將 Windows 10 電腦做為行動裝置管理。 每個 Intune 版本和 Windows 10 更新都包含以行動裝置管理架構為基礎的管理功能。 我們強烈建議您讓組織移至可做為行動裝置管理的 Windows 10。


> [!NOTE]
> 您可以使用 Intune 用戶端軟體將 Windows 8.1 或更新版本的裝置做為電腦管理，或做為行動裝置管理。 您無法對同一個裝置同時使用這兩種方法。 決定使用 Intune 用戶端軟體管理電腦之前請謹慎考慮。 本主題僅適用於執行 Intune 用戶端軟體來管理電腦電腦。

## <a name="requirements-for-intune-pc-client-management"></a>Intune 電腦用戶端管理的需求

**硬體：**以下列出安裝 Intune 用戶端軟體的最低硬體需求：

|需求|詳細資訊|
|---------------|--------------------|
|網路|用戶端要求電腦必須具有網際網路連線。|
|處理器和記憶體|請參考電腦作業系統的處理器和 RAM 需求。|
|磁碟空間|安裝用戶端軟體之前需有 200 MB 的可用磁碟空間。|

**軟體**：下列是安裝用戶端軟體的軟體需求：

|需求|詳細資訊|
|---------------|--------------------|
|作業系統 | 執行 Windows Vista 或更新版本的 Windows 裝置。 </br></br>**不支援家用版本。**|
|系統管理權限|安裝用戶端軟體的帳戶必須擁有該裝置的本機系統管理員權限。|
|Windows Installer 3.1|電腦至少必須有 Windows Installer 3.1。<br /><br />若要檢視電腦上的 Windows Installer 版本：<br /><br />  在電腦上，以滑鼠右鍵按一下 **%windir%\System32\msiexec.exe**，然後按一下 [內容]。<br /><br />您可以從 Microsoft Developer Network (MSDN) 網站上的 [Windows Installer Redistributables (Windows Installer 可轉散發套件)](http://go.microsoft.com/fwlink/?LinkID=234258) 下載最新版的 Windows Installer。|
|移除不相容的用戶端軟體|安裝 Intune 用戶端軟體之前，請從該電腦解除安裝任何 Configuration Manager、Operations Manager、Operations Management Suite 和 Service Manager 用戶端軟體。|

## <a name="deploying-the-intune-software-client"></a>部署 Intune 軟體用戶端
身為 Intune 系統管理員，您可以使用各種方式，讓使用者能夠使用 Intune 軟體用戶端。 如需指引，請參閱[在 Windows 電腦上安裝 Intune 軟體用戶端](install-the-windows-pc-client-with-microsoft-intune.md)。

## <a name="computer-management-capabilities-with-the-intune-client-software"></a>Intune 用戶端軟體的電腦管理功能
在大部分情況下，您將使用 Microsoft Intune 註冊您的裝置，這可以提供更多的功能。 不過，您也可以使用提供下列功能的 Intune 軟體用戶端來管理電腦︰

-   **[軟體更新管理](/intune-classic/deploy-use/keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune)** - 您可以讓電腦保持在最新狀態，並決定套用更新的時間。

-   **[Windows 防火牆原則](/intune-classic/deploy-use/help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune)** - 這有助於確保在公司中使用的電腦沒有處於非作用中狀態或設定不當的 Windows 防火牆。

-   **[反惡意程式碼防護](/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)** - Intune 包含 Endpoint Protection，可協助您的電腦防範惡意程式碼。

-   **[遠端協助](/intune-classic/deploy-use/common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client#request-and-provide-remote-assistance-to-windows-pcs-that-use-the-intune-client-software )** - Intune 可讓使用者連絡 IT 支援人員，該人員接著可以藉由使用 Intune 隨附的遠端桌面功能提供協助 (需要 TeamViewer 軟體)。

-   **[軟體授權管理](/intune-classic/deploy-use/manage-license-agreements-for-windows-pc-software-in-microsoft-intune)** - 追蹤軟體有多少可用的授權數目，並且追蹤正在使用多少可用的授權。
-   **[應用程式部署](/intune-classic/deploy-use/add-apps-for-windows-pcs-in-microsoft-intune)** - 將軟體部署到您所管理的電腦。 當您使用軟體用戶端管理電腦時，某些應用程式管理功能會無法使用。

<!-- - **Compliance settings reporting** -->

## <a name="policies-and-app-deployments-for-the-intune-software-client"></a>Intune 軟體用戶端的原則和應用程式部署

雖然 Intune 用戶端軟體透過管理軟體更新、Windows 防火牆和 Endpoint Protection 支援[協助保護電腦的管理功能](policies-to-protect-windows-pcs-in-microsoft-intune.md)，但使用 Intune 用戶端軟體管理的電腦無法作為其他 Intune 原則的目標，包括那些專用於行動裝置管理的 **Windows** 原則設定。

當您使用 Intune 用戶端軟體管理 Windows 電腦時，可以只使用 [電腦管理] 區段下的原則。

Intune 使用原則來管理 Windows 電腦，其管理方式類似 Windows Server Active Directory 網域服務 (AD DS) 群組原則物件 (GPO)。 如果您使用 Intune 管理已加入 Active Directory 網域的電腦，請[確定 Intune 原則不會與組織中其他 GPO 衝突](/intune-classic/deploy-use/resolve-gpo-and-microsoft-intune-policy-conflicts)。 若要深入了解，請參閱[適用於新手的群組原則](https://technet.microsoft.com/library/hh147307.aspx)。

  ![為新的 Windows 電腦原則選取範本](../media/select-template-for-pc-policy.png)

部署應用程式時，可以只使用 Windows Installer (.exe、.msi)。

  ![選取用戶端軟體檔案的平台及位置](../media/select-platform-of-software-files-for-pc-agent.png)

## <a name="common-tasks-for-windows-pcs"></a>Windows 電腦的一般工作

您可以使用 Intune 系統管理主控台在安裝此用戶端的 Windows 電腦上，執行其他一般電腦管理工作︰
- [使用原則簡化電腦管理](use-policies-to-simplify-windows-pc-management.md)：描述 Intune 的「電腦管理」原則，並列出 Microsoft Intune Center 的設定。

- [檢視 Windows 電腦的硬體與軟體清查](view-hardware-and-software-inventory-for-windows-pcs-in-microsoft-intune.md)：說明如何建立報告，其中列出關於電腦的硬體功能，以及電腦上所安裝之軟體的資訊。 另外也說明如何重新整理電腦清查以確保它是最新狀態。
- [淘汰 Windows 電腦](retire-a-windows-pc-with-microsoft-intune.md)：列出淘汰 Windows 電腦的步驟，並描述當您淘汰電腦時會發生什麼事。
- [管理 Windows 電腦的使用者裝置連結](manage-user-device-linking-for-windows-pcs-with-microsoft-intune.md)：說明在您對使用者部署軟體之前，需要將使用者連結到電腦的時機與方式。
- [對 Windows 電腦要求及提供遠端協助](request-and-provide-remote-assistance-for-windows-pcs-in-microsoft-intune.md)：說明 Intune 電腦使用者如何向您取得遠端協助，以及描述先決條件和 TeamViewer 安裝程式。

如需上述工作的詳細資訊，請參閱[一般電腦管理工作](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)。

## <a name="management-limitations-of-the-intune-client-software"></a>Intune 用戶端軟體的管理限制

有一些可以用於將電腦視為行動裝置加以管理的管理選項，無法在 Intune 用戶端軟體所管理的電腦上使用︰

-   完整抹除 (可使用選擇性抹除)
-   條件式存取

也請注意，在 Intune 系統管理主控台中，某些區段 (例如 [更新]、[保護] 及 [授權]) 只在您使用 Intune 用戶端軟體註冊裝置之後才會出現。

  ![只有電腦用戶端才會出現的系統管理主控台項目](../media/admin-console-settings-only-for-pc-agent.png)

## <a name="help-with-troubleshooting"></a>協助疑難排解問題

Intune 用戶端軟體通常是在背景中以無訊息模式執行，不需要太多使用者互動或疑難排解。 如需要解決電腦管理問題，可以查看記錄檔。 Intune 用戶端軟體和對應的記錄會安裝在 %Program Files%\Microsoft\OnlineManagement 目錄下。

您也可以檢閱[Microsoft Intune 的用戶端設定疑難排解](/intune-classic/troubleshoot/troubleshoot-client-setup-in-microsoft-intune)，查看可能會發生的問題，以及有無任何解決方法或因應措施。