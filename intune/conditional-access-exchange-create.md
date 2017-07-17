---
title: "建立及指派內部部署 Exchange 條件式存取原則"
titleSuffix: Intune Azure preview
description: "Intune Azure 預覽版︰如何在 Intune 中為 Exchange 內部部署及舊版的 Exchange Online Dedicated 設定條件式存取"
keywords: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 04/24/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 127dafcb-3f30-4745-a561-f62c9f095907
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 2f1775eb98d6518ce35dcc38852e167c5eada616
ms.contentlocale: zh-tw
ms.lasthandoff: 05/23/2017


---

# <a name="how-to-create-and-assign-a-conditional-access-policy-for-exchange-on-premises-and-legacy-exchange-online-dedicated-in-microsoft-intune-azure-preview"></a>如何在 Microsoft Intune Azure 預覽版中為 Exchange 內部部署及舊版的 Exchange Online Dedicated 建立及指派條件式存取原則

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

本主題逐步說明如何依據裝置合規性，為 Exchange 內部部署設定條件式存取的程式。

如果您有 Exchange Online Dedicated 環境，而且需要了解它是使用新版或舊版的設定，請連絡您的帳戶管理員。 若要控制 Exchange 內部部署或舊版 Exchange Online Dedicated 環境的電子郵件存取，請在 Intune 中設定 Exchange 內部部署的條件式存取。

## <a name="before-you-begin"></a>開始之前

在設定條件式存取之前，請確定下列事項：

- 您的 Exchange 版本必須是「Exchange 2010 SP1 或更新版本」。 支援 Exchange 伺服器用戶端存取伺服器 (CAS) 陣列。

- 您必須使用 [Exchange Active Sync 內部部署 Exchange Connector](exchange-connector-install.md)，將 Intune 連線至內部部署 Exchange。

    >[!IMPORTANT]
    >內部部署 Exchange Connector 僅適用於您的 Intune 租用戶，無法搭配任何其他租用戶使用。 您也應該確定適用於租用戶的 Exchange 連接器**只安裝在一部電腦上**。

- 連接器可以安裝在任何電腦上，只要該電腦能與 Exchange 伺服器通訊。

- 此連接器支援 **Exchange CAS 環境**。 想要的話，在技術上您可以將連接器直接安裝在 Exchange CAS 伺服器上，但不建議這麼做，因為這會增加伺服器負載。 設定連接器時，您必須將它設定成可以與其中一部 Exchange CAS 伺服器通訊。

- 必須以憑證式驗證或使用者認證項目來設定 **Exchange ActiveSync**。

- 設定條件式存取原則並以使用者為目標後，使用者使用的**裝置**必須符合下列條件，使用者才能連接到其電子郵件：
    - 已向 Intune **註冊**，或為加入網域的電腦。
    - 已在 **Azure Active Directory** 中註冊。 此外，必須向 Azure Active Directory 註冊用戶端 Exchange ActiveSync 識別碼。
<br></br>
- Intune 和 Office 365 客戶將會自動啟用 AAD DRS。 已部署 ADFS 裝置註冊服務的客戶不會在其內部部署 Active Directory 中看到已註冊的裝置。 **這不適用於 Windows 電腦和 Windows Phone 裝置**。

- 「符合」部署到該裝置的合規性原則。

- 若裝置不符合條件式存取設定，將會在使用者登入時，對其顯示下列訊息之一︰
    - 若裝置未向 Intune 註冊，或未在 Azure Active Directory 中註冊，將會顯示一則訊息，指示使用者如何安裝公司入口網站應用程式、如何註冊裝置，以及如何啟用電子郵件。 此程序也會將裝置的 Exchange ActiveSync 識別碼與 Azure Active Directory 中的裝置記錄相關聯。
    - 若裝置不合規，將會顯示一則訊息，將使用者導向 Intune 公司入口網站或公司入口網站應用程式，讓使用者能夠從中尋找到問題及其修復方法的相關資訊。

### <a name="support-for-mobile-devices"></a>支援行動裝置

- Windows Phone 8.1 和更新版本
- iOS 上的原生電子郵件應用程式。
- EAS 郵件用戶端 (例如 Android 4 或更新版本上的 Gmail)。
- EAS 郵件用戶端 **Android for Work 裝置**：Android for Work 裝置只支援**工作設定檔**中的 **Gmail** 和 **Nine Work** 應用程式。 Android for Work 若要使用條件式存取，除了必須部署 Gmail 或 Nine Work 應用程式的電子郵件設定檔之外，還必須將這些應用程式部署為必要安裝。

> [!NOTE]
> 不支援適用於 Android 和 iOS 的 Microsoft Outlook 應用程式。 Android for Work 即將在接下來幾個月陸續推出給 Intune 租用戶使用。

### <a name="support-for-pcs"></a>對電腦的支援

Windows 8.1 及更新版本上的原生「郵件」應用程式 (必須已向 Intune 註冊)


## <a name="configure-exchange-on-premises-access"></a>設定 Exchange 內部部署存取

1. 移至 [Azure 入口網站](https://portal.azure.com/)，並使用您的 Intune 認證登入。

2. 成功登入之後，您會看到 [Azure 儀表板]。

3. 選擇左功能表中的 [更多服務]，然後在文字方塊篩選中輸入 **Intune**。

4. 選擇 [Intune]，您會看到 [Intune 儀表板]。

5.  選擇 [條件式存取]，然後選擇

6. [內部部署] 刀鋒視窗會顯示條件式存取原則與受該原則影響之裝置的狀態。

7. 從 [管理] 下選擇 [Exchange 內部部署存取]。

8. 在 [Exchange 內部部署存取] 刀鋒視窗中選擇 [是]，以啟用 Exchange 內部部署存取控制。

      > [!NOTE]
      > 若未設定 Exchange Active Sync 內部部署連接器，將會停用此選項。  您必須先安裝及設定此連接器，才能為 Exchange 內部部署啟用條件式存取。 如需詳細資訊，請參閱[安裝 Intune 內部部署 Exchange 連接器](exchange-connector-install.md)

9. 從 [指派] 下選擇 [包含的群組]。  請使用應套用條件式存取的安全性使用者群組。 這會需要使用者向 Intune 註冊其裝置，而且必須符合合規性設定檔的規範。

10. 若要排除特定的使用者群組，可以選擇 [排除的群組]，然後選取要免套用裝置註冊與合規需求的使用者群組。

11. 從 [設定] 下選擇 [使用者通知]，可修改預設的電子郵件訊息。 當使用者裝置不合規範，卻又要存取 Exchange 內部部署時，即會將此訊息會傳送給使用者。 訊息範本會使用標記語言。  當您一邊輸入訊息時，會一邊顯示訊息的預覽。
    > [!TIP]
    > 若要深入了解標記語言，請參閱 Wikipedia 上的這篇[文章](https://en.wikipedia.org/wiki/Markup_language)。

12. 依據接下來的兩個步驟所述，在 [Advanced Exchange Active Sync access settings]\(進階 Exchange Activesync 存取設定) 刀鋒視窗中，為從不是由 Intune 管理的裝置存取設定全域預設規則及平台層級規則。

13. 對於不受條件式存取影響的裝置或其他規則，您可以選擇允許它們存取 Exchange 或加以封鎖。
  - 當您設定成允許存取時，所有裝置均能立即存取 Exchange 內部部署。  若**包含的群組**中之使用者的裝置稍後被評估為不符合合規性政策，或未向 Intune 註冊，將會予以封鎖。
  - 當您設定為禁止存取時，將會立即禁止所有裝置存取 Exchange 內部部署。  **包含的群組**中之使用者的裝置若已向 Intune 註冊，並經評估為符合規範，即可存取 Exchange 內部部署。 因為非執行 Samsung KNOX Standard 的 Android 裝置不支援此設定，所以一律無法 Exchange 內部部署。
<br></br>
14. 從 [裝置平台例外狀況] 下選擇 [新增]，以指定平台。 若將 [未受管理的裝置存取] 設定設定為 [封鎖]，即使已在平台例外狀況中指定要禁止的平台，仍會允許已經註冊且合規的裝置進行存取。 選擇 [確定]，以儲存設定。

15. 在 [內部部署] 刀鋒視窗中按一下 [儲存]，以儲存條件式存取原則。

## <a name="create-azure-ad-conditional-access-policies-in-intune-azure-preview"></a>在 Intune Azure 預覽版中建立 Azure AD 條件式存取原則

從 Intune 1704 版開始，系統管理員可以從 Intune Azure 預覽版建立 Azure AD 條件式存取原則，如此您就不需要在 Azure 和 Intune 工作負載之間切換。

> [!IMPORTANT]
> 您必須要有 Azure AD Premium 授權才能從 Intune Azure 預覽版入口網站建立 Azure AD 條件式存取原則。

### <a name="to-create-azure-ad-conditional-access-policy"></a>建立 Azure AD條件式存取原則

1. 在 [Intune 儀表板] 中，選擇 [條件式存取]。

2. 在 [條件式存取儀表板] 中，選擇 [Azure Active Directory 中的條件式存取]。

3. 選擇 [新增原則] 來建立新的 Azure AD 條件式存取原則。

    ![Azure AD 條件式存取原則](./media/Azure-AD-CA-Intune.png)

## <a name="see-also"></a>請參閱

[Azure Active Directory 中的條件式存取](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)