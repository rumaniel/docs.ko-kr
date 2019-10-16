---
title: '자습서: 아이리스 꽃 분류 - k-means 클러스터링'
description: 클러스터링 시나리오에서 ML.NET을 사용하는 방법 알아보기
author: pkulikov
ms.date: 09/30/2019
ms.topic: tutorial
ms.custom: mvc, seodec18, title-hack-0516
ms.openlocfilehash: e360cf2418e2003f9f40628c714e9e8ebd7c3e40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698554"
---
# <a name="tutorial-categorize-iris-flowers-using-k-means-clustering-with-mlnet"></a>자습서: ML.NET와 함께 k-means 클러스터링을 사용하여 아이리스 꽃 분류

이 자습서에서는 ML.NET을 사용하여 [아이리스 꽃 데이터 집합](https://en.wikipedia.org/wiki/Iris_flower_data_set)을 위해 [클러스터링 모델](../resources/tasks.md#clustering)을 빌드하는 방법을 보여줍니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> - 문제 이해
> - 적절한 기계 학습 작업 선택
> - 데이터 준비
> - 데이터 로드 및 변환
> - 학습 알고리즘 선택
> - 모델 학습
> - 예측에 모델 사용

## <a name="prerequisites"></a>전제 조건

- “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).

## <a name="understand-the-problem"></a>문제 이해

이 문제는 꽃 특징을 기반으로 아이리스 꽃 집합을 여러 그룹으로 나누는 것에 관한 것입니다. 그 특징은 꽃받침의 길이 및 너비와 꽃잎의 길이 및 너비입니다. 이 자습서에서는 각 꽃 유형이 알려지지 않은 것으로 가정합니다. 특정으로부터 데이터 집합의 구조를 파악하고 데이터 인스턴스가 이 구조에 어떻게 맞는지 예측해보려 합니다.

## <a name="select-the-appropriate-machine-learning-task"></a>적절한 기계 학습 작업 선택

각 꽃이 속한 그룹을 모르기 때문에 [감독되지 않는 기계 학습](../resources/glossary.md#unsupervised-machine-learning) 작업을 선택합니다. 같은 그룹의 요소를 다른 그룹의 요소보다 더 서로 유사한 방식으로 그룹의 데이터 집합을 나누려면 [클러스터링](../resources/tasks.md#clustering) 기계 학습 작업을 사용합니다.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

1. Visual Studio를 엽니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. **새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **.NET Core** 노드를 차례로 선택합니다. 그런 다음 **콘솔 앱(.NET Core)** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 "IrisFlowerClustering"을 입력한 다음, **확인** 단추를 선택합니다.

1. 프로젝트에서 *Data* 디렉터리를 만들어 데이터 집합과 모델 파일을 저장합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. “Data”를 입력하고 Enter 키를 누릅니다.

1. **Microsoft.ML** NuGet 패키지를 설치합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. "nuget.org"를 패키지 소스로 선택하고, **찾아보기** 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 **v1.0.0** 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

## <a name="prepare-the-data"></a>데이터 준비

1. [iris.data](https://github.com/dotnet/machinelearning/blob/master/test/data/iris.data) 데이터 집합을 다운로드하고 이전 단계에서 만든 *Data* 폴더에 저장합니다. 아이리스 데이터 집합에 대한 자세한 내용은 [아이리스 꽃 데이터 집합](https://en.wikipedia.org/wiki/Iris_flower_data_set) Wikipedia 페이지와 데이터 집합의 출처인 [아이리스 데이터 집합](https://archive.ics.uci.edu/ml/datasets/Iris) 페이지를 참조하세요.

1. **솔루션 탐색기**에서 *iris.data* 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

*iris.data* 파일에는 다음을 나타내는 5개의 열이 있습니다.

- 꽃받침 길이(cm)
- 꽃받침 너비(cm)
- 꽃잎 길이(cm)
- 꽃잎 너비(cm)
- 아이리스 꽃의 종류

클러스터링 예제에서 이 자습서는 마지막 열을 무시합니다.

## <a name="create-data-classes"></a>데이터 클래스 만들기

입력 데이터 및 예측에 대한 클래스를 만듭니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *IrisData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.
1. 새 파일에 다음 `using` 지시문을 추가합니다.

   [!code-csharp[Add necessary usings](~/samples/machine-learning/tutorials/IrisFlowerClustering/IrisData.cs#Usings)]

기존 클래스 정의를 제거하고 `IrisData` 및 `ClusterPrediction` 클래스를 정의하는 다음 코드를 *IrisData.cs* 파일에 추가합니다.

[!code-csharp[Define data classes](~/samples/machine-learning/tutorials/IrisFlowerClustering/IrisData.cs#ClassDefinitions)]

`IrisData`는 입력 데이터 클래스이며 각 데이터 집합의 각 특징에 대한 정의를 포함합니다. [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute) 특성을 사용하여 데이터 세트 파일에서 소스 열의 인덱스를 지정합니다.

`ClusterPrediction` 클래스는 `IrisData` 인스턴스에 적용된 클러스터링 모델의 출력을 나타냅니다. [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute) 속성을 사용하여 `PredictedClusterId` 및 `Distances` 필드를 각각 **PredictedLabel** 및 **Score** 열에 바인딩합니다. 클러스터링 작업의 경우 이들 열의 의미는 다음과 같습니다.

- **PredictedLabel**열에는 예측된 클러스터의 ID가 있습니다.
- **Score** 열에는 클러스터 중심까지 제곱 유클리드 거리가 있는 배열이 포함됩니다. 배열 길이는 클러스터와 같습니다.

> [!NOTE]
> `float` 유형을 사용하여 입력 및 예측 데이터 클래스에서 부동 소수점 값을 나타냅니다.

## <a name="define-data-and-model-paths"></a>데이터 및 모델 경로 정의

*Program.cs* 파일로 돌아가서 두 개의 필드를 추가하여 데이터 집합 파일에 대한 경로와 모델을 저장할 파일에 대한 경로를 저장합니다.

- `_dataPath`에는 모델을 학습하는 데 사용되는 데이터 집합이 있는 파일에 대한 경로가 포함됩니다.
- `_modelPath`에는 학습된 모델이 저장되는 파일에 대한 경로가 포함됩니다.

`Main` 메서드 바로 위에 다음 코드를 추가하여 해당 경로를 지정합니다.

[!code-csharp[Initialize paths](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#Paths)]

위의 코드를 컴파일하려면 *Program.cs* 파일의 맨 위에 있는 다음 `using` 지시문을 추가합니다.

[!code-csharp[Add usings for paths](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#UsingsForPaths)]

## <a name="create-ml-context"></a>ML 컨텍스트 만들기

*Program.cs* 파일 맨 위에 다음 추가 `using` 지시문을 추가합니다.

[!code-csharp[Add Microsoft.ML usings](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#MLUsings)]

`Main` 메서드에서 `Console.WriteLine("Hello World!");` 줄을 다음 코드로 바꿉니다.

[!code-csharp[Create ML context](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#CreateContext)]

<xref:Microsoft.ML.MLContext?displayProperty=nameWithType> 클래스는 기계 학습 환경 연결을 나타내며 데이터 로드, 모델 학습, 예측 및 기타 작업에 대한 로깅 및 진입점에 대한 메커니즘을 제공합니다. 이는 Entity Framework에서 `DbContext`를 사용하는 것과 개념이 비슷합니다.

## <a name="setup-data-loading"></a>데이터 로드 설정

`Main` 메서드에 다음 코드를 추가하여 데이터를 로드하는 방법을 설정합니다.

[!code-csharp[Create text loader](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#CreateDataView)]

제네릭 [`MLContext.Data.LoadFromTextFile` 확장 메서드](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)는 제공된 `IrisData` 형식에서 데이터 세트 스키마를 유추하고 변환기의 입력으로 사용할 수 있는 <xref:Microsoft.ML.IDataView>를 반환합니다.

## <a name="create-a-learning-pipeline"></a>학습 파이프라인 만들기

이 자습서의 경우 클러스터링 작업의 학습 파이프라인은 다음 두 단계로 구성됩니다.

- 로드된 열을 클러스터링 교육 담당자가 사용하는 하나의 **기능** 열로 연결합니다.
- <xref:Microsoft.ML.Trainers.KMeansTrainer> 교육 담당자를 사용하여 k-means++ 클러스터링 알고리즘을 사용하는 모델을 학습합니다.

`Main` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Create pipeline](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#CreatePipeline)]

코드는 데이터 세트를 3개의 클러스터로 분할해야 함을 지정합니다.

## <a name="train-the-model"></a>모델 학습

이전 섹션에서 추가된 단계는 교육을 위한 파이프라인을 준비했지만 아무 것도 실행되지 않았습니다. 다음 줄을 `Main` 메서드에 추가하여 데이터 로드 및 모델 학습을 수행합니다.

[!code-csharp[Train the model](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#TrainModel)]

### <a name="save-the-model"></a>모델 저장

이 시점에 기존 또는 새 .NET 애플리케이션에 통합할 수 있는 모델이 있습니다. 모델을 .zip 파일로 저장하려면 `Main` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Save the model](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#SaveModel)]

## <a name="use-the-model-for-predictions"></a>예측에 모델 사용

예측을 수행하려면 변환기 파이프라인을 통해 입력 형식의 인스턴스를 사용하고 출력 형식의 인스턴스를 생성하는 <xref:Microsoft.ML.PredictionEngine%602> 클래스를 사용합니다. 다음 줄을 `Main` 메서드에 추가하여 해당 클래스의 인스턴스를 만듭니다.

[!code-csharp[Create predictor](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#Predictor)]

[PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)은 데이터의 단일 인스턴스에 대한 예측을 수행할 수 있는 편리한 API입니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 단일 스레드 또는 프로토타입 환경에서 사용할 수 있습니다. 프로덕션 환경에서 성능 및 스레드 보안을 개선하려면 `PredictionEnginePool` 서비스를 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다. [ASP.NET Core 웹 API에서 `PredictionEnginePool`을 사용하는 방법](https://docs.microsoft.com/en-us/dotnet/machine-learning/how-to-guides/serve-model-web-api-ml-net#register-predictionenginepool-for-use-in-the-application)에 대한 자세한 내용은 이 가이드를 참조하세요.

> [!NOTE]
> `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

테스트 데이터 인스턴스를 수용할 수 있도록 `TestIrisData` 클래스를 만듭니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *TestIrisData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.
1. 다음 예제처럼 클래스를 static으로 수정합니다.

   [!code-csharp[Make class static](~/samples/machine-learning/tutorials/IrisFlowerClustering/TestIrisData.cs#Static)]

이 자습서에서는 이 클래스 내에 하나의 아이리스 데이터 인스턴스를 소개합니다. 이 모델로 실험할 다른 시나리오를 추가할 수 있습니다. 다음 코드를 `TestIrisData` 클래스에 추가합니다.

[!code-csharp[Test data](~/samples/machine-learning/tutorials/IrisFlowerClustering/TestIrisData.cs#TestData)]

지정된 항목이 속한 클러스터를 찾으려면 *Program.cs* 파일로 돌아가 다음 코드를 `Main` 메서드에 추가합니다.

[!code-csharp[Predict and output results](~/samples/machine-learning/tutorials/IrisFlowerClustering/Program.cs#PredictionExample)]

프로그램을 실행하여 지정된 데이터 인스턴스가 포함된 클러스터와 해당 인스턴스에서 클러스터 중심까지 제곱 거리를 확인합니다. 다음과 같은 결과가 나타나야 합니다.

```text
Cluster: 2
Distances: 11.69127 0.02159119 25.59896
```

지금까지 이제 아이리스 클러스터링을 위한 기계 학습 모델을 성공적으로 구축하고 예측을 위해 사용했습니다. [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/IrisFlowerClustering) GitHub 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - 문제 이해
> - 적절한 기계 학습 작업 선택
> - 데이터 준비
> - 데이터 로드 및 변환
> - 학습 알고리즘 선택
> - 모델 학습
> - 예측에 모델 사용

학습을 계속하고 더 많은 샘플을 찾으려면 GitHub 리포지토리를 체크 아웃하세요.
> [!div class="nextstepaction"]
> [dotnet/machinelearning GitHub 리포지토리](https://github.com/dotnet/machinelearning/)
