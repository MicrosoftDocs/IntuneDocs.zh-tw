---
title: "設定 Intune 裝置限制設定"
titleSuffix: Intune on Azure
description: "了解如何使用 Intune，設定您管理之裝置上的設定與功能。"
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 04/12/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 42f9b104-c1f6-4dfc-8aa4-1d33e1eaf61f
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: 8652b2b6db340f3b0cddcf538fa418c8774b1d6c
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2017
---
# <a name="how-to-configure-device-restriction-settings-in-microsoft-intune"></a>如何在 Microsoft Intune 中設定裝置限制設定

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

裝置限制可讓您控制各種類別中，您所管理的各種設定及功能，包括安全性、瀏覽器、硬體及資料共用設定。 例如，您可以建立裝置限制設定檔，禁止 iOS 裝置的使用者存取裝置相機 。

使用本主題中的資訊，可深入了解設定裝置限制設定檔的相關基本概念，然後可深入閱讀每個平台的主題，以了解裝置專屬內容。

## <a name="create-a-device-profile-containing-device-restriction-settings"></a>建立內含裝置限制設定的裝置設定檔

1. 登入 Azure 入口網站。
2. 選擇 [更多服務]  >  [監視 + 管理]  >  [Intune]。
3. 在 [Intune] 刀鋒視窗中選擇 [設定裝置]。
2. 在 [裝置設定] 刀鋒視窗中，選擇 [管理]  >  [設定檔]。
3. 在設定檔刀鋒視窗中，選擇 [建立設定檔]。
4. 在 [建立設定檔] 刀鋒視窗中，為裝置限制設定檔輸入 [名稱] 及 [描述]。
5. 從 [平台] 下拉式清單中，選取要套用自訂設定的裝置平台。 您目前可選擇下列平台之一，進行裝置限制設定︰
    - **Android**
    - **iOS**
    - **macOS**
    - **Windows Phone 8.1**
    - **Windows 8.1 及更新版本**
    - **Windows 10 及更新版本**
6. 從 [設定檔類型] 下拉式清單中，選擇 [裝置限制]。 若想要建立像是 Surface Hub 等 Windows 10 團隊版裝置之裝置限制設定檔，選擇 [裝置限制 (Windows 10 團隊版)]。
7. 您可設定的設定值取決於您選擇的平台而有所不同。 前往下列主題之一，即可取得每個平台的詳細設定︰
    - [Android 設定](device-restrictions-android.md)
    - [iOS 設定](device-restrictions-ios.md)
    - [macOS 設定](device-restrictions-macos.md)
    - [Windows Phone 8.1 設定](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 設定](device-restrictions-windows-10.md)
    - [Windows 10 團隊版設定](device-restrictions-windows-10-teams.md)
    - [Android for Work 設定](device-restrictions-android-for-work.md)
8. 當您完成時，請返回 [建立設定檔] 刀鋒視窗，然後點擊 [建立]。

隨即會建立設定檔，並會出現在 [設定檔清單] 刀鋒視窗上。
若想繼續，並將此設定檔指派給群組，請參閱[如何指派裝置設定檔](device-profile-assign.md)。

## <a name="example-of-device-restriction-settings"></a>裝置限制設定範例

在此概略範例中，您將建立會封鎖而無法使用 Android 裝置上內建相機應用程式的裝置限制原則。

![如何停用 Android 裝置上的相機](./media/disable-android-camera.png)
