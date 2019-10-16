---
title: 모델 다시 학습
description: ML.NET에서의 모델 다시 학습 방법 알아보기
ms.date: 05/03/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 1628d0669d8a9e677ff39b5869d3802d89d96410
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67397710"
---
# <a name="re-train-a-model"></a>모델 다시 학습

ML.NET에서 기계 학습 모델을 다시 학습하는 방법을 알아봅니다.

세계 및 관련 데이터는 지속적으로 변화합니다. 이 때문에 모델도 변화와 업데이트가 필요합니다. ML.NET은 매번 처음부터 다시 시작하는 것이 아니라 이전의 경험을 바탕으로 학습된 모델 매개 변수를 시작점으로 사용하여 모델을 다시 학습하는 기능을 제공합니다.  

다음 알고리즘은 ML.NET에서 다시 학습 가능합니다.

- [AveragedPerceptronTrainer](xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer)
- [FieldAwareFactorizationMachineTrainer](xref:Microsoft.ML.Trainers.FieldAwareFactorizationMachineTrainer)
- [LbfgsLogisticRegressionBinaryTrainer](xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer)
- [LbfgsMaximumEntropyMulticlassTrainer](xref:Microsoft.ML.Trainers.LbfgsMaximumEntropyMulticlassTrainer)
- [LbfgsPoissonRegressionTrainer](xref:Microsoft.ML.Trainers.LbfgsPoissonRegressionTrainer)
- [LinearSvmTrainer](xref:Microsoft.ML.Trainers.LinearSvmTrainer)
- [OnlineGradientDescentTrainer](xref:Microsoft.ML.Trainers.OnlineGradientDescentTrainer)
- [SgdCalibratedTrainer](xref:Microsoft.ML.Trainers.SgdCalibratedTrainer)
- [SgdNonCalibratedTrainer](xref:Microsoft.ML.Trainers.SgdNonCalibratedTrainer)
- [SymbolicSgdLogisticRegressionBinaryTrainer](xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer)

## <a name="load-pre-trained-model"></a>미리 학습된 모델 로드

먼저, 미리 학습된 모델을 애플리케이션에 로드합니다. 학습 파이프라인 및 모델 로드에 대한 자세한 정보는 관련 [방법 문서](./consuming-model-ml-net.md)를 참조하세요.

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

// Define DataViewSchema of data prep pipeline and trained model
DataViewSchema dataPrepPipelineSchema, modelSchema;

// Load data preparation pipeline
ITransformer dataPrepPipeline = mlContext.Model.Load("data_preparation_pipeline.zip", out dataPrepPipelineSchema);

// Load trained model
ITransformer trainedModel = mlContext.Model.Load("ogd_model.zip", out modelSchema);
```

## <a name="extract-pre-trained-model-parameters"></a>미리 학습된 모델 매개 변수 추출

모델이 로드되면 미리 학습된 모델의 [`Model`](xref:Microsoft.ML.Data.PredictionTransformerBase`1.Model*) 속성에 액세스하여 학습된 모델 매개 변수를 추출합니다. 미리 학습된 모델은 [`LinearRegressionModelParameters`](xref:Microsoft.ML.Trainers.LinearRegressionModelParameters)를 출력하는 [`RegressionPredictionTransformer`](xref:Microsoft.ML.Data.RegressionPredictionTransformer%601)를 만드는 선형 회귀 모델 [`OnlineGradientDescentTrainer`](xref:Microsoft.ML.Trainers.OnlineGradientDescentTrainer)를 사용하여 학습되었습니다. 이러한 선형 회귀 모델 매개 변수에는 학습된 편차 및 가중치와 모델 계수가 포함됩니다. 이런 값은 다시 학습되는 새 모델의 시작점이 됩니다.

```csharp
// Extract trained model parameters
LinearRegressionModelParameters originalModelParameters = 
    ((ISingleFeaturePredictionTransformer<object>)trainedModel).Model as LinearRegressionModelParameters;
```

## <a name="re-train-model"></a>모델 다시 학습

모델을 다시 학습하는 프로세스는 모델 학습과 차이가 없습니다. 유일한 차이점은 데이터와 함께 [`Fit`](xref:Microsoft.ML.Trainers.OnlineLinearTrainer`2.Fit*) 메서드도 원래 학습한 모델 매개 변수를 입력을 취하고 이를 다시 학습 프로세스의 시작점으로 사용한다는 점입니다.  

```csharp
// New Data
HousingData[] housingData = new HousingData[]
{
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

//Load New Data
IDataView newData = mlContext.Data.LoadFromEnumerable<HousingData>(housingData);

// Preprocess Data
IDataView transformedNewData = dataPrepPipeline.Transform(newData);

// Retrain model
RegressionPredictionTransformer<LinearRegressionModelParameters> retrainedModel = 
    mlContext.Regression.Trainers.OnlineGradientDescent()
        .Fit(transformedNewData, originalModelParameters);
```

## <a name="compare-model-parameters"></a>모델 매개 변수 비교

다시 학습이 실제로 일어나는지 어떻게 알 수 있나요? 한 가지 방법으로 다시 학습한 모델의 매개 변수가 원래 모델의 것과 다른지 비교할 수 있습니다. 아래 코드 샘플은 다시 학습한 모델 가중치에 대해 원래 항목을 비교하고 콘솔에 이를 출력합니다.

```csharp
// Extract Model Parameters of re-trained model
LinearRegressionModelParameters retrainedModelParameters = retrainedModel.Model as LinearRegressionModelParameters;

// Inspect Change in Weights
var weightDiffs = 
    originalModelParameters.Weights.Zip(
        retrainedModelParameters.Weights, (original, retrained) => original - retrained).ToArray();

Console.WriteLine("Original | Retrained | Difference");
for(int i=0;i < weightDiffs.Count();i++)
{
    Console.WriteLine($"{originalModelParameters.Weights[i]} | {retrainedModelParameters.Weights[i]} | {weightDiffs[i]}");
}
```

아래 표는 출력의 모습을 보여 줍니다. 

|원래 색 | 다시 학습 | 차이 |
|---|---|---|
| 33039.86 | 56293.76 | -23253.9 |
| 29099.14 | 49586.03 | -20486.89 |
| 28938.38 | 48609.23 | -19670.85 |
| 30484.02 | 53745.43 | -23261.41 |
