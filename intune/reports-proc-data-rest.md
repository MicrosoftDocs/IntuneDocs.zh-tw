---
title: "使用 REST 用戶端從資料倉儲 API 取得資料"
description: "使用 RESTful API 從 Intune 資料倉儲擷取資料。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: D6D15039-4036-446C-A58F-A5E18175720A
ms.reviewer: jeffgilb
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 1bbb0e8ba84e221df3a434da79c513939267648b
ms.sourcegitcommit: b8ef9d8387b4d9b2ea4e6ce937635304771e6532
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2017
---
# <a name="get-data-from-the-intune-data-warehouse-api-with-a-rest-client"></a>使用 REST 用戶端從 Intune 資料倉儲 API 取得資料

您可以透過 RESTful 端點存取 Intune 資料倉儲資料模型。 若要存取您的資料，您的用戶端必須使用 OAuth 2.0 向 Microsoft Azure Active Directory (Azure AD) 進行授權。 若要啟用存取權，請先在 Azure 中設定原生應用程式，並將權限授與 Microsoft Intune API。 您的本機用戶端會取得授權，接著用戶端可以透過原生應用程式與資料倉儲端點通訊。

設定用戶端從資料倉儲 API 取得資料的步驟需要您：

1. 在 Azure 中將用戶端應用程式建立為原生應用程式
3. 將 Microsoft Intune API 存取權授與用戶端應用程式
3. 建立本機 REST 用戶端以取得資料

使用下列步驟，以了解如何授權和使用 Postman 作為用戶端。 Postman 是針對 REST 用戶端進行疑難排解和開發以與 API 搭配使用的常用工具。 如需 Postman 的詳細資訊，請參閱 [Postman](https://www.getpostman.com) 網站。 本主題也包含 C# 程式碼範例。 此範例提供如何授權用戶端以及從 API 取得資料的範例。

## <a name="create-a-native-app-in-azure"></a>在 Azure 中建立原生應用程式

在 Azure 中建立原生應用程式。 此原生應用程式是用戶端應用程式。 本機用戶端要求認證時，在本機電腦上執行的用戶端會參考 Intune 資料倉儲 API。 

1. 登入您租用戶的 Azure 入口網站。 選擇 [Azure Active Directory] > [應用程式註冊]，以開啟 [應用程式註冊] 刀鋒視窗。
2. 按一下 [New app registration] (新增應用程式註冊)。
3. 鍵入應用程式詳細資料。
    1.  在 [名稱] 中，鍵入易記名稱 (例如 Intune 資料倉儲用戶端)。
    2.  在 [應用程式類型] 中，選取 [原生]。
    3.  在 [登入 URL] 中，鍵入 URL。 [登入 URL] 將取決於特定案例；不過，如果您計劃使用 Postman，請鍵入 `https://www.getpostman.com/oauth2/callback`。 向 Azure AD 進行驗證時，您將使用回呼進行用戶端驗證步驟。
4.  按一下 **建立**。

     ![Intune 資料倉儲 API](media\reports-get_rest_data_client_overview.png)

5. 記下此應用程式的 [應用程式識別碼]。 您將在下節中使用此識別碼。
6. 如果您計劃使用 Postman，請新增金鑰。 此金鑰是用作向 Azure AD 進行驗證的用戶端密碼。 新增金鑰：
    1.  在應用程式的 [設定] 刀鋒視窗中，按一下 [API 存取權] 下的 [金鑰]。
    2.  在 [描述] 中，鍵入金鑰名稱 (例如 Client-Secret)。
    3.  在 [期間] 中，選取 [1 年]。
    4.  按一下 **[儲存]**。 
    5.  複製金鑰值。 關閉 [金鑰] 的 [設定] 刀鋒視窗之後，就無法再擷取金鑰。

## <a name="grant-the-native-app-access-to-the-microsoft-intune-api"></a>將 Microsoft Intune API 存取權授與原生應用程式

您現在已在 Azure 中定義應用程式。 將存取權從原生應用程式授與 Microsoft Intune API。

1.  按一下原生應用程式。 您已將應用程式命名為「Intune 資料倉儲用戶端」這類名稱。
2.  從 [設定] 刀鋒視窗中，按一下 [必要權限]。
3.  在 [必要權限] 刀鋒視窗中，按一下 [新增]。
4.  按一下 [選取 API]。
5.  搜尋 Web 應用程式名稱。 它會命名為 **Microsoft Intune API**。
6.  按一下清單中的應用程式。
7.  按一下 [選取]。
8.  核取 [委派的權限] 方塊，以新增 [Get data warehouse information from Microsoft Intune] (從 Microsoft Intune 取得資料倉儲資訊)。

    ![啟用存取](media\reports-get_rest_data_client_access.png)

9.  按一下 [選取]。
10.  按一下 [完成]。
11.  選擇性地，在 [必要權限] 刀鋒視窗中，按一下 [授與權限]。 這會授與目前目錄中所有帳戶的存取權。 這會防止針對租用戶中的每位使用者顯示同意對話方塊。 如需詳細資訊，請參閱[整合應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)。
12.  按一下 [是]。

## <a name="get-data-from-the-microsoft-intune-api-with-postman"></a>使用 Postman 從 Microsoft Intune API 取得資料

您可以利用泛型 REST 用戶端 (例如 Postman) 來使用 Intune 資料倉儲 API。 Postman 可以深入了解 API 的功能、基礎 OData 資料模型，以及針對 API 資源連線進行疑難排解。 在本節中，您可以找到如何為本機用戶端產生 Auth2.0 權杖的資訊。 用戶端需要有此權杖，才能向 Azure AD 進行驗證以及存取 API 資源。

### <a name="information-you-will-need-to-make-the-call"></a>進行呼叫所需的資訊

您需要下列資訊，才能使用 Postman 進行 REST 呼叫：

| 屬性        | 描述                                                                                                                                                                          | 範例                                                                                       |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| 回呼 URL     | 在應用程式設定頁面中，將此項目設定為回呼 URL。                                                                                                                              | https://www.getpostman.com/oauth2/callback                                                    |
| 權杖名稱       | 用來將認證傳遞給 Azure 應用程式的字串。 此程序會產生您的權杖，以針對資料倉儲 API 進行呼叫。                          | Bearer                                                                                        |
| 驗證 URL         | 這是用來驗證的 URL。 | https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com |
| 存取權杖 URL | 這是用來授與權杖的 URL。                                                                                                                                              | https://login.microsoftonline.com/common/oauth2/token |
| 用戶端識別碼        | 您已在 Azure 中建立原生應用程式時建立並記下此項目。                                                                                               | 4184c61a-e324-4f51-83d7-022b6a81b991                                                          |
| 用戶端機密    | 您已在 Azure 中新增用戶端應用程式的金鑰時建立並記下它。                                                                                              | JZoRZGPmN9xwsUnfX9UW877dkV5Fn/qQClhr7SuyMUQ=                                                  |
| 範圍 (選擇性) | 空白                                                                                                                                                                               | 您可以將此欄位空白。                                                                     |
| 授與類型       | 權杖是授權碼。                                                                                                                                                  | 授權碼                                                                            |

您需要端點。 在此範例中，我們要從 **dates** 實體中擷取資料。 **dates** 實體的格式如下：`https://fef.{aus}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=beta`。 您將使用您的租用戶管理 URL。 您已在建立 Web 應用程式時使用租用戶管理 URL。

### <a name="make-the-rest-call"></a>進行 REST 呼叫

若要取得 Postman 的新存取權杖，您必須新增 Azure AD 授權 URL、用戶端識別碼和用戶端密碼。 Postman 將載入授權頁面，而您可在其中鍵入您的認證。

#### <a name="add-the-information-used-to-request-the-token"></a>新增用來要求權杖的資訊

1.  如果您尚未安裝 Postman，請進行下載。 若要下載 Postman，請參閱 [www.getpostman](https://www.getpostman.com)。
2.  開啟 Postman。 選擇 HTTP 作業 **GET**。
3.  將端點 URL 貼入位址中。 它應該看起來像這樣：  

    `https://fef.msua06.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=beta`
4.  選擇 [授權] 索引標籤，然後從 [類型] 清單中選取 [OAuth 2.0]。
5.  按一下 [Get New Access Token] (取得新存取權杖)。
6.  確認您已經在 Azure 中將回呼 URL 新增至應用程式。 回呼 URL 是 `https://www.getpostman.com/oauth2/callback`。
7.  在 [權杖名稱] 中，鍵入 [持有人]。
8.  新增 [驗證 URL]。 它應該看起來像這樣：  

    `https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com`
9.  新增 [存取權杖 URL]。 它應該看起來像這樣：  

     `https://login.microsoftonline.com/common/oauth2/token`

10. 從您已在 Azure 中建立並命名為 `Intune Data Warehouse Client` 的原生應用程式中，新增 [用戶端識別碼]。 它應該看起來像這樣：  

     `4184c61a-e324-4f51-83d7-022b6a81b991`

11. 新增在 Azure 中建立原生應用程式時定義為金鑰的 [用戶端密碼]。 它應該看起來像這樣： 

     `F360R69M0MS72OB6YAqTyXO9MsXZx/OJTgAE2HB4k2k=`

12. 選取 [授權碼]，並在本機要求存取權杖。

13. 按一下 [要求權杖]。

    ![權杖的資訊](media\reports-postman_getnewtoken.png)

14. 在 Active AD 授權頁面中，鍵入認證。 Postman 中的 [現有權杖] 清單現在包含名為 `Bearer` 的權杖。
16. 選擇權杖。 在 [Add token to] (將權杖新增至) 中，選取 [標頭]。
17. 按一下 [使用權杖]。 標頭清單包含授權的新金鑰值以及值 `Bearer <your-authorization-token>`。

#### <a name="send-the-call-to-the-endpoint-using-postman"></a>使用 Postman 將呼叫傳送至端點

1.  按一下 [傳送]。
2.  傳回的資料會出現在 Postman 回應主體中。

    ![Postman 200OK](media\reports-postman_200OK.png)

## <a name="create-a-rest-client-c-to-get-data-from-the-intune-data-warehouse"></a>從 Intune 資料倉儲建立 REST 用戶端 (C#) 以取得資料

下列範例包含簡單 REST 用戶端。 此程式碼會使用 .Net 程式庫中的 **httpClient** 類別。 用戶端取得 Azure AD 的認證之後，用戶端會建構 GET REST 呼叫，以從資料倉儲 API 擷取 dates 實體。

> [!Note]  
> 您可以存取 [GitHub](https://github.com/Microsoft/Intune-Data-Warehouse/blob/master/Samples/CSharp/Program.cs) 上的下列程式碼範例。 如需範例的最新變更和更新，請參閱 GitHub 存放庫。

1.  開啟 [Microsoft Visual Studio]。
2.  選擇 [檔案] > [新增專案]。 展開 [Visual C#]，然後選擇 [主控台應用程式 (.NET Framework)]。 
3.  將專案命名為 ` IntuneDataWarehouseSamples`，並瀏覽至您想要儲存專案的位置，然後按一下 [確定]。
3.  以滑鼠右鍵按一下方案總管中的方案名稱，然後選取 [管理方案的 NuGet 套件]。 按一下 [瀏覽]，然後在搜尋方塊中鍵入 `Microsoft.IdentityModel.Clients.ActiveDirectory'。
4. 選擇套件，並在 [Manage Packages for Your Solution] (管理解決方案的套件) 下選取 **IntuneDataWarehouseSamples** 專案，然後按一下 [安裝]。 
5. 按一下 [我接受]，以接受 NuGet 套件授權。
6. 從方案總管中，開啟 `Program.cs`。

    ![Visual Studio 中的專案](media\reports-get_rest_data_in.png)

7.  將 Program.cs 中的程式碼取代為下列程式碼：  
    ```csharp
namespace IntuneDataWarehouseSamples
{
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    class Program
    {
     static void Main(string[] args)
  {
   /**
    * TODO: Replace the below values with your own.
    * emailAddress - The email address of the user that you will authenticate as.
    *
    * password  - The password for the above email address.
    *    This is inline only for simplicity in this sample. We do not 
    *    recommend storing passwords in plaintext.
    *
    * applicationId - The application ID of the native app that was created in AAD.
    *
    * warehouseUrl   - The data warehouse URL for your tenant. This can be found in 
    *      the Azure portal.
    * 
    * collectionName - The name of the warehouse entity collection you would like to 
    *      access.
    */
   var emailAddress = "intuneadmin@yourcompany.com";
   var password = "password_of(intuneadmin@yourcompany.com)";
   var applicationId = "<Application ID>";
   var warehouseUrl = "https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=beta";
   var collectionName = "dates";

   var adalContext = new AuthenticationContext("https://login.windows.net/common/oauth2/token");
   AuthenticationResult authResult = adalContext.AcquireTokenAsync(
    resource: "https://api.manage.microsoft.com/",
    clientId: applicationId,
    userCredential: new UserPasswordCredential(emailAddress, password)).Result;

   var httpClient = new HttpClient();
   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);

   var uriBuilder = new UriBuilder(warehouseUrl);
   uriBuilder.Path += "/" + collectionName;

   HttpResponseMessage response = httpClient.GetAsync(uriBuilder.Uri).Result;

   Console.Write(response.Content.ReadAsStringAsync().Result);
   Console.ReadKey();
  }
    }
    ```

8.  更新程式碼範例中的 `TODO`。
9.  按 **Ctrl + F5**，以偵錯模式建置並執行 Intune.DataWarehouseAPIClient 用戶端。

    ![以 JSON 格式擷取的 date 實體。](media\reports-get_rest_data_output.png)

10.  檢閱主控台輸出。 此輸出包含從 Intune 租用戶的 **dates** 實體中提取的資料，且格式為 JSON。

## <a name="next-steps"></a>後續步驟

您可以在[使用 Intune 資料倉儲 API](reports-api-url.md) 中找到授權、API URL 結構和 OData 端點的詳細資料。 

您也可以參考 Intune 資料倉儲資料模型，以尋找 API 中所含的資料實體。 如需詳細資訊，請參閱 [Intune 資料倉儲 API 資料模型](reports-ref-data-model.md)。