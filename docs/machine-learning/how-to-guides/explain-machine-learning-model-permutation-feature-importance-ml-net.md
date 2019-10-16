---
title: 순열 기능 중요도를 사용하여 예측 모델 설명
description: ML.NET에서 순열 기능 중요도를 사용하여 모델의 기능 중요도 파악
ms.date: 08/29/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: 8090e4565a7e55aaa9cc9939e61eb728a169de8d
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736868"
---
# <a name="explain-model-predictions-using-permutation-feature-importance"></a>순열 기능 중요도를 사용하여 예측 모델 설명

PFI(순열 기능 중요도)를 사용한 예측에서 기능이 갖는 기여도를 해석하여 ML.NET 기계 학습 모델 예측을 설명하는 방법을 알아 봅니다.

기계 학습 모델은 종종 입력을 받아 출력을 생성하는 블랙 박스처럼 여겨지곤 합니다. 출력에 영향을 미치는 중간 단계 또는 기능 간 상호 작용은 거의 해석되지 않습니다. 의료 등, 다양한 일상에서 기계 학습의 도입이 증가하면서 기계 학습 모델이 그러한 의사 결정을 내리게 되는 이유를 해석하는 것이 매우 중요해졌습니다. 예를 들어, 기계 학습 모델에서 진단을 수행할 경우 의료 전문가가 해당 진단에 반영된 요소를 살펴볼 방법이 필요합니다. 올바른 진단을 제공하면 환자의 빠른 회복 여부에 큰 차이를 낼 수 있습니다. 따라서 모델의 설명 가능한 수준이 높을수록 의료 전문가는 더 자신 있게 모델의 의사 결정을 수락 또는 거부할 수 있습니다.

다양한 기법을 사용하여 모델을 설명하며, 그 방법 중 하나가 PFI입니다. PFI는 [Breiman의 *랜덤 포리스트* 논문](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)(섹션 10 참조)에서 착안한 분류 및 회귀 모델을 설명하는 데 사용되는 기법입니다. 높은 수준에서는, 전체 데이터 세트에 대해 한 번에 한 기능씩 임의로 데이터를 섞고 해당 성능 메트릭이 얼마나 감소하는지를 산출하는 방식으로 작동합니다. 변화가 클수록 해당 기능이 중요한 것입니다. 

또한 가장 중요한 기능을 강조 표시하므로 모델을 빌드하는 사람이 노이즈 및 학습 시간을 줄일 수 있는 더 의미 있는 기능의 하위 집합에 주력할 수 있습니다.

## <a name="load-the-data"></a>데이터 로드

이 샘플에 사용되는 데이터 세트의 기능은 1-12열에 있습니다. 목표는 `Price` 예측입니다. 

| Column | 기능 | 설명 
| --- | --- | --- |
| 1 | CrimeRate | 인당 범죄율
| 2 | ResidentialZones | 도시 내 주거지
| 3 | CommercialZones | 도시 내 비주거지
| 4 | NearWater | 수원 근접성
| 5 | ToxicWasteLevels | 독성 물질 수준(PPM)
| 6 | AverageRoomNumber | 가구 내 평균 방 수
| 7 | HomeAge | 가구 연령
| 8 | BusinessCenterDistance | 가장 가까운 비즈니스 지구까지 거리
| 9 | HighwayAccess | 고속도로 근접성
| 10 | TaxRate | 재산세율
| 11 | StudentTeacherRatio | 교사 학생 비율
| 12 | PercentPopulationBelowPoverty | 빈곤 인구 비율
| 13 | 가격 | 주택 가격

데이터 세트의 샘플은 다음과 같습니다.

```text
1,24,13,1,0.59,3,96,11,23,608,14,13,32
4,80,18,1,0.37,5,14,7,4,346,19,13,41
2,98,16,1,0.25,10,5,1,8,689,13,36,12
```

이 샘플의 데이터는 `HousingPriceData` 같은 클래스로 모델링하고 [`IDataView`](xref:Microsoft.ML.IDataView)에 로드할 수 있습니다.

```csharp
class HousingPriceData
{
    [LoadColumn(0)]
    public float CrimeRate { get; set; }

    [LoadColumn(1)]
    public float ResidentialZones { get; set; }

    [LoadColumn(2)]
    public float CommercialZones { get; set; }

    [LoadColumn(3)]
    public float NearWater { get; set; }

    [LoadColumn(4)]
    public float ToxicWasteLevels { get; set; }

    [LoadColumn(5)]
    public float AverageRoomNumber { get; set; }

    [LoadColumn(6)]
    public float HomeAge { get; set; }

    [LoadColumn(7)]
    public float BusinessCenterDistance { get; set; }

    [LoadColumn(8)]
    public float HighwayAccess { get; set; }

    [LoadColumn(9)]
    public float TaxRate { get; set; }

    [LoadColumn(10)]
    public float StudentTeacherRatio { get; set; }

    [LoadColumn(11)]
    public float PercentPopulationBelowPoverty { get; set; }

    [LoadColumn(12)]
    [ColumnName("Label")]
    public float Price { get; set; }
}
```

## <a name="train-the-model"></a>모델 학습

다음 코드 샘플은 선형 회귀 모델을 학습하여 주택 가격을 예측하는 프로세스를 보여 줍니다.

```csharp
// 1. Get the column name of input features.
string[] featureColumnNames = 
    data.Schema
        .Select(column => column.Name)
        .Where(columnName => columnName != "Label").ToArray();

// 2. Define estimator with data pre-processing steps
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", featureColumnNames)
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// 3. Create transformer using the data pre-processing estimator
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// 4. Pre-process the training data
IDataView preprocessedTrainData = dataPrepTransformer.Transform(data);

// 5. Define Stochastic Dual Coordinate Ascent machine learning estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// 6. Train machine learning model
var sdcaModel = sdcaEstimator.Fit(preprocessedTrainData);
```

## <a name="explain-the-model-with-permutation-feature-importance-pfi"></a>PFI(순열 기능 중요도)를 사용하여 모델 설명

ML.NET에서는 해당 작업에 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions) 메서드를 사용합니다.

```csharp
ImmutableArray<RegressionMetricsStatistics> permutationFeatureImportance = 
    mlContext
        .Regression
        .PermutationFeatureImportance(sdcaModel, preprocessedTrainData, permutationCount:3);
```

학습 데이터 세트에 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions)를 사용한 결과는 [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics) 개체의 [`ImmutableArray`](xref:System.Collections.Immutable.ImmutableArray)입니다. [`RegressionMetricsStatistics`](xref:Microsoft.ML.Data.RegressionMetricsStatistics)는 `permutationCount` 매개 변수에서 지정한 순열 수에 해당하는 여러 [`RegressionMetrics`](xref:Microsoft.ML.Data.RegressionMetrics) 관찰에 대해 평균, 표준 편차 같은 요약 통계를 제공합니다.

중요도, 이 경우 [`PermutationFeatureImportance`](xref:Microsoft.ML.PermutationFeatureImportanceExtensions)에서 계산한 R 제곱 메트릭의 절대 평균 감소를 가장 중요함에서 가장 중요하지 않음의 순서로 지정할 수 있습니다.  

```csharp
// Order features by importance
var featureImportanceMetrics =
    permutationFeatureImportance
        .Select((metric, index) => new { index, metric.RSquared })
        .OrderByDescending(myFeatures => Math.Abs(myFeatures.RSquared.Mean));

Console.WriteLine("Feature\tPFI");

foreach (var feature in featureImportanceMetrics)
{
    Console.WriteLine($"{featureColumnNames[feature.index],-20}|\t{feature.RSquared.Mean:F6}");
}
```

`featureImportanceMetrics`에서 각 기능에 대한 값을 출력하면 다음과 유사한 출력이 생성됩니다. 이 값은 제공된 데이터에 따라 달라지므로 결과가 다르게 보일 수 있습니다.  

| 기능 | R 제곱으로 변경 |
|:--|:--:|
HighwayAccess       |   -0.042731
StudentTeacherRatio |   -0.012730
BusinessCenterDistance| -0.010491
TaxRate             |   -0.008545
AverageRoomNumber   |   -0.003949
CrimeRate           |   -0.003665
CommercialZones     |   0.002749
HomeAge             |   -0.002426
ResidentialZones    |   -0.002319
NearWater           |   0.000203
PercentPopulationLivingBelowPoverty|    0.000031
ToxicWasteLevels    |   -0.000019

이 데이터 세트에 가장 중요한 기능 5개를 살펴보면 이 모델이 예측한 주택 가격은 고속도로 근접성, 지역 내 학교의 학생-교사 비율, 주요 업무 지구 근접성, 재산세율, 주택의 평균 방 수의 영향을 받습니다.
