---
title: Apple 使用者註冊支援的 Intune 動作與選項
titleSuffix: Microsoft Intune
description: 了解 Apple 使用者註冊支援哪些 Intune 動作與選項
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/2/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: acf1112f96b28b156b3c4857485de30d7ad553ef
ms.sourcegitcommit: 223d64a72ec85fe222f5bb10639da729368e6d57
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955245"
---
# <a name="intune-actions-and-options-supported-with-apple-user-enrollment"></a>Apple 使用者註冊支援的 Intune 動作與選項

使用者註冊支援一組裝置管理選項的子集。 如果將預先存在的設定檔套用至使用者註冊裝置，只會將使用者註冊支援的設定套用到該裝置。

## <a name="password-settings"></a>密碼設定

在使用者註冊裝置上，如果您設定任何密碼設定，[簡單密碼]  設定會自動設定為 [封鎖]  ，並強制執行一組 6 位數的 PIN。

例如，假設您設定 [密碼到期]  設定，並將此原則推播至使用者註冊的裝置。 裝置上會發生下列狀況：
- 會忽略 [密碼到期]  設定。
- 不允許使用簡單密碼，例如 `1111` 或 `1234`。
- 強制使用 6 位數 PIN。

## <a name="administrator-remote-device-actions-and-options"></a>系統管理員遠端裝置動作和選項
系統管理員可以在使用者註冊裝置上執行下列動作和選項：
- 淘汰
- 刪除
- 遠端鎖定
- 同步

不支援所有其他動作。

## <a name="end-user-actions"></a>終端使用者動作
在使用者註冊裝置上，終端使用者可以從公司入口網站應用程式和網站在他們的裝置上執行這些動作：
- 重新命名。 此動作只會套用至公司入口網站內的使用者對應名稱。 它不會在該內容之外將裝置名稱徹底重新命名。
- 移除
- 遠端鎖定
- 檢查狀態

## <a name="other-supported-options"></a>其他支援的選項

對於使用 Apple 使用者註冊所註冊的裝置，Intune 支援下列選項：
- 個別應用程式 VPN。 此支援會排除 Safari 網域，因為使用者註冊不支援進行 Safari 設定。
- WiFi 
- 取消註冊後移除公司應用程式
- 透過使用者授權的大量採購方案 (VPP) 進行應用程式部署
- 越獄偵測

下列是支援的限制：
- 在非受控應用程式中檢視公司文件
- 在公司應用程式中檢視非公司文件
- 允許非受控應用程式從受控連絡人帳戶讀取
- 將 AirDrop 視為非受控目的地
- 需要加密備份
- 受管理應用程式同步至雲端
- 在鎖定裝置時存取控制中心
- 裝置鎖定住時的通知中心存取
- 在鎖定裝置時使用今日檢視
- 防止螢幕擷取畫面
- 封鎖企業書籍備份
- 封鎖企業書籍中繼資料同步
- 需要加密備份
- 需要手錶具備手腕偵測功能
- 封鎖 Siri
- 禁止在鎖定裝置時使用 Siri
- 要求使用 Safari 詐騙警告
- 封鎖向 Apple 提交診斷報告


## <a name="options-not-supported"></a>不支援的選項
透過使用者註冊所註冊的裝置不支援下列選項。 如果需要這些選項，請檢查您自有裝置的裝置註冊，或檢查公司裝置的自動裝置註冊 (先前為「裝置註冊計劃」)。
- 針對受控 APFS 磁碟區以外的應用程式收集應用程式清查。
- 針對受控 APFS 磁碟區以外的憑證與佈建設定檔收集清查。
- 收集 UDID 與其他持續性裝置識別碼。
- 使用者註冊支援註冊的每個裝置都擁有一個唯一的註冊識別碼，但在取消註冊之後，不會保存此識別碼。
- 因為此限制的緣故，所以不支援下列 Intune 功能：
- 使用序列名稱的主體名稱格式的 SCEP 使用者設定檔
- 裝置層級 VPN。
- 裝置授權的 VPP 應用程式部署。
- 針對受控 APFS 磁碟區以外應用程式的 MDM 控制。
- 應用程式保護原則仍然會套用到這些應用程式。 不過，您將無法接管管理或部署這些應用程式的受控版本，除非使用者從裝置上刪除它們。
- 需要監督的動作、設定、設定和命令。 

## <a name="next-steps"></a>後續步驟

[設定 iOS 與 iPadOS 使用者註冊](ios-user-enrollment.md)