---
title: "驗證您的 MAM 設定 |Microsoft Docs"
description: "本主題說明如何測試並驗證 MAM 原則是否已正確設定且正常運作。"
keywords: 
author: andredm7
ms.author: andredm
manager: angerobe
ms.date: 12/19/2016
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 41d82597-e13e-4c3e-9151-e71392236ca0
ms.reviewer: joglocke
ms.custom: intune-classic
translationtype: Human Translation
ms.sourcegitcommit: d6ff74f0b46baf384dbdedf13ad75538dd33a089
ms.openlocfilehash: 080d8f4fd4b6e1b53df860f4319b1c199d504c06


---

# <a name="validating-your-mobile-application-management-setup"></a>驗證您的行動應用程式管理設定

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

本主題提供設定行動應用程式管理 (MAM) 後，檢查是否有問題的相關資訊。 本指南適用於 Azure 入口網站中的 MAM 原則。

### <a name="checking-for-symptoms"></a>檢查是否有徵兆
因為 MAM 是一種資料保護工具，所以使用者不太可能回報問題。 如果 MAM 設定有問題，使用者將可如同沒有 MAM 一般不受限制地進行存取，且不會察覺發生問題。 基於這個理由，建議您對可刻意測試 MAM 限制的一小群使用者試驗 MAM 原則，以驗證 MAM 設定。


### <a name="what-to-check"></a>要檢查的項目

如果測試顯示您的 MAM 原則行為不如預期，建議您檢查下列項目︰

- 使用者具有 MAM 授權嗎？
- 使用者具有 O365 授權嗎？
- 每個使用者的 MAM 應用程式狀態。 可能的應用程式狀態為 [已簽入] 和 [未簽入 (Not checked in)]。

#### <a name="user-mam-status"></a>使用者 MAM 狀態
1. 在 Azure 入口網站中依序選擇 [Intune 行動應用程式管理]  >  [設定]  >  [應用程式管理]  >  [所有設定]  >  [依使用者的應用程式報告 (App reporting by user)]  >  [使用者]。

2. 從清單中選擇使用者，或是搜尋並選擇使用者，然後選擇 [選取使用者]。 在 [應用程式報告] 資料行頂端，您會看到使用者是否具有 MAM 授權。 您會在下方看到使用者是否具有 O365 授權，以及使用者所有裝置的應用程式狀態。

![MAM 的應用程式狀態](..\media\ts-mam-user-apps.png)

### <a name="what-to-do"></a>解決方式
以下是要根據使用者狀態所採取的動作︰

- 如果使用者不具有 MAM 授權，依照[管理 Intune 授權](..\get-started\start-with-a-paid-subscription-to-microsoft-intune.md)中所述將 Intune 授權指派給使用者。
- 如果使用者不具有 O365 授權，替使用者取得授權。
- 如果使用者的應用程式列為 [未簽入 (Not checked in)]，檢查是否已替該應用程式正確地設定 MAM 原則。
- 請確保這些條件會套用至您想要套用 MAM 原則的所有使用者。

### <a name="see-also"></a>請參閱
[準備使用 Microsoft Intune 設定行動應用程式管理原則](..\deploy-use\get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune.md)

[使用 Microsoft Intune 的行動應用程式管理原則保護應用程式資料](..\deploy-use\protect-app-data-using-mobile-app-management-policies-with-microsoft-intune.md)



<!--HONumber=Dec16_HO2-->

