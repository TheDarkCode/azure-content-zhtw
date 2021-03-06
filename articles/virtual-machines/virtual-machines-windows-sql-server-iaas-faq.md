<properties
	pageTitle="Azure 虛擬機器上的 SQL Server 常見問題集 | Microsoft Azure"
	description="本文章提供在 Azure VM 上執行 SQL Server 的常見問題解答。"
	services="virtual-machines-windows"
	documentationCenter=""
	authors="v-shysun"
	manager="felixwu"
	editor=""
	tags="azure-service-management"/>

<tags
	ms.service="virtual-machines-windows"
	ms.devlang="na"
	ms.topic="article"
	ms.tgt_pltfrm="vm-windows-sql-server"
	ms.workload="infrastructure-services"
	ms.date="06/03/2016"
	ms.author="v-shysun"/>

# Azure 虛擬機器上的 SQL Server 常見問題集

本主題提供關於 [Azure 虛擬機器上的 SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/) 一些最常見的執行問題解答。

[AZURE.INCLUDE [支援免責聲明](../../includes/support-disclaimer.md)]

## 常見問題集

1. **如何使用 SQL Server 建立 Azure 虛擬機器？**

	做法有二種。最簡單的解決方法是建立包含 SQL Server 的虛擬機器。如需註冊 Azure 並從入口網站建立 SQL VM 的教學課程，請參閱[在 Azure 入口網站中佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。您也可以選擇手動在 VM 上安裝 SQL Server，並重複使用 [Azure 上透過軟體保證的授權流動性](https://azure.microsoft.com/pricing/license-mobility/)提供的內部部署授權。

1. **SQL VM 和 SQL Database 服務之間的差異為何？**

	從概念上來說，在 Azure 虛擬機器上執行 SQL Server 與在遠端資料中心中執行 SQL Server 並沒什麼不同。對比之下，[SQL Database](../sql-database/sql-database-technical-overview.md) 可提供資料庫即服務的功能。使用 SQL Database 時，您無法存取主控資料庫的機器。如需完整的比較，請參閱[選擇雲端 SQL Server 選項：Azure SQL (PaaS) Database 或 Azure VM 上的 SQL Server (IaaS)](../sql-database/sql-database-paas-vs-sql-server-iaas.md)。

1. **如何將內部部署 SQL Server 資料庫移轉至雲端？**

	首先，請使用 SQL Server 執行個體來建立 Azure 虛擬機器。然後將您的內部部署資料庫移轉至該執行個體。如需資料移轉策略，請參閱[將 SQL Server 資料庫移轉至 Azure VM 中的 SQL Server](virtual-machines-windows-migrate-sql.md)。

2. **是否可以變更已安裝的功能，或在相同的 VM 上安裝第二個 SQL Server 執行個體？**

	是。SQL Server 安裝媒體位於 **C** 磁碟機的資料夾中。您可從該位置執行 **Setup.exe** 來新增新的 SQL Server 執行個體，或變更機器上 SQL Server 的其他已安裝功能。

3. **如何將 Azure VM 中的 SQL Server 升級至新版本？**

	目前，在 Azure VM 中執行的 SQL Server 不提供任何就地升級。因此，請使用所需的 SQL Server 版本來建立新的 Azure 虛擬機器，然後使用標準[資料移轉技術](virtual-machines-windows-migrate-sql.md)，將資料庫移轉到新的伺服器。

4. **如何在 Azure VM 上安裝 SQL Server 授權版本？**

	將 SQL Server 安裝媒體複製到 Windows Server VM 上，然後在 VM 上安裝 SQL Server。基於授權原因，您必須具備 [Azure 上透過軟體保證的授權流動性](https://azure.microsoft.com/pricing/license-mobility/)。

5. **如果只用來待命/容錯移轉，仍必須支付 VM 的 SQL 成本嗎？**

	如果您要透過資源庫建立 SQL VM，就必須有個別的待命 SQL VM 授權，而這種授權的價格是相同的。如果您使用[授權流動性](https://azure.microsoft.com/pricing/license-mobility/)在虛擬機器上手動安裝 SQL Server，則可以選擇使用一個免費的被動 SQL 執行個體來進行容錯移轉。請檢閱相關限制和需求。

6. **如何將更新和 Service Pack 套用到 SQL Server VM 上？**

	虛擬機器可讓您控制主機電腦，包括套用更新的時間與方法。針對作業系統，您可以手動套用 Windows 更新，或是啟用名為[自動修補](virtual-machines-windows-classic-sql-automated-patching.md)的排程服務。自動修補會安裝任何標示為重要的更新，包括該類別目錄中的 SQL Server 更新。其他選擇性的 SQL Server 更新，則必須手動安裝。

7. **是否可以設定虛擬機器資源庫中未顯示的組態 (例如 Windows 2008 R2 + SQL Server 2012)？**

	否，針對包含 SQL Server 的虛擬機器資源庫映像，您必須選取其中一個提供的映像。

9. **如何在 Azure VM 上安裝 SQL 資料工具？**

	請從 [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013](https://www.microsoft.com/zh-TW/download/details.aspx?id=42313) 下載並安裝 SQL 資料工具。

## 資源

如需 Azure 虛擬機器上的 SQL Server 概觀，請觀看影片 [Azure VM is the best platform for SQL Server 2016 (Azure VM 是 SQL Server 2016 的最佳平台)](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016)。您也可以在 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)主題中，取得詳盡介紹。

其他資源包括：

- [在 Azure 入口網站中佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)
- [將資料庫移轉至 Azure VM 上的 SQL Server](virtual-machines-windows-migrate-sql.md)
- [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](virtual-machines-windows-sql-high-availability-dr.md)
- [Azure 虛擬機器中的 SQL Server 效能最佳作法](virtual-machines-windows-sql-performance.md)
- [Azure 虛擬機器中的 SQL Server 應用程式模式和開發策略](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md)

<!---HONumber=AcomDC_0727_2016-->