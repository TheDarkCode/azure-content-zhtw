<properties
	pageTitle="Azure Active Directory 中的自訂網域名稱的概念式概觀 | Microsoft Azure"
	description="說明在 Azure Active directory 中使用自訂網域名稱的概念性架構，包括單一登入同盟"
	services="active-directory"
	documentationCenter=""
	authors="jeffsta"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/18/2016"
	ms.author="curtand;jeffsta"/>

# Azure Active Directory 中的自訂網域名稱的概念式概觀

網域名稱是許多目錄資源識別項的重要部分：它可能是使用者的使用者名稱或電子郵件地址的一部分、群組位址的一部分，也可能是應用程式的應用程式識別碼 URI 的一部分。Azure Active Directory (Azure AD) 中的資源可包含已驗證為目錄 (其中含有資源) 所擁有的網域名稱。只有全域管理員可以在 Azure AD 中執行網域管理工作。

Azure AD 中的網域名稱是全域唯一的。一個網域名稱只可供一個 Azure AD 使用。如果某個 Azure AD 目錄已驗證網域名稱，則其他 Azure AD 目錄就不能驗證或使用該相同的網域名稱。

## 初始和自訂的網域名稱

Azure AD 中的每個網域名稱不是初始網域名稱就是自訂網域名稱。

每個 Azure AD 皆隨附形式為 contoso.onmicrosoft.com 的初始網域名稱。在建立目錄時，會建立網域名稱的這個第三個層級 (通常由建立該目錄的系統管理員建立)，在此範例中為 “contoso.onmicrosoft.com”。目錄的初始網域名稱無法變更或刪除。完整運作下的初始網域名稱，主要是用作為啟動載入的機制，直到自訂網域名稱經過驗證為止。

在大部分生產環境中，目錄會具有至少一個已驗證的自訂網域，例如 "contoso.com"，而且是可讓使用者看到的自訂網域。自訂網域名稱是由該組織所擁有和使用的網域名稱，例如 "contoso.com"，其用於裝載其網站。員工很熟悉此網域名稱，因為它是使用者用來登入公司網路或傳送及接收電子郵件之使用者名稱的一部分。

自訂網域名稱必須先加入目錄中並經過驗證，才可供 Azure AD 使用。

## 已驗證和未驗證的網域名稱

目錄的初始網域名稱會由 Azure AD 隱含評估為已驗證。系統管理員在 Azure AD 中新增自訂網域名稱時，其最初是未驗證的狀態。Azure AD 不允許任何目錄資源使用未經過驗證的網域名稱。如此可確保只有一個目錄可以使用特定的網域名稱，而且確定使用網域名稱的組織實際擁有該網域名稱。

Azure AD 會透過在網域名稱的網域名稱服務 (DNS) 區域檔案中尋找特定的項目，來驗證網域名稱的擁有權。若要驗證網域名稱的擁有權，系統管理員可以從 Azure AD 取得 Azure AD 將尋找的 DNS 項目，並將該項目加入網域名稱的 DNS 區域檔案。該網域的網域名稱註冊機構會負責維護 DNS 區域檔案。驗證網域的步驟可在[將自訂網域加入 Azure AD 目錄](active-directory-add-domain.md)一文中找到。

將 DNS 項目加入網域名稱的區域檔案中，並不會影響其他的網域服務，例如電子郵件或虛擬主機。

## 同盟和受管理的網域名稱

您可以設定 Azure AD 中的自訂網域名稱以讓使用者在內部部署 Active Directory 與 Azure AD 之間獲得同盟的登入體驗。為同盟設定網域除了需要更新 Azure AD 中的特殊權限資源，也需要更新您的 Windows Server Active Directory。設定同盟網域的工作必須在 Azure AD Connect 中或使用 PowerShell 來完成。無法從 Azure 傳統入口網站起始同盟自訂網域的工作。[請觀看這段影片以了解如何設定 AD FS，讓使用者能利用 Azure AD Connect 登入](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)。

未同盟的網域有時也稱為受管理的網域。Azure AD 目錄的初始網域會隱含評估為受管理的網域。

## 主要網域名稱

目錄的主要網域名稱是系統管理員在 [Azure 傳統入口網站](https://manage.windowsazure.com/)或其他入口網站 (例如 Office 365 管理入口網站) 中建立新的使用者時，預先選取作為使用者名稱「網域」部分之預設值的網域名稱。目錄只能有一個主要網域名稱。系統管理員可以將主要網域名稱變更為任何未同盟的已驗證自訂網域，或是變更為初始網域。

## Azure AD 和其他 Microsoft Online Services 中的網域名稱

必須先在 Azure AD 中驗證網域名稱，才可將其提供 Exchange Online、SharePoint Online 和 Intune 等另一個 Microsoft Online Service 使用。這些其他的服務通常會要求系統管理員新增一或多個服務特定的 DNS 項目。

Azure Web 應用程式使用其本身的機制來驗證網域的擁有權。網域必須驗證是否可用於 Azure AD，即使它先前已驗證可供仰賴該 Azure AD 之訂用帳戶中的 Azure Web 應用程式使用也是如此。Azure Web 應用程式可使用已在不同於保護 Web 應用程式之目錄的目錄中，進行過驗證的網域名稱。

## 管理網域名稱

您可以在 Azure 傳統入口網站和 PowerShell 中完成網域管理工作。許多工作可使用 Azure AD 圖形 API (公開預覽中) 來完成。

-   [新增和驗證自訂網域名稱](active-directory-add-domain.md)

-   [在 Azure 傳統入口網站中管理網域](active-directory-add-manage-domain-names.md)

-   [使用 PowerShell 管理 Azure AD 中的網域名稱](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

-   [使用 Azure AD 圖形 API 管理 Azure AD 中的網域名稱](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

<!---HONumber=AcomDC_0720_2016-->