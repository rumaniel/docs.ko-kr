---
title: ASP.NET Core Web API에 모델 배포
description: ASP.NET Core Web API를 사용하여 인터넷을 통해 ML.NET 감정 분석 기계 학습 모델 제공
ms.date: 09/11/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc,how-to
ms.openlocfilehash: 42f8d51f2547cd6f3240a05420b2da10b7cf52e3
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72179388"
---
# <a name="deploy-a-model-in-an-aspnet-core-web-api"></a>ASP.NET Core Web API에 모델 배포

ASP.NET Core Web API를 사용하여 웹에서 미리 학습된 ML.NET 기계 학습 모델을 서비스하는 방법을 살펴봅니다. 웹 API를 통해 모델을 서비스하면 표준 HTTP 메서드를 통한 예측을 사용할 수 있습니다.

> [!NOTE]
> `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

## <a name="prerequisites"></a>전제 조건

- “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).
- PowerShell.
- 미리 학습된 모델입니다. [ML.NET 감정 분석 자습서](../tutorials/sentiment-analysis.md)를 사용하여 자체 모델을 빌드하거나 이 [미리 학습된 감정 분석 기계 학습 모델](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip) 다운로드

## <a name="create-aspnet-core-web-api-project"></a>ASP.NET Core Web API 프로젝트 만들기

1. Visual Studio 2017을 엽니다. 메뉴 모음에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다. [새 프로젝트] 대화 상자에서 **Visual C#** 노드와 **Web** 노드를 차례로 선택합니다. 그런 다음, **ASP.NET Core 웹 애플리케이션** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 “SentimentAnalysisWebAPI”를 입력한 다음, **확인** 단추를 선택합니다.

1. 다른 유형의 ASP.NET Core 프로젝트를 표시하는 창에서 **API**를 선택하고 **확인** 단추를 선택합니다.

1. 프로젝트에서 *MLModels* 디렉터리를 만들어 미리 빌드된 기계 학습 모델 파일을 저장합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 [추가] > [새 폴더]를 선택합니다. “MLModels”를 입력하고 Enter 키를 누릅니다.

1. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, [설치] 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 [라이선스 승인] 대화 상자에서 **동의함** 단추를 선택합니다.

1. **Microsoft.Extensions.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 원본으로 선택하고, 찾아보기 탭을 선택하고, **Microsoft.Extensions.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, 설치 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 [라이선스 승인] 대화 상자에서 **동의함** 단추를 선택합니다.

### <a name="add-model-to-aspnet-core-web-api-project"></a>ASP.NET Core Web API 프로젝트에 모델 추가

1. 미리 빌드된 모델을 *MLModels* 디렉터리에 복사합니다.
1. 솔루션 탐색기에서 모델 zip 파일을 마우스 오른쪽 단추로 클릭하고 [속성]을 선택합니다. [고급] 아래에서 [출력 디렉터리에 복사] 값을 [변경된 내용만 복사]로 변경합니다.

## <a name="create-data-models"></a>데이터 모델 만들기

입력 데이터 및 예측에 대한 일부 클래스를 만들어야 합니다. 새 클래스를 프로젝트에 추가합니다.

1. 프로젝트에서 *DataModels* 디렉터리를 만들어 데이터 모델을 저장합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 [추가] > [새 폴더]를 선택합니다. “DataModels”를 입력하고 **Enter** 키를 누릅니다.

2. 솔루션 탐색기에서 *DataModels* 디렉터리를 마우스 오른쪽 단추로 클릭하고 [추가] > [새 항목]을 선택합니다.
3. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다. *SentimentData.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *SentimentData.cs*의 맨 위에 추가합니다.

    ```csharp
    using Microsoft.ML.Data;
    ```
    
    기존 클래스 정의를 제거하고 다음 코드를 **SentimentData.cs** 파일에 추가합니다.
    
    ```csharp
    public class SentimentData
    {
        [LoadColumn(0)]
        public string SentimentText;

        [LoadColumn(1)]
        [ColumnName("Label")]
        public bool Sentiment;
    }
    ```

4. 솔루션 탐색기에서 *DataModels* 디렉터리를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 항목**을 선택합니다.
5. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentPrediction.cs*로 변경합니다. 그런 다음, [추가] 단추를 선택합니다. *SentimentPrediction.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *SentimentPrediction.cs*의 맨 위에 추가합니다.

    ```csharp
    using Microsoft.ML.Data;
    ```
    
    기존 클래스 정의를 제거하고 다음 코드를 *SentimentPrediction.cs* 파일에 추가합니다.
    
    ```csharp
    public class SentimentPrediction : SentimentData
    {

        [ColumnName("PredictedLabel")]
        public bool Prediction { get; set; }

        public float Probability { get; set; }

        public float Score { get; set; }
    }
    ```

    `SentimentPrediction`는 `SentimentData`에서 상속됩니다. 이렇게 하면 모델에서 생성된 출력과 함께 `SentimentText` 속성의 원래 데이터를 더 쉽게 볼 수 있습니다. 

## <a name="register-predictionenginepool-for-use-in-the-application"></a>애플리케이션에서 사용하기 위해 PredictionEnginePool 등록

단일 예측을 수행하려면 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)을 만들어야 합니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 또한 애플리케이션 내에서 필요한 모든 위치에서 인스턴스를 만들어야 합니다. 애플리케이션이 커지면 이 프로세스를 관리할 수 없게 됩니다. 성능 및 스레드 보안을 개선하려면 종속성 주입과 `PredictionEnginePool` 서비스를 함께 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다.

다음 링크에서는 [ASP.NET Core에서 종속성 주입](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-2.1)에 대한 자세한 정보를 제공합니다.

1. *Startup.cs* 클래스를 열고 다음 using 문을 파일 맨 위에 추가합니다.

    ```csharp
    using Microsoft.AspNetCore.Builder;
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.DependencyInjection;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

2. *ConfigureServices* 메서드에 다음 코드를 추가합니다.

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
        services.AddPredictionEnginePool<SentimentData, SentimentPrediction>()
            .FromFile(modelName: "SentimentAnalysisModel", filePath:"MLModels/sentiment_model.zip", watchForChanges: true);
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

## <a name="create-predict-controller"></a>예측 컨트롤러 만들기

들어오는 HTTP 요청을 처리하려면 컨트롤러를 만듭니다.

1. 솔루션 탐색기에서 *Controllers* 디렉터리를 마우스 오른쪽 단추로 클릭하고 **추가 > 컨트롤러**를 선택합니다.
1. **새 항목 추가** 대화 상자에서 **API 컨트롤러 비어 있음**을 선택하고 **추가**를 선택합니다.
1. 프롬프트에서 **컨트롤러 이름** 필드를 *PredictController.cs*로 변경합니다. 그런 다음, [추가] 단추를 선택합니다. *PredictController.cs* 파일이 코드 편집기에서 열립니다. 다음 using 문을 *PredictController.cs*의 맨 위에 추가합니다.

    ```csharp
    using System;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.ML;
    using SentimentAnalysisWebAPI.DataModels;
    ```

    기존 클래스 정의를 제거하고 다음 코드를 *PredictController.cs* 파일에 추가합니다.
    
    ```csharp
    public class PredictController : ControllerBase
    {
        private readonly PredictionEnginePool<SentimentData, SentimentPrediction> _predictionEnginePool;

        public PredictController(PredictionEnginePool<SentimentData,SentimentPrediction> predictionEnginePool)
        {
            _predictionEnginePool = predictionEnginePool;
        }

        [HttpPost]
        public ActionResult<string> Post([FromBody] SentimentData input)
        {
            if(!ModelState.IsValid)
            {
                return BadRequest();
            }

            SentimentPrediction prediction = _predictionEnginePool.Predict(modelName: "SentimentAnalysisModel", example: input);

            string sentiment = Convert.ToBoolean(prediction.Prediction) ? "Positive" : "Negative";

            return Ok(sentiment);
        }
    }
    ```

이 코드는 종속성 주입을 통해 가져오는 컨트롤러의 생성자에 `PredictionEnginePool`을 전달하여 할당합니다. 그런 다음, `Predict` 컨트롤러의 `Post` 메서드가 `PredictionEnginePool`을 사용하여 `Startup` 클래스에 등록된 `SentimentAnalysisModel`로 예측을 수행하고 성공하면 결과를 사용자에게 다시 반환합니다.

## <a name="test-web-api-locally"></a>로컬로 Web API 테스트

이제 모든 것이 설정되면 애플리케이션을 테스트할 수 있습니다.

1. 애플리케이션을 실행합니다.
1. PowerShell을 열고 PORT가 애플리케이션이 수신 대기 중인 포트인 경우 다음 코드를 입력합니다.

    ```powershell
    Invoke-RestMethod "https://localhost:<PORT>/api/predict" -Method Post -Body (@{SentimentText="This was a very bad steak"} | ConvertTo-Json) -ContentType "application/json"
    ```

    성공하면 출력이 아래 텍스트와 같이 표시됩니다.
    
    ```powershell
    Negative
    ```

지금까지 ASP.NET Core Web API를 사용하여 인터넷을 통해 예측을 수행하도록 모델을 제공했습니다.

## <a name="next-steps"></a>다음 단계

- [Azure에 배포](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs#deploy-the-app-to-azure)
