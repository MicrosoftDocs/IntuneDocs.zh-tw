---
title: "註冊 iOS 裝置 - Apple Configurator 與設定助理"
titleSuffix: Intune Azure preview
description: "Intune Azure 預覽版︰了解如何使用 Apple Configurator 透過設定助理，來註冊公司擁有的 iOS 裝置。"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 04/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 6d384cd0-b662-41e7-94f5-0c96790ab20a
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: e6b0bc51515a2b72c7574a7ca7e29c094f3bdbdb
ms.contentlocale: zh-tw
ms.lasthandoff: 05/23/2017


---

# <a name="enroll-ios-devices-with-apple-configurator-and-setup-assistant"></a>使用 Apple Configurator 與設定助理來註冊 iOS 裝置

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

Intune 支援使用 Mac 電腦上所執行的 [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12)，來註冊屬公司擁有的 iOS 裝置。 此處理程序會將裝置重設為原廠設定，並將裝置備妥可執行設定助理，以及為裝置的新使用者安裝公司原則。

>[!NOTE]
>此註冊方法不能與[裝置註冊管理員](device-enrollment-manager-enroll.md)方法一起使用。

您可以使用 Apple Configurator，將 iOS 裝置重設為原廠設定，並準備好裝置以讓裝置的新使用者進行設定。 這個方法需要您透過 USB 將 iOS 裝置連線到 Mac 電腦，以設定公司註冊，且該方法之前提為假設您使用 Apple Configurator 2.0。 大多數的情況會需要將原則套用至 iOS 裝置 (包括使用者親和性)，以啟用 Intune 公司入口網站應用程式。

註冊 iOS 裝置的其他方法，詳述於 [Choose how to enroll iOS devices in Intune](enrollment-method-choose-ios.md) (選擇如何在 Intune 中註冊 iOS 裝置)。

## <a name="prerequisites"></a>必要條件

請於設定 iOS 裝置註冊之前，先完成下列必要條件︰

- [取得 Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)
- 確認您確實可存取 iOS 裝置
- 具有裝置序號 (請參閱 [How to get an iOS serial number](https://support.apple.com//HT204308) (如何取得 iOS 序號))
- 備好 USB 連接線
- 請確定的 Mac 電腦已安裝有 [Apple Configurator 2.0](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12)
- [新增 Apple Configurator 序號](apple-configurator-serial-numbers-add.md)


## <a name="create-an-apple-configurator-profile-for-devices"></a>為建立裝置 Apple Configurator 設定檔

裝置註冊設定檔會定義套用至裝置群組的設定。 下列步驟示範如何針對使用 Apple Configurator 註冊的 iOS 裝置，建立裝置註冊設定檔。

1. 在 Azure 入口網站中，選擇 [更多服務] > [監視 + 管理] > [Intune]。

2. 在 Intune 刀鋒視窗上，選擇 [註冊裝置]，然後選擇 [Apple 註冊]。

3. 在 [管理 Apple Configurator 註冊設定] 下，選取 [AC 設定檔]。

4. 在 [Apple Configurator 註冊設定檔] 刀鋒視窗中，選取 [建立]。

5. 在 [建立註冊設定檔] 刀鋒視窗中，為設定檔輸入名稱以及描述。

6. 為 [使用者親和性] 選擇具備此設定檔的裝置，在註冊時要或不要有使用者親和性。

   - **搭配使用者親和性進行註冊** - 裝置必須在初始設定期間與使用者建立關聯，之後便可以存取公司資料與電子郵件。 應要為受管理的裝置 (屬於使用者且需要將公司入口網站用於安裝應用程式等服務) 設定使用者親和性。

   - **不搭配使用者親和性進行註冊** - 該裝置不會與使用者建立關聯。 針對執行工作而不需存取本機使用者資料的裝置，請使用此關係。 需要使用者關聯的應用程式 (包含用於安裝企業營運應用程式的公司入口網站應用程式) 將無法運作。

7. 選取 [建立]儲存該設定檔。

## <a name="assign-serial-numbers-to-an-apple-configurator-profile"></a>為 Apple Configurator 設定檔指派序號

建立 Apple Configurator 設定檔之後，可為設定檔指派裝置序號。 若要能夠指派序號，必須先將其新增至 Intune 中，步驟如[新增 Apple Configurator 序號](apple-configurator-serial-numbers-add.md)中所述。

### <a name="assign-serial-numbers-to-apple-configurator-profiles"></a>為 Apple Configurator 設定檔指派序號

1. 在 Azure 入口網站中，選擇 [更多服務] > [監視 + 管理] > [Intune]。

2. 從 [Apple Configurator 註冊設定檔] 刀鋒視窗中，選取要指派序號的設定檔。

3. 在為設定檔命名的刀鋒視窗中，選取 [序號]  >  [指派]。

4. 選取要指派給設定檔的序號，然後選取 [指派] 按鈕。

## <a name="export-the-profile-to-ios-devices"></a>將設定檔匯出到 iOS 裝置

在建立設定檔並指派序號之後，必須從 Intune 匯出設定檔 URL 或如下所述之格式的檔案。 然後手動將其匯入 Mac 上的 Apple Configurator 方案，Apple Configurator 方案接著會將其部署到裝置。

### <a name="export-a-profile-using-setup-assistant-enrollment"></a>使用設定助理註冊匯出設定檔

1. 在 Azure 入口網站中，選擇 [更多服務] > [監視 + 管理] > [Intune]。

2. 在 [Apple Configurator 註冊設定檔] 刀鋒視窗上，選取要匯出的設定檔。

3. 在 [設定檔] 刀鋒視窗中，選取 [匯出設定檔]。

4. 在連結著 iOS 裝置的情況下，將設定檔 URL 複製到 [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) 中。 您稍後將在 Apple Configurator 中上傳它，以定義 iOS 裝置所使用的 Intune 設定檔。

  您將在下列程序中使用 Apple Configurator 將這個設定檔 URL 上傳至 Apple 服務，以定義 iOS 裝置所使用的 Intune 設定檔。

5. 使用 Apple Configurator 將此設定檔 URL 上傳至 Apple 服務，以定義 iOS 裝置所使用的 Intune 設定檔。
 1.  在 Mac 電腦上，開啟 [Apple Configurator 2] 在功能表列中，選擇 [Apple Configurator 2]，然後選擇 [喜好設定]。
  > [!WARNING]
  > 在註冊過程，會將裝置重設為原廠設定。 最佳做法是將裝置重設，並加以啟動。 當您將裝置連線時，裝置應該會在 **Hello** 畫面。

  2. 在 [喜好設定] 窗格中，選取 [伺服器]，然後選擇加號 (+) 來啟動 [MDM 伺服器精靈]。 選擇 **[下一步]**。

  3. 透過 Microsoft Intune，在 iOS 裝置的 [設定助理] 註冊下輸入 MDM 伺服器的**主機名稱或 URL** 及**註冊 URL**。 對於 [註冊 URL]，輸入從 Intune 匯出的註冊設定檔 URL。 選擇 **[下一步]**。  

    您可以放心地忽略指出「伺服器 URL 未經驗證」的警告。 請選擇 [下一步] 以繼續，直到精靈完成為止。

  4.  將 iOS 行動裝置連線到具有 USB 介面卡的 Mac 電腦。
  > [!WARNING]
  > 在註冊過程，會將裝置重設為原廠設定。 最佳做法是將裝置重設，並加以啟動。 當您啟動設定助理時，裝置應該會在 [Hello] 畫面上。

  5.  選擇 [準備]。 在 [準備 iOS 裝置] 窗格上，選取 [手動]，然後選擇 [下一步]。
  6. 在 [Enroll in MDM Server]\(在 MDM 伺服器中註冊) 窗格上，選取您建立的伺服器名稱，然後選擇 [下一步]。
  7. 在 [監督裝置]窗格上，選取監督層級，然後選擇 [下一步]。
  8. 在 [Create an Organization]\(建立組織) 窗格上，選擇 [組織] 或建立新的組織，然後選擇 [下一步]。
  9. 在 [Configure iOS Setup Assistant]\(設定 iOS 設定助理) 窗格上，選擇要呈現給使用者的步驟，然後選擇 [準備]。 若出現提示，請驗證以更新信任設定。  
  10. 當 iOS 裝置完成準備時，請拔除 USB 纜線。  
6.  **散發裝置**。
    裝置現在已準備好進行公司註冊。 關閉裝置，並將它們散發給使用者。 當使用者啟動其裝置時，設定助理就會啟動。

    請參閱[如何指導使用者使用 Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/how-to-educate-your-end-users-about-microsoft-intune)。 您也可以引導使用者參閱[搭配 Intune 使用 iOS 或 macOS 裝置](https://docs.microsoft.com/intune/deploy-use/how-to-educate-your-end-users-about-microsoft-intune)

## <a name="how-users-install-and-use-the-company-portal-on-their-devices"></a>使用者在其裝置安裝及使用公司入口網站的方式

已設定使用者親和性的裝置可以安裝並執行公司入口網站 App，以下載 App 及管理裝置。 使用者收到裝置之後，必須如下所示完成一些額外的步驟，來完成設定助理並安裝公司入口網站應用程式。
