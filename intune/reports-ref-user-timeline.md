---
title: "資料倉儲使用者實體時間軸 | Microsoft Docs"
description: "Intune 資料倉儲以時間軸的方式呈現使用者。"
keywords: "Intune 資料倉儲"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 11/14/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 363D148E-688F-4830-B6DE-AB4FE3648817
ms.reviewer: jeffgilb
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: ce43234003da859b81dd499f22f7280db5bda41b
ms.sourcegitcommit: d26930f45ba9e6292a49bcb08defb5b3f14b704b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2017
---
# <a name="user-lifetime-representation-in-the-intune-data-warehouse"></a>Intune 資料倉儲中的使用者存留期表示法

您可以使用資料快照集儲存到 Intune 資料倉儲中的日期，來回答有關以時間為基礎之趨勢的問題。 例如，您可以查看在一個月內開始新增的使用者數目。 您可能也會詢問已經從系統移除之使用者的數目。

為了提供這樣的深入見解，資料倉儲會儲存歷史資訊。 這表示它可以追蹤某個實體的存留期。 當實體建立時、實體狀態變更時，及實體被刪除時，倉儲都會記錄。 利用以每日快照集這樣的量化度量所擷取的歷程記錄，您可以比較某一天與其前一天，依此類推。

因為實體的狀態會變更，所以處理實體存留期可能令人困惑。 也就是說，如果您查看第 30 天的快照集，使用者資料列可能未以作用中的狀態存在於資料中。 而在第 29 到 28 天，該實體資料列可能以作用中的狀態存在。 然後在第 28 天之前，該使用者完全不存在。

我們來逐步檢視實體的存留期可能會更清楚。

假設使用者 **John Smith**，在 2017/06/01 被指派授權，然後 **User** 資料表會有下列項目： 
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| John Smith | FALSE | 2017/06/01 | 9999/12/31 | TRUE
 
John Smith 在 2017/07/25 放棄他的授權。 **User** 資料表有下列項目。 在現有資料列中的變更以 `marked` 顯示。 

| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| John Smith | FALSE | 2017/06/01 | `07/26/2017` | `FALSE` 
| John Smith | TRUE | 2017/07/26 | 9999/12/31 | TRUE 

第一個資料列指出 John Smith 自 2017/06/01 到 2017/07/25 存在於 Intune 中。 第二個資料列指出該使用者在 2017/07/25 被刪除，且不再存在於 Intune 中。

假設 John Smith 在 2017/08/31 取得新授權，則 User 資料表會有下列項目：
 
| DisplayName | IsDeleted | StartDateInclusiveUTC | EndDateExclusiveUTC | IsCurrent 
| -- | -- | -- | -- | -- |
| John Smith | FALSE | 2017/06/01 | 2017/07/26 | FALSE 
| John Smith | TRUE | 2017/07/26 | `08/31/2017` | `FALSE` 
| John Smith | FALSE | 2017/08/31 | 9999/12/31 | TRUE 
 
若要查看所有使用者的目前狀態，可以套用 `IsCurrent = TRUE` 的 篩選條件。 
 
若只要查看現有使用者，可以套用 `IsCurrent = TRUE AND IsDeleted = FALSE` 的篩選條件。

## <a name="dimension-tables-in-the-entity-lifetime"></a>實體存留期的維度資料表

為了儲存實體的狀態變更歷程記錄，Intune 不會刪除資料列。 而是將資料列標記為已刪除， 這稱為虛刪除。 維度資料表使用不同的中繼資料資料行來追蹤資料列的存留期。 

最常使用的中繼資料資料行是： 

| 中繼資料屬性名稱  | 值的解讀 |
|--|--|
| IsDeleted | 指出實體在 Intune 中是否已被刪除。 |
| StartDateInclusiveUTC  | 實體載入到 Intune 資料倉儲的 UTC 日期。 實體可能在匯入到 Intune 資料倉儲之前就已經建立。 |
| DeletedDateUTC  | 實體在 Intune 中刪除的 UTC 日期。 |  

以前置詞 **Row** 開頭的任何中繼資料資料行 (例如 **RowLastModifiedDateTimeUTC**) 都表示資料列在 Intune 資料倉儲中建立或修改的時間。 倉儲是 Intune 中資料的下游。 這個值與實體在 Intune 中的存留期沒有關聯性。  
 
若只要查看目前存在的維度實體，可以套用 **IsDeleted = FALSE** 的篩選條件。

## <a name="next-steps"></a>後續步驟

 - 若要深入了解 **Current User** 實體，請參閱 [Current User 實體的參考](reports-ref-current-user.md)。
 - 若要深入了解 **User** 實體，請參閱 [User 實體的參考](reports-ref-user.md)。