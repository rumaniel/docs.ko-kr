---
title: Azure Functions에 모델 배포
description: Azure Functions를 사용하여 인터넷을 통해 예측하기 위한 ML.NET 감정 분석 기계 학습 모델 제공
ms.date: 09/12/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to
ms.openlocfilehash: 2abd8588aa314b630c995e0c78b5869ec00a89df
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72179368"
---
# <a name="deploy-a-model-to-azure-functions"></a>Azure Functions에 모델 배포

Azure Functions 서버리스 환경을 통해 HTTP에서의 예측을 위해 미리 학습된 ML.NET 기계 학습 모델을 배포하는 방법을 알아봅니다.

> [!NOTE]
> `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

## <a name="prerequisites"></a>전제 조건

- “.NET Core 플랫폼 간 개발” 워크로드 및 “Azure 개발”이 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).
- Microsoft.NET.Sdk.Functions NuGet 패키지 버전 1.0.28 이상
- [Azure Functions 도구](/azure/azure-functions/functions-develop-vs#check-your-tools-version)
- PowerShell
- 미리 학습된 모델입니다. [ML.NET 감정 분석 자습서](../tutorials/sentiment-analysis.md)를 사용하여 자체 모델을 빌드하거나 이 [미리 학습된 감정 분석 기계 학습 모델](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip) 다운로드

## <a name="create-azure-functions-project"></a>Azure Functions 프로젝트 만들기

1. Visual Studio 2017을 엽니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. **새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **Cloud** 노드를 차례로 선택합니다. 그런 다음, **Azure Functions** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 “SentimentAnalysisFunctionsApp”을 입력한 다음, **확인** 단추를 선택합니다.
1. **새 프로젝트** 대화 상자에서 프로젝트 옵션 위의 드롭다운을 열고 **Azure Functions v2(.NET Core)** 를 선택합니다. 그런 다음, **HTTP 트리거** 프로젝트를 선택한 후 **확인** 단추를 선택합니다.
1. 프로젝트에서 *MLModels* 디렉터리를 만들어 모델을 저장합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. “MLModels”를 입력하고 Enter 키를 누릅니다.

1. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

1. **Microsoft.Azure.Functions.Extensions NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고 찾아보기 탭을 선택합니다. **Microsoft.Azure.Functions.Extensions**를 검색하고 목록에서 해당 패키지를 선택한 다음, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

1. **Microsoft.Extensions.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 원본으로 선택하고, 찾아보기 탭을 선택하고, **Microsoft.Extensions.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

1. **Microsoft.NET.Sdk.Functions NuGet 패키지**를 버전 1.0.28 이상으로 업데이트합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고 설치 탭을 선택합니다. **Microsoft.NET.Sdk.Functions**를 검색하고 목록에서 해당 패키지를 선택한 다음, 버전 드롭다운에서 1.0.28 이상을 선택하고 **업데이트** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

## <a name="add-pre-trained-model-to-project"></a>프로젝트에 미리 학습된 모델 추가

1. 미리 빌드된 모델을 *MLModels* 폴더에 복사합니다.
1. 솔루션 탐색기에서 미리 빌드된 모델 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

## <a name="create-azure-function-to-analyze-sentiment"></a>감정을 분석하는 Azure Function 만들기

감정을 예측하는 클래스를 만듭니다. 새 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.

1. **새 항목 추가** 대화 상자에서 **Azure 함수**를 선택하고 **이름** 필드를 *AnalyzeSentiment.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

1. **새 Azure 함수** 대화 상자에서 **HTTP 트리거**를 선택합니다. 그런 다음, **확인** 단추를 선택합니다.

    *AnalyzeSentiment.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *AnalyzeSentiment.cs*의 맨 위에 추가합니다.

    [!code-csharp [AnalyzeUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L1-L11)]

    기본적으로 `AnalyzeSentiment` 클래스는 `static`입니다. 클래스 정의에서 `static` 키워드를 제거합니다.

    ```csharp
    public class AnalyzeSentiment
    {
    
    }
    ```

## <a name="create-data-models"></a>데이터 모델 만들기

입력 데이터 및 예측에 대한 일부 클래스를 만들어야 합니다. 새 클래스를 프로젝트에 추가합니다.

1. 프로젝트에서 *DataModels* 디렉터리를 만들어 데이터 모델을 저장합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 폴더**를 선택합니다. “DataModels”를 입력하고 Enter 키를 누릅니다.
2. 솔루션 탐색기에서 *DataModels* 디렉터리를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 항목**을 선택합니다.
3. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다. 

    *SentimentData.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *SentimentData.cs*의 맨 위에 추가합니다.

    [!code-csharp [SentimentDataUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L1)]

    기존 클래스 정의를 제거하고 다음 코드를 *SentimentData.cs* 파일에 추가합니다.

    [!code-csharp [SentimentData](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentData.cs#L5-L13)]

4. 솔루션 탐색기에서 *DataModels* 디렉터리를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 항목**을 선택합니다.
5. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentPrediction.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다. *SentimentPrediction.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *SentimentPrediction.cs*의 맨 위에 추가합니다.

    [!code-csharp [SentimentPredictionUsings](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L1)]

    기존 클래스 정의를 제거하고 다음 코드를 *SentimentPrediction.cs* 파일에 추가합니다.

    [!code-csharp [SentimentPrediction](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/DataModels/SentimentPrediction.cs#L5-L14)]

    `SentimentPrediction`은 `SentimentText` 속성의 원래 데이터와 모델에서 생성된 출력에 대한 액세스를 제공하는 `SentimentData`에서 상속됩니다.

## <a name="register-predictionenginepool-service"></a>PredictionEnginePool 서비스 등록

단일 예측을 수행하려면 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)을 만들어야 합니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 또한 애플리케이션 내에서 필요한 모든 위치에서 인스턴스를 만들어야 합니다. 애플리케이션이 커지면 이 프로세스를 관리할 수 없게 됩니다. 성능 및 스레드 보안을 개선하려면 종속성 주입과 `PredictionEnginePool` 서비스를 함께 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다.

[종속성 주입](https://en.wikipedia.org/wiki/Dependency_injection)에 대한 자세한 내용은 다음 링크를 참조하세요.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *Startup.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다. 

    *Startup.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *Startup.cs*의 맨 위에 추가합니다.

    ```csharp
    using Microsoft.Azure.Functions.Extensions.DependencyInjection;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisFunctionsApp;
    using SentimentAnalysisFunctionsApp.DataModels;
    ```

    using 문 아래의 기존 코드를 제거하고 다음 코드를 *Startup.cs* 파일에 추가합니다.

    ```csharp
    [assembly: FunctionsStartup(typeof(Startup))]
    namespace SentimentAnalysisFunctionsApp
    {
        public class Startup : FunctionsStartup
        {
            public override void Configure(IFunctionsHostBuilder builder)
            {
                builder.Services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
                    .FromFile(modelName: "SentimentAnalysisModel", filePath:"MLModels/sentiment_model.zip", watchForChanges: true);
            }
        }
    }
    ```

개략적으로 이 코드는 애플리케이션을 수동으로 초기화하지 않고도 애플리케이션에서 요청할 때 나중에 사용할 수 있도록 자동으로 개체 및 서비스를 초기화합니다. 

기계 학습 모델은 정적이지 않습니다. 새 학습 데이터를 사용할 수 있게 되면 모델을 다시 학습하고 다시 배포합니다. 최신 버전의 모델을 애플리케이션으로 가져오는 한 가지 방법은 전체 애플리케이션을 다시 배포하는 것입니다. 그러나 이 경우 애플리케이션 가동 중지 시간이 발생합니다. `PredictionEnginePool` 서비스는 애플리케이션을 가동 중지하지 않으면서 업데이트된 모델을 다시 로드하는 메커니즘을 제공합니다. 

`watchForChanges` 매개 변수를 `true`로 설정하면 `PredictionEnginePool`은 파일 시스템 변경 알림을 수신 대기하고 파일이 변경될 때 이벤트를 발생시키는 [`FileSystemWatcher`](xref:System.IO.FileSystemWatcher)를 시작합니다. 그러면 `PredictionEnginePool`에서 모델을 자동으로 다시 로드하도록 지정할 수 있는 메시지가 표시됩니다.

모델은 `modelName` 매개 변수로 식별되므로 변경 시, 애플리케이션당 두 개 이상의 모델이 다시 로드될 수 있습니다. 

> [!TIP]
> 또는 원격으로 저장된 모델을 사용하는 경우 `FromUri` 메서드를 사용할 수 있습니다. `FromUri`는 파일 변경 이벤트를 감시하지 않고, 원격 위치에서 변경 내용을 폴링합니다. 폴링 간격의 기본값은 5분입니다. 애플리케이션의 요구 사항에 따라 폴링 간격을 늘리거나 줄일 수 있습니다. 아래 코드 샘플에서 `PredictionEnginePool`은 1분마다 지정된 URI에 저장된 모델을 폴링합니다.
>    
>```csharp
>builder.Services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
>   .FromUri(
>       modelName: "SentimentAnalysisModel", 
>       uri:"https://github.com/dotnet/samples/raw/master/machine-learning/models/sentimentanalysis/sentiment_model.zip", 
>       period: TimeSpan.FromMinutes(1));
>```

## <a name="load-the-model-into-the-function"></a>함수에 모델 로드

*AnalyzeSentiment* 클래스 안에 다음 코드를 삽입합니다.

[!code-csharp [AnalyzeCtor](~/machinelearning-samples/samples/csharp/end-to-end-apps/ScalableMLModelOnAzureFunction/SentimentAnalysisFunctionsApp/AnalyzeSentiment.cs#L18-L24)]

이 코드는 종속성 주입을 통해 가져오는 함수의 생성자에 `PredictionEnginePool`을 전달하여 할당합니다.

## <a name="use-the-model-to-make-predictions"></a>모델을 사용하여 예측하기

*AnalyzeSentiment* 클래스에서 *Run* 메서드의 기존 구현을 다음 코드로 바꿉니다.

```csharp
[FunctionName("AnalyzeSentiment")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequest req,
ILogger log)
{
    log.LogInformation("C# HTTP trigger function processed a request.");

    //Parse HTTP Request Body
    string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
    SentimentData data = JsonConvert.DeserializeObject<SentimentData>(requestBody);

    //Make Prediction
    SentimentPrediction prediction = _predictionEnginePool.Predict(modelName: "SentimentAnalysisModel", example: data);

    //Convert prediction to string
    string sentiment = Convert.ToBoolean(prediction.Prediction) ? "Positive" : "Negative";

    //Return Prediction
    return (ActionResult)new OkObjectResult(sentiment);
}
```

`Run` 메서드가 실행되면 HTTP 요청에서 수신되는 데이터가 직렬 해제되어 `PredictionEnginePool`에 대한 입력으로 사용됩니다. 그런 다음, `Predict` 메서드가 `Startup` 클래스에 등록된 `SentimentAnalysisModel`을 사용하여 예측을 수행하고 성공하면 결과를 사용자에게 다시 반환합니다.

## <a name="test-locally"></a>로컬로 테스트

이제 모든 것이 설정되었으므로 애플리케이션을 테스트할 수 있습니다.

1. 애플리케이션 실행
1. PowerShell을 열고 PORT가 애플리케이션을 실행 중인 포트인 경우 프롬프트에 코드를 입력합니다. 일반적으로 포트는 7071입니다.

    ```powershell
    Invoke-RestMethod "http://localhost:<PORT>/api/AnalyzeSentiment" -Method Post -Body (@{SentimentText="This is a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    성공하면 출력이 아래 텍스트와 같이 표시됩니다.
    
    ```powershell
    Negative
    ```

지금까지 Azure 함수를 사용하여 인터넷을 통해 예측을 수행하도록 모델을 제공했습니다.

## <a name="next-steps"></a>다음 단계

- [Azure에 배포](/azure/azure-functions/functions-develop-vs#publish-to-azure)
