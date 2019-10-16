---
title: Databricks에 .NET for Apache Spark 애플리케이션 배포
description: Databricks에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 살펴봅니다.
ms.date: 05/17/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 035a3c36337413153ee0370aec154d48b84a4711
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957244"
---
# <a name="deploy-a-net-for-apache-spark-application-to-databricks"></a>Databricks에 .NET for Apache Spark 애플리케이션 배포

이 자습서에서는 Databricks에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 설명합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
>
> - Microsoft.Spark.Worker 준비
> - Spark .NET 앱 게시
> - Databricks에 앱 배포
> - 앱 실행

## <a name="prerequisites"></a>전제 조건

시작하기 전에 다음을 수행합니다.

- [Databricks CLI](https://docs.databricks.com/user-guide/dev-tools/databricks-cli.html)를 다운로드합니다.
- [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 로컬 머신에 다운로드합니다. 이 도우미 스크립트는 나중에 .NET for Apache Spark 종속 파일을 Spark 클러스터의 작업자 노드에 복사하는 데 사용합니다.

## <a name="prepare-worker-dependencies"></a>작업자 종속성 준비

**Microsoft.Spark.Worker**는 Spark 클러스터의 개별 작업자 노드에 있는 백 엔드 구성 요소입니다. C# UDF(사용자 정의 함수)를 실행하려면 Spark는 .NET CLR를 시작하여 UDF를 실행하는 방법을 이해해야 합니다. **Microsoft.Spark.Worker**는 이 기능을 사용하도록 설정하는 Spark에 대한 클래스 컬렉션을 제공합니다.

1. 클러스터에 배포할 [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) Linux netcoreapp 릴리스를 선택합니다.

   예를 들어 `netcoreapp2.1`을 사용하는 `.NET for Apache Spark v0.1.0`이 필요한 경우 [Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz](https://github.com/dotnet/spark/releases/download/v0.1.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz)를 다운로드합니다.

2. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: DBFS)에 `Microsoft.Spark.Worker.<release>.tar.gz` 및 [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 업로드합니다.

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

4. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: DBFS)에 다음을 업로드합니다.

   - `microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar`: 이 jar은 [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet 패키지의 일부로 포함되며 앱의 빌드 출력 디렉터리에 공동 배치됩니다.
   - `<your app>.zip`
   - 각 실행기의 작업 디렉터리에 배치할 파일(예: 모든 작업자에 액세스할 수 있는 공통 데이터 또는 종속성 파일) 또는 어셈블리(예: 앱에서 사용하는 사용자 정의 함수 또는 라이브러리가 포함된 DLL).

## <a name="deploy-to-databricks"></a>Databricks에 배포

[Databricks](https://databricks.com)는 Apache Spark를 사용하여 클라우드 기반 빅 데이터 처리를 제공하는 플랫폼입니다.

> [!Note] 
> [Azure Databricks](https://azure.microsoft.com/services/databricks/) 및 [AWS Databricks](https://databricks.com/aws)는 Linux 기반입니다. 따라서 Databricks에 앱을 배포하려면 앱이 .NET Standard와 호환되며 [.NET Core 컴파일러](https://dotnet.microsoft.com/download)를 사용하여 앱을 컴파일하는지 확인합니다.

Databricks를 사용하면 .NET for Apache Spark 앱을 기존 활성 클러스터에 제출하거나 작업을 시작할 때마다 새 클러스터를 만들 수 있습니다. 이 작업을 수행하려면 .NET for Apache Spark 앱을 제출하기 전에 **Microsoft.Spark.Worker**를 설치해야 합니다.

### <a name="deploy-microsoftsparkworker"></a>Microsoft.Spark.Worker 배포

이 단계는 클러스터에 한 번만 필요합니다.

1. [db-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh) 및 [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh
)를 로컬 머신에 다운로드합니다.

2. 클러스터에 다운로드하여 설치할 **Microsoft.Spark.Worker** 릴리스를 가리키도록 **db-init.sh**를 수정합니다.

3. [Databricks CLI](https://docs.databricks.com/user-guide/dev-tools/databricks-cli.html)를 설치합니다.

4. Databricks CLI에 대한 [인증 세부 정보를 설정](https://docs.databricks.com/user-guide/dev-tools/databricks-cli.html#set-up-authentication)합니다.

5. 다음 명령을 사용하여 Databricks 클러스터에 파일을 업로드합니다.

   ```bash
   cd <path-to-db-init-and-install-worker>
   databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
   databricks fs cp install-worker.sh dbfs:/spark-dotnet/install-worker.sh
   ```

6. Databricks 작업 영역으로 이동합니다. 왼쪽 메뉴에서 **클러스터**를 선택한 후 **클러스터 만들기**를 선택합니다.

7. 클러스터를 적절히 구성한 후 **Init 스크립트**를 설정하고 클러스터를 만듭니다.

   ![스크립트 동작 이미지](./media/databricks-deployment/deployment-databricks-init-script.png)

## <a name="run-your-app"></a>앱 실행 

`set JAR` 또는 `spark-submit`을 사용하여 작업을 Databricks에 제출할 수 있습니다.

### <a name="use-set-jar"></a>JAR 설정 사용

[JAR 설정](https://docs.databricks.com/user-guide/jobs.html#create-a-job)을 사용하여 기존 활성 클러스터에 작업을 제출할 수 있습니다.

#### <a name="one-time-setup"></a>일 회 설정

1. Databricks 클러스터로 이동하여 왼쪽 메뉴에서 **작업**을 선택합니다. 그런 다음, **JAR 설정**을 선택합니다.

2. 해당하는 `microsoft-spark-<spark-version>-<spark-dotnet-version>.jar` 파일을 업로드합니다.

3. 매개 변수를 적절하게 설정합니다.

   | 매개 변수   | 값                                                |
   |-------------|------------------------------------------------------|
   | 기본 클래스  | org.apache.spark.deploy.dotnet.DotnetRunner          |
   | 인수   | /dbfs/apps/<your-app-name>.zip <your-app-main-class> |

4. 이전 섹션에서 **Init 스크립트**를 만든 기존 클러스터를 가리키도록 **클러스터**를 구성합니다.

#### <a name="publish-and-run-your-app"></a>앱 게시 및 실행

1. [Databricks CLI](https://docs.databricks.com/user-guide/dev-tools/databricks-cli.html)를 사용하여 Databricks 클러스터에 애플리케이션을 업로드합니다.

      ```bash
      cd <path-to-your-app-publish-directory>
      databricks fs cp <your-app-name>.zip dbfs:/apps/<your-app-name>.zip
      ```

2. 이 단계는 앱 어셈블리(예: 종속성과 함께 사용자 정의 함수를 포함하는 DLL)를 각 **Microsoft.Spark.Worker**의 작업 디렉터리에 배치해야 하는 경우에만 필요합니다.

   - Databricks 클러스터에 애플리케이션 어셈블리 업로드
      
      ```bash
      cd <path-to-your-app-publish-directory>
      databricks fs cp <assembly>.dll dbfs:/apps/dependencies
      ```

   - [db-init.sh](https://github.com/dotnet/spark/blob/master/deployment/db-init.sh)에서 앱 종속성 섹션의 주석 처리를 제거한 후 앱 종속성 경로를 가리키고 Databricks 클러스터에 업로드하도록 해당 섹션을 수정합니다.
   
      ```bash
      cd <path-to-db-init-and-install-worker>
      databricks fs cp db-init.sh dbfs:/spark-dotnet/db-init.sh
      ```
   
   - 클러스터를 다시 시작합니다.

3. Databricks 작업 영역에서 Databricks 클러스터로 이동합니다. **작업**에서 작업을 선택한 후 **지금 실행**을 선택하여 작업을 실행합니다.

### <a name="use-spark-submit"></a>spark-submit 사용

[spark-submit](https://spark.apache.org/docs/latest/submitting-applications.html) 명령을 사용하여 새 클러스터에 작업을 제출할 수 있습니다.

1. [작업을 만들고](https://docs.databricks.com/user-guide/jobs.html) **spark-submit 구성**을 선택합니다.

2. 다음 매개 변수를 사용하여 `spark-submit`을 구성합니다.

      ```bash
      ["--files","/dbfs/<path-to>/<app assembly/file to deploy to worker>","--class","org.apache.spark.deploy.dotnet.DotnetRunner","/dbfs/<path-to>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar","/dbfs/<path-to>/<app name>.zip","<app bin name>","app arg1","app arg2"]
      ```

3. Databricks 작업 영역에서 Databricks 클러스터로 이동합니다. **작업**에서 작업을 선택한 후 **지금 실행**을 선택하여 작업을 실행합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Databricks에 .NET for Apache Spark 애플리케이션을 배포했습니다. Databricks에 대해 자세히 알아보려면 Azure Databricks 설명서를 참조하세요.

> [!div class="nextstepaction"]
> [Azure Databricks 설명서](https://docs.microsoft.com/azure/azure-databricks/)
