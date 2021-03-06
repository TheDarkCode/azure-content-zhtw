<properties
	pageTitle="從 DirSync 和 Azure AD Sync 升級 |Microsoft Azure"
	description="描述如何從 DirSync 和 Azure AD Sync 升級至 Azure AD Connect。"
	services="active-directory"
	documentationCenter=""
	authors="andkjell"
	manager="stevenpo"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="06/27/2016"
	ms.author="andkjell"/>


# 升級 Windows Azure Active Directory Sync (“DirSync”) 和 Azure Active Directory Sync (“Azure AD Sync”)
Azure AD Connect 是連接內部部署目錄與 Azure AD 和 Office 365 的最佳方式。這是將 Azure AD Connect 從 Windows Azure Active Directory Sync (DirSync) 或 Azure AD Sync 升級的最佳時機，因為這些工具現在已淘汰，而且會在 2017 年 4 月 13 日結束支援。

已淘汰的兩個身分識別同步處理工具會提供給單一樹系客戶 (DirSync)，以及多樹系和其他進階客戶 (Azure AD Sync)。這些較舊的工具已經取代為適用於所有案例的單一解決方案︰Azure AD Connect。它提供新的功能、增強功能和新案例的支援。若要能夠繼續同步處理內部部署身分識別資料至 Azure AD 和 Office 365，強烈建議您升級至 Azure AD Connect。

最新版的 DirSync 發行於 2014 年 7 月，而最新版的 Azure AD Sync 發行於 2015 年 5 月。

## 何謂 Azure AD Connect
Azure AD Connect 是 DirSync 和 Azure AD Sync 的後續產品。它結合了兩者支援的所有案例。您可以在[整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md) 中進一步了解。

## 淘汰排程

日期 | 註解
 --- | ---
2016 年 4 月 13 日 | Windows Azure Active Directory Sync (“DirSync”) 和 Microsoft Azure Active Directory Sync (“Azure AD Sync”) 已宣布淘汰。
2017 年 4 月 13 日 | 支援結束。客戶必須先升級至 Azure AD Connect 才能開啟支援案例。

## 如何轉換為 Azure AD Connect
如果您正在執行 DirSync，有兩種方式可以升級︰就地升級和平行部署。對大多數的客戶，以及如果您擁有最新的作業系統和少於 50,000 個物件，建議採用就地升級。在其他情況下，建議執行平行部署，DirSync 組態會移至執行 Azure AD Connect 的新伺服器。

如果您使用 Azure AD Sync，建議採用就地升級。如果您想要，您也可以並行安裝新的 Azure AD Connect 伺服器，並且執行從 Azure AD 同步伺服器到 Azure AD Connect 的變換移轉。

方案 | 案例
----- | -----
[從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md) | <li>如果您有已在執行中的現有 DirSync 伺服器。</li>
[從 Azure AD Sync 升級](active-directory-aadconnect-upgrade-previous-version.md)| <li>如果您要從 Azure AD Sync 移動。</li>

如果您想要了解如何從 DirSync Azure AD Connect 執行就地升級，請參閱這個第 9 頻道視訊︰

> [AZURE.VIDEO azure-active-directory-connect-in-place-upgrade-from-legacy-tools]

## 常見問題集
**問：我是使用 Connect，卻收到來自 Azure 團隊及/或來自 Office 365 郵件中心的訊息。** 這項通知也會傳送給使用 Azure AD Connect 組建編號 1.0.*.0 (使用 1.1 發行前版本) 的客戶。Microsoft 建議客戶使用最新的 Azure AD Connect 版本。1.1 版的[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)功能可讓您持續輕鬆擁有最新的 Azure AD Connect 安裝版本。

**問︰DirSync/Azure AD Sync 會在 2017 年 4 月 13 日停止運作嗎？** 不會。這些工具不再能夠與 Azure AD 進行通訊的日期會在日後發佈。您將會在本主題中找到該資訊 (如果可供參閱)。

**問：哪些 DirSync 版本可以進行升級？** 目前使用的任何 DirSync 版本皆支援升級。

**問︰什麼是 FIM/MIM 的 Azure AD 連接器？** FIM/MIM 的 Azure AD 連接器**尚未**宣布淘汰。它目前在**功能凍結**狀態；不會新增任何功能，而且不會收到任何錯誤修正。Microsoft 建議使用它的客戶規劃從它移至 Azure AD Connect。強烈建議不要使用它啟動任何新的部署。此連接器會在未來宣布淘汰。

## 其他資源

* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

<!---HONumber=AcomDC_0629_2016-->