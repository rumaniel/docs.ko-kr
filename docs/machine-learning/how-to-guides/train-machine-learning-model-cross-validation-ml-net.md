---
title: 교차 유효성 검사를 사용하여 기계 학습 모델을 학습합니다.
description: 교차 유효성 검사를 사용하여 ML.NET에서 더 강력한 기계 학습 모델을 구축하는 방법을 알아봅니다. 교차 유효성 검사는 학습 데이터를 여러 파티션으로 분할하고 이 파티션에서 여러 알고리즘을 학습하는 학습 및 모델 평가 기법입니다.
ms.date: 08/29/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to,title-hack-0625
ms.openlocfilehash: f29103d0cf59cdec10a641b05ce359bf95c01ccd
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169054"
---
# <a name="train-a-machine-learning-model-using-cross-validation"></a>교차 유효성 검사를 사용하여 기계 학습 모델을 학습합니다.

교차 유효성 검사를 사용하여 ML.NET에서 더 강력한 기계 학습 모델을 학습하는 방법을 알아봅니다. 

교차 유효성 검사는 학습 데이터를 여러 파티션으로 분할하고 이 파티션에서 여러 알고리즘을 학습하는 학습 및 모델 평가 기법입니다. 이 기법은 학습 프로세스 밖에서 데이터를 유지하여 모델의 견고성을 높입니다. 보이지 않는 관찰에 대한 성능 향상 외에도, 데이터 제약 환경에서 데이터 세트가 더 적은 학습 모델에 효과적인 도구가 될 수 있습니다.

## <a name="the-data-and-data-model"></a>데이터 및 데이터 모델

다음 형식을 갖는 파일의 데이터를 가정합니다.

```text
Size (Sq. ft.), HistoricalPrice1 ($), HistoricalPrice2 ($), HistoricalPrice3 ($), Current Price ($)
620.00, 148330.32, 140913.81, 136686.39, 146105.37
550.00, 557033.46, 529181.78, 513306.33, 548677.95
1127.00, 479320.99, 455354.94, 441694.30, 472131.18
1120.00, 47504.98, 45129.73, 43775.84, 46792.41
```

데이터는 `HousingData` 같은 클래스로 모델링하고 [`IDataView`](xref:Microsoft.ML.IDataView)에 로드할 수 있습니다.

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

## <a name="prepare-the-data"></a>데이터 준비

데이터를 사용하여 기계 학습 모델을 빌드하기 전에 미리 처리합니다. 이 샘플에서는 `Size` 및 `HistoricalPrices` 열을 하나의 기능 벡터로 결합합니다. 이것은 [`Concatenate`](xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate*) 메서드를 사용하여 새 열 `Features`에 출력합니다. ML.NET 알고리즘에서 예상하는 형식으로 데이터를 가져오는 것 외에도, 열을 연결하면 개별 열 각각에 대해서가 아니라 연결된 열에 대해 한 번만 작업을 적용하므로 파이프라인에서 이후의 작업을 최적화합니다. 

열이 단일 벡터로 결합되면 [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*)가 `Features` 열에 적용되어 같은 0-1 범위에서 `Size` 및 `HistoricalPrices`를 가져옵니다. 

```csharp
// Define data prep estimator
IEstimator<ITransformer> dataPrepEstimator = 
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data prep transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// Transform data
IDataView transformedData = dataPrepTransformer.Transform(data);
```

## <a name="train-model-with-cross-validation"></a>교차 유효성 검사를 통한 모델 학습

데이터를 사전 처리한 후에는 모델을 학습합니다. 먼저 수행할 기계 학습 작업과 가장 밀접하게 연결되는 알고리즘을 선택합니다. 예측된 값이 연속 숫자 값이므로 이 작업은 회귀입니다. ML.NET이 구현한 회귀 알고리즘 중 하나는 [`StochasticDualCoordinateAscentCoordinator`](xref:Microsoft.ML.Trainers.SdcaRegressionTrainer) 알고리즘입니다. 교차 유효성 검사를 통해 모델을 학습하려면 [ `CrossValidate` ](xref:Microsoft.ML.RegressionCatalog.CrossValidate*) 메서드를 사용합니다. 

> [!NOTE]
> 이 샘플에서는 선형 회귀 모델을 사용하지만 CrossValidate는 ML.NET에서 변칙 검색을 제외한 모든 다른 기계 학습 모델에 적용할 수 있습니다.

```csharp
// Define StochasticDualCoordinateAscent algorithm estimator
IEstimator<ITransformer> sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Apply 5-fold cross validation
var cvResults = mlContext.Regression.CrossValidate(transformedData, sdcaEstimator, numberOfFolds: 5);
```

[`CrossValidate`](xref:Microsoft.ML.RegressionCatalog.CrossValidate*)는 다음 작업을 수행합니다.

1. `numberOfFolds` 매개 변수에 지정된 값에 부합하는 수의 파티션으로 데이터를 분할합니다. 각 파티션의 결과는 [`TrainTestData`](xref:Microsoft.ML.DataOperationsCatalog.TrainTestData) 개체입니다.
1. 모델은 학습 데이터 세트에 대해 지정된 기계 학습 알고리즘 평가자를 사용하여 각 파티션에 대해 학습됩니다.
1. 각 모델의 성능은 테스트 데이터 세트에 대해 [`Evaluate`](xref:Microsoft.ML.RegressionCatalog.Evaluate*) 메서드를 사용하여 평가됩니다. 
1. 각각의 모델에 대해 모델과 메트릭이 반환됩니다.

`cvResults`에 저장된 결과는 [`CrossValidationResult`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601) 개체의 컬렉션입니다. 이 개체는 각각 [`Model`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601.Model) 및 [`Metrics`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601.Metrics) 속성에서 액세스할 수 있는 학습 모델과 메트릭을 포함합니다. 이 샘플에서 `Model` 속성은[`ITransformer`](xref:Microsoft.ML.ITransformer) 형식이고 `Metrics` 속성은 [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) 형식입니다. 

## <a name="evaluate-the-model"></a>모델 평가

다양한 학습 모델에 대한 메트릭은 개별 [`CrossValidationResult`](xref:Microsoft.ML.TrainCatalogBase.CrossValidationResult%601) 개체의 `Metrics` 속성을 통해 액세스할 수 있습니다. 이 경우 [R 제곱 메트릭](https://en.wikipedia.org/wiki/Coefficient_of_determination)이 `rSquared` 변수를 통해 액세스 및 저장됩니다. 

```csharp
IEnumerable<double> rSquared = 
    cvResults
        .Select(fold => fold.Metrics.RSquared);
```

`rSquared` 변수의 콘텐츠를 검사할 경우 출력은 0-1 범위의 5개 값이며 1에 가까울수록 적합한 값입니다. R 제곱 같은 메트릭을 사용하여 가장 적합한 값에서 가장 부족한 값까지 모델을 선택합니다. 그런 다음, 최고 모델을 선택하여 예측하거나 추가적인 작업을 수행합니다.

```csharp
// Select all models
ITransformer[] models =
    cvResults
        .OrderByDescending(fold => fold.Metrics.RSquared)
        .Select(fold => fold.Model)
        .ToArray();

// Get Top Model
ITransformer topModel = models[0];
```
