---
title: 在 Microsoft Intune 中設定 macOS 裝置的有線網路設定 - Azure | Microsoft Docs
titleSuffix: ''
description: 建立或新增適用於 macOS 裝置的有線網路裝置組態設定檔。 請查看不同的設定，包括在 Microsoft Intune 中新增憑證、選擇 EAP 類型，以及選取驗證方法。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/4/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7dba36d03489bcdeee3c3c1f69a4995823dd21ee
ms.sourcegitcommit: df8e2c052fafb2d5d4e9b4fcd831ae0ecf7f8d16
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74994328"
---
# <a name="add-wired-network-settings-for-macos-devices-in-microsoft-intune"></a>在 Microsoft Intune 中新增適用于 macOS 裝置的有線網路設定

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

您可以建立含有特定有線網路設定的設定檔，然後將此設定檔部署到您的 macOS 裝置。 Microsoft Intune 提供許多功能，包括驗證您的網路、新增 PKS 或 SCEP 憑證等等。 

## <a name="before-you-begin"></a>開始之前

[建立裝置設定檔](device-profile-create.md)。

> [!NOTE]
> 這些設定適用于所有的註冊類型。 如需註冊類型的詳細資訊，請參閱[macOS 註冊](../enrollment/macos-enroll.md)。

## <a name="profiles"></a>Profiles

- **配置檔案類型**：選擇 [**有線網路**]。
- **網路介面**： 
- **EAP 類型**：選擇用來驗證安全無線連線的可延伸驗證通訊協定 (EAP) 類型。 選項包括：
  - **EAP-FAST**：輸入**受保護的存取認證 (PAC) 設定**。 此選項使用受保護的存取認證，用來建立用戶端與驗證伺服器之間已驗證的通道。 選項包括：
    - **請勿使用 (PAC)**
    - **使用 (PAC)** ：如果現有的 PAC 檔案已存在，請使用它。
    - **使用及佈建 PAC**：建立 PAC 檔案並新增到您的裝置。
    - **使用及匿名佈建 PAC**：建立 PAC 檔案，並在未向伺服器驗證的情況下新增到您的裝置。
  - **EAP-TLS**：另請輸入：
    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。
    - **用戶端驗證** - **用戶端驗證的用戶端憑證 (身分識別憑證)** ：選擇 也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
  - **EAP-TTLS**：另請輸入：
    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。
    - **用戶端驗證** - 選擇 [驗證方法]  。 選項包括：
      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 另請輸入：
        - **非 EAP 方法 (內部識別)** ：選擇驗證連線的方式。 請務必選擇與您的 Wi-Fi 網路設定相同的通訊協定。
          選項包括：[未加密的密碼 (PAP)]  、[Challenge Handshake 驗證通訊協定 (CHAP)]  、[Microsoft CHAP (MS-CHAP)]  ，或 [Microsoft CHAP 第 2 版 (MS-CHAP v2)] 
      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。
  - **LEAP**
  - **PEAP**：另請輸入：
    - **伺服器信任** - **憑證伺服器名稱**：[ 新增]  您信任之憑證授權單位 (CA) 核發的憑證中所使用的一或多個通用名稱。 輸入此資訊時，可以略過連線到此 Wi-Fi 網路時，使用者裝置上顯示的動態信任視窗。
    - **伺服器驗證的根憑證**：選擇現有受信任的根憑證設定檔。 當用戶端連線到網路時，會向伺服器提供此憑證，並用來驗證連線。
    - **用戶端驗證** - 選擇 [驗證方法]  。 選項包括：
      - **使用者名稱和密碼**：提示使用者輸入使用者名稱和密碼以驗證連線。 
      - **憑證**：選擇也會部署到裝置的 SCEP 或 PKCS 用戶端憑證設定檔。 此憑證是裝置提供給伺服器以驗證連線的身分識別。
      - **識別隱私權 (外部識別)** ：指定回應 EAP 識別要求時所要傳送的文字。 此文字可以是任何值，例如 `anonymous`。 在驗證期間，一開始會先傳送此匿名識別，隨後以安全通道傳送真正的識別。

## <a name="next-steps"></a>後續步驟

設定檔已建立，但它不會執行任何動作。 接者，請[指派此設定檔](device-profile-assign.md)並[監視其狀態](device-profile-monitor.md)。

在[android](wi-fi-settings-android.md)、 [android Enterprise](wi-fi-settings-android-enterprise.md)、 [iOS](wi-fi-settings-ios.md)和[Windows 10](wi-fi-settings-windows.md)裝置上設定 wi-fi 設定。