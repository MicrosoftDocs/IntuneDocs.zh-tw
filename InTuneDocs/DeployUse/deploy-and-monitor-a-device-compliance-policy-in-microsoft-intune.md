---
# required metadata

title: 在 Microsoft Intune 中部署和監視相容性原則 | Microsoft Intune
description:
keywords:
author: karthikaraman
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: d8f246d4-0d86-4c8b-a1bf-9977985506d8

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 在 Microsoft Intune 中部署和監視裝置相容性原則
## 部署相容性原則
將您[建立的](create-a-device-compliance-policy-in-microsoft-intune.md)相容性原則部署到組織中的一或多個使用者或裝置群組。

1.  在 [原則] 工作區中，選取您要部署的原則，然後選擇 [管理部署]
![在頂端顯示 [管理部署] 功能表選項的相容性原則頁面的螢幕擷取畫面](./media/intune-sa-3c-deploy-compliance-policy2.png)

2.  在 [管理部署] 對話方塊中，選擇您要部署原則的一個或多個群組，然後選擇 [新增] > [確定]
![管理部署對話方塊的螢幕擷取畫面 您可以將相容性原則部署到使用者和/或裝置。 使用已建立並同步處理至 Intune 的 Active Directory 群組，或在 Intune 主控台中手動建立這些群組。

若要深入了解如何部署原則，請參閱[部署組態原則](manage-settings-and-features-on-your-devices-with-microsoft-intune-policies.md) 使用 [原則] 工作區的 [概觀] 頁面上的狀態摘要和警示，來識別需要注意的原則問題。

> [!IMPORTANT]此外，狀態摘要還會顯示在 [儀表板]  工作區中。

## 若未部署相容性原則，但卻啟用了 Exchange 條件式存取原則，則將允許所有目標裝置進行存取。
如何解決 Intune 原則衝突 將多個 Intune 原則套用至一個裝置時，可能會發生原則衝突。

-   如果原則設定重疊，Intune 會使用下列規則解決任何衝突︰

-   若衝突的設定來自 Intune 設定原則與相容性原則，即使設定原則中的設定更為安全，相容性原則中的設定仍優先於設定原則中的設定。

## 若您已部署多項相容性原則，將會取其中最安全的原則。

#### 監視相容性原則

1.  檢視裝置不符合相容性原則的裝置

2.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com) 中，選擇 [群組] > [所有裝置]

3.  按兩下裝置清單中的裝置名稱。

4.  選擇 [原則] 索引標籤，以查看該裝置的原則清單。
![從 [篩選] 下拉式清單中，選取 [不符合相容性原則]](./media/intune-sa-3e-view-device-noncompliance.png)

#### 在篩選清單中顯示選項清單的螢幕擷取畫面

1.  檢視健全情況證明報表

2.  在 [Microsoft Intune 管理主控台](https://manage.microsoft.com)中，選擇 [報表] 在 [健全情況證明報表 - 建立新報表] 頁面中，您可以檢視內含 Intune 所收集之所有 Windows 10 健全情況證明資料的報表。 您也可以使用篩選，利用一部分的資料子集來建立報表。


## 篩選可以根據裝置類型、作業系統或僅一部分資料點。
後續步驟

[您現在可以使用相容性原則搭配條件式存取原則，在組織中控制服務的存取。](restrict-access-to-email-and-o365-services-with-microsoft-intune.md)


### 限制存取電子郵件和 O365 服務
[請參閱](introduction-to-device-compliance-policies-in-microsoft-intune.md)


<!--HONumber=May16_HO2-->

