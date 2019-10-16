---
title: '자습서: 영화 추천기 빌드 - 행렬 인수분해'
description: 이 자습서에서는 .NET Core 콘솔 애플리케이션에서 ML.NET으로 영화 추천기를 빌드하는 방법을 보여 줍니다. 이 단계에서는 C#과 Visual Studio 2019를 사용합니다.
author: briacht
ms.date: 09/30/2019
ms.custom: mvc, title-hack-0516
ms.topic: tutorial
ms.openlocfilehash: 1db2ad6c078cb6201b2a6a4e2f8572f589cee684
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700959"
---
# <a name="tutorial-build-a-movie-recommender-using-matrix-factorizaton-with-mlnet"></a>자습서: ML.NET에서 행렬 인수분해를 사용하여 영화 추천기 빌드

이 자습서에서는 .NET Core 콘솔 애플리케이션에서 ML.NET으로 영화 추천기를 빌드하는 방법을 보여 줍니다. 이 단계에서는 C#과 Visual Studio 2019를 사용합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> * 기계 학습 알고리즘 선택
> * 데이터 준비 및 로드
> * 모델 빌드 및 학습
> * 모델 평가
> * 모델 배포 및 사용

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/MovieRecommendation) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="machine-learning-workflow"></a>기계 학습 워크플로

다음 단계를 수행하여 기타 모든 ML.NET 작업을 수행할 수 있습니다.

1. [데이터 로드](#load-your-data)
2. [모델 빌드 및 학습](#build-and-train-your-model)
3. [모델 평가](#evaluate-your-model)
4. [모델 사용](#use-your-model)

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).

## <a name="select-the-appropriate-machine-learning-task"></a>적절한 기계 학습 작업 선택

영화 목록을 추천하거나 관련 제품 목록을 권장하는 것과 같은 몇 가지 방법으로 권장 문제에 접근할 수 있지만, 이 경우 사용자가 특정 영화에 어떤 등급(1-5)을 부여할지 예측하고 정의된 임계값(등급이 높을수록 사용자가 특정 영화를 좋아할 가능성이 높음)이 높을수록 해당 영화를 추천합니다.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

### <a name="create-a-project"></a>프로젝트 만들기

1. Visual Studio 2017을 엽니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. **새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **.NET Core** 노드를 차례로 선택합니다. 그런 다음 **콘솔 앱(.NET Core)** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 "MovieRecommender"를 입력한 다음, **확인** 단추를 선택합니다.

2. 프로젝트에 *Data*라는 디렉터리를 만들어 데이터 세트를 저장합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. “Data”를 입력하고 Enter 키를 누릅니다.

3. **Microsoft.ML** 및 **Microsoft.ML.Recommender** NuGet 패키지를 설치합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. "nuget.org"를 패키지 소스로 선택하고, **찾아보기** 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다. **Microsoft.ML.Recommender**에 대해 이 단계를 반복합니다.

4. *Program.cs* 파일 맨 위에 다음 `using` 문을 추가합니다.

    [!code-csharp[UsingStatements](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#UsingStatements "Add necessary usings")]

### <a name="download-your-data"></a>데이터 다운로드

1. 두 개의 데이터 세트를 다운로드하여 이전에 만든 *Data* 폴더에 저장합니다.

   * [*recommendation-ratings-train.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/MatrixFactorization_MovieRecommendation/Data/recommendation-ratings-train.csv)를 마우스 오른쪽 단추로 클릭하고 "링크(또는 대상)를 다른 이름으로 저장..."을 선택합니다.
   * [*recommendation-ratings-test.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/MatrixFactorization_MovieRecommendation/Data/recommendation-ratings-test.csv)를 마우스 오른쪽 단추로 클릭하고 "링크(또는 대상)를 다른 이름으로 저장..."을 선택합니다.

     \*.csv 파일을 *Data* 폴더에 저장하거나 다른 곳에 저장한 후 \*.csv 파일을 *Data* 폴더로 이동합니다.

2. 솔루션 탐색기에서 각 \*.csv 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

   ![VS의 최신 버전이면 복사](./media/movie-recommendation/copytoout.gif)

## <a name="load-your-data"></a>데이터 로드

ML.NET 프로세스의 첫 번째 단계는 모델 학습 및 테스트 데이터를 준비하고 로드하는 것입니다.

권장 등급 데이터는 `Train` 및 `Test` 데이터 세트로 분할됩니다. `Train` 데이터는 모델에 맞게 사용됩니다. `Test` 데이터는 학습된 모델로 예측하고 모델 성능을 평가하는 데 사용됩니다. `Train` 및 `Test` 데이터로 80/20 분할을 하는 것이 일반적입니다.

다음은 \*.csv 파일의 데이터 미리 보기입니다.

![데이터 미리 보기](./media/movie-recommendation/csv-dataset-preview.png)

\*.csv 파일에는 다음 네 개의 열이 있습니다.

* `userId`
* `movieId`
* `rating`
* `timestamp`

기계 학습에서 예측을 수행하는 데 사용되는 열을 [Features](../resources/glossary.md#feature)라고 하고, 반환된 예측이 있는 열을 [Label](../resources/glossary.md#label)이라고 합니다.

영화 등급을 예측하려는 경우 등급 열은 `Label`입니다. 다른 세 개의 열 `userId`, `movieId` 및 `timestamp`는 모두 `Features`가 `Label`을 예측하는 데 사용됩니다.

| 기능      | 레이블         |
| ------------- |:-------------:|
| `userId`        |    `rating`     |
| `movieId`      |               |
| `timestamp`     |               |

`Label`을 예측하는 데 사용되는 `Features`를 결정하는 것은 사용자에게 달려 있습니다. 또한 [Feature Permutation 중요도](../how-to-guides/determine-global-feature-importance-in-model.md)와 같은 방법을 사용하여 최상의 `Features`를 선택할 수 있습니다.

이 경우, 타임스탬프는 사용자가 특정 영화를 평가하는 방식에 실제로 영향을 주지 않고 더 정확한 예측에 기여하지 않기 때문에 `timestamp` 열을 `Feature`로 제거해야 합니다.

| 기능      | 레이블         |
| ------------- |:-------------:|
| `userId`        |    `rating`     |
| `movieId`      |               |

다음으로, 입력 클래스에 대한 데이터 구조를 정의해야 합니다.

새 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **추가 > 새 항목**을 선택합니다.

2. **새 항목 추가 대화 상자**에서 **클래스**를 선택하고 **이름** 필드를 *MovieRatingData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

*MovieRatingData.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *MovieRatingData.cs*의 맨 위에 추가합니다.

```csharp
using Microsoft.ML.Data;
```

기존 클래스 정의를 제거하고 *MovieRatingData.cs*에 다음 코드를 추가하여 `MovieRating`라는 클래스를 만듭니다.

[!code-csharp[MovieRatingClass](~/samples/machine-learning/tutorials/MovieRecommendation/MovieRatingData.cs#MovieRatingClass "Add the Movie Rating class")]

`MovieRating`은 입력 데이터 클래스를 지정합니다. [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) 특성은 데이터 세트에서 로드해야 하는 열(열 인덱스 기준)을 지정합니다. `userId` 및 `movieId` 열은 `Features`(모델에서 `Label`을 예측하기 위해 제공하는 입력)이고, 등급 열은 예측할 `Label`(모델의 출력)입니다.

*MovieRatingData.cs*의 `MovieRating` 클래스 뒤에 다음 코드를 추가하여 예측 결과를 나타내는 또 다른 클래스(`MovieRatingPrediction`)를 만듭니다.

[!code-csharp[PredictionClass](~/samples/machine-learning/tutorials/MovieRecommendation/MovieRatingData.cs#PredictionClass "Add the Movie Prediction Class")]

*Program.cs*에서 `Console.WriteLine("Hello World!")`을 `Main()` 내부의 다음 코드로 바꿉니다.

[!code-csharp[MLContext](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#MLContext "Add MLContext")]

[MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작점이며, `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

`Main()` 다음에 `LoadData()`라는 메서드를 만듭니다.

```csharp
public static (IDataView training, IDataView test) LoadData(MLContext mlContext)
{

}
```

> [!NOTE]
> 이 메서드는 다음 단계에서 return 문을 추가할 때까지 오류를 제공합니다.

데이터 경로 변수를 초기화하여 \*.csv 파일에서 데이터를 로드하고 `LoadData()`의 다음 코드 줄로 다음 항목을 추가하여 `Train` 및 `Test` 데이터를 `IDataView` 개체로 반환합니다.

[!code-csharp[LoadData](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#LoadData "Load data from data paths")]

ML.NET의 데이터는 [IDataView 클래스](xref:Microsoft.ML.IDataView)로 표시됩니다. `IDataView`는 표 형식 데이터(숫자 및 텍스트)를 유연하고 효율적으로 설명하는 방법입니다. 데이터를 텍스트 파일 또는 실시간(예: SQL 데이터베이스 또는 로그 파일)에서 `IDataView` 개체로 로드할 수 있습니다.

[LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)은 데이터 스키마를 정의하고 파일에서 읽습니다. 데이터 경로 변수를 가져와서 `IDataView`를 반환합니다. 이 경우, `Test` 및 `Train` 파일의 경로를 제공하고 텍스트 파일 헤더(열 이름을 올바르게 사용할 수 있도록)와 쉼표 문자 데이터 구분 기호(기본 구분 기호는 탭)를 모두 나타냅니다.

`Main()` 메서드에서 다음 코드를 추가하여 `LoadData()` 메서드를 호출하고 `Train` 및 `Test` 데이터를 반환합니다.

[!code-csharp[LoadDataMain](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#LoadDataMain "Add LoadData method to Main")]

## <a name="build-and-train-your-model"></a>모델 빌드 및 학습

ML.NET에는 세 가지 주요 개념이 있습니다. [데이터](../resources/glossary.md#data), [변환기](../resources/glossary.md#transformer) 및 [평가자](../resources/glossary.md#estimator).

기계 학습 알고리즘은 특정 형식의 데이터가 필요합니다. `Transformers`는 표 형식 데이터를 호환 가능한 형식으로 변환하는 데 사용됩니다.

![변환기 이미지](./media/movie-recommendation/transformer.png)

`Estimators`를 생성하여 ML.NET에서 `Transformers`를 만듭니다. `Estimators`는 데이터를 가져와서 `Transformers`를 반환합니다.

![평가자 이미지](./media/movie-recommendation/estimator.png)

모델 학습에 사용할 권장 학습 알고리즘은 `Estimator`의 예입니다.

다음 단계를 수행하여 `Estimator`를 빌드합니다.

다음 코드를 사용하여 `LoadData()` 메서드 바로 뒤에 `BuildAndTrainModel()` 메서드를 만듭니다.

```csharp
public static ITransformer BuildAndTrainModel(MLContext mlContext, IDataView trainingDataView)
{

}
```

> [!NOTE]
> 이 메서드는 다음 단계에서 return 문을 추가할 때까지 오류를 제공합니다.

`BuildAndTrainModel()`에 다음 코드를 추가하여 데이터 변환을 정의합니다.

[!code-csharp[DataTransformations](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#DataTransformations "Define data transformations")]

`userId` 및 `movieId`는 실제 값이 아닌 사용자와 영화 제목을 나타내기 때문에 [MapValueToKey()](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A) 메서드를 사용하여 각 `userId` 및 각 `movieId`를 숫자 키 형식 `Feature` 열(권장 알고리즘에서 허용하는 형식)로 변환하고 새 데이터 세트 열로 추가합니다.

| userId | movieId | 레이블 | userIdEncoded | movieIdEncoded |
| ------------- |:-------------:| -----:|-----:|-----:|
| 1 | 1 | 4 | userKey1 | movieKey1 |
| 1 | 3 | 4 | userKey1 | movieKey2 |
| 1 | 6 | 4 | userKey1 | movieKey3 |

기계 학습 알고리즘을 선택하고 `BuildAndTrainModel()`의 다음 코드 줄로 다음 항목을 추가하여 데이터 변환 정의에 추가합니다.

[!code-csharp[AddAlgorithm](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#AddAlgorithm "Add the training algorithm with options")]

[MatrixFactorizationTrainer](xref:Microsoft.ML.RecommendationCatalog.RecommendationTrainers.MatrixFactorization%28Microsoft.ML.Trainers.MatrixFactorizationTrainer.Options%29)는 권장 학습 알고리즘입니다.  [Matrix Factorization](https://en.wikipedia.org/wiki/Matrix_factorization_(recommender_systems))은 사용자가 이전에 제품을 평가한 방법에 대한 데이터가 있을 때 권장되는 일반적인 접근 방법입니다. 이는 이 자습서의 데이터 세트에 해당됩니다. 다른 데이터를 사용할 수 있는 경우에 대한 기타 권장 알고리즘이 있습니다(자세한 내용은 아래의 [기타 권장 알고리즘](#other-recommendation-algorithms) 섹션 참조).

이 경우, `Matrix Factorization` 알고리즘은 "공동 작업 필터링"이라는 방법을 사용합니다. 이 방법은 사용자 1이 특정 문제에 대해 사용자 2와 의견이 같으면, 다른 문제에 대해 사용자 1이 사용자 2와 동일한 방식으로 느낄 가능성이 높다고 가정합니다.

예를 들어 사용자 1과 사용자 2가 영화를 비슷하게 평가한다면 사용자 2는 사용자 1이 시청하고 높게 평가한 영화를 즐길 가능성이 더 높습니다.

| | `Incredibles 2 (2018)` | `The Avengers (2012)` | `Guardians of the Galaxy (2014)` |
| -------------:|-------------:| -----:|-----:|
| 사용자 1 | 시청하고 좋아하는 영화 | 시청하고 좋아하는 영화 | 시청하고 좋아하는 영화 |
| 사용자 2 | 시청하고 좋아하는 영화 | 시청하고 좋아하는 영화 | 시청하지 않음 -- 추천 영화 |

`Matrix Factorization` 강사는 몇 가지 [옵션](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer.Options)이 있으며, 아래의 [알고리즘 하이퍼 매개 변수](#algorithm-hyperparameters) 섹션에서 자세히 읽을 수 있습니다.

모델을 `Train` 데이터에 맞추고 `BuildAndTrainModel()` 메서드에서 다음 줄의 코드로 다음 항목을 추가하여 학습된 모델을 반환합니다.

[!code-csharp[FitModel](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#FitModel "Call the Fit method and return back the trained model")]

[Fit()](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer.Fit%28Microsoft.ML.IDataView,Microsoft.ML.IDataView%29) 메서드는 제공된 학습 데이터 세트를 통해 모델을 학습합니다. 기술적으로 데이터를 변환하고 학습을 적용하여 `Estimator` 정의를 실행하고, 학습된 모델인 `Transformer`를 반환합니다.

`Main()` 메서드에서 다음 줄의 코드로 다음 항목을 추가하여 `BuildAndTrainModel()` 메서드를 호출하고 학습된 모델을 반환합니다.

[!code-csharp[BuildTrainModelMain](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#BuildTrainModelMain "Add BuildAndTrainModel method in Main")]

## <a name="evaluate-your-model"></a>모델 평가

모델을 학습한 후에는 테스트 데이터를 사용하여 모델의 성능을 평가합니다.

다음 코드를 사용하여 `BuildAndTrainModel()` 메서드 바로 뒤에 `EvaluateModel()` 메서드를 만듭니다.

```csharp
public static void EvaluateModel(MLContext mlContext, IDataView testDataView, ITransformer model)
{

}
```

`EvaluateModel()`에 다음 코드를 추가하여 `Test`데이터를 변환합니다.

[!code-csharp[Transform](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#Transform "Transform the test data")]

[Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) 메서드는 테스트 데이터 세트의 여러 입력 행을 예측합니다.

`EvaluateModel()` 메서드에서 다음 코드 줄로 다음 항목을 추가하여 모델을 평가합니다.

[!code-csharp[Evaluate](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#Evaluate "Evaluate the model using predictions from the test data")]

예측 집합이 있으면 [Evaluate()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A) 메서드는 모델을 평가하여 예측된 값을 테스트 데이터 세트의 실제 `Labels`와 비교하고, 모델 수행 방법에 대한 메트릭을 반환합니다.

`EvaluateModel()` 메서드에 다음 코드 줄로 다음 항목을 추가하여 평가 메트릭을 콘솔에 인쇄합니다.

[!code-csharp[PrintMetrics](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#PrintMetrics "Print the evaluation metrics")]

`EvaluateModel()` 메서드를 호출하려면 `Main()` 메서드에서 다음 코드 줄로 다음 항목을 추가합니다.

[!code-csharp[EvaluateModelMain](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#EvaluateModelMain "Add EvaluateModel method in Main")]

지금까지의 출력은 다음 텍스트와 비슷해야 합니다.

```console
=============== Training the model ===============
iter      tr_rmse          obj
   0       1.5403   3.1262e+05
   1       0.9221   1.6030e+05
   2       0.8687   1.5046e+05
   3       0.8416   1.4584e+05
   4       0.8142   1.4209e+05
   5       0.7849   1.3907e+05
   6       0.7544   1.3594e+05
   7       0.7266   1.3361e+05
   8       0.6987   1.3110e+05
   9       0.6751   1.2948e+05
  10       0.6530   1.2766e+05
  11       0.6350   1.2644e+05
  12       0.6197   1.2541e+05
  13       0.6067   1.2470e+05
  14       0.5953   1.2382e+05
  15       0.5871   1.2342e+05
  16       0.5781   1.2279e+05
  17       0.5713   1.2240e+05
  18       0.5660   1.2230e+05
  19       0.5592   1.2179e+05
=============== Evaluating the model ===============
Rms: 0.994051469730769
RSquared: 0.412556298844873
```

이 출력에는 20번의 반복이 있습니다. 각각의 반복에서 오류의 측정값은 줄어들고 0에 가깝게 수렴합니다.

`root of mean squared error`(RMS 또는 RMSE)는 모델 예측 값과 테스트 데이터 세트 관찰 값 간의 차이를 측정하는 데 사용됩니다. 기술적으로 오차 제곱 평균의 제곱근입니다. RMS가 낮을수록 더 나은 모델입니다.

`R Squared`는 데이터가 모델에 얼마나 잘 맞는지를 나타냅니다. 범위는 0에서 1까지입니다. 0 값은 데이터가 무작위이거나 모델에 맞지 않음을 의미합니다. 값 1은 모델이 데이터와 정확히 일치함을 의미합니다. `R Squared` 점수를 가능한 한 1에 가깝게 합니다.

성공한 모델 빌드하는 것은 반복적인 프로세스입니다. 자습서에서는 작은 데이터 세트를 사용하여 빠른 모델 학습을 제공하므로 이 모델은 초기 품질이 좋지 않습니다. 모델 품질에 만족하지 않는 경우 더 큰 학습 데이터 세트를 제공하거나 각 알고리즘에 대한 다양한 하이퍼 매개 변수와 함께 다양한 학습 알고리즘을 선택하여 모델 품질을 개선할 수 있습니다. 자세한 내용은 아래 [모델 개선](#improve-your-model) 섹션을 참조하세요.

## <a name="use-your-model"></a>모델 사용

이제 학습된 모델을 사용하여 새 데이터를 예측할 수 있습니다.

다음 코드를 사용하여 `EvaluateModel()` 메서드 바로 뒤에 `UseModelForSinglePrediction()` 메서드를 만듭니다.

```csharp
public static void UseModelForSinglePrediction(MLContext mlContext, ITransformer model)
{

}
```

`UseModelForSinglePrediction()`에 다음 코드를 추가하여 등급을 예측하려면 `PredictionEngine`을 사용합니다.

[!code-csharp[PredictionEngine](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#PredictionEngine "Create Prediction Engine")]

[PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)은 데이터의 단일 인스턴스에 대한 예측을 수행할 수 있는 편리한 API입니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 단일 스레드 또는 프로토타입 환경에서 사용할 수 있습니다. 프로덕션 환경에서 성능 및 스레드 보안을 개선하려면 `PredictionEnginePool` 서비스를 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다. [ASP.NET Core 웹 API에서 `PredictionEnginePool`을 사용하는 방법](https://docs.microsoft.com/en-us/dotnet/machine-learning/how-to-guides/serve-model-web-api-ml-net#register-predictionenginepool-for-use-in-the-application)에 대한 자세한 내용은 이 가이드를 참조하세요.

> [!NOTE]
> `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

`testInput`이라는 `MovieRating`의 인스턴스를 만들고 `UseModelForSinglePrediction()` 메서드에서 다음 코드 줄로 다음 항목을 추가하여 예측 엔진에 전달합니다.

[!code-csharp[MakeSinglePrediction](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#MakeSinglePrediction "Make a single prediction with the Prediction Engine")]

[Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) 함수는 단일 데이터 열의 대한 예측을 수행합니다.

그런 다음, `Score` 또는 예측 등급을 사용하여 movieId 10을 통해 사용자 6에게 영화를 추천할지 여부를 결정할 수 있습니다. `Score`가 높을수록 사용자가 특정 영화를 좋아할 가능성이 높아집니다. 이 경우, 예측된 등급이 >3.5인 영화를 추천한다고 가정해 보겠습니다.

결과를 인쇄하려면 `UseModelForSinglePrediction()` 메서드에서 다음 코드 줄로 다음 항목을 추가합니다.

[!code-csharp[PrintResults](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#PrintResults "Print the recommendation prediction results")]

`UseModelForSinglePrediction()` 메서드를 호출하려면 `Main()` 메서드에서 다음 코드 줄로 다음 항목을 추가합니다.

[!code-csharp[UseModelMain](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#UseModelMain "Add UseModelForSinglePrediction method in Main")]

이 메서드의 출력은 다음 텍스트와 비슷해야 합니다.

```console
=============== Making a prediction ===============
Movie 10 is recommended for user 6
```

### <a name="save-your-model"></a>모델 저장

최종 사용자 애플리케이션에서 모델을 사용하여 예측하려면 먼저 모델을 저장해야 합니다.

다음 코드를 사용하여 `UseModelForSinglePrediction()` 메서드 바로 뒤에 `SaveModel()` 메서드를 만듭니다.

```csharp
public static void SaveModel(MLContext mlContext, DataViewSchema trainingDataViewSchema, ITransformer model)
{

}
```

`SaveModel()` 메서드의 다음 코드를 추가하여 학습된 모델을 저장합니다.

[!code-csharp[SaveModel](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#SaveModel "Save the model to a zip file")]

이 메서드는 학습된 모델을 .zip 파일("Data" 폴더에 있음)에 저장한 다음, 이를 다른 .NET 애플리케이션에서 예측을 수행하는 데 사용할 수 있습니다.

`SaveModel()` 메서드를 호출하려면 `Main()` 메서드에서 다음 코드 줄로 다음 항목을 추가합니다.

[!code-csharp[SaveModelMain](~/samples/machine-learning/tutorials/MovieRecommendation/Program.cs#SaveModelMain "Create SaveModel method in Main")]

### <a name="use-your-saved-model"></a>저장된 모델 사용

학습된 모델을 저장한 후에는 다양한 환경에서 모델을 사용할 수 있습니다(앱에서 학습된 기계 학습 모델을 작동하는 방법에 대한 자세한 내용은 ["방법 가이드"](../how-to-guides/consuming-model-ml-net.md) 참조).

## <a name="results"></a>결과

위의 단계를 수행한 후 콘솔 앱을 실행합니다(Ctrl + F5). 위의 단일 예측 결과는 다음과 비슷해야 합니다. 경고 또는 처리 메시지가 표시될 수 있지만, 이해하기 쉽도록 이러한 메시지는 다음 결과에서 제거되었습니다.

```console
=============== Training the model ===============
iter      tr_rmse          obj
   0       1.5382   3.1213e+05
   1       0.9223   1.6051e+05
   2       0.8691   1.5050e+05
   3       0.8413   1.4576e+05
   4       0.8145   1.4208e+05
   5       0.7848   1.3895e+05
   6       0.7552   1.3613e+05
   7       0.7259   1.3357e+05
   8       0.6987   1.3121e+05
   9       0.6747   1.2949e+05
  10       0.6533   1.2766e+05
  11       0.6353   1.2636e+05
  12       0.6209   1.2561e+05
  13       0.6072   1.2462e+05
  14       0.5965   1.2394e+05
  15       0.5868   1.2352e+05
  16       0.5782   1.2279e+05
  17       0.5713   1.2227e+05
  18       0.5637   1.2190e+05
  19       0.5604   1.2178e+05
=============== Evaluating the model ===============
Rms: 0.977175077487166
RSquared: 0.43233349213192
=============== Making a prediction ===============
Movie 10 is recommended for user 6
=============== Saving the model to a file ===============
```

지금까지 이제 영화 추천을 위한 기계 학습 모델을 성공적으로 빌드했습니다. [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/MovieRecommendation) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="improve-your-model"></a>모델 개선

보다 정확한 예측을 할 수 있도록 모델의 성능을 개선할 수 있는 몇 가지 방법이 있습니다.

### <a name="data"></a>데이터

각 사용자 및 영화 id에 대한 충분한 샘플이 있는 학습 데이터를 추가하면 권장 모델의 품질을 개선하는 데 도움이 될 수 있습니다.

[교차 유효성 검사](../how-to-guides/train-cross-validation-ml-net.md)는 임의로 데이터를 하위 집합으로 분할하여(이 자습서에서처럼 테스트 데이터 세트를 추출하는 대신) 그룹 중 일부는 학습 데이터로, 일부는 테스트 데이터로 가져오는 모델을 평가하는 기법입니다. 이 메서드는 모델 품질 면에서 학습-테스트 분할을 수행하는 것보다 뛰어난 성능을 냅니다.

### <a name="features"></a>기능

이 자습서에서는 데이터 세트에서 제공하는 세 개의 `Features`(`user id`, `movie id` 및 `rating`)만 사용합니다.

시작은 좋지만 실제로는 데이터 세트에 포함된 다른 특성 또는 `Features`(예: 나이, 성별, 지리적 위치 등)를 추가할 수 있습니다. 관련성이 높은 `Features`를 추가하면 권장 모델의 성능을 향상시킬 수 있습니다.

`Features`가 기계 학습 작업에 가장 관련이 있는지 확실하지 않은 경우, ML.NET에서 가장 영향력 있는 `Features`를 검색하기 위해 제공되는 FCC(Feature Contribution Calculation) 및 [Feature Permutation 중요도](../how-to-guides/determine-global-feature-importance-in-model.md)를 사용할 수도 있습니다.

### <a name="algorithm-hyperparameters"></a>알고리즘 하이퍼 매개 변수

ML.NET은 좋은 기본 학습 알고리즘을 제공하지만 알고리즘의 [하이퍼 매개 변수](../resources/glossary.md#hyperparameter)를 변경하여 성능을 더욱 미세하게 변경할 수 있습니다.

`Matrix Factorization`의 경우 [NumberOfIterations](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer.Options.NumberOfIterations) 및 [ApproximationRank](xref:Microsoft.ML.Trainers.MatrixFactorizationTrainer.Options.ApproximationRank)와 같은 하이퍼 매개 변수로 실험하여 더 나은 결과를 얻을 수 있는지 확인합니다.

예를 들어 이 자습서에서 알고리즘 옵션은 다음과 같습니다.

```csharp
var options = new MatrixFactorizationTrainer.Options
{
    MatrixColumnIndexColumnName = "userIdEncoded",
    MatrixRowIndexColumnName = "movieIdEncoded",
    LabelColumnName = "Label",
    NumberOfIterations = 20,
    ApproximationRank = 100
};
```

### <a name="other-recommendation-algorithms"></a>기타 권장 알고리즘

공동 작업 필터링을 사용하는 행렬 인수 분해 알고리즘은 영화 추천을 수행하는 유일한 방법입니다. 대부분의 경우 등급 데이터를 사용할 수 없고 사용자로부터 영화 기록만 사용할 수 있습니다. 다른 경우에는 사용자의 등급 데이터 이상만 가질 수 있습니다.

| 알고리즘       | 시나리오           | 예제  |
| ------------- |:-------------:| -----:|
| 하나의 클래스 행렬 인수 분해 | userId 및 movieId만 있을 때 이 옵션을 사용합니다. 이 스타일 권장 사항은 공동 구매 시나리오 또는 함께 자주 구매되는 제품을 기반으로 합니다. 즉, 구매 주문 내역에 따라 고객에게 제품 세트를 추천합니다. | [>사용해 보기](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/MatrixFactorization_ProductRecommendation) |
| 필드 인식 인수 분해 머신 | userId, productId 및 등급(예: 제품 설명 또는 제품 가격) 이외에 더 많은 기능이 있는 경우 이 옵션을 사용하여 권장 사항을 지정합니다. 이 메서드는 또한 공동 작업 필터링 접근 방식을 사용합니다. | [>사용해 보기](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/end-to-end-apps/Recommendation-MovieRecommender) |

### <a name="new-user-scenario"></a>새로운 사용자 시나리오

공동 작업 필터링의 일반적인 문제 중 하나는 추론을 도출할 이전 데이터가 없는 새로운 사용자가 있을 때 발생하는 콜드 시작 문제입니다. 이 문제는 종종 새로운 사용자에게 프로필을 만들고 이전에 시청한 영화를 평가하도록 요청함으로써 해결됩니다. 이 메서드는 사용자에 다소 부담을 주지만 등급 기록이 없는 새로운 사용자에 대한 일부 시작 데이터를 제공합니다.

## <a name="resources"></a>리소스

이 자습서에 사용된 데이터는 [MovieLens 데이터 세트](http://files.grouplens.org/datasets/movielens/)에서 파생되었습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.

> [!div class="checklist"]
>
> * 기계 학습 알고리즘 선택
> * 데이터 준비 및 로드
> * 모델 빌드 및 학습
> * 모델 평가
> * 모델 배포 및 사용

다음 자습서로 이동하여 자세히 알아보기
> [!div class="nextstepaction"]
> [감정 분석](sentiment-analysis.md)
