---
title: "在免費試用版中建立群組來組織使用者和裝置"
description: "當您註冊免費 30 天的 Microsoft Intune 評估時，如何建立裝置群組和使用者群組。"
keywords: 
author: lindavr
ms.author: lindavr
manager: angrobe
ms.date: 11/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 7162cad3-5c14-43f3-a760-833ffd7786b1
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 084cc155a64a58582e3008df10e86c1e5266054d
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2017
---
# <a name="create-groups-to-organize-evaluation-subscription-users-and-devices"></a>建立群組來組織評估訂閱使用者和裝置

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Intune 中的群組讓您在管理裝置和使用者時有絕佳的彈性。 您可以設定群組，使其符合組織的需求 (例如依據地理位置、部門或硬體特性)，並且使用它們來大規模地執行各種系統管理工作，從設定一組使用者的原則，到部署應用程式至一組裝置。

## <a name="create-a-device-group"></a>建立裝置群組
您可以使用裝置群組來部署軟體與更新，並設定 Microsoft Intune 代理程式設定與 Windows 防火牆設定原則。 例如，使用下列步驟設定 "My Trial Devices" 群組：

1.  在 [Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [群組] &gt; [概觀] &gt; [建立群組]。

2.  在 [群組名稱] 中輸入 "My Trial Devices"，並從父群組清單中選取 [所有裝置]，然後選擇 [下一步]。

3.  在 [定義成員資格準則]  頁面上，選取 [所有裝置]  ，以指出群組同時包含行動裝置和電腦。

4.  在 [定義直接成員資格] 頁面上，選擇 [下一步] 。 如果您先前建立的群組未包含所有的裝置，而且您想要新增特定裝置到新群組，您可以在這個步驟中完成。

5.  在 [摘要] 頁面上，檢閱將要採取的動作，然後選擇 [完成]。

您可以在 [群組]  工作區之 [所有裝置]  下的 [群組] 清單中，找到新建立的群組。 您也可以從這裡編輯或刪除該群組。

## <a name="create-a-user-group"></a>建立使用者群組
以使用者群組來部署軟體和裝置原則。 例如，使用下列步驟設定 "My Trial Users" 群組：

1.  在 [Intune 管理主控台](https://manage.microsoft.com/)中，選擇 [群組] &gt; [概觀] &gt; [建立群組]。

2.  在 [群組名稱] 中輸入 "My Trial Users"，然後從父群組清單中選取 [所有使用者]，然後選擇 [下一步]。

3.  在 [定義成員資格準則]  頁面上，將 [群組成員資格啟動方式]  設定為 [父群組中的所有使用者] 。

4.  在 [排除這些安全性群組中的成員] 旁，選擇 [瀏覽]，然後選取 [公司系統管理員]。 這個排除動作可讓您管理 My Trial Users 群組，同時又不影響公司系統管理員帳戶 (也稱為租用戶系統管理員)。

5.  在 [定義直接成員資格] 頁面上，選擇 [下一步] 。 由於您要讓 My Trial Users 群組包含除了公司系統管理員以外的所有使用者，因此在此步驟不需要執行任何動作。

6.  在 [摘要] 頁面上，檢閱將要採取的動作，然後選擇 [完成]。

您可以在 [群組]  工作區之 [所有使用者]  下的 [群組] 清單中，找到新建立的群組。 您也可以從這裡編輯或刪除該群組。

若要深入了解如何使用群組，請參閱[利用 Microsoft Intune，使用群組管理使用者和裝置](/intune-classic/Deploy-Use/use-groups-to-manage-users-and-devices-with-microsoft-intune)。

## <a name="next-steps"></a>後續步驟
[建立原則](get-started-with-a-30-day-trial-of-microsoft-intune-step-4.md)  