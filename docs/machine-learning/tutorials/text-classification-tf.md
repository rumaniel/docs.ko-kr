---
title: '자습서: 미리 학습된 TensorFlow 모델을 사용하여 영화 리뷰의 감정 분석'
description: 이 자습서에서는 미리 학습된 TensorFlow 모델을 사용하여 웹 사이트 댓글의 감정을 분류하는 방법을 보여 줍니다. 이진 감정 분류자는 Visual Studio를 사용하여 개발된 C# 콘솔 애플리케이션입니다.
ms.date: 09/30/2019
ms.topic: tutorial
ms.custom: mvc
ms.author: nakersha
author: natke
ms.openlocfilehash: e25e884769ad62d3d888986b1475000b543b24b1
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700934"
---
# <a name="tutorial-analyze-sentiment-of-movie-reviews-using-a-pre-trained-tensorflow-model-in-mlnet"></a>자습서: ML.NET에서 미리 학습된 TensorFlow 모델을 사용하여 영화 리뷰의 감정 분석

이 자습서에서는 미리 학습된 TensorFlow 모델을 사용하여 웹 사이트 댓글의 감정을 분류하는 방법을 보여 줍니다. 이진 감정 분류자는 Visual Studio를 사용하여 개발된 C# 콘솔 애플리케이션입니다.

이 자습서에서 사용되는 TensorFlow 모델은 IMDB 데이터베이스의 영화 리뷰를 사용하여 학습되었습니다. 애플리케이션 개발이 완료되면 영화 리뷰 텍스트를 제공할 수 있으며, 애플리케이션이 리뷰가 긍정적 또는 부정적 감정인지 여부를 알려 줍니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> * 미리 학습된 TensorFlow 모델 로드
> * 웹 사이트 댓글 텍스트를 모델에 적합한 기능으로 변환
> * 모델로 예측 수행

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TextClassificationTF) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019).

## <a name="setup"></a>설정

### <a name="create-the-application"></a>애플리케이션 만들기

1. "TextClassificationTF"라는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

2. 프로젝트에서 *Data* 디렉터리를 만들어 데이터 세트 파일을 저장합니다.

3. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. 패키지 소스로 "nuget.org"를 선택하고 **찾아보기** 탭을 선택합니다. **Microsoft.ML**을 검색하고 원하는 패키지를 선택한 다음, **설치** 단추를 선택합니다. 선택한 패키지의 사용 조건에 동의하여 설치를 진행합니다. **Microsoft.ML.TensorFlow**에 대해 이 단계를 반복합니다.

### <a name="add-the-tensorflow-model-to-the-project"></a>TensorFlow 모델을 프로젝트에 추가합니다.

> [!NOTE]
> 이 자습서의 모델은 [dotnet/machinelearning-testdata](https://github.com/dotnet/machinelearning-testdata/tree/master/Microsoft.ML.TensorFlow.TestModels/sentiment_model) GitHub 리포지토리에서 가져온 것입니다. 모델은 TensorFlow SavedModel 형식입니다.

1. [sentiment_model zip 파일](https://github.com/dotnet/samples/blob/master/machine-learning/models/textclassificationtf/sentiment_model.zip?raw=true)을 다운로드하고 압축을 해제합니다

    zip 파일에는 다음 항목이 포함되어 있습니다.

    * `saved_model.pb`: TensorFlow 모델 자체입니다. 이 모델은 IMDB 리뷰 문자열의 텍스트를 나타내는 기능의 고정 길이(크기 600) 정수 배열을 사용하고, 합계가 1인 두 확률, 즉 입력 리뷰가 긍정적 감정일 확률과 입력 리뷰가 부정적 감정일 확률을 출력합니다.
    * `imdb_word_index.csv`: 개별 단어에서 정수 값으로의 매핑입니다. 이 매핑은 TensorFlow 모델에 대한 입력 기능을 생성하는 데 사용됩니다.

2. 가장 안쪽의 `sentiment_model` 디렉터리의 내용을 *TextClassificationTF* 프로젝트 `sentiment_model` 디렉터리에 복사합니다. 이 디렉터리에는 다음 이미지와 같이 이 자습서에 필요한 모델 및 추가 지원 파일이 포함되어 있습니다.

   ![sentiment_model 디렉터리 내용](./media/text-classification-tf/sentiment-model-files.png)

3. 솔루션 탐색기에서 `sentiment_model` 디렉터리 및 하위 디렉터리의 각 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="add-using-statements-and-global-variables"></a>Using 문 및 전역 변수 추가

1. *Program.cs* 파일 맨 위에 다음 추가 `using` 문을 추가합니다.

   [!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/TextClassificationTF/Program.cs#AddUsings "Add necessary usings")]

1. 저장된 모델 파일 경로와 기능 벡터 길이를 보관할 두 개의 전역 변수를 `Main` 메서드 바로 위에 만듭니다.

   [!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/TextClassificationTF/Program.cs#DeclareGlobalVariables "Declare global variables")]

    * `_modelPath`는 학습된 모델의 파일 경로입니다.
    * `FeatureLength`는 모델에 필요한 정수 기능 배열의 길이입니다.

### <a name="model-the-data"></a>데이터 모델링

영화 리뷰는 자유 형식 텍스트입니다. 이 애플리케이션은 여러 불연속 단계에서 모델에 필요한 입력 형식으로 텍스트를 변환합니다.

우선 텍스트를 개별 단어로 분할하고 제공된 매핑 파일을 사용하여 각 단어를 정수 인코딩으로 매핑합니다. 이 변환의 결과는 문장의 단어 수에 해당하는 길이의 가변 길이 정수 배열입니다.

|속성| 값|형식|
|-------------|-----------------------|------|
|ReviewText|this film is really good|string|
|VariableLengthFeatures|14,22,9,66,78,... |int[]|

그러면 가변 길이 기능 배열의 크기가 고정 길이 600으로 조정됩니다. 이것이 TensorFlow 모델에 필요한 길이입니다.

|속성| 값|형식|
|-------------|-----------------------|------|
|ReviewText|this film is really good|string|
|VariableLengthFeatures|14,22,9,66,78,... |int[]|
|기능|14,22,9,66,78,... |int[600]|

1. `Main` 메서드 다음에 입력 데이터에 대한 클래스를 만듭니다.

    [!code-csharp[MovieReviewClass](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#MovieReviewClass "Declare movie review type")]

    입력 데이터 클래스 `MovieReview`에는 사용자 댓글(`ReviewText`)의 `string`이 있습니다.

1. `Main` 메서드 다음에 가변 길이 기능에 대한 클래스를 만듭니다.

    [!code-csharp[VariableLengthFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#VariableLengthFeatures "Declare variable length features type")]

    `VariableLengthFeatures` 속성에는 이를 벡터로 지정하기 위한 [VectorType](xref:Microsoft.ML.Data.VectorTypeAttribute.%23ctor%2A) 특성이 있습니다.  모든 벡터 요소는 같은 유형이어야 합니다. 열 수가 많은 데이터 세트에서 여러 열을 단일 벡터로 로드하면 데이터 변환을 적용할 때 데이터 전달 횟수가 줄어듭니다.

    이 클래스는 `ResizeFeatures` 작업에 사용됩니다. 해당 속성(이 경우에는 하나뿐)의 이름은 사용자 지정 매핑 동작에 대한 _입력_으로 사용할 수 있는 DataView의 열을 나타내는 데 사용됩니다.

1. `Main` 메서드 다음에 고정 길이 기능에 대한 클래스를 만듭니다.

    [!code-csharp[FixedLengthFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#FixedLengthFeatures)]

    이 클래스는 `ResizeFeatures` 작업에 사용됩니다. 해당 속성(이 경우에는 하나뿐)의 이름은 사용자 지정 매핑 동작에 대한 _출력_으로 사용할 수 있는 DataView의 열을 나타내는 데 사용됩니다.

    `Features` 속성의 이름은 TensorFlow 모델에 의해 결정됩니다. 이 속성 이름은 변경할 수 없습니다.

1. `Main` 메서드 다음에 예측에 대한 클래스를 만듭니다.

    [!code-csharp[Prediction](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#Prediction "Declare prediction class")]

    `MovieReviewSentimentPrediction`은 모델 학습 후 사용되는 예측 클래스입니다. `MovieReviewSentimentPrediction`에는 단일 `float` 배열(`Prediction`)과 `VectorType` 특성이 있습니다.

### <a name="create-the-mlcontext-lookup-dictionary-and-action-to-resize-features"></a>MLContext, 조회 사전 및 기능 크기 조정 작업 만들기

[MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작 지점입니다. `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

1. `Main` 메서드의 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 바꾸어 mlContext 변수를 선언하고 초기화합니다.

   [!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateMLContext "Create the ML Context")]

1. 다음 표에 표시된 것처럼 [`LoadFromTextFile`](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%2A) 메서드를 사용하여 파일에서 매핑 데이터를 로드하여 단어를 정수로 인코딩하는 사전을 만듭니다.

    |단어     |인덱스    |
    |---------|---------|
    |kids     |  362    |
    |want     |  181    |
    |wrong    |  355    |
    |effects  |  302    |
    |feeling  |  547    |

    아래 코드를 추가하여 조회 맵을 만듭니다.

    [!code-csharp[CreateLookupMap](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateLookupMap)]

1. 다음 코드 줄을 사용하여 가변 길이 단어 정수 배열의 크기를 고정 크기 정수 배열로 조정하는 `Action`을 추가합니다.

   [!code-csharp[ResizeFeatures](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#ResizeFeatures)]

## <a name="load-the-pre-trained-tensorflow-model"></a>미리 학습된 TensorFlow 모델 로드

1. 코드를 추가하여 TensorFlow 모델을 로드합니다.

    [!code-csharp[LoadTensorFlowModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#LoadTensorFlowModel)]

    모델이 로드되면 해당 입력 및 출력 스키마를 추출할 수 있습니다. 스키마는 관심 및 학습 전용으로 표시됩니다. 최종 애플리케이션이 작동하기 위해 이 코드가 필요하지는 않습니다.

    [!code-csharp[GetModelSchema](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#GetModelSchema)]

    입력 스키마는 정수 인코딩 단어의 고정 길이 배열입니다. 출력 스키마는 리뷰의 감정이 부정적인지 또는 긍정적인지를 나타내는 확률의 부동 소수점 배열입니다. 긍정적 감정의 확률과 부정적 감정의 확률은 보수이므로 이들 값의 합은 1입니다.

## <a name="create-the-mlnet-pipeline"></a>ML.NET 파이프라인 만들기

1. 파이프라인을 만들고 다음 코드 줄과 같이 [TokenizeIntoWords](xref:Microsoft.ML.TextCatalog.TokenizeIntoWords%2A) 변환을 사용하여 텍스트를 단어로 분할해 입력 텍스트를 단어로 나눕니다.

   [!code-csharp[TokenizeIntoWords](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#TokenizeIntoWords)]

   [TokenizeIntoWords](xref:Microsoft.ML.TextCatalog.TokenizeIntoWords%2A) 변환은 공백을 사용하여 텍스트/문자열을 단어로 구문 분석합니다. 새 열을 만들고 각 입력 문자열을 사용자 정의 구분 기호를 기반으로 하는 부분 문자열의 벡터로 분할합니다.

1. 위에서 선언한 조회 테이블을 사용하여 단어를 해당 정수 인코딩으로 매핑합니다.

    [!code-csharp[MapValue](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#MapValue)]

1. 가변 길이 정수 인코딩의 크기를 모델에 필요한 고정 길이에 맞게 조정합니다.

    [!code-csharp[CustomMapping](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CustomMapping)]

1. 로드된 TensorFlow 모델을 사용하여 입력을 분류합니다.

    [!code-csharp[ScoreTensorFlowModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#ScoreTensorFlowModel)]

    TensorFlow 모델 출력은 `Prediction/Softmax`입니다. `Prediction/Softmax`은 TensorFlow 모델에 의해 결정된 이름입니다. 이 이름은 변경할 수 없습니다.

1. 출력 예측에 대한 새 열을 만듭니다.

    [!code-csharp[SnippetCopyColumns](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#SnippetCopyColumns)]

    `Prediction/Softmax` 열을 C# 클래스에서 속성으로 사용할 수 있는 이름을 가진 열로 복사해야 합니다. `Prediction`. C# 속성 이름에 `/` 문자는 허용되지 않습니다.

## <a name="create-the-mlnet-model-from-the-pipeline"></a>파이프라인에서 ML.NET 모델 만들기

1. 코드를 추가하여 파이프라인에서 모델을 만듭니다.

    [!code-csharp[SnippetCreateModel](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#SnippetCreateModel)]

    ML.NET 모델은 `Fit` 메서드를 호출하여 파이프라인의 추정기 체인에서 만들어집니다. 이 경우에는 TensorFlow 모델이 이미 학습되었으므로 모델을 만들기 위해 데이터 맞춤을 수행하지 않습니다. `Fit` 메서드의 요구 사항을 충족하기 위해 빈 데이터 보기 개체를 제공합니다.

## <a name="use-the-model-to-make-a-prediction"></a>모델로 예측 수행

1. `Main` 메서드 아래에 `PredictSentiment` 메서드를 추가합니다.

    ```csharp
    public static void PredictSentiment(MLContext mlContext, ITransformer model)
    {

    }
    ```

1. `PredictSentiment()` 메서드의 첫째 줄과 같이 다음 코드를 추가하여 `PredictionEngine`을 만듭니다.

    [!code-csharp[CreatePredictionEngine](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreatePredictionEngine)]

    [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)은 데이터의 단일 인스턴스에 대한 예측을 수행할 수 있는 편리한 API입니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 단일 스레드 또는 프로토타입 환경에서 사용할 수 있습니다. 프로덕션 환경에서 성능 및 스레드 보안을 개선하려면 `PredictionEnginePool` 서비스를 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다. [ASP.NET Core 웹 API에서 `PredictionEnginePool`을 사용하는 방법](https://docs.microsoft.com/en-us/dotnet/machine-learning/how-to-guides/serve-model-web-api-ml-net#register-predictionenginepool-for-use-in-the-application)에 대한 자세한 내용은 이 가이드를 참조하세요.

    > [!NOTE]
    > `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

1. `MovieReview` 인스턴스를 만들어 댓글을 추가하여 `Predict()` 메서드에서 학습된 모델의 예측을 테스트합니다.

    [!code-csharp[CreateTestData](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CreateTestData)]

1. `PredictSentiment()` 메서드의 다음 코드 줄을 추가하여 테스트 댓글 데이터를 `Prediction Engine`에 전달합니다.

    [!code-csharp[Predict](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#Predict)]

1. [Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) 함수는 단일 데이터 행에 대한 예측을 수행합니다.

    |속성| 값|형식|
    |-------------|-----------------------|------|
    |예측|[0.5459937, 0.454006255]|float[]|

1. 다음 코드를 사용하여 감정 예측을 표시합니다.

    [!code-csharp[DisplayPredictions](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#DisplayPredictions)]

1. `Main` 메서드의 끝에 `PredictSentiment` 호출을 추가합니다.

    [!code-csharp[CallPredictSentiment](~/samples/machine-learning/tutorials/TextClassificationTF/Program.cs#CallPredictSentiment)]

## <a name="results"></a>결과

애플리케이션을 빌드하고 실행합니다.

다음과 같은 결과가 나타나야 합니다. 처리 중 메시지가 표시됩니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 이러한 메시지는 다음 결과에서 제거되었습니다.

```console
Number of classes: 2
Is sentiment/review positive ? Yes
```

지금까지 이제 ML.NET에서 미리 학습된 `TensorFlow` 모델을 재사용하여 메시지 감정을 분류하고 예측하기 위한 기계 학습 모델을 성공적으로 빌드했습니다.

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TextClassificationTF) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> * 미리 학습된 TensorFlow 모델 로드
> * 웹 사이트 댓글 텍스트를 모델에 적합한 기능으로 변환
> * 모델로 예측 수행
