---
title: ML.NET 자동화 ML API 사용 방법
description: ML.NET 자동화 ML API는 모델 빌드 프로세스를 자동화하고 배포 준비된 모델을 생성합니다. 자동화된 기계 학습 작업을 구성하기 위해 사용할 수 있는 옵션에 대해 알아보세요.
ms.date: 04/24/2019
ms.custom: mvc,how-to
ms.openlocfilehash: a7057337fb6ff19a1e402d7bf74a766b246ea3c1
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332714"
---
# <a name="how-to-use-the-mlnet-automated-machine-learning-api"></a>ML.NET 자동화 기계 학습 API 사용 방법

자동화된 기계 학습(AutoML)은 기계 학습을 데이터에 적용하는 프로세스를 자동화합니다. 데이터 세트가 있는 경우 AutoML **실험**을 실행하여 다른 데이터 기능화, 기계 학습 알고리즘, 하이퍼 매개 변수에 대해 반복하여 최상의 모델을 선택할 수 있습니다.

> [!NOTE]
> 이 항목은 현재 미리 보기 중인 ML.NET용 자동화된 기계 학습 API에 대해 다룹니다. 자료가 변경될 수 있습니다.

## <a name="load-data"></a>데이터 로드

자동화된 기계 학습은 [IDataView](xref:Microsoft.ML.IDataView)로 데이터 세트 불러오기를 지원합니다. 데이터의 형식은 탭으로 구분된 값(TSV) 파일과 쉼표로 구분된 값(CSV) 파일이 될 수 있습니다.

예:

```csharp
using Microsoft.ML;
using Microsoft.ML.AutoML;
    // ...
    MLContext mlContext = new MLContext();
    IDataView trainDataView = mlContext.Data.LoadFromTextFile<SentimentIssue>("my-data-file.csv", hasHeader: true);
```

## <a name="select-the-machine-learning-task-type"></a>기계 학습 작업 유형 선택
실험을 만들기 전에 해결하려는 기계 학습 문제의 유형을 파악합니다. 자동화 기계 학습에서는 다음 ML 작업을 지원합니다.

* 이진 분류
* 다중 클래스 분류
* 재발

## <a name="create-experiment-settings"></a>실험 설정 만들기

파악된 ML 작업 유형에 대한 실험 설정 만들기

* 이진 분류

  ```csharp
  var experimentSettings = new BinaryExperimentSettings();
  ```

* 다중 클래스 분류

  ```csharp
  var experimentSettings = new MulticlassExperimentSettings();
  ```

* 재발

  ```csharp
  var experimentSettings = new RegressionExperimentSettings();
  ```

## <a name="configure-experiment-settings"></a>실험 설정 구성

실험은 구성 기능이 뛰어납니다. 구성 설정 전체 목록은 [AutoML API 문서](https://docs.microsoft.com/dotnet/api/?view=automl-dotnet)를 참조하세요.

예를 들면 다음과 같습니다.

1. 실험을 실행할 수 있는 최대 시간을 지정합니다.

    ```csharp
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    ```

1. 완료를 예약하기 전에 실험을 취소할 취소 토큰을 사용합니다.

    ```csharp
    experimentSettings.CancellationToken = cts.Token;

    // Cancel experiment after the user presses any key
    CancelExperimentAfterAnyKeyPress(cts);
    ```

1. 다른 최적화 메트릭을 지정합니다.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.OptimizingMetric = RegressionMetric.MeanSquaredError;
    ```

1. `CacheDirectory` 설정은 AutoML 작업 중 학습된 모든 모델이 저장될 디렉터리의 포인터입니다. `CacheDirectory`가 null로 설정된 경우 모델은 디스크로 기록되는 대신 메모리에 유지됩니다.
 
    ```csharp
    experimentSettings.CacheDirectory = null;
    ```

1. 특정 트레이너를 사용하지 않도록 자동화된 ML을 지시합니다.

    최적화할 트레이너의 기본 목록은 작업당 탐색됩니다. 이 목록은 각 실험에 대해 수정할 수 있습니다. 예를 들어 데이터 세트에서 느리게 실행되는 트레이너는 목록에서 제거할 수 있습니다. 하나의 특정 트레이너 호출 `experimentSettings.Trainers.Clear()`를 최적화하려면 사용하려는 트레이너를 추가합니다.

    ```csharp
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.Trainers.Remove(RegressionTrainer.LbfgsPoissonRegression);
    experimentSettings.Trainers.Remove(RegressionTrainer.OnlineGradientDescent);
    ```

ML 작업당 지원되는 트레이너 목록은 아래의 해당 링크에서 확인할 수 있습니다.

* [지원되는 이진 분류 알고리즘](xref:Microsoft.ML.AutoML.BinaryClassificationTrainer)
* [지원되는 다중 클래스 분류 알고리즘](xref:Microsoft.ML.AutoML.MulticlassClassificationTrainer)
* [지원되는 회귀 알고리즘](xref:Microsoft.ML.AutoML.RegressionTrainer)

## <a name="optimizing-metric"></a>최적화 메트릭

위의 예와 같이 최적화 메트릭은 모델 학습 중 최적화할 메트릭을 결정합니다. 선택할 수 있는 최적화 메트릭은 사용자가 선택하는 작업 유형에 따라 결정됩니다. 다음은 사용 가능한 메트릭 목록입니다.

|[이진 분류](xref:Microsoft.ML.AutoML.BinaryClassificationMetric) | [다중 클래스 분류](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric) |[재발](xref:Microsoft.ML.AutoML.RegressionMetric)
|-- |-- |--
|정확도| LogLoss | RSquared
|AreaUnderPrecisionRecallCurve | LogLossReduction | MeanAbsoluteError
|AreaUnderRocCurve | MacroAccuracy | MeanSquaredError
|F1Score | MicroAccuracy | RootMeanSquaredError
|NegativePrecision | TopKAccuracy
|NegativeRecall |
|PositivePrecision
|PositiveRecall

## <a name="data-pre-processing-and-featurization"></a>데이터 사전 처리 및 기능화

> [!NOTE]
> 기능 열은 [`Boolean`](https://docs.microsoft.com/en-us/dotnet/api/system.boolean), [`Single`](https://docs.microsoft.com/en-us/dotnet/api/system.single) 및 [`String`](https://docs.microsoft.com/en-us/dotnet/api/system.string) 유형만 지원합니다.

데이터 사전 처리는 기본적으로 발생하며 사용자를 위해 다음 단계가 자동으로 수행됩니다.

1. 유용한 정보가 없는 기능 삭제

    학습 및 유효성 검사 세트에서 유용한 정보가 없는 기능 삭제 여기에는 모든 누락된 값, 모든 행 전체에서 동일한 값, 또는 카디널리티가 매우 높은(예: 해시, ID 또는 GUID) 기능이 포함됩니다.

1. 누락 값 표시 및 귀속

    데이터 형식에 대한 기본값으로 누락 값 셀을 채웁니다. 입력 열과 동일한 슬롯 개수로 표시기 기능을 추가합니다. 입력 열이 누락된 경우 추가된 표시기 기능의 값은 `1`이며, 그렇지 않으면 `0`입니다.

1. 추가 기능 생성
    
    텍스트 기능: 유니그램 및 트라이그램을 사용하는 BOW(Bag of words) 기능
    
    범주 기능: 카디널리티가 낮은 기능에 대한 원 핫 인코딩(One-hot encoding), 카디널리티가 높은 범주 기능에 대한 원 핫 해시 인코딩(one-hot-hash encoding)

1. 변환 및 인코딩

    범주 기능으로 변환된 매우 적은 고유 값이 있는 텍스트 기능 범주 기능의 카디널리티에 따라 원 핫 인코딩(One-hot encoding) 또는 원 핫 해시 인코딩(one-hot-hash encoding)을 수행합니다.

## <a name="exit-criteria"></a>종료 기준

작업을 완료하는 기준을 정의합니다.

1. 일정한 시간 후 종료 - 실험 설정에서 `MaxExperimentTimeInSeconds`를 사용하여 작업을 계속 실행할 수 있는 시간(초)를 정의할 수 있습니다.

1. 취소 토큰 시 종료 - 완료를 예정하기 전에 작업을 취소할 수 있는 취소 토큰을 사용할 수 있습니다.

    ```csharp
    var cts = new CancellationTokenSource();
    var experimentSettings = new RegressionExperimentSettings();
    experimentSettings.MaxExperimentTimeInSeconds = 3600;
    experimentSettings.CancellationToken = cts.Token;
    ```

## <a name="create-an-experiment"></a>실험 만들기

실험 설정을 구성했다면 실험을 만들 준비가 된 것입니다.

```csharp
RegressionExperiment experiment = mlContext.Auto().CreateRegressionExperiment(experimentSettings);
```

## <a name="run-the-experiment"></a>실험 실행

실험을 실행하면 데이터 전처리, 학습 알고리즘 선택 및 하이퍼 매개 변수 튜닝이 트리거됩니다. AutoML은 `MaxExperimentTimeInSeconds`에 도달하거나 실험이 종료되기 전까지 기능화, 학습 알고리즘 및 하이퍼 매개 변수 조합을 계속 생성합니다.

```csharp
ExperimentResult<RegressionMetrics> experimentResult = experiment
    .Execute(trainingDataView, LabelColumnName, progressHandler: progressHandler);
```

유효성 검사 데이터에서 통과하고 싶은 경우 `Execute()`에 대한 기타 오버로드, 열 목적을 나타내는 열 정보 또는 prefeaturizer를 살펴봅니다.

## <a name="training-modes"></a>학습 모드

### <a name="training-dataset"></a>학습 데이터 세트

AutoML은 학습 데이터를 제공할 수 있는 오버로드된 실험 Execute 메서드를 제공합니다. 내부적으로 자동화된 ML은 데이터를 학습-검증 분할로 나눕니다.

```csharp
experiment.Execute(trainDataView);   
```

### <a name="custom-validation-dataset"></a>사용자 지정 유효성 검사 데이터 세트

보통 시계열 데이터가 있는 케이스이기 때문에 임의 분할이 허용되지 않는 경우 사용자 지정 유효성 검사 데이터 세트를 사용합니다. 사용자 고유의 유효성 검사 데이터 세트를 지정할 수 있습니다. 이 모델은 하나 이상의 임의 데이터 세트 대신 지정된 유효성 검사 데이터 세트를 기준으로 평가됩니다.

```csharp
experiment.Execute(trainDataView, validationDataView);   
```

## <a name="explore-model-metrics"></a>모델 메트릭 탐색

ML 실험의 각 반복 후 해당 작업과 관련된 메트릭이 저장됩니다.

예를 들어, 최적으로 실행된 유효성 검사 메트릭에 액세스할 수 있습니다.

```csharp
RegressionMetrics metrics = experimentResult.BestRun.ValidationMetrics;
Console.WriteLine($"R-Squared: {metrics.RSquared:0.##}");
Console.WriteLine($"Root Mean Squared Error: {metrics.RootMeanSquaredError:0.##}");
```

다음은 ML 작업당 사용 가능한 모든 메트릭입니다.

* [이진 분류 메트릭](xref:Microsoft.ML.AutoML.BinaryClassificationMetric)
* [다중 클래스 분류 메트릭](xref:Microsoft.ML.AutoML.MulticlassClassificationMetric)
* [재발 메트릭](xref:Microsoft.ML.AutoML.RegressionMetric)

## <a name="see-also"></a>참고 항목

전체 코드 샘플 등에 대한 자세한 내용은 [dotnet/machinelearning-samples](https://github.com/dotnet/machinelearning-samples/tree/master#automate-mlnet-models-generation-preview-state) GitHub 리포지토리에 방문하세요.
