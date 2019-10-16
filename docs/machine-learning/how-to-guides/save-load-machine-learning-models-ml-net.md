---
title: 학습된 모델 저장 및 로드
description: 학습된 모델 저장 및 로드 방법 알아보기
ms.date: 05/03/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: e3d4a51ceaf707d30c5072b91d7baf7fe02ef433
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65065586"
---
# <a name="save-and-load-trained-models"></a>학습된 모델 저장 및 로드

애플리케이션에서 학습된 모델을 저장 및 로드하는 방법을 알아봅니다. 

모델 빌드 프로세스 전체에서 모델은 메모리에 상주하며 애플리케이션의 수명 주기 동안 액세스할 수 있습니다. 그러나 애플리케이션이 실행을 멈추었을 때 모델이 로컬 또는 원격으로 저장되지 않은 경우 더 이상 액세스할 수 없게 됩니다. 일반적으로 모델은 유추 또는 재교육을 위해 다른 애플리케이션에서 학습한 뒤에 사용됩니다. 따라서 모델을 저장하는 것이 중요합니다. 아래 설명한 것처럼 데이터 준비 및 모델 학습 파이프라인을 사용할 때는 이 문서의 후속 섹션에서 설명하는 단계를 통해 모델을 저장 및 로드합니다. 이 샘플은 선형 회귀 모델을 사용하지만 같은 프로세스가 다른 ML.NET 알고리즘에 적용됩니다.

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
    }
};

// Create MLContext
MLContext mlContext = new MLContext();

// Load Data
IDataView data = mlContext.Data.LoadFromEnumerable<HousingData>(housingData);

// Define data preparation estimator
EstimatorChain<RegressionPredictionTransformer<LinearRegressionModelParameters>> pipelineEstimator =
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"))
        .Append(mlContext.Regression.Trainers.Sdca());

// Train model
ITransformer trainedModel = pipelineEstimator.Fit(data);

// Save model
mlContext.Model.Save(trainedModel, data.Schema, "model.zip");
```

대부분의 모델 및 데이터 준비 파이프라인은 같은 클래스 집합에서 상속되므로 이 구성 요소에 대한 저장 및 로드 메서드 서명은 같습니다. 사용 사례에 따라 데이터 준비 파이프라인 및 모델을 한 [`ITransformer`](xref:Microsoft.ML.ITransformer)를 출력하는 단일 [`EstimatorChain`](xref:Microsoft.ML.Data.TransformerChain%601)에 결합하거나 별도로 구분하여 각각에 대한 개별 [`ITransformer`](xref:Microsoft.ML.ITransformer)를 만듭니다. 

## <a name="save-a-model-locally"></a>로컬로 모델 저장

모델을 저장할 때는 다음 두 가지가 필요합니다.

1. 모델의 [`ITransformer`](xref:Microsoft.ML.ITransformer)
2. [`ITransformer`](xref:Microsoft.ML.ITransformer) 예상 입력의 [`DataViewSchema`](xref:Microsoft.ML.DataViewSchema)

모델을 학습한 후에는 [`Save`](xref:Microsoft.ML.ModelOperationsCatalog.Save*) 메서드를 통해 학습된 모델을 입력 데이터의 `DataViewSchema`를 사용하여 `model.zip` 파일에 저장합니다. 

```csharp
// Save Trained Model
mlContext.Model.Save(trainedModel, data.Schema, "model.zip");
```

## <a name="load-a-model-stored-locally"></a>로컬로 저장된 모델 로드

로컬로 저장된 모델은 `ASP.NET Core` 및 `Serverless Web Applications`처럼 다른 프로세스나 애플리케이션에서 사용할 수 있습니다. 자세한 정보는 [웹 API에서 ML.NET 사용](./serve-model-web-api-ml-net.md) 및 [ML.NET 서버리스 웹앱 배포](./serve-model-serverless-azure-functions-ml-net.md) 방법 문서를 참조하세요. 

별도의 애플리케이션이나 프로세스에서는 파일 경로와 함께 [`Load`](xref:Microsoft.ML.ModelOperationsCatalog.Load*) 메서드를 사용하여 학습된 모델을 애플리케이션에 가져옵니다.

```csharp
//Define DataViewSchema for data preparation pipeline and trained model
DataViewSchema modelSchema;

// Load trained model
ITransformer trainedModel = mlContext.Model.Load("model.zip", out modelSchema);
```

## <a name="load-a-model-stored-remotely"></a>원격으로 저장된 모델 로드

원격 위치에 저장된 데이터 준비 파이프라인과 모델을 애플리케이션에 로드하려면 [`Load`](xref:Microsoft.ML.ModelOperationsCatalog.Load*) 메서드에서 파일 경로 대신 [`Stream`](xref:System.IO.Stream)을 사용합니다.

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

// Define DataViewSchema and ITransformers
DataViewSchema modelSchema;
ITransformer trainedModel;

// Load data prep pipeline and trained model 
using (HttpClient client = new HttpClient())
{
    Stream modelFile = await client.GetStreamAsync("<YOUR-REMOTE-FILE-LOCATION>");

    trainedModel = mlContext.Model.Load(modelFile, out modelSchema);
}
```

## <a name="working-with-separate-data-preparation-and-model-pipelines"></a>별도 데이터 준비 및 모델 파이프라인 작업

> [!NOTE]
> 별도 데이터 준비 및 모델 학습 파이프라인 작업은 선택 사항입니다. 파이프라인을 분리하면 더 쉽게 학습된 모델 매개 변수를 검사할 수 있습니다. 예측을 위해 데이터 준비 및 모델 학습 작업을 포함하는 단일 파이프라인을 더 쉽게 저장 및 로드합니다.

별도 데이터 준비 파이프라인 및 모델을 작업할 경우 두 파이프라인을 동시에 저장 및 로드해야 한다는 점을 제외하고는 단일 파이프라인과 동일한 프로세스가 적용됩니다.

별도 데이터 준비 및 모델 학습 파이프라인 제공:

```csharp
// Define data preparation estimator
IEstimator<ITransformer> dataPrepEstimator =
    mlContext.Transforms.Concatenate("Features", new string[] { "Size", "HistoricalPrices" })
        .Append(mlContext.Transforms.NormalizeMinMax("Features"));

// Create data preparation transformer
ITransformer dataPrepTransformer = dataPrepEstimator.Fit(data);

// Define StochasticDualCoordinateAscent regression algorithm estimator
var sdcaEstimator = mlContext.Regression.Trainers.Sdca();

// Pre-process data using data prep operations
IDataView transformedData = dataPrepTransformer.Transform(data);

// Train regression model
RegressionPredictionTransformer<LinearRegressionModelParameters> trainedModel = sdcaEstimator.Fit(transformedData);
```

### <a name="save-data-preparation-pipeline-and-trained-model"></a>데이터 준비 파이프라인 및 학습된 모델 저장

데이터 준비 파이프라인 및 학습된 모델을 저장하려면 다음 명령을 사용합니다.

```csharp
// Save Data Prep transformer
mlContext.Model.Save(dataPrepTransformer, data.Schema, "data_preparation_pipeline.zip");

// Save Trained Model
mlContext.Model.Save(trainedModel, transformedData.Schema, "model.zip");
```

### <a name="load-data-preparation-pipeline-and-trained-model"></a>데이터 준비 파이프라인 및 학습된 모델 로드 

별도 프로세스나 애플리케이션에서 다음과 같이 데이터 준비 파이프라인과 학습된 모델을 로드합니다.

```csharp
// Create MLContext
MLContext mlContext = new MLContext();

// Define data preparation and trained model schemas
DataViewSchema dataPrepPipelineSchema, modelSchema;

// Load data preparation pipeline and trained model
ITransformer dataPrepPipeline = mlContext.Model.Load("data_preparation_pipeline.zip",out dataPrepPipelineSchema);
ITransformer trainedModel = mlContext.Model.Load("model.zip", out modelSchema);
```
