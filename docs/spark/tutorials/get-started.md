---
title: .NET for Apache Spark 시작
description: Windows에서 .NET Core를 사용하여 .NET for Apache Spark 앱을 실행하는 방법을 살펴봅니다.
ms.date: 06/27/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: c4dbce74d0d8c0a682250a8021d983ef2990971f
ms.sourcegitcommit: d7c298f6c2e3aab0c7498bfafc0a0a94ea1fe23e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72250318"
---
# <a name="tutorial-get-started-with-net-for-apache-spark"></a>자습서: .NET for Apache Spark 시작

이 자습서에서는 Windows에서 .NET Core를 사용하여 .NET for Apache Spark 앱을 실행하는 방법을 설명합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
>
> * .NET for Apache Spark를 위한 Windows 환경 준비
> * **Microsoft.Spark.Worker** 다운로드
> * 간단한 .NET for Apache Spark 애플리케이션 빌드 및 실행

## <a name="prepare-your-environment"></a>환경 준비

시작하기 전에 명령줄에서 `dotnet`, `java`, `mvn`, `spark-shell`을 실행할 수 있는지 확인합니다. 환경이 이미 준비된 경우 다음 섹션으로 건너뛸 수 있습니다. 임의 또는 모든 명령을 실행할 수 없는 경우 다음 단계를 수행합니다.

1. [.NET Core 2.1x SDK](https://dotnet.microsoft.com/download/dotnet-core/2.1)를 다운로드하여 설치합니다. SDK를 설치하면 `dotnet` 도구 체인이 PATH에 추가됩니다. PowerShell 명령 `dotnet --version`을 사용하여 설치를 확인합니다.

2. 최신 업데이트와 함께 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 또는 [Visual Studio 2019](https://visualstudio.microsoft.com/vs/preview/)를 설치합니다. Community, Professional 또는 Enterprise를 사용할 수 있습니다. Community 버전은 무료입니다.

   설치 중에 다음 워크로드를 선택합니다.
      * .NET 데스크톱 개발
          * 필요한 모든 구성 요소
          * .NET Framework 4.6.1 개발 도구
      * .NET Core 플랫폼 간 개발
          * 필요한 모든 구성 요소

3. [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)을 설치합니다.

    * 운영 체제에 적합한 버전을 선택합니다. 예를 들어 Windows x64 머신의 경우 **jdk-8u201-windows-x64.exe**를 선택합니다.
    * PowerShell 명령 `java -version`을 사용하여 설치를 확인합니다.

4. [Apache Maven 3.6.0+](https://maven.apache.org/download.cgi)를 설치합니다.
    * [Apache Maven 3.6.0](http://mirror.metrocast.net/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip)을 다운로드합니다.
    * 로컬 디렉터리로 추출합니다. 예: `c:\bin\apache-maven-3.6.0\`.
    * Apache Maven을 [PATH 환경 변수](https://www.java.com/en/download/help/path.xml)에 추가합니다. `c:\bin\apache-maven-3.6.0\`으로 추출한 경우 `c:\bin\apache-maven-3.6.0\bin`을 PATH에 추가합니다.
    * PowerShell 명령 `mvn -version`을 사용하여 설치를 확인합니다.

5. [Apache Spark 2.3 이상](https://spark.apache.org/downloads.html)을 설치합니다. Apache Spark 2.4 이상은 지원되지 않습니다.
    * [Apache Spark 2.3 이상](https://spark.apache.org/downloads.html)을 다운로드하여 [7-zip](https://www.7-zip.org/) 또는 [WinZip](https://www.winzip.com/)과 같은 도구를 사용하여 로컬 폴더에 추출합니다. 예를 들어 `c:\bin\spark-2.3.2-bin-hadoop2.7\`로 추출할 수 있습니다.
    * Apache Spark를 [PATH 환경 변수](https://www.java.com/en/download/help/path.xml)에 추가합니다. `c:\bin\spark-2.3.2-bin-hadoop2.7\`로 추출한 경우 `c:\bin\spark-2.3.2-bin-hadoop2.7\bin`을 PATH에 추가합니다.
    * `SPARK_HOME`이라는 [새 환경 변수](https://www.java.com/en/download/help/path.xml)를 추가합니다. `C:\bin\spark-2.3.2-bin-hadoop2.7\`로 추출한 경우 **변수 값**에 `C:\bin\spark-2.3.2-bin-hadoop2.7\`을 사용합니다.
    * 명령줄에서 `spark-shell`을 실행할 수 있는지 확인합니다.

6. [WinUtils](https://github.com/steveloughran/winutils)를 설정합니다.
    * [WinUtils 리포지토리](https://github.com/steveloughran/winutils)에서 **winutils.exe** 이진 파일을 다운로드합니다. Spark 배포의 컴파일에 사용된 Hadoop 버전을 선택합니다. 예를 들어 **Spark 2.3.2**에 **hadoop-2.7.1**을 사용합니다. Hadoop 버전은 Spark 설치 폴더 이름의 끝에 주석으로 처리됩니다.
    * **winutils.exe** 이진 파일을 선택한 디렉터리에 저장합니다. 예: `c:\hadoop\bin`.
    * `bin` 없이 **winutils.exe**가 있는 디렉터리를 반영하도록 `HADOOP_HOME`을 설정합니다. 예: `c:\hadoop`.
    * `%HADOOP_HOME%\bin`을 포함하도록 PATH 환경 변수를 설정합니다.

다음 섹션으로 이동하기 전에 명령줄에서 `dotnet`, `java`, `mvn`, `spark-shell`을 실행할 수 있는지 다시 확인합니다.

## <a name="download-the-microsoftsparkworker-release"></a>Microsoft.Spark.Worker 릴리스 다운로드

1. .NET for Apache Spark GitHub 릴리스 페이지에서 로컬 머신으로 [Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) 릴리스를 다운로드합니다. 예를 들어 `c:\bin\Microsoft.Spark.Worker\` 경로에 다운로드할 수 있습니다.

2. `DOTNET_WORKER_DIR`라는 [새 환경 변수](https://www.java.com/en/download/help/path.xml)를 만들고 **Microsoft.Spark.Worker**를 다운로드하여 추출한 디렉터리로 설정합니다. 예: `c:\bin\Microsoft.Spark.Worker`.

## <a name="clone-the-net-for-apache-spark-github-repo"></a>.NET for Apache Spark GitHub 리포지토리 복제

다음 [GitBash](https://gitforwindows.org/) 명령을 사용하여 머신에 .NET for Apache Spark 리포지토리를 복제합니다.

```bash
git clone https://github.com/dotnet/spark.git c:\github\dotnet-spark
```

## <a name="write-a-net-for-apache-spark-app"></a>.NET for Apache Spark 앱 작성

1. **Visual Studio**를 열고 **파일 > 새 프로젝트 만들기 > 콘솔 앱(.NET Core)** 으로 이동합니다. 애플리케이션 이름을 **HelloSpark**로 지정합니다.

2. [Microsoft.Spark NuGet 패키지](https://www.nuget.org/profiles/spark)를 설치합니다. NuGet 패키지 설치에 대한 자세한 내용은 [NuGet 패키지를 설치하는 다양한 방법](https://docs.microsoft.com/nuget/consume-packages/ways-to-install-a-package)을 참조하세요.

3. **솔루션 탐색기**에서 **Program.cs**를 열고 다음 C# 코드를 작성합니다.

   ```csharp
     var spark = SparkSession.Builder().GetOrCreate();
     var df = spark.Read().Json("people.json");
     df.Show();
   ```

4. 솔루션을 빌드합니다.

## <a name="run-your-net-for-apache-spark-app"></a>.NET for Apache Spark 앱 실행

1. **PowerShell**을 열고 앱이 저장된 폴더로 디렉터리를 변경합니다.

   ```powershell
   cd <your-app-output-directory>
   ```

2. 다음 콘텐츠를 사용하여 **people.json** 파일을 만듭니다.

   ```json
   {"name":"Michael"}
   {"name":"Andy", "age":30}
   {"name":"Justin", "age":19}
   ```

3. 다음 PowerShell 명령을 사용하여 앱을 실행합니다.

   ```powershell
    spark-submit `
    --class org.apache.spark.deploy.dotnet.DotnetRunner `
    --master local `
    microsoft-spark-2.4.x-<version>.jar `
    dotnet HelloSpark.dll
    ```

지금까지 .NET for Apache Spark 앱을 작성하고 실행했습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> * .NET for Apache Spark를 위한 Windows 환경 준비
> * **Microsoft.Spark.Worker** 다운로드
> * 간단한 .NET for Apache Spark 애플리케이션 빌드 및 실행

자세한 내용은 리소스 페이지를 참조하세요.
> [!div class="nextstepaction"]
> [.NET for Apache Spark 리소스](../resources/index.md)
