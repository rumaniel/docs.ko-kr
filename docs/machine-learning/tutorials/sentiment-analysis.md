---
title: 감정 분석 이진 분류 시나리오에서 ML.NET 사용
description: 감정 예측을 통해 적절한 작업을 수행하는 방법을 이해하기 위해 이진 분류 시나리오에서 ML.NET을 사용하는 방법을 살펴봅니다.
ms.date: 06/04/2018
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: fd0a1ad246c6d50db35e3d0f0332a82b256902c1
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453166"
---
# <a name="tutorial-use-mlnet-in-a-sentiment-analysis-binary-classification-scenario"></a>자습서: 감정 분석 이진 분류 시나리오에서 ML.NET 사용

> [!NOTE]
> 이 항목은 현재 미리 보기로 제공되는 ML.NET을 참조하며, 자료는 변경될 수 있습니다. 자세한 내용은 [ML.NET 소개](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)를 참조하세요.

이 샘플 자습서에서는 ML.NET을 사용하여 Visual Studio 2017에서 C#를 사용하는 .NET Core 콘솔 응용 프로그램을 통해 감정 분류자를 만드는 방법에 대해 설명합니다.

이 자습서에서는 다음 방법을 학습합니다.
> [!div class="checklist"]
> * 문제 이해
> * 적절한 기계 학습 작업 선택
> * 데이터 준비
> * 학습 파이프라인 만들기
> * 분류자 로드
> * 모델 학습
> * 다른 데이터 집합을 사용하여 모델 평가
> * 모델을 사용하여 테스트 데이터 결과 예측

## <a name="sentiment-analysis-sample-overview"></a>감정 분석 샘플 개요

샘플은 ML.NET을 사용하여 감정을 긍정적 또는 부정적으로 분류하고 예측하는 모델을 학습시키는 콘솔 앱입니다. 또한 품질 분석을 위해 두 번째 데이터 집합을 사용하여 모델을 평가합니다. 감정 데이터 집합은 WikiDetox 프로젝트에서 가져옵니다.

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

* [Wikipedia detox 줄 데이터 탭 구분 파일(wikiPedia-detox-250-line-data.tsv)](https://github.com/dotnet/machinelearning/blob/master/test/data/wikipedia-detox-250-line-data.tsv).
* [Wikipedia detox 줄 테스트 탭 구분 파일(wikipedia-detox-250-line-test.tsv)](https://github.com/dotnet/machinelearning/blob/master/test/data/wikipedia-detox-250-line-test.tsv).

## <a name="machine-learning-workflow"></a>기계 학습 워크플로

이 자습서는 프로세스가 체계적으로 이동할 수 있도록 하는 기계 학습 워크플로를 따릅니다.

워크플로 단계는 다음과 같습니다.

1. **문제 이해**
2. **데이터 수집**
3. **데이터 전처리 및 기능 엔지니어링**
4. **모델 학습 및 예측**
5. **모델 평가**
6. **모델 연산화**

### <a name="understand-the-problem"></a>문제 이해

먼저 문제를 이해해야 하므로 모델 빌드 및 학습을 지원할 수 있는 부분으로 문제를 구분할 수 있습니다. 문제를 구분하면 결과를 예측하고 평가할 수 있습니다.

이 자습서의 문제는 들어오는 웹 사이트 댓글 감정을 이해하여 적절한 작업을 수행하는 것입니다.

모델 학습에 사용할 데이터의 감정 텍스트와 감정 값 및 평가 후 조작에 사용할 수 있는 예측 감정 값으로 문제를 구분할 수 있습니다.

그런 다음, 기계 학습 작업 선택에 도움이 되는 감정을 **확인**해야 합니다.

## <a name="select-the-appropriate-machine-learning-task"></a>적절한 기계 학습 작업 선택

이 문제에서 다음 사실을 알 수 있습니다.

학습 데이터: 웹 사이트 댓글은 긍정적 또는 부정적(**감정**)일 수 있습니다.
다음 예제와 같이 새로운 웹 사이트 댓글의 **감정**을 긍정적 또는 부정적으로 예측합니다.

* Wikipedia에 의미 없는 내용을 추가하지 마세요.
* 그는 최고이고 기사에 이 내용이 언급되어야 합니다.

분류 기계 학습 작업이 이 시나리오에 가장 적합합니다.

### <a name="about-the-classification-task"></a>분류 작업 정보

분류는 데이터를 사용하여 데이터 항목 또는 행의 범주, 형식 또는 클래스를 **확인**하는 기계 학습 작업입니다. 예를 들어 분류를 사용하여 다음을 수행할 수 있습니다.

* 감정을 긍정적 또는 부정적으로 식별합니다.
* 전자 메일을 스팸, 정크 또는 정상으로 분류합니다.
* 환자의 실험실 샘플이 종양성인지 확인합니다.
* 영업 캠페인에 응답하는 고객의 성향을 기준으로 고객을 분류합니다.

일반적으로 분류 작업은 다음 형식 중 하나입니다.

* 이진: A 또는 B.
* 다중 클래스: 단일 모델을 사용하여 예측할 수 있는 여러 범주.

## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

1. Visual Studio 2017을 엽니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. **새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **.NET Core** 노드를 차례로 선택합니다. 그런 다음 **콘솔 앱(.NET Core)** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 “SentimentAnalysis”를 입력한 다음, **확인** 단추를 선택합니다.

2. 프로젝트에서 *Data* 디렉터리를 만들어 데이터 집합 파일을 저장합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. “Data”를 입력하고 Enter 키를 누릅니다.

3. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

### <a name="prepare-your-data"></a>데이터 준비

1. [WikiPedia detox-250-line-data.tsv](https://github.com/dotnet/machinelearning/blob/master/test/data/wikipedia-detox-250-line-data.tsv) 및 [wikipedia-detox-250-line-test.tsv](https://github.com/dotnet/machinelearning/blob/master/test/data/wikipedia-detox-250-line-test.tsv) 데이터 집합을 다운로드하여 이전에 만든 *Data* 폴더에 저장합니다. 첫 번째 데이터 집합은 기계 학습 모델을 교육하고 두 번째 데이터 집합은 모델이 얼마나 정확한지 평가하는 데 사용할 수 있습니다.

2. 솔루션 탐색기에서 각 \*.tsv 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

*Program.cs* 파일 맨 위에 다음 추가 `using` 문을 추가합니다.

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#1 "Add necessary usings")]

최근에 다운로드한 파일의 경로를 포함할 세 개의 전역 필드를 만들어야 합니다.

* `_dataPath`에는 모델을 학습시키는 데 사용되는 데이터 집합의 경로가 포함됩니다.
* `_testDataPath`에는 모델을 평가하는 데 사용되는 데이터 집합의 경로가 포함됩니다.
* `_modelPath`에는 학습된 모델이 저장되는 경로가 포함됩니다.

`Main` 메서드 바로 위의 줄에 다음 코드를 추가하여 해당 경로를 지정합니다.

[!code-csharp[Declare file variables](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#2 "Declare variables to store data files")]

입력 데이터 및 예측에 대한 일부 클래스를 만들어야 합니다. 새 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.

1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *SentimentData.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *SentimentData.cs*의 맨 위에 추가합니다.

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/SentimentAnalysis/SentimentData.cs#1 "Add necessary usings")]

기존 클래스 정의를 제거하고 두 개의 클래스 `SentimentData` 및 `SentimentPrediction`가 있는 다음 코드를 *SentimentData.cs* 파일에 추가합니다.

[!code-csharp[DeclareTypes](../../../samples/machine-learning/tutorials/SentimentAnalysis/SentimentData.cs#2 "Declare data record types")]

`SentimentData`는 입력 데이터 집합 클래스이며 긍정적 또는 부정적 감정 값을 가진 `float`(`Sentiment`) 및 댓글 문자열(`SentimentText`)을 포함합니다. 두 필드에 모두 `Column` 특성이 연결되어 있습니다. 이 특성은 데이터 파일의 각 필드 순서와 어떤 것이 `Label` 필드인지 설명합니다. `SentimentPrediction`은 모델이 학습된 후 예측에 사용되는 클래스입니다. 여기에는 단일 부울(`Sentiment`)과 `PredictedLabel` `ColumnName` 특성이 포함됩니다. `Label`은 모델을 만들고 학습시키는 데 사용되며 두 번째 데이터 집합과 함께 모델을 평가하는 데도 사용됩니다. `PredictedLabel`은 예측 및 평가 중에 사용됩니다. 평가를 위해 학습 데이터가 있는 입력, 예측 값 및 모델이 사용됩니다.

*Program.cs* 파일에서 다음 예제와 같이 `void`를 `async Task`로 바꿔 `Main` 메서드 시그니처를 변경합니다.

```csharp
static async Task Main(string[] args) 
{

}
```

나중에 모델을 zip 파일로 저장할 것이고 해당 외부 작업이 완료될 때까지 프로그램이 대기해야 하므로 <xref:System.Threading.Tasks.Task> 반환 형식을 사용하여 `async`를 `Main`에 추가합니다.

> [!NOTE]
> *비동기 기본* 메서드를 통해 `Main` 메서드에서 `await`를 사용할 수 있습니다. 자세한 내용은 C# 프로그래밍 가이드의 [async main](../../../docs/csharp/programming-guide/main-and-command-args/index.md) 항목을 참조하세요.

`Main` 메서드에서 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 바꿉니다.

[!code-csharp[Train](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#3 "Train your model")]

`Train` 메서드는 다음 작업을 실행합니다.

* 데이터를 로드 또는 수집합니다.
* 데이터를 전처리 및 기능화합니다.
* 모델을 학습시킵니다.
* 테스트 데이터를 기반으로 감정을 예측합니다.

다음 코드를 사용하여 `Main` 메서드 바로 뒤에 `Train` 메서드를 만듭니다.

```csharp
public static async Task<PredictionModel<SentimentData, SentimentPrediction>> Train()
{

}
```

## <a name="ingest-the-data"></a>데이터 수집

데이터 로드, 데이터 처리/기능화 및 모델을 포함할 <xref:Microsoft.ML.Legacy.LearningPipeline>의 새 인스턴스를 초기화합니다. 다음 코드를 `Train` 메서드의 첫 번째 줄로 추가합니다.

[!code-csharp[LearningPipeline](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#5 "Create a learning pipeline")]

<xref:Microsoft.ML.Legacy.Data.TextLoader> 개체는 파이프라인의 첫 번째 부분이며 학습 파일 데이터를 로드합니다.

[!code-csharp[TextLoader](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#6 "Add a text loader to the pipeline")]

## <a name="data-preprocess-and-feature-engineering"></a>데이터 전처리 및 기능 엔지니어링

데이터 전처리 및 정리는 데이터 집합이 기계 학습에 효과적으로 사용되기 전에 수행되는 중요한 작업입니다. 원시 데이터는 종종 정리되지 않고 불안정하며 값이 누락될 수 있습니다. 이러한 모델링 작업 없이 데이터를 사용하면 잘못된 결과를 얻을 수 있습니다. ML.NET의 변환 파이프라인을 사용하면 학습 또는 테스트 전에 데이터에 적용되는 사용자 지정 변환 집합을 작성할 수 있습니다. 변환의 기본 목적은 데이터 기능화입니다. 변환 파이프라인의 장점은 변환 파이프라인 정의 후에 파이프라인을 저장하여 테스트 데이터에 적용하는 것입니다.

<xref:Microsoft.ML.Legacy.Transforms.TextFeaturizer>를 적용하여 `SentimentText` 열을 기계 학습 알고리즘에 사용되는 `Features`라는 [숫자 벡터](../resources/glossary.md#numerical-feature-vector)로 변환합니다. 이것이 전처리/기능화 단계입니다. ML.NET에서 사용 가능한 추가 구성 요소를 사용하면 모델에서 더 나은 결과를 얻을 수 있습니다. `TextFeaturizer`를 다음 코드 줄로 파이프라인에 추가합니다.

[!code-csharp[TextFeaturizer](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#7 "Add a TextFeaturizer to the pipeline")]

## <a name="choose-a-learning-algorithm"></a>학습 알고리즘 선택

<xref:Microsoft.ML.Legacy.Trainers.FastTreeBinaryClassifier> 개체는 이 파이프라인에서 사용할 의사 결정 트리 학습자입니다. 기능화 단계와 비슷하게 ML.NET에서 사용 가능한 다양한 학습자를 시도하고 매개 변수를 변경하면 다른 결과가 생성됩니다. 튜닝의 경우 <xref:Microsoft.ML.Legacy.Trainers.FastTreeBinaryClassifier.NumTrees>, <xref:Microsoft.ML.Legacy.Trainers.FastTreeBinaryClassifier.NumLeaves> 및 <xref:Microsoft.ML.Legacy.Trainers.FastTreeBinaryClassifier.MinDocumentsInLeafs> 같은 [하이퍼 매개 변수](../resources/glossary.md#hyperparameter)를 설정합니다. 이러한 하이퍼 매개 변수는 모델에 영향을 주기 전에 설정되며 모델별로 다릅니다. 성능을 위해 의사 결정 트리를 튜닝하는 데 사용되므로 값이 클수록 성능에 부정적인 영향을 줄 수 있습니다.

`Train` 메서드에 다음 코드를 추가합니다.

[!code-csharp[BinaryClassifier](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#8 "Add a fast binary tree classifier")]

## <a name="train-the-model"></a>모델 학습

로드되고 변환된 데이터 집합을 기반으로 <xref:Microsoft.ML.Legacy.PredictionModel%602> 모델을 학습시킵니다. `pipeline.Train<SentimentData, SentimentPrediction>()`은 파이프라인을 학습시킵니다(데이터를 로드하고 기능화기 및 학습자를 학습시킴). 이 문제가 발생할 때까지 실험이 실행되지 않습니다.

`Train` 메서드에 다음 코드를 추가합니다.

[!code-csharp[TrainModel](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#9 "Train the model")]

### <a name="save-and-return-the-model-trained-to-use-for-evaluation"></a>평가에 사용하기 위해 학습된 모델 저장 및 반환

이 시점에 기존 또는 새 .NET 응용 프로그램에 통합할 수 있는 모델이 있습니다. 반환하기 전에 모델을 .zip 파일로 저장하려면 다음 코드를 `Train`의 다음 줄에 추가합니다.

[!code-csharp[SaveModel](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#10 "Save the model")]

`Train` 메서드의 끝에 모델을 반환합니다.

[!code-csharp[ReturnModel](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#11 "Return the model")]

## <a name="evaluate-the-model"></a>모델 평가

이제 모델을 만들고 학습시켰으므로 품질 보증 및 유효성 검사를 위해 다른 데이터 집합을 사용하여 평가해야 합니다. `Evaluate` 메서드에서는 `Train`에서 만들어진 모델을 전달하여 평가합니다. 다음 코드와 같이 `Train` 바로 뒤에 `Evaluate` 메서드를 만듭니다.

```csharp
public static void Evaluate(PredictionModel<SentimentData, SentimentPrediction> model)
{

}
```

`Evaluate` 메서드는 다음 작업을 실행합니다.

* 테스트 데이터 집합을 로드합니다.
* 이진 평가자를 만듭니다.
* 모델을 평가하고 메트릭을 만듭니다.
* 메트릭을 표시합니다.

다음 코드를 사용하여 `Train` 메서드 호출 바로 아래에 `Main` 메서드의 새 메서드 호출을 추가합니다.

[!code-csharp[CallEvaluate](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#12 "Call the Evaluate method")]

<xref:Microsoft.ML.Legacy.Data.TextLoader> 클래스는 동일한 스키마를 사용하여 새 테스트 데이터 집합을 로드합니다. 이 데이터 집합을 품질 검사로 사용하여 모델을 평가할 수 있습니다. `Evaluate` 메서드에 다음 코드를 추가합니다.

[!code-csharp[LoadText](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#13 "Load the test dataset")]

<xref:Microsoft.ML.Legacy.Models.BinaryClassificationEvaluator> 개체는 지정된 데이터 집합을 사용하여 `PredictionModel`에 대한 품질 메트릭을 계산합니다. 해당 메트릭을 확인하려면 다음 코드를 사용하여 `Evaluate` 메서드의 다음 줄로 평가자를 추가합니다.

[!code-csharp[BinaryEvaluator](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#14 "Create the binary evaluator")]

<xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics>에는 이진 분류 평가자가 계산한 전체 메트릭이 포함됩니다. 모델의 품질을 확인하기 위해 이러한 메트릭을 표시하려면 먼저 메트릭을 가져와야 합니다. 다음 코드를 추가합니다.

[!code-csharp[CreateMetrics](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#15 "Evaluate the model and create metrics")]

### <a name="displaying-the-metrics-for-model-validation"></a>모델 유효성 검사를 위해 메트릭 표시

다음 코드를 사용하여 메트릭을 표시하고, 결과를 공유한 다음, 작업을 수행합니다.

[!code-csharp[DisplayMetrics](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#16 "Display selected metrics")]

## <a name="predict-the-test-data-outcomes-with-the-model"></a>모델을 사용하여 테스트 데이터 결과 예측

다음 코드를 사용하여 `Evaluate` 메서드 바로 뒤에 `Predict` 메서드를 만듭니다.

```csharp
public static void Predict(PredictionModel<SentimentData, SentimentPrediction> model)
{

}
```

`Predict` 메서드는 다음 작업을 실행합니다.

* 테스트 데이터를 만듭니다.
* 테스트 데이터를 기반으로 감정을 예측합니다.
* 보고를 위해 테스트 데이터 및 예측을 결합합니다.
* 예측 결과를 표시합니다.

다음 코드를 사용하여 `Evaluate` 메서드 호출 바로 아래에 `Main` 메서드의 새 메서드 호출을 추가합니다.

[!code-csharp[CallEvaluate](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#17 "Call the Predict method")]

몇몇 댓글을 추가하여 `Predict` 메서드에서 학습된 모델의 예측을 테스트합니다.

[!code-csharp[PredictionData](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#18 "Create test data for predictions")]

이제 모델이 있으므로 <xref:Microsoft.ML.Legacy.PredictionModel.Predict%2A?displayProperty=nameWithType> 메서드를 사용하여 댓글 데이터의 긍정적 또는 부정적 감정을 예측하는 데 모델을 사용할 수 있습니다. 예측을 가져오려면 새 데이터에서 `Predict`를 사용합니다. 입력 데이터는 문자열이고 모델은 기능화를 포함합니다. 파이프라인은 학습 및 예측 중에 동기화됩니다. 특별히 예측을 위해 전처리/기능화 코드를 작성할 필요가 없고 동일한 API가 배치 및 일회성 예측을 둘 다 처리합니다.

[!code-csharp[Predict](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#19 "Create predictions of sentiments")]

### <a name="model-operationalization-prediction"></a>모델 연산화: 예측

결과를 공유하고 이에 따라 작업을 수행하기 위해 `SentimentText` 및 해당 감정 예측을 표시합니다. 이것을 반환된 데이터를 운영 정책의 일부로 사용하는 연산화라고 합니다. 다음 <xref:System.Console.WriteLine?displayProperty=nameWithType> 코드를 사용하여 결과에 대한 헤더를 만듭니다.

[!code-csharp[OutputHeaders](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#20 "Display prediction outputs")]

예측 결과를 표시하기 전에 감정과 예측을 결합하여 예측된 감정이 있는 원래 주석을 확인합니다. 다음 코드는 <xref:System.Linq.Enumerable.Zip%2A> 메서드를 사용하여 작업이 수행되도록 하므로, 다음으로 해당 코드를 추가합니다.

[!code-csharp[BuildTuples](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#21 "Build the pairs of sentiment data and predictions")]

이제 `SentimentText` 및 `Sentiment`를 클래스로 결합했으므로 <xref:System.Console.WriteLine?displayProperty=nameWithType> 메서드를 사용하여 결과를 표시할 수 있습니다.

[!code-csharp[DisplayPredictions](../../../samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#22 "Display the predictions")]

유추된 튜플 요소 이름은 C# 7.1의 새로운 기능이고 프로젝트의 기본 언어 버전은 C# 7.0이므로 언어 버전을 C# 7.1 이상으로 변경해야 합니다.
이 작업을 하려면 **솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **빌드** 탭을 선택하고 **고급** 단추를 선택합니다. 드롭다운에서 **C# 7.1**(또는 이상 버전)을 선택합니다. **확인** 단추를 선택합니다.

## <a name="results"></a>결과

다음과 같은 결과가 나타나야 합니다. 파이프라인이 처리할 때 메시지를 표시합니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 이러한 결과는 다음 결과에서 제거되었습니다.

```

PredictionModel quality metrics evaluation
------------------------------------------
Accuracy: 66.67%
Auc: 94.44%
F1Score: 75.00%

Sentiment Predictions
---------------------
Sentiment: Please refrain from adding nonsense to Wikipedia. | Prediction: Negative
Sentiment: He is the best, and the article should say that. | Prediction: Positive

```

지금까지 이제 메시지 감정을 분류하고 예측하기 위한 기계 학습 모델을 성공적으로 빌드했습니다. [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/SentimentAnalysis) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법을 학습했습니다.
> [!div class="checklist"]
> * 문제 이해
> * 적절한 기계 학습 작업 선택
> * 데이터 준비
> * 학습 파이프라인 만들기
> * 분류자 로드
> * 모델 학습
> * 다른 데이터 집합을 사용하여 모델 평가
> * 모델을 사용하여 테스트 데이터 결과 예측

다음 자습서로 이동하여 자세히 알아보기
> [!div class="nextstepaction"]
> [택시 요금 예측기](taxi-fare.md)
