---
title: 모델 구축에 사용할 데이터 준비
description: ML.NET에서 변형을 사용하여 추가 처리 또는 모델 빌드를 위해 데이터를 조작하고 준비하는 방법을 알아봅니다.
author: luisquintanilla
ms.author: luquinta
ms.date: 09/11/2019
ms.custom: mvc, how-to, title-hack-0625
ms.openlocfilehash: 4452aef351f33df532f3c673307dedbbf71631b8
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929368"
---
# <a name="prepare-data-for-building-a-model"></a>모델 구축에 사용할 데이터 준비

ML.NET을 사용하여 추가 처리 또는 모델 빌드를 위해 데이터를 준비하는 방법을 알아봅니다.

데이터는 정리되어 있지 않고 흩어져 있는 경우가 많습니다. ML.NET 기계 학습 알고리즘에서는 단일 숫자 벡터 형식의 입력 또는 기능을 예상합니다. 마찬가지로 예측할 값(레이블), 특히 범주 데이터의 경우에는 인코딩해야 합니다. 따라서 데이터를 준비하는 목적 중 하나가 ML.NET 알고리즘에서 예상하는 형식으로 데이터를 가져오는 것입니다. 

## <a name="filter-data"></a>데이터 필터링

데이터 세트의 일부 데이터는 분석하기에 관련성이 없는 경우가 있습니다. 관련 없는 데이터를 제거하는 접근법이 필터링입니다. [`DataOperationsCatalog`](xref:Microsoft.ML.DataOperationsCatalog)에는 모든 데이터를 포함하는 [`IDataView`](xref:Microsoft.ML.IDataView)에서 수행하여 관심 있는 데이터 요소만 포함하는 [IDataView](xref:Microsoft.ML.IDataView)를 반환하는 일련의 필터 작업 세트가 있습니다. 필터 작업이 [`TransformsCatalog`](xref:Microsoft.ML.TransformsCatalog)의 것과 같은 [`IEstimator`](xref:Microsoft.ML.IEstimator%601) 또는 [`ITransformer`](xref:Microsoft.ML.ITransformer)가 아니므로, [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) 또는 [`TransformerChain`](xref:Microsoft.ML.Data.TransformerChain%601) 데이터 준비 파이프라인으로 포함할 수는 없습니다. 

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 입력 데이터 사용:

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

열 값에 기반하여 데이터를 필터링하려면 [`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) 메서드를 사용합니다.

```csharp
// Apply filter
IDataView filteredData = mlContext.Data.FilterRowsByColumn(data, "Price", lowerBound: 200000, upperBound: 1000000);
```

위의 샘플에서는 데이터 세트에서 가격대가 200000 ~ 1000000인 행을 가져옵니다. 이 필터를 적용하면 데이터에서 마지막 두 개 행만 반환되고 첫 행은 가격이 100000이고 지정한 범위에 속하지 않으므로 제외됩니다.

## <a name="replace-missing-values"></a>누락된 값 대체

데이터 세트에서 값이 누락되는 경우는 일반적입니다. 누락된 값을 다루는 접근법 중 하나는 데이터에서 평균 값 등 다른 의미 있는 값인 경우 지정된 유형에 대한 기본 값으로 대체하는 것입니다. 

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 입력 데이터 사용:

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=float.NaN
    }
};
```

목록의 마지막 요소에 `Price`에 대한 누락된 값이 있습니다. `Price` 열의 누락된 값을 대체하려면 [`ReplaceMissingValues`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) 메서드를 사용하여 이 누락된 값을 채우세요.

> [!IMPORTANT]
> [`ReplaceMissingValue`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*)은 숫자 데이터에만 작용합니다.

```csharp
// Define replacement estimator
var replacementEstimator = mlContext.Transforms.ReplaceMissingValues("Price", replacementMode: MissingValueReplacingEstimator.ReplacementMode.Mean);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer replacementTransformer = replacementEstimator.Fit(data);

// Transform data
IDataView transformedData = replacementTransformer.Transform(data);
```

ML.NET은 다양한 [대체 모드](xref:Microsoft.ML.Transforms.MissingValueReplacingEstimator.ReplacementMode) 지원합니다. 위의 샘플에서는 해당 열의 평균 값으로 누락된 값을 채울 `Mean` 대체 모드를 사용합니다. 대체하면 데이터에서 100,000과 300,000의 평균인 200,000으로 마지막 요소에 대한 `Price` 속성을 채웁니다. 

## <a name="use-normalizers"></a>노멀라이저 사용

[정규화](https://en.wikipedia.org/wiki/Feature_scaling)는 알고리즘이 보다 빠르게 수렴할 수 있도록 동일한 척도가 아닌 기능을 표준화하는 데 사용하는 데이터 사전 처리 기법입니다. 예를 들어, 나이와 수입과 같은 값의 범위는 나이가 일반적으로 0-100 범위, 수입이 0에서 수천 범위로 상당히 다양합니다. 정규화 변형에 대한 보다 자세한 목록과 설명은 [변형 페이지](../resources/transforms.md)를 참조하세요. 

### <a name="min-max-normalization"></a>최소-최대 정규화

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 입력 데이터 사용:

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms = 2f,
        Price = 200000f
    },
    new HomeData
    {
        NumberOfBedrooms = 1f,
        Price = 100000f
    }
};
```

정규화는 단일 숫자 값뿐 아니라 벡터를 포함하는 열에도 적용할 수 있습니다. [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*) 메서드를 사용하는 최소-최대 정규화를 통해 `Price` 열의 데이터를 정규화합니다.

```csharp
// Define min-max estimator
var minMaxEstimator = mlContext.Transforms.NormalizeMinMax("Price");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer minMaxTransformer = minMaxEstimator.Fit(data);

// Transform data
IDataView transformedData = minMaxTransformer.Transform(data);
```

원래 가격 값 `[200000,100000]`은 0-1 범위에서 출력 값을 생성하는 `MinMax` 정규화 공식을 사용하여 `[ 1, 0.5 ]`로 변환됩니다.

### <a name="binning"></a>범주화

[범주화](https://en.wikipedia.org/wiki/Data_binning)는 연속적인 값을 별도의 값 표현으로 변환합니다. 예를 들어, 기능 중 하나가 나이라고 가정하면 범주화는 실제 나이 값 대신, 해당 값의 범위를 만듭니다. 0-18, 19-35 등이 각 범주가 될 수 있습니다. 

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 입력 데이터 사용:

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

[`NormalizeBinning`](xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning*) 메서드를 사용하여 데이터를 bin으로 정규합니다. `maximumBinCount` 매개 변수를 사용하면 데이터를 분류하는 데 필요한 bin 수를 지정할 수 있습니다. 이 예에서는 데이터가 2개의 bin으로 분류됩니다.  

```csharp
// Define binning estimator
var binningEstimator = mlContext.Transforms.NormalizeBinning("Price", maximumBinCount: 2);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
var binningTransformer = binningEstimator.Fit(data);

// Transform Data
IDataView transformedData = binningTransformer.Transform(data);
```

범주화 결과로, `[0,200000,Infinity]`의 bin 범위가 만들어집니다. 따라서 첫 번째 관찰 값이 0-200000이고 나머지가 200000보다 크지만, 무한보다는 적기 때문에 결과로 만들지는 bin은 `[0,1,1]`입니다.

## <a name="work-with-categorical-data"></a>범주 데이터 작업

숫자 이외의 범주 데이터는 기계 학습 모델을 빌드하는 데 사용하려면 숫자로 변환되어야 합니다. 

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드되는 다음 입력 데이터 사용:

```csharp
CarData[] cars = new CarData[] 
{
    new CarData
    {
        Color="Red",
        VehicleType="SUV"
    },
    new CarData
    {
        Color="Blue",
        VehicleType="Sedan"
    },
    new CarData
    {
        Color="Black",
        VehicleType="SUV"
    }
};
```

범주 `VehicleType` 속성은 [`OneHotEncoding`](xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*) 메서드를 사용해 숫자로 변환할 수 있습니다. 

```csharp
// Define categorical transform estimator
var categoricalEstimator = mlContext.Transforms.Categorical.OneHotEncoding("VehicleType");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer categoricalTransformer = categoricalEstimator.Fit(data);

// Transform Data
IDataView transformedData = categoricalTransformer.Transform(data);
```

결과로 만들어지는 변형은 `VehicleType`의 텍스트 값을 숫자로 변환합니다. `VehicleType` 열의 항목은 변형이 적용되면 다음이 됩니다. 

```text
[
    1, // SUV
    2, // Sedan
    1 // SUV
]
```

## <a name="work-with-text-data"></a>텍스트 데이터 작업

텍스트 데이터는 기계 학습 모델을 빌드하기 위해 사용하려면 숫자로 변형되어야 합니다. 텍스트 변형에 대한 보다 자세한 목록과 설명은 [변형 페이지](../resources/transforms.md)를 참조하세요.

[`IDataView`](xref:Microsoft.ML.IDataView)로 로드된 아래 데이터와 같은 데이터 사용:

```csharp
ReviewData[] reviews = new ReviewData[]
{
    new ReviewData
    {
        Description="This is a good product",
        Rating=4.7f
    },
    new ReviewData
    {
        Description="This is a bad product",
        Rating=2.3f
    }
};
```

텍스트를 숫자 벡터 표현으로 변형하는 최소 단계는 [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) 메서드를 사용하는 것입니다. [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) 변형을 사용하여, 입력 텍스트 열에 일련의 변형이 적용되면 lg 정규화된 단어 및 문자 n그램을 나타내는 숫자 벡터가 만들어집니다. 

```csharp
// Define text transform estimator
var textEstimator  = mlContext.Transforms.Text.FeaturizeText("Description");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer textTransformer = textEstimator.Fit(data);

// Transform data
IDataView transformedData = textTransformer.Transform(data);
```

결과로 만들어지는 변형은 `Description` 열의 텍스트 값을 아래 출력과 유사하게 보이는 숫자 벡터로 변환합니다.

```text
[ 0.2041241, 0.2041241, 0.2041241, 0.4082483, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0, 0, 0, 0, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0 ]
```

복잡한 텍스트 처리 단계를 [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601)으로 통합하여 노이즈를 제거하고 필요에 따라 필요한 처리량을 줄일 수도 있습니다.

```csharp
// Define text transform estimator
var textEstimator = mlContext.Transforms.Text.NormalizeText("Description")
    .Append(mlContext.Transforms.Text.TokenizeIntoWords("Description"))
    .Append(mlContext.Transforms.Text.RemoveDefaultStopWords("Description"))
    .Append(mlContext.Transforms.Conversion.MapValueToKey("Description"))
    .Append(mlContext.Transforms.Text.ProduceNgrams("Description"))
    .Append(mlContext.Transforms.NormalizeLpNorm("Description"));
```

`textEstimator`에는 [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) 메서드에서 수행하는 작업의 하위 세트가 있습니다. 보다 복잡한 파이프라인의 이점은 데이터에 적용되는 변형에 대한 제어와 가시성입니다. 

다음은 예로 첫 번째 항목을 사용하여 `textEstimator`에서 정의하는 변형 단계에서 생성되는 결과에 대한 자세한 설명입니다.

**원문: This is a good product**

|변형 | 설명 | 결과
|--|--|--|
|1. NormalizeText | 모든 문자를 기본적으로 소문자로 변환합니다. | this is a good product
|2. TokenizeWords | 문자를 개별 단어로 분할합니다. | ["this","is","a","good","product"]
|3. RemoveDefaultStopWords | *is* 및 *a*와 같은 불용어를 제거합니다. | ["good","product"]
|4. MapValueToKey | 입력 데이터에 기반하여 값을 키(범주)에 매핑합니다. |  [1,2]
|5. ProduceNGrams | 텍스트를 연속 단어 시퀀스로 변형합니다. | [1,1,1,0,0]
|6. NormalizeLpNorm | lp-norm으로 입력 크기를 조정합니다. | [ 0.577350529, 0.577350529, 0.577350529, 0, 0 ]
