---
title: "註冊公司所擁有的 iOS 裝置"
description: "使用 Apple 裝置註冊方案 (DEP) 或 Apple Configurator 來註冊公司擁有的 iOS 裝置"
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 02/21/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 2d3ca4ab-f20c-4d56-9413-f8ef19cf0722
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 42da9c874183287bc9485035ae39e94efbaa3e8b
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2017
---
# <a name="enroll-corporate-owned-ios-devices-in-microsoft-intune"></a>在 Microsoft Intune 中註冊屬公司擁有的 iOS 裝置

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Microsoft Intune 支援透過 Apple 裝置註冊方案 (DEP) 或 Mac 電腦上所執行的 [Apple Configurator](https://go.microsoft.com/fwlink/?LinkId=518017) 工具，來註冊公司所擁有的 iOS 裝置。

**必要條件：**[Apple 推播通知服務憑證](set-up-ios-and-mac-management-with-microsoft-intune.md)

您可以使用下列三種方式之一來註冊公司已註冊的 iOS 裝置：

- Apple Configurator，使用設定助理或直接註冊
- 裝置註冊方案
- 公司入口網站應用程式

>[!NOTE]
>Apple Configurator 與裝置註冊方案的註冊方法，不可與[裝置註冊管理員](enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune.md)方法一起使用。

所有 iOS 裝置預設都可以在 Intune 中註冊。 若要阻擋註冊個人或公司擁有的裝置，請以系統管理員認證登入 [Microsoft Intune 管理員入口網站](https://manage.microsoft.com)。 選擇 [管理員] > [行動裝置管理] > [註冊規則]，然後清除適用的選項。

## <a name="use-apple-configurator"></a>使用 Apple Configurator

您可以透過匯出公司註冊設定檔，然後將 iOS 裝置連線到執行 Apple Configurator 的 Mac 來註冊那些行動裝置。 Apple Configurator 支援兩種註冊方式：

- **設定助理註冊**：將裝置重設為原廠設定值，並準備好裝置以供裝置的新使用者進行設定。 此方法需要系統管理員透過 USB 將 iOS 裝置連接到執行 [Apple Configurator](https://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 電腦以預先設定註冊。 裝置接著將會傳遞至其使用者，該使用者將會執行設定助理程序。 此程序將會以使用者的公司或學校憑證設定裝置，並完成註冊程序。 如需詳細資訊，請參閱[使用 Apple Configurator 和設定助理來註冊 iOS 裝置](ios-setup-assistant-enrollment-in-microsoft-intune.md)。

- **直接註冊**：建立 Apple Configurator 相容的檔案以供裝置期間使用。 註冊的裝置未重設為原廠值，但不具有任何使用者關係。 此方法需要系統管理員透過 USB 將 iOS 裝置連接到執行 [Apple Configurator](https://go.microsoft.com/fwlink/?LinkId=518017) 的 Mac 電腦以註冊裝置。 如需詳細資訊，請參閱[使用 Apple Configurator 和直接註冊來註冊 iOS 裝置](ios-direct-enrollment-in-microsoft-intune.md)。

## <a name="use-the-device-enrollment-program-dep"></a>使用裝置註冊方案 (DEP)
DEP 會以「無線」的方式將設定檔部署到透過 DEP 購買的裝置上。 當使用者在裝置上執行設定助理時，該裝置便會在 Intune 中註冊。 如需詳細資訊，請參閱[註冊裝置註冊方案 iOS 裝置](ios-device-enrollment-program-in-microsoft-intune.md)。

## <a name="use-the-company-portal-on-dep-enrolled-or-apple-configurator-enrolled-devices"></a>在已註冊 DEP 或 Apple Configurator 的裝置上使用公司入口網站

已設定使用者親和性的裝置可以安裝並執行公司入口網站 App，以下載 App 及管理裝置。 使用者收到裝置之後，他們必須完成一些額外步驟，以完成設定助理並安裝公司入口網站 App。

需要有使用者親和性，才能支援下項項目︰
  - 行動應用程式管理 (MAM) 應用程式
  - 對電子郵件和公司資料進行條件式存取
  - 公司入口網站應用程式

**使用者如何註冊具有使用者親和性的屬公司擁有 iOS 裝置**
1. 當使用者將其裝置開啟時，系統會提示他們完成設定助理。 設定期間，系統會提示使用者輸入其認證。 他們必須輸入與其 Intune 中訂閱相關聯的認證 (也就是唯一的個人識別碼或 UPN)。

2. 設定期間，系統會提示使用者輸入 Apple ID。 使用者必須提供 Apple ID 以允許裝置安裝「公司入口網站」。 他們也可以在安裝完成後，從 iOS 設定功能表提供 ID。

3. 設定完成之後，該 iOS 裝置必須從 App Store 安裝公司入口網站 App。

4. 使用者現在可以使用於設定裝置時所用的 UPN 來登入公司入口網站。

5. 登入之後，系統會提示使用者註冊其裝置。 第一個步驟是識別裝置。 App 會在清單中顯示已經過公司註冊並指派給使用者 Intune 帳戶的 iOS 裝置。 使用者應該要選擇相符的裝置。

  如果此裝置尚未經過公司註冊，使用者應該選擇 [新裝置] 來繼續標準註冊流程。

6. 在下一個畫面中，使用者必須確認新裝置的序號。 使用者可以點選 [確認序號] 連結，來啟動「設定」App 以確認序號。 使用者必須在公司入口網站 App 中輸入序號的最後四個字元。

  此步驟會確認裝置是公司在 Intune 中註冊的裝置。 如果裝置上的序號不符，則可能選取了錯誤的裝置。 使用者應該返回上一個畫面，並選取不同的裝置。

7. 序號通過驗證後，公司入口網站 App 會重新導向至「公司入口網站」網站，以完成註冊。 該網站接著將會提示使用者返回 App。

8. 現在已經完成註冊。 使用者現在已可使用裝置的完整功能。

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>關於無使用者親和性之公司擁有的受管理的裝置

設定為無使用者親和性的裝置並不支援公司入口網站，且不應該安裝該 App。 [公司入口網站] 是針對有公司認證且需要存取個人化公司資源 (如電子郵件) 的使用者而設計。 註冊為無使用者親和性的裝置並非專供單一使用者登入使用。 Kiosk、銷售點 (POS)，或共用公用程式裝置，皆屬註冊為無使用者親和性的常見案例。

如果需要使用者親和性，請在註冊裝置之前確認裝置的註冊設定檔已選取 [使用者親和性]。 若要變更裝置的親和性狀態，您必須將裝置淘汰並重新註冊該裝置。



### <a name="see-also"></a>請參閱
[Microsoft Intune 中註冊裝置的必要條件](prerequisites-for-enrollment.md)