---
title: "設定 Skycure 與 Intune 整合"
description: "設定 Skycure 與 Microsoft Intune 整合。"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 93722f66-7641-4a3f-b1fb-3a0a58a36675
ms.reviewer: heenamac
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 1d5a59f34a5dacdc2e1a0d5c6601b4ede1a908e4
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2017
---
# <a name="set-up-the-skycure-integration-with-intune"></a>設定 Skycure 與 Intune 整合

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

您必須將 Skycure 應用程式新增至 Azure AD，才能使用單一登入功能。

## <a name="before-you-begin"></a>開始之前

### <a name="azure-ad-account-used-to-integrate-intune-and-skycure"></a>用來整合 Intune 與 Skycure 的 Azure AD 帳戶

-   在開始 Skycure 基本設定程序之前，請確定您已經在 [Skycure 管理主控台](https://aad.skycure.com)中正確設定 Azure AD 帳戶。

### <a name="full-integration-vs-read-only"></a>完整整合與唯讀

Skycure 支援兩種與 Intune 整合的模式：

-   **唯讀整合 (基本設定)：**僅清查來自 Azure Active Directory 的裝置，並將它們填入 Skycure 主控台。
<br>
    -   如果未在 Skycure 管理主控台中選取 [向 Intune 報告裝置的健全狀況和風險] 和 [也向 Intune 報告安全性事件] 方塊，則整合將會是唯讀，並因此一律不會變更 Intune 中的裝置狀態 (符合規範或不符合規範)。
<br></br>
-   **完整整合：**允許 Skycure 向 Intune 報告裝置的風險和安全性事件詳細資料，這會在兩個雲端服務之間建立雙向通訊。

### <a name="how-the-skycure-apps-are-used-with-azure-ad-and-intune"></a>Skycure 應用程式如何搭配 Azure AD 和 Intune 使用？

-   **iOS 應用程式︰**允許使用者使用 iOS 應用程式登入 Azure AD。

-   **Android 應用程式︰**允許使用者使用 Android 應用程式登入 Azure AD。

-   **管理應用程式︰**這是 Skycure Azure AD 多租用戶應用程式，可啟用與 Intune 的服務對服務通訊。

## <a name="to-set-up-the-read-only-integration-between-intune-and-skycure"></a>設定 Intune 和 Skycure 之間的唯讀整合

> [!IMPORTANT]
> Skycure 系統管理員認證必須是屬於 Azure Active Directory 有效使用者的電子郵件，否則登入將會失敗。 Skycure 會使用 Azure Active Directory，透過單一登入 (SSO) 來驗證它的系統管理員。

1.  移至 [Skycure 管理主控台](https://aad.skycure.com)。

2.  輸入您的「Skycure 系統管理員認證」，然後按一下 [繼續]。

3.  移至 [設定]，選擇 [Intune 整合] 底下的 [基本設定]。

4.  在 [iOS 應用程式] 標籤上，按一下 [新增至 Active Directory]。

    ![Skycure 管理主控台上的 iOS 應用程式](../media/mtp/skycure-setup-1.png)

5.  隨即會開啟登入頁面。請輸入您的 Intune 認證，然後按一下 [接受]。

    ![iOS 應用程式 Intune 登入提示](../media/mtp/skycure-setup-2.png)

6.  一旦將應用程式新增至 Azure AD，您就可以在 Skycure 管理主控台上看到指示，指出應用程式已成功新增至 Azure AD。

    ![iOS 應用程式完成畫面](../media/mtp/skycure-setup-3.png)

> [!NOTE]
> 針對 [Skycure Android] 和 [管理] 應用程式重複相同程序。

### <a name="add-an-azure-ad-security-group-into-skycure"></a>將 Azure AD 安全性群組新增至 Skycure

您需要新增包含所有執行 Skycure 之裝置的 Azure AD 安全性群組。

1.  輸入並選取所有執行 Skycure 之裝置的安全性群組，然後按一下 [套用變更]。

    ![設定安全性群組 Skycure 管理主控台](../media/mtp/skycure-setup-4.png)

Skycure 會將執行其 Mobile Threat Defense 服務的裝置，與 Azure AD 安全性群組同步。

![在 Skycure 管理主控台上完成的安全性群組設定](../media/mtp/skycure-setup-5.png)

## <a name="set-up-the-full-integration-between-intune-and-skycure"></a>設定 Intune 和 Skycure 之間的完整整合

1.  移至 [Skycure 管理主控台](https://aad.skycure.com)。

2.  輸入您的「Skycure 系統管理員認證」，然後按一下 [繼續]。

3.  移至 [設定]，選擇 [Intune 整合] 底下的 [完整整合]。

4.  選取下列設定：

    a.  向 Intune 報告裝置的健全狀況和風險

    b。  也向 Intune 報告安全性事件

5.  按一下 [套用變更]。

    ![完成的 Skycure 完整整合](../media/mtp/skycure-setup-6.png)

## <a name="next-steps"></a>後續步驟

[在 Intune 中啟用 Skycure Mobile Threat Defense (英文)](/intune-classic/deploy-use/enable-skycure-mobile-threat-defense-in-intune)