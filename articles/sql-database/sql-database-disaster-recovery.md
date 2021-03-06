<properties 
   pageTitle="SQL Database 災害復原 | Microsoft Azure" 
   description="了解如何使用 Azure SQL Database 的主動式異地複寫和異地還原功能，從區域資料中心中斷或失敗情況復原資料庫。" 
   services="sql-database" 
   documentationCenter="" 
   authors="CarlRabeler" 
   manager="jhubbard" 
   editor="monicar"/>

<tags
   ms.service="sql-database"
   ms.devlang="NA"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA" 
   ms.date="07/20/2016"
   ms.author="carlrab"/>

# 還原 Azure SQL Database 或容錯移轉到次要資料庫

Azure SQL Database 提供下列功能，以從中斷復原：

- [主動式異地複寫](sql-database-geo-replication-overview.md)
- [異地還原](sql-database-recovery-using-backups.md#point-in-time-restore)

若要了解商務持續性案例，以及支援這些案例的功能，請參閱[商務持續性](sql-database-business-continuity.md)。

### 準備中斷事件

如果要使用主動式異地複寫或異地備援備份成功復原到另一個資料區域，您必須準備一台伺服器，以便在另一個資料中心中斷時成為新的主要伺服器，以及將定義好的步驟寫成文件並經過測試，以確保順利復原。這些準備步驟包括︰

- 識別在另一個區域中要成為新主要伺服器的邏輯伺服器。至少要有一部或者每部次要伺服器都具有主動式異地複寫。如果是異地還原，這通常會是在資料庫所在區域的[配對區域](../best-practices-availability-paired-regions.md)中的伺服器。
- 識別並選擇性地定義所需的伺服器層級防火牆規則，讓使用者可以存取新的主要資料庫。
- 決定要如何重新導向使用者至新的主要伺服器，例如變更連接字串或變更 DNS 項目。
- 識別並選擇性地建立登入，新主要伺服器的 master 資料庫中必須有這些登入，並確保這些登入在 master 資料庫中有適當的權限 (如果有的話)。如需詳細資訊，請參閱[災害復原後的 SQL Database 安全性](sql-database-geo-replication-security-config.md)
- 識別需要更新的警示規則以對應至新的主要資料庫。
- 將目前主要資料庫上的稽核設定整理成文件
- 執行[災害復原演練](sql-database-disaster-recovery-drills.md)。若要模擬異地還原中斷，您可以刪除或重新命名來源資料庫，讓應用程式連線失敗。若要模擬主動式異地複寫中斷，您可以停用 Web 應用程式或連接到資料庫的的虛擬機器，或是容錯移轉資料庫，讓應用程式連線失敗。

## 何時起始復原

復原作業會影響應用程式。它需要變更 SQL 連接字串，或使用 DNS 重新導向，並且可能會導致永久的資料遺失。因此，只有在中斷情況可能持續超過應用程式的復原時間目標時，才應該執行這項作業。將應用程式部署至生產環境之後，您應該定期監視應用程式健全狀況，並利用下列資料點判斷是否需要復原：

1.	從應用程式層到資料庫的連接發生永久性失敗。
2.	Azure 入口網站顯示有關區域中影響廣泛之事件的警示。
3.	Azure SQL Database 伺服器標示為已降級。

視您應用程式的停機容忍度和可能的商務責任而定，您可以考慮下列復原選項。

使用[取得可復原資料庫](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) 以取得異地複寫的最近還原點。

## 等候服務復原

Azure 團隊會努力儘快還原服務可用性，但需視根本原因而言，有可能需要數小時或數天的時間。如果您的應用程式可以容忍長時間停機，您可以等待復原完成。在此情況下，您不需要採取任何動作。您可以在 [Azure 服務健康狀態儀表板](https://azure.microsoft.com/status/)上看見目前的服務狀態。在區域復原後，您應用程式的可用性將會還原。

## 容錯移轉至異地複寫的次要資料庫

如果您應用程式的停機可能會導致商務責任，您應該在應用程式中使用異地複寫的資料庫。這可讓應用程式在發生中斷時，快速還原不同區域的可用性。了解如何[設定異地複寫](sql-database-geo-replication-portal.md)。

若要還原資料庫的可用性，您必須使用其中一種支援的方法，開始容錯移轉到異地複寫的次要資料庫。

使用下列其中一份指南，容錯移轉至異地複寫的次要資料庫：

- [使用 Azure 入口網站容錯移轉至異地複寫的次要資料庫](sql-database-geo-replication-portal.md)
- [使用 PowerShell 容錯移轉至異地複寫的次要資料庫](sql-database-geo-replication-powershell.md)
- [使用 T-SQL 容錯移轉至異地複寫的次要資料庫](sql-database-geo-replication-transact-sql.md)

## 使用異地還原進行復原

如果您應用程式的停機不會導致任何商務責任，您可以使用異地還原做為復原應用程式資料庫的方法。它會從其最新的異地備援備份建立資料庫的複本。

使用下列其中一份指南，將資料庫異地還原到新的區域︰

- [使用 Azure 入口網站將資料庫異地還原到新的區域](sql-database-geo-restore-portal.md)
- [使用 PowerShell 將資料庫異地還原到新的區域](sql-database-geo-restore-powershell.md)

## 在復原之後設定資料庫

如果您使用異地複寫容錯移轉或異地復原來從中斷復原，您必須確定已正確設定新資料庫的連接，才能繼續執行正常的應用程式功能。以下工作檢查清單可協助您準備產生復原的資料庫。

### 更新連接字串

因為復原的資料庫將位於不同的伺服器，所以您必須更新應用程式的連接字串以指向該伺服器。

如需變更連接字串的詳細資訊，請參閱[連線庫](sql-database-libraries.md)的適當開發語言。

### 設定防火牆規則

您需要確認伺服器和資料庫上設定的防火牆規則符合主要伺服器與主要資料庫上設定的防火牆規則。如需詳細資訊，請參閱[如何：進行防火牆設定 (Azure SQL Database)](sql-database-configure-firewall-settings.md)。


### 設定登入和資料庫使用者

您需要確定應用程式使用的所有登入，都存在於主控已復原資料庫的伺服器上。如需詳細資訊，請參閱[異地複寫的安全性設定](sql-database-geo-replication-security-config.md)。

>[AZURE.NOTE] 您應該在災害復原演練期間設定和測試伺服器防火牆規則與登入 (及其權限)。這些伺服器層級物件及其設定可能無法在中斷期間使用。

### 設定遙測警示

您必須確定現有的警示規則設定已更新，才能對應至復原的資料庫和不同的伺服器。

如需資料庫警示規則的詳細資訊，請參閱[接收警示通知](../azure-portal/insights-receive-alert-notifications.md)和[追蹤服務健全狀況](../azure-portal/insights-service-health.md)。

### 啟用稽核

如果需要稽核才能存取您的資料庫，則您必須在資料庫復原之後啟用稽核。用戶端應用程式必須在 *.database.secure.windows.net 的模式中使用安全連接字串，才能有良好的稽核指標。如需詳細資訊，請參閱[開始使用 SQL 資料庫稽核](sql-database-auditing-get-started.md)。


## 後續步驟

- 若要了解 Azure SQL Database 自動備份，請參閱 [SQL Database 自動備份](sql-database-automated-backups.md)
- 若要了解商務持續性設計及復原案例，請參閱[持續性案例](sql-database-business-continuity.md)
- 若要了解如何使用自動備份進行復原，請參閱[從服務起始的備份還原資料庫](sql-database-recovery-using-backups.md)

<!---HONumber=AcomDC_0803_2016-->