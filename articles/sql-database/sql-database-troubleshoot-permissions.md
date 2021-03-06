<properties
	pageTitle="如何執行管理工作，例如重設管理密碼 |Microsoft Azure"
	description="描述如何在 SQL Database 中執行一般管理工作。例如，重設管理密碼，授與和移除存取權。"
	services="sql-database"
	documentationCenter=""
	authors="v-shysun"
	manager="felixwu"
	editor=""
	keywords="重設管理密碼"/>

<tags
	ms.service="sql-database"
	ms.workload="data-management"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/06/2016"
	ms.author="v-shysun"/>

# 如何在 Azure SQL Database 中執行重設管理密碼等一般管理工作
使用本主題中的步驟即可快速授與或移除 Azure SQL Database 的存取權。如需更完整的資訊，請參閱：

- [管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)
- [保護您的 SQL Database](sql-database-security.md)
- [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](https://msdn.microsoft.com/library/bb510589)


[AZURE.INCLUDE [支援免責聲明](../../includes/support-disclaimer.md)]

## 重設邏輯伺服器的系統管理員密碼

- 在 [Azure 入口網站](https://portal.azure.com)中，按一下 [SQL Server]、從清單中選取伺服器，然後按一下 [重設密碼]。

## 為協助確保只有授權的 IP 位址可以存取伺服器
- 請參閱[如何：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)。

## 若要在使用者資料庫中建立自主的資料庫使用者
- 使用 [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) 陳述式，並參閱[自主的資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。

## 若要使用 Azure Active Directory 驗證自主的資料庫使用者
- 請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](sql-database-aad-authentication.md)。

## 若要在虛擬 master 資料庫中建立高權限使用者的其他登入
- 使用 [CREATE LOGIN](https://msdn.microsoft.com/library/ms189751.aspx) 陳述式，並參閱[管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)的＜管理登入＞一節以獲得詳細資訊。

<!---HONumber=AcomDC_0713_2016-->