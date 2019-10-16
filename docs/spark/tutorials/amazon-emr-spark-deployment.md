---
title: Amazon EMR Spark에 .NET for Apache Spark 애플리케이션 배포
description: Amazon EMR Spark에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 살펴봅니다.
ms.date: 05/17/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 0eea5a40ae4643c7447e2f7281dc8b0db609ca79
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117949"
---
# <a name="deploy-a-net-for-apache-spark-application-to-amazon-emr-spark"></a>Amazon EMR Spark에 .NET for Apache Spark 애플리케이션 배포

이 자습서에서는 Amazon EMR Spark에 .NET for Apache Spark 애플리케이션을 배포하는 방법을 설명합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
>
> * Microsoft.Spark.Worker 준비
> * Spark .NET 앱 게시
> * Amazon EMR Spark에 앱 배포
> * 앱 실행

## <a name="prerequisites"></a>전제 조건

시작하기 전에 다음을 수행합니다.

* [AWS CLI](https://aws.amazon.com/cli/)를 다운로드합니다.
* [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 로컬 머신에 다운로드합니다. 이 도우미 스크립트는 나중에 .NET for Apache Spark 종속 파일을 Spark 클러스터의 작업자 노드에 복사하는 데 사용합니다.

## <a name="prepare-worker-dependencies"></a>작업자 종속성 준비

**Microsoft.Spark.Worker**는 Spark 클러스터의 개별 작업자 노드에 있는 백 엔드 구성 요소입니다. C# UDF(사용자 정의 함수)를 실행하려면 Spark는 .NET CLR를 시작하여 UDF를 실행하는 방법을 이해해야 합니다. **Microsoft.Spark.Worker**는 이 기능을 사용하도록 설정하는 Spark에 대한 클래스 컬렉션을 제공합니다.

1. 클러스터에 배포할 [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) Linux netcoreapp 릴리스를 선택합니다.

   예를 들어 `netcoreapp2.1`을 사용하는 `.NET for Apache Spark v0.1.0`이 필요한 경우 [Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz](https://github.com/dotnet/spark/releases/download/v0.1.0/Microsoft.Spark.Worker.netcoreapp2.1.linux-x64-0.1.0.tar.gz)를 다운로드합니다.

2. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: S3)에 `Microsoft.Spark.Worker.<release>.tar.gz` 및 [install-worker.sh](https://github.com/dotnet/spark/blob/master/deployment/install-worker.sh)를 업로드합니다.

## <a name="prepare-your-net-for-apache-spark-app"></a>.NET for Apache Spark 앱 준비

1. [시작](get-started.md) 자습서를 따라 앱을 빌드합니다.

2. Spark .NET 앱을 자체 포함으로 게시합니다.

   Linux에서 다음 명령을 실행합니다.

   ```dotnetcli
   dotnet publish -c Release -f netcoreapp2.1 -r ubuntu.16.04-x64
   ```

3. 게시된 파일에 대해 `<your app>.zip`을 생성합니다.

   `zip`을 사용하여 Linux에서 다음 명령을 실행합니다.

   ```bash
   zip -r <your app>.zip .
   ```

4. 클러스터가 액세스할 수 있는 분산 파일 시스템(예: S3)에 다음 항목을 업로드합니다.

   * `microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar`: 이 jar은 [Microsoft.Spark](https://www.nuget.org/packages/Microsoft.Spark/) NuGet 패키지의 일부로 포함되며 앱의 빌드 출력 디렉터리에 공동 배치됩니다.
   * `<your app>.zip`
   * 각 실행기의 작업 디렉터리에 배치할 파일(예: 모든 작업자에 액세스할 수 있는 공통 데이터 또는 종속성 파일) 또는 어셈블리(예: 앱에서 사용하는 사용자 정의 함수 또는 라이브러리가 포함된 DLL).

## <a name="deploy-to-amazon-emr-spark"></a>Amazon EMR Spark에 배포

[Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html)은 AWS에서 빅 데이터 프레임워크 실행을 간소화하는 관리형 클러스터 플랫폼입니다.

> [!NOTE] 
> Amazon EMR Spark는 Linux 기반입니다. 따라서 Amazon EMR Spark에 앱을 배포하려면 앱이 .NET Standard와 호환되며 [.NET Core 컴파일러](https://dotnet.microsoft.com/download)를 사용하여 앱을 컴파일하는지 확인합니다.

### <a name="deploy-microsoftsparkworker"></a>Microsoft.Spark.Worker 배포

이 단계는 클러스터를 만들 때만 필요합니다.

[부트스트랩 작업](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html)을 사용하여 클러스터를 만드는 동안 `install-worker.sh`를 실행합니다.

AWS CLI를 사용하여 Linux에서 다음 명령을 실행합니다.

```bash
aws emr create-cluster \
--name "Test cluster" \
--release-label emr-5.23.0 \
--use-default-roles \
--ec2-attributes KeyName=myKey \
--applications Name=Spark \
--instance-count 3 \
--instance-type m1.medium \
--bootstrap-actions Path=s3://mybucket/<some dir>/install-worker.sh,Name="Install Microsoft.Spark.Worker",Args=["aws","s3://mybucket/<some dir>/Microsoft.Spark.Worker.<release>.tar.gz","/usr/local/bin"]
```

## <a name="run-your-app"></a>앱 실행

Amazon EMR Spark에서 앱을 실행하는 두 가지 방법은 spark-submit 및 Amazon EMR Steps입니다.

### <a name="use-spark-submit"></a>spark-submit 사용

[spark-submit](https://spark.apache.org/docs/latest/submitting-applications.html) 명령을 사용하여 Amazon EMR Spark에 .NET for Apache Spark 작업을 제출할 수 있습니다.

1. 클러스터의 노드 중 하나로 `ssh`를 실행합니다.

2. `spark-submit`를 실행합니다.

   ```bash
   spark-submit \
   --master yarn \
   --class org.apache.spark.deploy.dotnet.DotnetRunner \
   --files <comma-separated list of assemblies that contain UDF definitions, if any> \
   s3://mybucket/<some dir>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar \
   s3://mybucket/<some dir>/<your app>.zip <your app> <app args>
   ```

### <a name="use-amazon-emr-steps"></a>Amazon EMR Steps 사용

[Amazon EMR Steps](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-submit-step.html)는 EMR 클러스터에 설치된 Spark 프레임워크에 작업을 제출하는 데 사용할 수 있습니다.

AWS CLI를 사용하여 Linux에서 다음 명령을 실행합니다.

```bash
aws emr add-steps \
--cluster-id j-xxxxxxxxxxxxx \
--steps Type=spark,Name="Spark Program",Args=[--master,yarn,--files,s3://mybucket/<some dir>/<udf assembly>,--class,org.apache.spark.deploy.dotnet.DotnetRunner,s3://mybucket/<some dir>/microsoft-spark-<spark_majorversion.spark_minorversion.x>-<spark_dotnet_version>.jar,s3://mybucket/<some dir>/<your app>.zip,<your app>,<app arg 1>,<app arg 2>,...,<app arg n>],ActionOnFailure=CONTINUE
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Amazon EMR Spark에 .NET for Apache Spark 애플리케이션을 배포했습니다. .NET for Apache Spark 예제 프로젝트를 진행하려면 GitHub로 이동합니다.

> [!div class="nextstepaction"]
> [.NET for Apache Spark 샘플](https://github.com/dotnet/spark/tree/master/examples)
