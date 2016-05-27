---
# required metadata

title: 應用程式部署問題疑難排解 | Microsoft Intune
description:
keywords:
author: Nbigman
manager: jeffgilb
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 28ac298e-fb73-4c1c-b3fd-8336639e05e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: jeffgilb
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Microsoft Intune 的應用程式部署問題疑難排解
本主題會協助您解決 Microsoft Intune 的相關應用程式部署問題

如果此資訊無法解決您的問題，請參閱[如何取得 Microsoft Intune 支援](how-to-get-support-for-microsoft-intune.md)，以尋找更多方法來取得協助。


## 一般應用程式部署問題

### 如果您無法登入 Intune 公司入口網站

1.  請查看您的帳戶是否存在於 [Office 365 入口網站](http://go.microsoft.com/fwlink/p/?LinkId=698854)中，或帳戶是否已停用。

2.  確定您已在 [Office 365 入口網站](http://go.microsoft.com/fwlink/p/?LinkId=698854)中，完成此帳戶的佈建。

3.  在 [Office 365 入口網站](http://go.microsoft.com/fwlink/p/?LinkId=698854)中，確定您已使用正確的使用者名稱和密碼登入 Intune，且使用者名稱格式如下：joe@domain.com。

### 如果公司入口網站中沒有連絡 IT 的資訊

1.  在 Intune 管理主控台中，按一下 [管理員]  &gt;  [公司入口網站]

2.  設定 [連絡 IT]  詳細資料。

### 若您在清單中找不到特定的應用程式

1.  請確定您查看的應用程式清單，屬於應用程式部署所屬的使用者或裝置。

2.  確定裝置符合應用程式的需求。

### 下載應用程式時若收到錯誤

1.  確定每個使用者都沒有多個並行的下載。 每位使用者一次只能下載一個應用程式。

2.  確定每個帳戶的同時下載數目並未過多。 請稍候數分鐘，然後再試一次。

3.  如果您收到無法安裝、安裝取消或需要重試的 iOS 原生訊息，可能是因為流量過大。 請稍候數分鐘，然後再試一次。

4.  若 iOS 應用程式下載進度列顯示下載已完成，但應用程式安裝失敗，表示您提供的應用程式檔案可能有問題。

### 若按下 iOS 應用程式的連結會將您連入 iTunes App Store 中的舊有位置

1.  目前開啟的 iTunes App Store 工作階段連入了舊版應用程式頁面。

2.  關閉裝置上的 iTunes App Store，然後重試連結。

### 若在啟動 iOS 應用程式時收到錯誤

1.  可能是應用程式的到期日無效。

### 若應用程式在上傳時一直卡在「進行中」

1.  上傳應用程式時，會先新增中繼資料，然後再新增應用程式套件。 上傳中繼資料後，應用程式會呈現進行中狀態。 若您應用程式處於進行中狀態的時間超乎尋常，請刪除應用程式，然後再重新上傳一次。

2.  請勿在應用程式處於「進行中」狀態下管理應用程式的部署。

### 若在安裝 iOS 應用程式時發生失敗

1.  請確定您的組織防火牆可讓您存取 Apple 佈建與憑證網站。

2.  如需詳細資訊，請檢視 Apple 開發人員文件。

### 錯誤︰發行者不存在
您使用新增其他軟體合約來新增協力廠商授權合約。 您嘗試從 [其他軟體授權合約] 頁面新增發行者。 頁面會依字母順序提供現有發行者的清單。
您輸入遺漏的發行者，但是收到錯誤發行者不存在 

這是預設設計。 Intune 只提供授權追蹤給受歡迎的軟體項目。 在 Intune 可做為授權工作負載中的選項之前，它需要至少 4 個不同的帳戶回報軟體。

### 如果受管理的應用程式不報告安裝狀態

在 2014 年 11 月 Microsoft Intune 服務更新之前安裝的受管理應用程式，其安裝狀態尚未收集。 對於在這項服務更新之前安裝受管理應用程式的裝置，請用適當的部署動作 (例如 [可用安裝] )，更新每個相關聯的應用程式部署。 每部裝置都會在自動檢查有無可用的應用程式時更新應用程式。 如需詳細資訊，請參閱[使用 Microsoft Intune 更新應用程式](/intune/deploy-use/update-apps-using-microsoft-intune)

## <a name="BKMK_SoftDistErrorCodes"></a>應用程式部署錯誤碼
下表列出部署 Intune 應用程式時可能發生的常見錯誤、其可能的原因及可行的解決方案，協助您疑難排解問題。

|錯誤碼|可能的問題|建議的解決方式|
|--------------|--------------------|------------------------|
|0x80073CFF<br /><br />0x80CF201C (用戶端錯誤)|若要安裝此應用程式，您必須具有已啟用側載功能的系統。|確定應用程式套件已經由信任的簽章簽署，而且已經安裝在已加入網域並啟用 AllowAllTrustedApps 原則的電腦上，或已經安裝在具有已啟用 AllowAllTrustedApps 原則 (在註冊 Windows RT 裝置時套用) 之 Windows 側載授權的電腦上。|
|0x80073CF0|無法開啟套件。|可能的原因：<br /><br />-   套件未經簽署。<br />-   發行者名稱與簽署憑證主體不符。<br /><br />查看 AppxPackagingOM 事件記錄檔以取得詳細資訊。|
|0x80073CF3|套件更新失敗、具相依項目或發生驗證衝突|可能的原因：<br /><br />-   傳入的套件與安裝的套件衝突。<br />-   找不到指定的套件相依項目。<br />-   套件不支援正確的處理器架構。<br /><br />查看 AppXDeployment-Server 事件記錄檔以取得詳細資訊。|
|0x80073CFB|提供的套件已經安裝，不允許重新安裝套件|如果您要安裝的套件與已經安裝的套件不同，可能就會收到這項錯誤。 請確認數位簽章也包含在套件中。 重建或重新簽署套件後，該套件之位元就不再與先前安裝的套件相同。 此錯誤有下列兩種可能的修正選項：<br /><br />-   遞增應用程式的版本號碼，然後再重建及重新簽署應用程式。<br />-   在安裝新套件之前，針對系統上的每個使用者移除舊套件。|

### 後續步驟
如果這項疑難排解資訊對您沒有幫助，請連絡 Microsoft 支援服務，如[如何取得 Microsoft Intune 的支援](how-to-get-support-for-microsoft-intune.md)中所述


<!--HONumber=May16_HO2-->

