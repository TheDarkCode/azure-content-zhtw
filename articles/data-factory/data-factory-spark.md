<properties 
	pageTitle="從 Azure Data Factory 叫用 Spark 程式" 
	description="了解如何從 Azure Data Factory 使用 MapReduce 活動叫用 Spark 程式。" 
	services="data-factory" 
	documentationCenter="" 
	authors="spelluru" 
	manager="jhubbard" 
	editor="monicar"/>

<tags 
	ms.service="data-factory" 
	ms.workload="data-services" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="08/25/2016" 
	ms.author="spelluru"/>

# 從 Data Factory 叫用 Spark 程式
## 簡介
您可以使用 Data Factory 管線的 MapReduce 活動，在 HDInsight Spark 叢集上執行 Spark 程式。如需有關使用活動的詳細資訊，請在閱讀本文之前先參閱 [MapReduce 活動](data-factory-map-reduce.md)一文。

## GitHub 上的 Spark 範例
[Spark - Data Factory sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) 示範如何使用 MapReduce 活動叫用 Spark 程式。Spark 程式只是將資料從一個 Azure Blob 容器複製到另一個。

## Data Factory 實體
**Spark-ADF/src/ADFJsons** 資料夾包含 Data Factory 實體的檔案 (連結的服務、資料集、管線)。

這個範例有兩個**連結服務**︰Azure 儲存體和 Azure HDInsight。在 **StorageLinkedService.json** 中指定 Azure 儲存體名稱和金鑰值，以及在 **HDInsightLinkedService.json** 中指定 clusterUri、userName 和密碼。

這個範例中有兩個**資料集**︰**input.json** 和 **output.json**。這些檔案都位於 [資料集] 資料夾中。這些檔案代表 MapReduce 活動的輸入和輸出資料集

您可以在 **ADFJsons/Pipeline** 資料夾中找到範例管線。請檢閱管線以了解如何使用 MapReduce 活動來叫用 Spark 程式。

MapReduce 活動被設定為叫用 Azure 儲存體之 **adflibs** 容器中的 **com.adf.sparklauncher.jar** (在 StorageLinkedService.json 中指定)。這個程式的原始程式碼位於 Spark-ADF/src/main/java/com/adf/ 資料夾中，它會呼叫 spark-submit 並執行 Spark 作業。

> [AZURE.IMPORTANT] 
在使用範例之前，請先詳閱 [README.TXT](https://github.com/Azure/Azure-DataFactory/blob/master/Samples/Spark/README.txt) 以了解最新資訊及其他資訊。
>  
> 請搭配這個方法使用您自己的 HDInsight Spark 叢集，以使用 MapReduce 活動來叫用 Spark 程式。不支援使用隨選 HDInsight 叢集。


## 另請參閱
- [Hive 活動](data-factory-hive-activity.md)
- [Pig 活動](data-factory-pig-activity.md)
- [MapReduce 活動](data-factory-map-reduce.md)
- [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
- [叫用 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

<!---HONumber=AcomDC_0831_2016-->