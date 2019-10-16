---
title: Azure HDInsight에 .NET for Apache Spark 애플리케이션 배포
description: HDInsight에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 살펴봅니다.
ms.date: 05/17/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 2e8da5497035a83fde75bf91a7d21437d510b480
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117976"
---
# <a name="deploy-a-net-for-apache-spark-application-to-azure-hdinsight"></a>Azure HDInsight에 .NET for Apache Spark 애플리케이션 배포

이 자습서에서는 Azure HDInsight에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 설명합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
>
> * Microsoft.Spark.Worker 준비
> * Spark .NET 앱 게시
> * Azure HDInsight에 앱 배포
> * 앱 실행

## <a name="prerequisites"></a>전제 조건

시작하기 전에 다음을 수행합니다.

* [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/)를 다운로드합니다.
* [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 로컬 머신에 다운로드합니다. 이 도우미 스크립트는 나중에 .NET for Apache Spark 종속 파일을 Spark 클러스터의 작업자 노드에 복사하는 데 사용합니다.

## <a name="prepare-worker-dependencies"></a>작업자 종속성 준비

**Microsoft.Spark.Worker**는 Spark 클러스터의 개별 작업자 노드에 있는 백 엔드 구성 요소입니다. C# UDF(사용자 정의 함수)를 실행하려면 Spark는 .NET CLR를 시작하여 UDF를 실행하는 방법을 이해해야 합니다. **Microsoft.Spark.Worker**는 이 기능을 사용하도록 설정하는 Spark에 대한 클래스 컬렉션을 제공합니다.

1. 클러스터에 배포할 [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) Linux netcoreapp 릴리스를 선택합니다.

   예를 들어 `netcoreapp2.1`을 사용하는 `.NET for Apache Spark v0.1.0`이 필요한 경우 [Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz](https://github.com/dotnet/spark/releases/download/v0.1.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz)를 다운로드합니다.

2. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: HDFS, WASB, ADLS)에 `Microsoft.Spark.Worker.<release>.tar.gz` 및 [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 업로드합니다.

## <a name="prepare-your-net-for-apache-spark-app"></a>.NET for Apache Spark 앱 준비

1. [시작](get-started.md) 자습서를 따라 앱을 빌드합니다.

2. Spark .NET 앱을 자체 포함으로 게시합니다.

   Linux에서 다음 명령을 실행할 수 있습니다.

   ```dotnetcli
   dotnet publish -c Release -f netcoreapp2.1 -r ubuntu.16.04-x64
   ```

3. 게시된 파일에 대해 `<your app>.zip`을 생성합니다.

   `zip`을 사용하여 Linux에서 다음 명령을 실행할 수 있습니다.

   ```bash
   zip -r <your app>.zip .
   ```

4. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: HDFS, WASB, ADLS)에 다음을 업로드합니다.

   * `microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar`: 이 jar은 [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet 패키지의 일부로 포함되며 앱의 빌드 출력 디렉터리에 공동 배치됩니다.
   * `<your app>.zip`
   * 각 실행기의 작업 디렉터리에 배치할 파일(예: 모든 작업자에 액세스할 수 있는 공통 데이터 또는 종속성 파일) 또는 어셈블리(예: `app`에서 사용하는 사용자 정의 함수 또는 라이브러리가 포함된 DLL).

## <a name="deploy-to-azure-hdinsight-spark"></a>Azure HDInsight Spark에 배포

[Azure HDInsight Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-overview)는 사용자가 Azure에서 Spark 클러스터를 시작하고 구성할 수 있는 클라우드에 있는 Apache Spark의 Microsoft 구현입니다. 따라서 HDInsight Spark 클러스터를 사용하여 [Azure Storage](https://azure.microsoft.com/services/storage/) 또는 [Azure Data Lake Storage](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-data-lake-storage-gen2)에 저장된 데이터를 처리할 수 있습니다.

> [!NOTE]
> Azure HDInsight Spark는 Linux 기반입니다. Azure HDInsight Spark에 앱을 배포하려면 앱이 .NET Standard와 호환되며 [.NET Core 컴파일러](https://dotnet.microsoft.com/download)를 사용하여 앱을 컴파일하는지 확인합니다.

### <a name="deploy-microsoftsparkworker"></a>Microsoft.Spark.Worker 배포

이 단계는 클러스터에 한 번만 필요합니다.

[HDInsight 스크립트 동작](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)을 사용하여 클러스터에서 `install-worker.sh`를 실행합니다.

|설정|값|
|-------|-----|
|스크립트 유형|사용자 지정|
|name|Microsoft.Spark.Worker 설치|
|Bash 스크립트 URI|`install-worker.sh`를 업로드한 URI입니다. 예를 들면 `abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/install-worker.sh`과 같습니다.|
|노드 유형|작업자|
|매개 변수|`install-worker.sh`에 대한 매개 변수입니다. 예를 들어 `install-worker.sh`를 Azure Data Lake Gen 2에 업로드한 경우 `azure abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/Microsoft.Spark.Worker.<release>.tar.gz /usr/local/bin`입니다.|

![스크립트 동작 이미지](./media/hdinsight-deployment/deployment-hdi-action-script.png)

## <a name="run-your-app"></a>앱 실행

`spark-submit` 또는 Apache Livy를 사용하여 Azure HDInsight에 작업을 제출할 수 있습니다.

### <a name="use-spark-submit"></a>spark-submit 사용

[spark-submit](https://spark.apache.org/docs/latest/submitting-applications.html) 명령을 사용하여 Azure HDInsight에 .NET for Apache Spark 작업을 제출할 수 있습니다.
 
1. 클러스터의 헤드 노드 중 하나로 `ssh`를 실행합니다.

1. `spark-submit`를 실행합니다.

   ```bash
   spark-submit \
   --master yarn \
   --class org.apache.spark.deploy.dotnet.DotnetRunner \
   --files <comma-separated list of assemblies that contain UDF definitions, if any> \
   abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar \
   abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/<your app>.zip <your app> <app arg 1> <app arg 2> ... <app arg n>
   ```

### <a name="use-apache-livy"></a>Apache Livy 사용

Apache Spark REST API인 [Apache Livy](https://livy.incubator.apache.org/)를 사용하여 Azure HDInsight Spark 클러스터에 .NET for Apache Spark 작업을 제출할 수 있습니다. 자세한 내용은 [Apache Livy를 사용한 원격 작업](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-livy-rest-interface)을 참조하세요.

`curl`을 사용하여 Linux에서 다음 명령을 실행할 수 있습니다.

```bash
curl -k -v -X POST "https://<your spark cluster>.azurehdinsight.net/livy/batches" \
-u "<hdinsight username>:<hdinsight password>" \
-H "Content-Type: application/json" \
-H "X-Requested-By: <hdinsight username>" \
-d @- << EOF
{
    "file":"abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar",
    "className":"org.apache.spark.deploy.dotnet.DotnetRunner",
    "files":["abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/<udf assembly>", "abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/<file>"],
    "args":["abfss://<your-file-system-name>@<your-storage-account-name>.dfs.core.windows.net/<some dir>/<your app>.zip","<your app>","<app arg 1>","<app arg 2>,"...","<app arg n>"]
}
EOF
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Azure HDInsight에 .NET for Apache Spark 애플리케이션을 배포했습니다. HDInsight에 대해 자세히 알아보려면 Azure HDInsight 설명서를 참조하세요.

> [!div class="nextstepaction"]
> [Azure HDInsight 설명서](https://docs.microsoft.com/azure/hdinsight/)
