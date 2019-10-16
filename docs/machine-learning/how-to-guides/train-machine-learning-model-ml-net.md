---
title: 모델 학습 및 평가
description: ML.NET을 사용한 기계 학습 모델 빌드, 메트릭 수집 및 성능 측정 방법을 알아봅니다. 기계 학습 모델은 새 데이터를 사용하여 예측을 수행하기 위해 학습 데이터에서 패턴을 식별합니다.
ms.date: 08/29/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to, title-hack-0625
ms.openlocfilehash: fc735f28bad91b9714d7e6bf2a9c7c620acacc4d
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929343"
---
# <a name="train-and-evaluate-a-model"></a>모델 학습 및 평가

ML.NET을 사용한 기계 학습 모델 빌드, 메트릭 수집 및 성능 측정 방법을 알아봅니다. 이 샘플에서는 회귀 모델을 학습하지만 개념은 대부분의 다른 알고리즘에 널리 적용할 수 있습니다.

## <a name="split-data-for-training-and-testing"></a>학습 및 테스트를 위한 데이터 분할

기계 학습 모델의 목표는 학습 데이터 안에서 패턴을 식별하는 것입니다. 이러한 패턴은 새 데이터를 사용하여 예측을 수행하는 데 사용됩니다.

데이터는 `HousingData` 같은 클래스로 모델링할 수 있습니다.

```csharp
public class HousingData
{
    [LoadColumn(0)]
    public float Size { get; set; }

    [LoadColumn(1, 3)]
    [VectorType(3)]
    public float[] HistoricalPrices { get; set; }

    [LoadColumn(4)]
    [ColumnName("Label")]
    public float CurrentPrice { get; set; }
}
```

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 데이터의 경우:

```csharp
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 600f,
        HistoricalPrices = new float[] { 100000f ,125000f ,122000f },
        CurrentPrice = 170000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 200000f, 250000f, 230000f },
        CurrentPrice = 225000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 126000f, 130000f, 200000f },
        CurrentPrice = 195000f
    },
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f,175000f,210000f },
        CurrentPrice = 205000f
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f },
        CurrentPrice = 210000f
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f },
        CurrentPrice = 180000f
    }
};
```

[`TrainTestSplit`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestSplit*) 메서드를 사용하여 데이터를 학습 및 테스트 집합으로 분할합니다. 그 결과는 학습 집합용 하나와 테스트 집합용 하나 등, 두 [`IDataView`](xref:Microsoft.ML.IDataView) 멤버를 갖는 [`TrainTestData`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestData) 개체가 됩니다. 데이터 분할 백분율은 `testFraction` 매개 변수로 결정됩니다. 아래 코드 조각은 원래 데이터의 20%를 테스트 집합용으로 보유합니다.

```csharp
DataOperationsCatalog.TrainTestData dataSplit = mlContext.Data.TrainTestSplit(data, testFraction: 0.2);
IDataView trainData = dataSplit.TrainSet;
IDataView testData = dataSplit.TestSet;
```

## <a name="prepare-the-data"></a>데이터 준비

기계 학습 모델로 학습하려면 먼저 데이터를 미리 처리해야 합니다. 데이터 준비에 대한 자세한 정보는 [데이터 준비 방법 문서](prepare-data-ml-net.md) 및 [`transforms page`](../resources/transforms.md)에서 확인할 수 있습니다.

ML.NET 알고리즘은 입력 열 형식에 제약 조건이 있습니다. 또한 값을 지정하지 않은 경우 입력 및 출력 열에 기본값을 사용합니다.

### <a name="working-with-expected-column-types"></a>예상한 열 형식 작업

ML.NET의 기계 학습 알고리즘은 입력으로 알려진 크기의 부동 소수점 벡터를 기대합니다. 모든 데이터가 이미 숫자 형식이고 다 함께 처리될 예정이라면(즉 이미지 픽셀) 데이터 모델에 [`VectorType`](xref:Microsoft.ML.Data.VectorTypeAttribute) 특성을 적용합니다. 

데이터의 일부가 숫자가 아니며 열마다 각기 다른 데이터 변환을 적용하려는 경우 모든 열이 처리된 뒤에 [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*) 메서드를 사용하여 모든 개별 열을 새 열에 출력되는 단일 기능 벡터로 결합합니다. 

다음 코드 조각은 `Size` 및 `HistoricalPrices` 열을 새 열 `Features`에 출력되는 단일 기능 벡터로 결합합니다. 배율에 차이가 있기 때문에 [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*)는 데이터 표준화를 위해 `Features` 열에 적용됩니다.

```csharp
// Define Data Prep Estimator
// 1. Concatenate Size and Historical into a single feature vector output to a new column called Features
// 2. Normalize Features vector
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", "Size", "HistoricalPrices")
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data prep transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(trainData);

// Apply transforms to training data
IDataView transformedTrainingData = dataPrepTransformer.Transform(trainData);
```

### <a name="working-with-default-column-names"></a>기본 열 이름 작업

지정하지 않은 경우 ML.NET 알고리즘은 기본 열 이름을 사용합니다. 모든 학습자는 알고리즘 입력을 위해 `featureColumnName` 매개 변수를 가지며 해당하는 경우 예상된 값에 대한 매개 변수 `labelColumnName`도 갖습니다. 이러한 값은 기본적으로 각각 `Features` 및 `Label`입니다. 

미리 처리하는 중에 [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*) 메서드를 사용하여 `Features`라는 새 열을 만들면 알고리즘의 매개 변수에서 기능 열을 지정할 필요가 없습니다. 미리 처리된 `IDataView`에 이미 존재하기 때문입니다. 레이블 열은 `CurrentPrice`이지만 데이터 모델에서 [`ColumnName`](xref:Microsoft.ML.Data.ColumnNameAttribute) 특성을 사용하므로 ML.NET이 `CurrentPrice` 열의 이름을 `Label`로 바꿉니다. 이 때문에 `labelColumnName` 매개 변수를 기계 학습 모델 평가자에 제공할 필요가 없습니다. 

기본 열 이름을 사용하지 않으려면 이후의 코드 조각에서 설명하는 것처럼 기계 학습 알고리즘 평가자를 정의할 때 기능과 레이블 열 이름을 매개 변수로 전달합니다.

```csharp
var UserDefinedColumnSdcaEstimator = mlContext.Regression.Trainers.Sdca(labelColumnName: "MyLabelColumnName", featureColumnName: "MyFeatureColumnName");
```

## <a name="train-the-machine-learning-model"></a>기계 학습 모델 학습

데이터를 미리 처리한 후에는 [`Fit`](xref:Microsoft.ML.Trainers.TrainerEstimatorBase`2.Fit*) 메서드를 사용하여 [`StochasticDualCoordinateAscent`](xref:Microsoft.ML.Trainers.SdcaRegressionTrainer) 회귀 알고리즘으로 기계 학습 모델을 학습합니다.

```csharp
// Define StochasticDualCoordinateAscent regression algorithm estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Build machine learning model
var trainedModel = sdcaEstimator.Fit(transformedTrainingData);
```

## <a name="extract-model-parameters"></a>모델 매개 변수 추출

모델을 학습한 후에는 검사 또는 재학습을 위해 학습한 [`ModelParameters`](xref:Microsoft.ML.Trainers.ModelParametersBase%601)를 추출합니다. [`LinearRegressionModelParameters`](xref:Microsoft.ML.Trainers.LinearRegressionModelParameters)는 편차와 학습된 계수 또는 학습된 모델의 가중치를 제공합니다. 

```csharp
var trainedModelParameters = trainedModel.Model as LinearRegressionModelParameters;
```

> [!NOTE]
> 다른 모델에는 해당 작업에 특정한 매개 변수가 있습니다. 예를 들어, [K-Means 알고리즘](xref:Microsoft.ML.Trainers.KMeansTrainer)은 무게 중심에 따라 클러스터에 데이터를 배치하며 [`KMeansModelParameters`](xref:Microsoft.ML.Trainers.KMeansModelParameters)에는 이러한 학습된 무게 중심을 저장하는 속성이 있습니다. 자세한 정보는 [`Microsoft.ML.Trainers` API 설명서](xref:Microsoft.ML.Trainers)에서 이름에 `ModelParameters`가 포함된 클래스를 찾아보세요. 

## <a name="evaluate-model-quality"></a>모델 품질 평가

최상의 모델을 선택하기 위해 테스트 데이터에서 성능을 반드시 평가해야 합니다. [`Evaluate`](xref:Microsoft.ML.RegressionCatalog.Evaluate*) 메서드를 사용하여 학습된 모델에 대한 여러 메트릭을 측정합니다.

> [!NOTE]
> `Evaluate` 메서드는 수행된 기계 학습 작업에 따라 다른 메트릭을 생성합니다. 자세한 정보는 [`Microsoft.ML.Data` API 설명서](xref:Microsoft.ML.Data)에서 이름에 `Metrics`가 포함된 클래스를 찾아보세요. 

```csharp
// Measure trained model performance
// Apply data prep transformer to test data
IDataView transformedTestData = dataPrepTransformer.Transform(testData);

// Use trained model to make inferences on test data
IDataView testDataPredictions = trainedModel.Transform(transformedTestData);

// Extract model metrics and get RSquared
RegressionMetrics trainedModelMetrics = mlContext.Regression.Evaluate(testDataPredictions);
double rSquared = trainedModelMetrics.RSquared;
```

앞의 코드 샘플에서:  

1. 테스트 데이터 세트는 앞에서 정의한 데이터 준비 변환을 통해 미리 처리됩니다. 
2. 학습된 기계 학습 모델을 사용하여 테스트 데이터에 대한 예측을 수행합니다.
3. `Evaluate` 메서드에서 테스트 데이터 세트의 `CurrentPrice` 열 값을 새 출력 예측의 `Score` 열과 비교하여 회귀 모델의 메트릭을 계산하는데, 이 중 하나인 R 제곱이 `rSquared` 변수에 저장됩니다.

> [!NOTE]
> 이 작은 예제에서 R 제곱은 데이터의 크기 제한으로 인해 0-1 범위에 있지 않은 숫자입니다. 실제 시나리오에서는 0과 1 사이의 값이 됩니다.
