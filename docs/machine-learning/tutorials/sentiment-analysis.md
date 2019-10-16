---
title: '자습서: 웹 사이트 주석 분석 -이진 분류'
description: 이 자습서에서는 웹 사이트 주석에서 감정을 분류하고 적절한 조치를 취하는 .NET Core 콘솔 애플리케이션을 만드는 방법을 보여 줍니다. 감정 이진 분류자는 Visual Studio에서 C#을 사용합니다.
ms.date: 09/30/2019
ms.topic: tutorial
ms.custom: mvc, seodec18
ms.openlocfilehash: c6b9d51a8ab91b4365c909993211f11ab3436808
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700853"
---
# <a name="tutorial-analyze-sentiment-of-website-comments-with-binary-classification-in-mlnet"></a>자습서: ML.NET에서 이진 분류를 사용하여 웹 사이트 주석의 감정 분석

이 자습서에서는 웹 사이트 주석에서 감정을 분류하고 적절한 조치를 취하는 .NET Core 콘솔 애플리케이션을 만드는 방법을 보여 줍니다. 이 감정 이진 분류자는 Visual Studio 2017에서 C#을 사용합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> - 콘솔 애플리케이션 만들기
> - 데이터 준비
> - 데이터 로드
> - 모델 빌드 및 학습
> - 모델 평가
> - 모델로 예측 수행
> - 결과 보기

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/SentimentAnalysis) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="prerequisites"></a>전제 조건

- “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

- [UCI Sentiment Labeled Sentences 데이터 세트](https://archive.ics.uci.edu/ml/machine-learning-databases/00331/sentiment%20labelled%20sentences.zip)(zip 파일)

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

1. "SentimentAnalysis"라고 하는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

2. 프로젝트에서 *Data* 디렉터리를 만들어 데이터 세트 파일을 저장합니다.

3. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. 패키지 소스로 "nuget.org"를 선택하고 **찾아보기** 탭을 선택합니다. **Microsoft.ML**을 검색하고 원하는 패키지를 선택한 다음, **설치** 단추를 선택합니다. 선택한 패키지의 사용 조건에 동의하여 설치를 진행합니다. **Microsoft.ML.FastTree** NuGet 패키지에 대해 동일한 작업을 수행합니다.

## <a name="prepare-your-data"></a>데이터 준비

> [!NOTE]
> 이 자습서의 데이터 세트는 ‘From Group to Individual Labels using Deep Features’(Kotzias 외, KDD 2015)에서 제공되고 UCI Machine Learning Repository(Dua, D. 및 Karra Taniskidou, E. (2017))에서 호스트됩니다. UCI Machine Learning Repository[http://archive.ics.uci.edu/ml ]. Irvine, CA: University of California, School of Information and Computer Science.

1. [UCI Sentiment Labeled Sentences 데이터 세트 ZIP 파일](https://archive.ics.uci.edu/ml/machine-learning-databases/00331/sentiment%20labelled%20sentences.zip)을 다운로드하여 압축을 풉니다.

2. 만든 *Data* 디렉터리에 `yelp_labelled.txt` 파일을 복사합니다.

3. 솔루션 탐색기에서 `yelp_labeled.txt` 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

1. *Program.cs* 파일 맨 위에 다음 추가 `using` 문을 추가합니다.

    [!code-csharp[AddUsings](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#AddUsings "Add necessary usings")]

2. 최근에 다운로드한 데이터 세트 파일 경로 및 저장된 모델 파일 경로를 포함할 두 개의 글로벌 필드를 만듭니다.

    - `_dataPath`에는 모델을 학습시키는 데 사용되는 데이터 세트의 경로가 포함됩니다.
    - `_modelPath`에는 학습된 모델이 저장되는 경로가 포함됩니다.

3. `Main` 메서드 바로 위의 줄에 다음 코드를 추가하여 해당 경로를 지정합니다.

    [!code-csharp[Declare global variables](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#DeclareGlobalVariables "Declare global variables")]

4. 이제 입력 데이터 및 예측에 대한 클래스를 만듭니다. 새 클래스를 프로젝트에 추가합니다.

    - **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.

    - **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *SentimentData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

5. *SentimentData.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *SentimentData.cs*의 맨 위에 추가합니다.

    [!code-csharp[AddUsings](~/samples/machine-learning/tutorials/SentimentAnalysis/SentimentData.cs#AddUsings "Add necessary usings")]

6. 기존 클래스 정의를 제거하고 두 개의 클래스 `SentimentData` 및 `SentimentPrediction`가 있는 다음 코드를 *SentimentData.cs* 파일에 추가합니다.

    [!code-csharp[DeclareTypes](~/samples/machine-learning/tutorials/SentimentAnalysis/SentimentData.cs#DeclareTypes "Declare data record types")]

### <a name="how-the-data-was-prepared"></a>데이터를 준비하는 방법
입력 데이터 세트 클래스 `SentimentData`는 사용자 주석에 대한 `string`(`SentimentText`) 및 감정에 대해 1(긍정) 또는 0(부정) 값을 갖는 `bool`(`Sentiment`)를 갖습니다. 두 필드에는 각 필드의 데이터 파일 순서를 설명하는 [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) 특성이 연결되어 있습니다.  또한 `Sentiment` 속성에는 `Label` 필드로 지정하는 [ColumnName](xref:Microsoft.ML.Data.ColumnNameAttribute.%23ctor%2A) 특성이 있습니다. 다음 예제 파일에는 머리글 행이 없고 다음과 같이 표시됩니다.

|SentimentText                         |감정(레이블) |
|--------------------------------------|----------|
|웨이트리스의 서비스가 좀 느렸습니다.|    0     |
|모양이 별로 였습니다.                    |    0     |
|우와... 여기가 좋았습니다.              |    1     |
|서비스가 매우 신속합니다.              |    1     |

`SentimentPrediction`은 모델 학습 후에 사용되는 예측 클래스입니다. 출력 예측과 함께 입력 `SentimentText`를 표시할 수 있도록 `SentimentData`에서 상속됩니다. `Prediction` 부울은 새 입력 `SentimentText`와 함께 제공될 때 모델이 예측하는 값입니다.

출력 클래스 `SentimentPrediction`에는 `Score`(모델에서 계산한 원시 점수) 및 `Probability`(긍정적인 감정이 있는 텍스트의 가능성에 따라 조정된 점수)가 포함되어 있습니다.

이 자습서에서 가장 중요한 속성은 `Prediction`입니다.

## <a name="load-the-data"></a>데이터 로드
ML.NET의 데이터는 [IDataView 클래스](xref:Microsoft.ML.IDataView)로 표시됩니다. `IDataView`는 표 형식 데이터(숫자 및 텍스트)를 유연하고 효율적으로 설명하는 방법입니다. 데이터를 텍스트 파일 또는 실시간(예: SQL 데이터베이스 또는 로그 파일)에서 `IDataView` 개체로 로드할 수 있습니다.

[MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작 지점입니다. `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

앱을 준비한 다음, 데이터를 로드합니다.

1. `Main` 메서드의 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 바꾸어 mlContext 변수를 선언하고 초기화합니다.

    [!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CreateMLContext "Create the ML Context")]

2. `Main()` 메서드에 아래 코드를 다음 코드 줄로 추가합니다.

    [!code-csharp[CallLoadData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CallLoadData)]

3. 다음 코드를 사용하여 `Main()` 메서드 바로 뒤에 `LoadData()` 메서드를 만듭니다.

    ```csharp
    public static TrainTestData LoadData(MLContext mlContext)
    {

    }
    ```

    `LoadData()` 메서드는 다음 작업을 실행합니다.

    - 데이터를 로드합니다.
    - 로드된 데이터 세트를 학습 및 테스트 세트로 분할합니다.
    - 분할된 학습 및 테스트 데이터 세트를 반환합니다.

4. 다음 코드를 `LoadData()` 메서드의 첫 번째 줄로 추가합니다.

    [!code-csharp[LoadData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#LoadData "loading dataset")]

    [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)은 데이터 스키마를 정의하고 파일에서 읽습니다. 데이터 경로 변수를 가져와서 `IDataView`를 반환합니다.

### <a name="split-the-dataset-for-model-training-and-testing"></a>데이터 세트를 모델 학습 및 테스트용으로 분할

모델을 준비할 때는 일부 데이터 세트는 학습에, 일부 데이터 세트는 모델 정확도 테스트에 사용합니다.

1. 로드된 데이터를 필요한 데이터 세트로 분할하려면 `LoadData()` 메서드에 아래 코드를 다음 줄로 추가합니다.

    [!code-csharp[SplitData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#SplitData "Split the Data")]

    앞의 코드는 [TrainTestSplit()](xref:Microsoft.ML.DataOperationsCatalog.TrainTestSplit%2A) 메서드를 사용하여 로드된 데이터 세트를 학습으로 분할하고 데이터 세트를 테스트하며 [TrainTestData](xref:Microsoft.ML.DataOperationsCatalog.TrainTestData) 클래스에 반환합니다. `testFraction` 매개 변수로 데이터의 테스트 집합 백분율을 지정합니다. 기본값은 10%이며, 여기서는 20%를 사용하여 데이터를 더 평가합니다.

2. `splitDataView` 메서드의 끝에 `LoadData()`를 반환합니다.

    [!code-csharp[ReturnSplitData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#ReturnSplitData)]

## <a name="build-and-train-the-model"></a>모델 빌드 및 학습

1. `BuildAndTrainModel` 메서드에 다음 호출을 `Main()` 메서드의 다음 코드 줄로 추가합니다.

    [!code-csharp[CallBuildAndTrainModel](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CallBuildAndTrainModel)]

    `BuildAndTrainModel()` 메서드는 다음 작업을 실행합니다.

    - 데이터를 추출하고 변환합니다.
    - 모델을 학습시킵니다.
    - 테스트 데이터를 기반으로 감정을 예측합니다.
    - 모델을 반환합니다.

2. 다음 코드를 사용하여 `Main()` 메서드 바로 뒤에 `BuildAndTrainModel()` 메서드를 만듭니다.

    ```csharp
    public static ITransformer BuildAndTrainModel(MLContext mlContext, IDataView splitTrainSet)
    {

    }
    ```

### <a name="extract-and-transform-the-data"></a>데이터 추출 및 변환

1. `FeaturizeText`를 다음 코드 줄로 추가합니다.

    [!code-csharp[FeaturizeText](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#FeaturizeText "Featurize the text")]

    이전 코드의 `FeaturizeText()` 메서드는 텍스트 열(`SentimentText`)을 기계 학습 알고리즘에서 사용하는 숫자 키 형식 `Features` 열로 변환하여 새 데이터 세트 열로 추가합니다.

    |SentimentText                         |감정 |기능              |
    |--------------------------------------|----------|----------------------|
    |웨이트리스의 서비스가 좀 느렸습니다.|    0     |[0.76, 0.65, 0.44, …] |
    |모양이 별로 였습니다.                    |    0     |[0.98, 0.43, 0.54, …] |
    |우와... 여기가 좋았습니다.              |    1     |[0.35, 0.73, 0.46, …] |
    |서비스가 매우 신속합니다.              |    1     |[0.39, 0, 0.75, …]    |

### <a name="add-a-learning-algorithm"></a>학습 알고리즘 추가

이 앱은 항목 또는 데이터 행을 분류하는 분류 알고리즘을 사용합니다. 앱은 웹 사이트 주석을 긍정 또는 부정으로 분류하므로 이진 분류 작업을 사용합니다.

`BuildAndTrainModel()`의 다음 코드 줄로 다음을 추가하여 데이터 변환 정의에 기계 학습 작업을 추가합니다.

[!code-csharp[SdcaLogisticRegressionBinaryTrainer](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#AddTrainer "Add a SdcaLogisticRegressionBinaryTrainer")]

[SdcaLogisticRegressionBinaryTrainer](xref:Microsoft.ML.Trainers.SdcaLogisticRegressionBinaryTrainer)는 분류 학습 알고리즘입니다. 이것은 `estimator`에 추가되며, 기록 데이터에서 학습할 기능화된 `SentimentText`(`Features`) 및 `Label` 입력 매개 변수를 수락합니다.

### <a name="train-the-model"></a>모델 학습

모델을 `splitTrainSet` 데이터에 맞추고 `BuildAndTrainModel()` 메서드에서 다음 줄의 코드로 다음 항목을 추가하여 학습된 모델을 반환합니다.

[!code-csharp[TrainModel](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#TrainModel "Train the model")]

[Fit()](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer.Fit%28Microsoft.ML.IDataView,Microsoft.ML.IDataView%29) 메서드는 데이터 세트를 변환하고 학습을 적용하여 모델을 학습합니다.

### <a name="return-the-model-trained-to-use-for-evaluation"></a>평가에 사용하기 위해 학습된 모델 반환

 `BuildAndTrainModel()` 메서드의 끝에 모델을 반환합니다.

[!code-csharp[ReturnModel](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#ReturnModel "Return the model")]

## <a name="evaluate-the-model"></a>모델 평가

모델을 학습한 후 테스트 데이터를 사용하여 모델의 성능 유효성을 검사합니다.

1. 다음 코드로 `BuildAndTrainModel()` 바로 뒤에 `Evaluate()` 메서드를 만듭니다.

    ```csharp
    public static void Evaluate(MLContext mlContext, ITransformer model, IDataView splitTestSet)
    {

    }
    ```

    `Evaluate()` 메서드는 다음 작업을 실행합니다.

    - 테스트 데이터 세트를 로드합니다.
    - BinaryClassification 평가자를 만듭니다.
    - 모델을 평가하고 메트릭을 만듭니다.
    - 메트릭을 표시합니다.

2. 다음 코드를 사용하여 `BuildAndTrainModel()` 메서드 호출 바로 아래에 `Main()` 메서드의 새 메서드 호출을 추가합니다.

    [!code-csharp[CallEvaluate](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CallEvaluate "Call the Evaluate method")]

3. `Evaluate()`에 다음 코드를 추가하여 `splitTestSet`데이터를 변환합니다.

    [!code-csharp[PredictWithTransformer](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#TransformData "Predict using the Transformer")]

    이전 코드는 [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) 메서드를 사용하여 여러 제공된 테스트 데이터 세트 입력 행에 대한 예측을 합니다.

4. `Evaluate()` 메서드에서 다음 코드 줄로 다음 항목을 추가하여 모델을 평가합니다.

    [!code-csharp[ComputeMetrics](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#Evaluate "Compute Metrics")]

예측 집합(`predictions`)이 있으면 [Evaluate()](xref:Microsoft.ML.BinaryClassificationCatalog.Evaluate%2A) 메서드는 모델을 평가하여 예측된 값을 테스트 데이터 세트의 실제 `Labels`와 비교하고, 모델 수행 방법에 대한 [CalibratedBinaryClassificationMetrics](xref:Microsoft.ML.Data.CalibratedBinaryClassificationMetrics) 개체를 반환합니다.

### <a name="displaying-the-metrics-for-model-validation"></a>모델 유효성 검사를 위해 메트릭 표시

다음 코드를 사용하여 메트릭을 표시합니다.

[!code-csharp[DisplayMetrics](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#DisplayMetrics "Display selected metrics")]

- `Accuracy` 메트릭은 테스트 세트에서 정확한 예측의 비율인 모델 정확도를 가져옵니다.

- `AreaUnderRocCurve` 메트릭은 모델이 긍정 및 부정 클래스 분류의 정확도를 자신하는 정도를 표시합니다. `AreaUnderRocCurve`를 가능한 근접하게 하고자 합니다.

- `F1Score` 메트릭은 모델의 F1 점수를 가져옵니다. [정밀도](../resources/glossary.md#precision)와 [회수](../resources/glossary.md#recall) 사이의 균형을 측정한 값입니다.  `F1Score`를 가능한 근접하게 하고자 합니다.

### <a name="predict-the-test-data-outcome"></a>테스트 데이터 결과 예측

1. 다음 코드를 사용하여 `Evaluate()` 메서드 바로 뒤에 `UseModelWithSingleItem()` 메서드를 만듭니다.

    ```csharp
    private static void UseModelWithSingleItem(MLContext mlContext, ITransformer model)
    {

    }
    ```

    `UseModelWithSingleItem()` 메서드는 다음 작업을 실행합니다.

    - 테스트 데이터의 단일 댓글을 만듭니다.
    - 테스트 데이터를 기반으로 감정을 예측합니다.
    - 보고를 위해 테스트 데이터 및 예측을 결합합니다.
    - 예측 결과를 표시합니다.

2. 다음 코드를 사용하여 `Evaluate()` 메서드 호출 바로 아래에 `Main()` 메서드의 새 메서드 호출을 추가합니다.

    [!code-csharp[CallUseModelWithSingleItem](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CallUseModelWithSingleItem "Call the UseModelWithSingleItem method")]

3. 다음 코드를 추가하여 `UseModelWithSingleItem()` 메서드의 첫 줄로 만듭니다.

    [!code-csharp[CreatePredictionEngine](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CreatePredictionEngine1 "Create the PredictionEngine")]

    [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)은 데이터의 단일 인스턴스에 대한 예측을 수행할 수 있는 편리한 API입니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 단일 스레드 또는 프로토타입 환경에서 사용할 수 있습니다. 프로덕션 환경에서 성능 및 스레드 보안을 개선하려면 `PredictionEnginePool` 서비스를 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다. [ASP.NET Core 웹 API에서 `PredictionEnginePool`을 사용하는 방법](https://docs.microsoft.com/en-us/dotnet/machine-learning/how-to-guides/serve-model-web-api-ml-net#register-predictionenginepool-for-use-in-the-application)에 대한 자세한 내용은 이 가이드를 참조하세요.

    > [!NOTE]
    > `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.
    
4. `SentimentData` 인스턴스를 만들어 댓글을 추가하여 `UseModelWithSingleItem()` 메서드에서 학습된 모델의 예측을 테스트합니다.

    [!code-csharp[PredictionData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CreateTestIssue1 "Create test data for single prediction")]

5. 다음을 `UseModelWithSingleItem()` 메서드의 다음 코드 줄로 추가하여 테스트 주석 데이터를 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)에 전달합니다.

    [!code-csharp[Predict](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#Predict "Create a prediction of sentiment")]

    [Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) 함수는 단일 데이터 행에 대한 예측을 수행합니다.

6. 다음 코드를 사용하여 `SentimentText` 및 해당 감정 예측을 표시합니다.

    [!code-csharp[OutputPrediction](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#OutputPrediction "Display prediction output")]

## <a name="use-the-model-for-prediction"></a>예측에 모델 사용

### <a name="deploy-and-predict-batch-items"></a>일괄 처리 항목 배포 및 예측

1. 다음 코드를 사용하여 `UseModelWithSingleItem()` 메서드 바로 뒤에 `UseModelWithBatchItems()` 메서드를 만듭니다.

    ```csharp
    public static void UseModelWithBatchItems(MLContext mlContext, ITransformer model)
    {

    }
    ```

    `UseModelWithBatchItems()` 메서드는 다음 작업을 실행합니다.

    - 일괄 처리 테스트 데이터를 만듭니다.
    - 테스트 데이터를 기반으로 감정을 예측합니다.
    - 보고를 위해 테스트 데이터 및 예측을 결합합니다.
    - 예측 결과를 표시합니다.

2. 다음 코드를 사용하여 `UseModelWithSingleItem()` 메서드 호출 바로 아래에 `Main` 메서드의 새 메서드 호출을 추가합니다.

    [!code-csharp[CallPredictModelBatchItems](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CallUseModelWithBatchItems "Call the CallUseModelWithBatchItems method")]

3. 몇몇 댓글을 추가하여 `UseModelWithBatchItems()` 메서드에서 학습된 모델의 예측을 테스트합니다.

    [!code-csharp[PredictionData](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#CreateTestIssues "Create test data for predictions")]

### <a name="predict-comment-sentiment"></a>주석 감정 예측

모델을 사용하여 [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) 메서드를 통한 주석 데이터 감정 예측:

[!code-csharp[Predict](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#Prediction "Create predictions of sentiments")]

### <a name="combine-and-display-the-predictions"></a>예측 결합 및 표시

다음 코드를 사용하여 예측에 대한 헤더를 만듭니다.

[!code-csharp[OutputHeaders](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#AddInfoMessage "Display prediction outputs")]

`SentimentPrediction`은 `SentimentData`에서 상속되므로 `Transform()` 메서드가 예측된 필드로 `SentimentText`를 입력했습니다. ML.NET 프로세스를 처리하면서 각 구성 요소가 열을 추가하므로 결과를 쉽게 표시합니다.

[!code-csharp[DisplayPredictions](~/samples/machine-learning/tutorials/SentimentAnalysis/Program.cs#DisplayResults "Display the predictions")]

## <a name="results"></a>결과

다음과 같은 결과가 나타나야 합니다. 처리 중 메시지가 표시됩니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 이러한 결과는 다음 결과에서 제거되었습니다.

```console
Model quality metrics evaluation
--------------------------------
Accuracy: 83.96%
Auc: 90.51%
F1Score: 84.04%

=============== End of model evaluation ===============

=============== Prediction Test of model with a single sample and test dataset ===============

Sentiment: This was a very bad steak | Prediction: Negative | Probability: 0.1027377
=============== End of Predictions ===============

=============== Prediction Test of loaded model with a multiple samples ===============

Sentiment: This was a horrible meal | Prediction: Negative | Probability: 0.1369192
Sentiment: I love this spaghetti. | Prediction: Positive | Probability: 0.9960636
=============== End of predictions ===============

=============== End of process ===============
Press any key to continue . . .

```

지금까지 이제 메시지 감정을 분류하고 예측하기 위한 기계 학습 모델을 성공적으로 빌드했습니다.

성공한 모델 빌드하는 것은 반복적인 프로세스입니다. 자습서에서는 작은 데이터 세트를 사용하여 빠른 모델 학습을 제공하므로 이 모델은 초기 품질이 좋지 않습니다. 모델 품질에 만족하지 않는 경우 더 큰 학습 데이터 세트를 제공하거나 각 알고리즘에 대한 다양한 [하이퍼 매개 변수](../resources/glossary.md##hyperparameter)와 함께 다양한 학습 알고리즘을 선택하여 모델 품질을 개선할 수 있습니다.

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/SentimentAnalysis) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - 콘솔 애플리케이션 만들기
> - 데이터 준비
> - 데이터 로드
> - 모델 빌드 및 학습
> - 모델 평가
> - 모델로 예측 수행
> - 결과 보기

다음 자습서로 이동하여 자세히 알아보기
> [!div class="nextstepaction"]
> [문제 분류](github-issue-classification.md)
