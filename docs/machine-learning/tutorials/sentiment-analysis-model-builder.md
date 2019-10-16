---
title: '자습서: 감정 분석 - 이진 분류'
description: 이 자습서에서는 웹 사이트 주석에서 감정을 분류하고 적절한 조치를 취하는 Razor Pages 애플리케이션을 만드는 방법을 보여 줍니다. 감정 이진 분류자는 Visual Studio에서 모델 작성기를 사용합니다.
ms.date: 10/08/2019
author: luisquintanilla
ms.author: luquinta
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 4a97fb70caafd7b0003830259ddbb0ec72a2ca8a
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180265"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-in-a-web-application-using-mlnet-model-builder"></a>자습서: ML.NET 모델 작성기를 사용하여 웹 애플리케이션에서 웹 사이트 댓글 감정 분석

웹 애플리케이션에서 실시간으로 댓글의 감정을 분석하는 방법에 대해 알아봅니다.

이 자습서에서는 실시간으로 웹 사이트 댓글에서 감정을 분류하는 ASP.NET Core Razor Pages 애플리케이션을 만드는 방법을 보여 줍니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
>
> - ASP.NET Core Razor Pages 애플리케이션 만들기
> - 데이터 준비 및 이해
> - 시나리오 선택
> - 데이터 로드
> - 모델 학습
> - 모델 평가
> - 예측에 모델 사용

> [!NOTE]
> 모델 작성기는 현재 미리 보기로 제공됩니다.

[dotnet/samples](https://github.com/dotnet/machinelearning-samples) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

필수 구성 요소 및 설치 지침 목록을 보려면 [모델 작성기 설치 가이드](../how-to-guides/install-model-builder.md)를 방문하세요.

## <a name="create-a-razor-pages-application"></a>Razor Pages 애플리케이션 만들기

1. **ASP.NET Core Razor Pages 애플리케이션**을 만듭니다.

    1. Visual Studio를 열고 메뉴 모음에서 **파일 > 새로 만들기 > 프로젝트**를 선택합니다.
    1. [새 프로젝트] 대화 상자에서 **Visual C#** 노드와 **Web** 노드를 차례로 선택합니다.
    1. 그런 다음, **ASP.NET Core 웹 애플리케이션** 프로젝트 템플릿을 선택합니다.
    1. **이름** 텍스트 상자에 "SentimentRazor"를 입력합니다.
    1. **솔루션용 디렉터리 만들기** 확인란은 기본적으로 선택되어 있습니다. 선택되어 있지 않다면 직접 선택합니다.
    1. **확인** 단추를 선택합니다.
    1. 다른 유형의 ASP.NET Core 프로젝트를 표시하는 창에서 **웹 애플리케이션**을 선택하고 **확인** 단추를 선택합니다.

## <a name="prepare-and-understand-the-data"></a>데이터 준비 및 이해

[Wikipedia detox 데이터 세트](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)를 다운로드합니다. 웹 페이지가 열리면 페이지를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 저장**을 선택하여 컴퓨터의 아무 위치에 파일을 저장합니다.

*wikipedia-detox-250-line-data.tsv* 데이터 세트의 각 행은 사용자가 Wikipedia에 남긴 다른 검토를 나타냅니다. 첫 번째 열은 텍스트의 감정(0은 무해, 1은 유해)를 나타내고, 두 번째 열은 사용자가 남긴 댓글을 나타냅니다. 열은 탭으로 구분됩니다. 데이터는 다음과 같습니다.

| 감정 | SentimentText |
| :---: | :---: |
1 | ==RUDE== Dude, you are rude upload that carl picture back, or else.
1 | == OK! ==  IM GOING TO VANDALIZE WILD ONES WIKI THEN!!!
0 | I hope this helps.

## <a name="choose-a-scenario"></a>시나리오 선택

![Visual Studio의 모델 작성기 마법사](./media/sentiment-analysis-model-builder/model-builder-screen.png)

모델을 학습하려면 모델 작성기에서 제공하는 사용 가능한 기계 학습 시나리오 목록에서 선택해야 합니다.

1. **솔루션 탐색기**에서 *SentimentRazor* 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Machine Learning**을 선택합니다.
1. 이 샘플에서 감정 분석은 시나리오입니다. 모델 분석기 도구의 *시나리오* 단계에서 **감정 분석** 시나리오를 선택합니다.

## <a name="load-the-data"></a>데이터 로드

모델 작성기는 SQL Server 데이터베이스 또는 로컬 파일 `csv` 또는 `tsv` 형식의 두 가지 소스에서 데이터를 허용합니다.

1. 모델 작성기 도구의 데이터 단계의 데이터 원본 드롭다운에서 **파일**을 선택합니다.
1. **파일 선택** 텍스트 상자 옆의 있는 단추를 선택하고 파일 탐색기를 사용하여 *wikipedia-detox-250-line-data.tsv* 파일을 선택합니다.
1. **예측할 열(레이블)** 드롭다운에서 **감정**을 선택합니다.
1. **열 입력(기능)** 드롭다운의 기본값을 그대로 둡니다.
1. **학습** 링크를 선택하여 모델 작성기 도구의 다음 단계로 이동합니다.

## <a name="train-the-model"></a>모델 학습

이 자습서에서 감정 분석 모델을 학습하는 데 사용되는 기계 학습 작업은 이진 분류입니다. 모델 학습 프로세스 중에 모델 작성기는 다른 이진 분류 알고리즘 및 설정을 통해 개별 모델을 학습하여 데이터 세트에 가장 적합한 모델을 찾습니다.

모델을 학습하는 데 필요한 시간은 데이터 양에 비례합니다. 모델 작성기는 데이터 소스의 크기에 따라 **학습 시간(초)** 의 기본값을 자동으로 선택합니다.

1. 모델 작성기는 **학습 시간(초)** 값을 10초로 설정하지만 이 값을 30초로 늘립니다. 더 긴 시간 동안 학습하면 모델 작성기가 최상의 모델을 찾아 더 많은 알고리즘과 매개 변수의 조합을 탐색할 수 있습니다.
1. **학습 시작**을 선택합니다.

    학습 프로세스 전체에서 진행률 데이터는 학습 단계의 `Progress` 섹션에 표시됩니다.

    - 상태는 학습 프로세스의 완료 상태를 표시합니다.
    - 가장 높은 정확도는 모델 작성기가 현재까지 찾은 최고 성능 모델의 정확도를 표시합니다. 더 높은 정확도는 테스트 데이터에서 모델이 더 정확하게 예측된다는 것을 의미합니다.
    - 최상의 알고리즘은 모델 작성기가 현재까지 찾은 최고 성능 알고리즘의 이름을 표시합니다.
    - 마지막 알고리즘은 모델 작성기가 가장 최근에 학습하기 위해 사용한 알고리즘의 이름을 표시합니다.

1. 학습이 완료되면 **평가** 링크를 선택하여 다음 단계로 이동합니다.

## <a name="evaluate-the-model"></a>모델 평가

학습 단계의 결과는 최상의 성능을 가진 하나의 모델이 됩니다. 모델 작성기 도구의 평가 단계에서 출력 섹션에는 **최상의 모델** 항목의 가장 성능이 좋은 모델에서 사용되는 알고리즘과 더불어 **최상의 모델 정확도**의 메트릭이 포함됩니다. 또한 상위 5개 모델 및 해당 메트릭을 포함하는 요약 테이블입니다.

정확도 메트릭에 만족하지 않는 경우 모델 정확도를 개선하기 위한 몇 가지 쉬운 방법은 모델을 학습하거나 더 많은 데이터를 사용하기 위한 시간을 늘리는 것입니다. 그렇지 않으면 **코드** 링크를 선택하여 모델 작성기 도구의 최종 단계로 이동합니다.

## <a name="add-the-code-to-make-predictions"></a>코드를 추가하여 예측하기

학습 프로세스의 결과로 두 개의 프로젝트가 만들어질 수 있습니다.

### <a name="reference-the-trained-model"></a>학습된 모델 참조

1. 모델 작성기 도구의 *코드* 단계에서 **프로젝트 추가**를 선택하여 자동 생성된 프로젝트를 솔루션에 추가합니다.

    **솔루션 탐색기**에 다음 프로젝트가 표시될 것입니다.

    - *SentimentRazorML.ConsoleApp*: 모델 학습 및 예측 코드가 포함된 .NET Core 콘솔 애플리케이션입니다.
    - *SentimentRazorML.Model*: 입력 및 출력 모델 데이터의 스키마를 정의하는 데이터 모델뿐만 아니라 학습 중 가장 성능이 뛰어난 모델의 저장된 버전을 포함하는 .NET Standard 클래스 라이브러리입니다.

    이 자습서에서는 *SentimentRazorML.Model* 프로젝트만을 사용합니다. 예측이 콘솔이 아니라 *SentimentRazor* 웹 애플리케이션에서 수행되기 때문입니다. *SentimentRazorML.ConsoleApp*은 점수 매기기에 사용되지 않지만 나중에 새 데이터를 사용하여 모델을 다시 학습하는 데 사용할 수 있습니다. 재학습은 이 자습서에서 다루지 않습니다.

### <a name="configure-the-predictionengine-pool"></a>PredictionEngine 풀 구성

단일 예측을 수행하려면 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)을 만들어야 합니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 또한 애플리케이션 내에서 필요한 모든 위치에서 인스턴스를 만들어야 합니다. 애플리케이션이 커지면 이 프로세스를 관리할 수 없게 됩니다. 성능 및 스레드 보안을 개선하려면 종속성 주입과 `PredictionEnginePool` 서비스를 함께 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다.

1. *Microsoft.Extensions.ML* NuGet 패키지를 설치합니다.

    1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
    1. 패키지 원본으로 "nuget.org"를 선택합니다.
    1. **찾아보기** 탭을 선택하고 **Microsoft.Extensions.ML**을 검색합니다.
    1. 목록에서 패키지를 선택하고 **설치** 단추를 선택합니다.
    1. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택합니다.
    1. 나열된 패키지 라이선스 조건에 동의하면 **라이선스 수락** 대화 상자에서 **동의함** 단추를 선택합니다.

1. *SentimentRazor* 프로젝트에서 *Startup.cs* 파일을 엽니다.
1. *Microsoft.Extensions.ML* NuGet 패키지 및 *SentimentRazorML.Model* 프로젝트를 참조하도록 다음 using 문을 추가합니다.

    ```csharp
    using System.IO;
    using Microsoft.Extensions.ML;
    using SentimentRazorML.Model;
    ```

1. 학습된 모델 파일의 위치를 저장하는 전역 변수를 만듭니다.

    ```csharp
    private readonly string _modelPath;
    ```

1. 모델 파일은 애플리케이션의 어셈블리 파일과 함께 build 디렉터리에 저장됩니다. 보다 쉽게 액세스할 수 있도록 `Configure` 메서드를 따라 `GetAbsolutePath`라는 도우미 메서드를 만듭니다.

    ```csharp
    public static string GetAbsolutePath(string relativePath)
    {
        FileInfo _dataRoot = new FileInfo(typeof(Program).Assembly.Location);
        string assemblyFolderPath = _dataRoot.Directory.FullName;

        string fullPath = Path.Combine(assemblyFolderPath, relativePath);
        return fullPath;
    }    
    ```

1. `Startup` 클래스 생성자에서 `GetAbsolutePath` 메서드를 사용하여 `_modelPath`를 설정합니다.

    ```csharp
    _modelPath = GetAbsolutePath("MLModel.zip");
    ```

1. `ConfigureServices` 메서드에서 애플리케이션에 대해 `PredictionEnginePool`을 구성합니다.

    ```csharp
    services.AddPredictionEnginePool<ModelInput, ModelOutput>()
            .FromFile(_modelPath);
    ```

### <a name="create-sentiment-analysis-handler"></a>감정 분석 처리기 만들기

예측은 애플리케이션의 기본 페이지에서 수행됩니다. 따라서 사용자 입력을 취하고 `PredictionEnginePool`을 사용하여 예측을 반환하는 메서드를 추가해야 합니다.

1. *Pages* 디렉터리에 있는 *Index.cshtml.cs* 파일을 열고 다음 using 문을 추가합니다.

    ```csharp
    using Microsoft.Extensions.ML;
    using SentimentRazorML.Model;
    ```

    `Startup` 클래스에서 구성된 `PredictionEnginePool`을 사용하려면 해당 클래스를 사용하려는 모델의 생성자에 삽입해야 합니다.

1. `IndexModel` 클래스 내부에서 `PredictionEnginePool`을 참조하는 변수를 추가합니다.

    ```csharp
    private readonly PredictionEnginePool<ModelInput, ModelOutput> _predictionEnginePool;
    ```

1. `IndexModel` 클래스에서 생성자를 만들고 `PredictionEnginePool` 서비스를 여기에 삽입합니다.

    ```csharp
    public IndexModel(PredictionEnginePool<ModelInput, ModelOutput> predictionEnginePool)
    {
        _predictionEnginePool = predictionEnginePool;
    }    
    ```

1. `PredictionEnginePool`을 사용하여 웹 페이지에서 받은 사용자 입력으로부터 예측을 수행하는 메서드 처리기를 만듭니다.

    1. `OnGet` 메서드 아래 `OnGetAnalyzeSentiment`라는 새 메서드를 만듭니다.

        ```csharp
        public IActionResult OnGetAnalyzeSentiment([FromQuery] string text)
        {

        }
        ```

    1. 사용자의 입력이 비어 있거나 null인 경우 `OnGetAnalyzeSentiment` 메서드 내에서 *중립* 감정을 반환합니다.

        ```csharp
        if (String.IsNullOrEmpty(text)) return Content("Neutral");
        ```

    1. 입력이 유효할 경우 `ModelInput`의 새 인스턴스를 만듭니다.

        ```csharp
        var input = new ModelInput { SentimentText = text };
        ```

    1. `PredictionEnginePool`을 사용하여 감정을 예측합니다.

        ```csharp
        var prediction = _predictionEnginePool.Predict(input);
        ```

    1. 다음 코드를 사용하여 예측된 `bool` 값을 유해 또는 무해로 변환합니다.

        ```csharp
        var sentiment = Convert.ToBoolean(prediction.Prediction) ? "Toxic" : "Not Toxic";
        ```

    1. 마지막으로 감정을 웹 페이지로 반환합니다.

        ```csharp
        return Content(sentiment);
        ```

### <a name="configure-the-web-page"></a>웹 페이지 구성

`OnGetAnalyzeSentiment`에서 반환하는 결과는 `Index` 웹 페이지에 동적으로 표시됩니다.

1. *Pages* 디렉터리에서 *Index. cshtml* 파일을 열고 해당 내용을 다음 코드로 바꿉니다.

    [!code-cshtml [IndexPage](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/Pages/Index.cshtml)]

1. 다음으로, *wwwroot\css* 디렉터리에서 *site.css* 페이지 끝에 css 스타일 코드를 추가합니다.

    [!code-css [CssStyling](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/css/site.css#L61-L105)]

1. 그런 다음 웹 페이지에서 `OnGetAnalyzeSentiment` 처리기로 입력을 보내는 코드를 추가합니다.

    1. *wwwroot\js* 디렉터리에 있는 *site.js* 파일에서 `OnGetAnalyzeSentiment` 처리기에 사용자 입력을 사용하여 GET HTTP 요청을 하는 `getSentiment`라는 함수를 만듭니다.

        [!code-javascript [GetSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L5-L10)]

    1. 그 아래에 감정이 예측되면 웹 페이지에서 표식의 위치를 동적으로 업데이트하는 `updateMarker`라는 또 다른 함수를 추가합니다.

        [!code-javascript [UpdateMarkerMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L12-L15)]

    1. 사용자의 입력을 가져와 `getSentiment` 함수를 사용하여 `OnGetAnalyzeSentiment` 함수에 보내고 `updateMarker` 함수를 사용하여 표식을 업데이트하는 `updateSentiment`라는 이벤트 처리기 함수를 만듭니다.

        [!code-javascript [UpdateSentimentMethod](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L17-L34)]

    1. 마지막으로 이벤트 처리기를 등록하고 `id=Message` 특성을 사용하여 `textarea` 요소에 바인딩합니다.

        [!code-javascript [UpdateSentimentEvtHandler](~/machinelearning-samples/samples/modelbuilder/BinaryClassification_Sentiment_Razor/SentimentRazor/wwwroot/js/site.js#L36)]

## <a name="run-the-application"></a>애플리케이션 실행

이제 애플리케이션이 설정되었으므로 브라우저에서 시작해야 하는 애플리케이션을 실행합니다.

애플리케이션이 시작되면 *Model Builder is cool!* 을 텍스트 영역에 입력합니다. 예측된 감정이 *무해*로 표시되어야 합니다.

![예측된 감정 창이 있는 실행 창](./media/sentiment-analysis-model-builder/web-app.png)

모델 작성기에서 생성된 프로젝트를 나중에 다른 솔루션 내에서 참조해야 하는 경우 `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` 디렉터리 내에서 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - ASP.NET Core Razor Pages 애플리케이션 만들기
> - 데이터 준비 및 이해
> - 시나리오 선택
> - 데이터 로드
> - 모델 학습
> - 모델 평가
> - 예측에 모델 사용

### <a name="additional-resources"></a>추가 리소스

이 자습서에서 언급한 항목에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [모델 작성기 시나리오](../automate-training-with-model-builder.md#scenarios)
- [이진 분류](../resources/glossary.md#binary-classification)
- [이진 분류 모델 메트릭](../resources/metrics.md#metrics-for-binary-classification)
