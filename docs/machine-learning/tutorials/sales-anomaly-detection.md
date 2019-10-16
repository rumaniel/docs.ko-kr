---
title: '자습서: 제품 판매의 변칙 검색'
description: 제품 판매 데이터에 대한 변칙 검색 애플리케이션을 빌드하는 방법을 알아봅니다. 이 자습서에서는 Visual Studio 2019에서 C#을 사용하여 .NET Core 콘솔 애플리케이션을 만듭니다.
ms.date: 07/17/2019
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
ms.openlocfilehash: ed75f1ba0b102ba73eb5671667b5731519c12eb0
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929049"
---
# <a name="tutorial-detect-anomalies-in-product-sales-with-mlnet"></a>자습서: ML.NET을 사용하여 제품 판매의 변칙 검색

제품 판매 데이터에 대한 변칙 검색 애플리케이션을 빌드하는 방법을 알아봅니다. 이 자습서에서는 Visual Studio에서 C#을 사용하여 .NET Core 콘솔 애플리케이션을 만듭니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> * 데이터 로드
> * 급증 변칙 검색에 대한 변환 작성
> * 변환으로 급증 변칙 검색
> * 변화점 변칙 검색에 대한 변환 작성
> * 변환으로 변화점 변칙 검색

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019).

* [product-sales.csv 데이터 세트](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)

>[!NOTE]
> `product-sales.csv`에서 데이터 형식은 “3년간 샴푸 판매량” 데이터 세트(출처: DataMarket, 제공: TSDL(시계열 데이터 라이브러리), 작성: Rob Hyndman)에 기반합니다.
> "3년간 샴푸 판매량”데이터 세트는 DataMarket 기본 오픈 라이선스 하에 사용이 허가되었습니다.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

1. "ProductSalesAnomalyDetection"이라고 하는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

2. 프로젝트에 이름이 *Data*인 디렉터리를 만들어 데이터 세트 파일을 저장합니다.

3. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. "nuget.org"를 패키지 소스로 선택하고, 찾아보기 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 **v1.0.0** 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다. **Microsoft.ML.TimeSeries v0.12.0**에 대해 이 단계를 반복합니다.

4. *Program.cs* 파일 맨 위에 다음 `using` 문을 추가합니다.

    [!code-csharp[AddUsings](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddUsings "Add necessary usings")]

### <a name="download-your-data"></a>데이터 다운로드

1. 데이터 세트를 다운로드하여 이전에 만든 *Data* 폴더에 저장합니다.

   * [*product-sales.csv*](https://raw.githubusercontent.com/dotnet/machinelearning-samples/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)를 마우스 오른쪽 단추로 클릭하고 "링크(또는 대상)를 다른 이름으로 저장..."을 선택합니다.

     \*.csv 파일을 *Data* 폴더에 저장하거나 다른 곳에 저장한 후 \*.csv 파일을 *Data* 폴더로 이동합니다.

2. 솔루션 탐색기에서 \*.csv 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

다음 표는 \*.csv 파일의 데이터 미리 보기입니다.

|월  |ProductSales |
|-------|-------------|
|1-Jan  |    271      |
|2-Jan  |    150.9    |
|.....  |    .....    |
|1-Feb  |    199.3    |
|.....  |    .....    |

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

그런 다음 입력 및 예측 클래스 데이터 구조를 정의합니다.

새 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **추가 > 새 항목**을 선택합니다.

2. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *ProductSalesData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

   *ProductSalesData.cs* 파일이 코드 편집기에서 열립니다.

3. 다음 `using` 문을 *ProductSalesData.cs*의 맨 위에 추가합니다.

   ```csharp
   using Microsoft.ML.Data;
   ```

4. 기존 클래스 정의를 제거하고 두 개의 클래스 `ProductSalesData` 및 `ProductSalesPrediction`이 있는 다음 코드를 *ProductSalesData.cs* 파일에 추가합니다.

    [!code-csharp[DeclareTypes](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/ProductSalesData.cs#DeclareTypes "Declare data record types")]

    `ProductSalesData`은 입력 데이터 클래스를 지정합니다. [LoadColumn](xref:Microsoft.ML.Data.LoadColumnAttribute.%23ctor%28System.Int32%29) 특성은 데이터 세트에서 로드해야 하는 열(열 인덱스 기준)을 지정합니다.

    `ProductSalesPrediction`을 통해서는 예측 데이터 클래스를 지정합니다. 변칙 검색의 경우 예측은 변칙, 원시 점수 및 p 값이 있는지를 나타내는 경고로 구성됩니다. P 값이 0에 가까울수록 이상 발생 가능성이 큽니다.

5. 최근에 다운로드한 데이터 세트 파일 경로 및 저장된 모델 파일 경로를 포함할 두 개의 글로벌 필드를 만듭니다.

    * `_dataPath`에는 모델을 학습시키는 데 사용되는 데이터 세트의 경로가 포함됩니다.
    * `_docsize`에는 데이터 세트 파일의 레코드 수가 있습니다. `_docSize`를 사용하여 `pvalueHistoryLength`를 계산합니다.

6. `Main` 메서드 바로 위의 줄에 다음 코드를 추가하여 해당 경로를 지정합니다.

    [!code-csharp[Declare global variables](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DeclareGlobalVariables "Declare global variables")]

### <a name="initialize-variables-in-main"></a>Main에서 변수 초기화

1. `Main` 메서드의 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 대체하여 `mlContext` 변수를 선언하고 초기화합니다.

    [!code-csharp[CreateMLContext](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateMLContext "Create the ML Context")]

    [MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작점이며, `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

### <a name="load-the-data"></a>데이터 로드

ML.NET의 데이터는 [IDataView 클래스](xref:Microsoft.ML.IDataView)로 표시됩니다. `IDataView`는 표 형식 데이터(숫자 및 텍스트)를 유연하고 효율적으로 설명하는 방법입니다. 데이터를 텍스트 파일 또는 다른 소스(예: SQL 데이터베이스 또는 로그 파일)에서 `IDataView` 개체로 로드할 수 있습니다.

1. 아래 코드를 `Main()` 메서드의 다음 줄로 추가합니다.

    [!code-csharp[LoadData](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#LoadData "loading dataset")]

    [LoadFromTextFile()](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)은 데이터 스키마를 정의하고 파일에서 읽습니다. 데이터 경로 변수를 가져와서 `IDataView`를 반환합니다.

## <a name="time-series-anomaly-detection"></a>시계열 변칙 검색

변칙 검색은 예기치 않거나 비정상적인 이벤트 또는 동작을 플래그합니다. 문제를 살펴봐야 할 곳에 대한 단서를 제공하고 "이상한가?"라는 질문에 대해 답할 수 있도록 도와줍니다.

![이상한가](./media/sales-anomaly-detection/anomalydetection.png)

변칙 검색은 시계열 데이터의 이상값 즉, 예상치 않거나 “이상한” 동작이 발생한 지정된 시계열의 지점을 검색하는 프로세스로서,

변칙 검색은 다양한 방법으로 유용하게 사용할 수 있습니다. 예를 들면 다음과 같습니다.

자동차가 있다면 다음 사항을 알고 싶을 것입니다. 이 오일 게이지 판독치가 정상인가? 누유가 있나?
전력 소비를 모니터링하는 경우 다음 사항을 알고 싶을 것입니다. 정전이 있나?

검색할 수 있는 시간 시계열 변칙에는 다음과 같은 두 종류가 있습니다.

* **급증** - 시스템에서 변칙 동작의 일시적인 버스트를 나타냅니다.

* **변화점** - 시스템에서 시간에 따른 지속적인 변화의 시작점을 나타냅니다.

ML.NET에서 IID 급증 검색 또는 IID 변화점 검색 알고리즘은 [독립적이고 동일하게 분산된 데이터 세트](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables)에 적합합니다.

다른 자습서의 모델과 달리 시계열 변칙 검색기 변환은 입력 데이터에서 직접 작동합니다. `IEstimator.Fit()` 메서드를 통해 변환을 생성하는 데 학습 데이터가 필요하지 않습니다. 그러나 `ProductSalesData`의 빈 목록에서 생성된 데이터 뷰에서 제공되는 데이터 스키마가 필요합니다.

급증 및 변화점을 검색하기 위해 동일한 제품 판매 데이터를 분석할 예정입니다. 모델 빌드 및 학습 프로세스는 급증 검색과 변화점 검색에 동일하지만, 특정 검색 알고리즘이 사용된다는 기본적인 차이점이 있습니다.

## <a name="spike-detection"></a>급증 검색

스파이크 검색의 목표는 대다수의 시계열 데이터 값과는 상당히 다른 갑작스럽지만 일시적인 버스트를 식별하는 것입니다. 의심스러운 희귀 항목, 이벤트 또는 관찰 사항을 시기적절하게 검색하여 최소화해야 합니다. 정전, 사이버 공격 또는 바이러스성 웹 콘텐츠 등의 다양한 변칙을 검색하기 위해 다음과 같은 접근 방식을 사용할 수 있습니다. 다음 이미지는 시계열 데이터 세트에서 급증의 예입니다.

![SpikeDetection](./media/sales-anomaly-detection/SpikeDetection.png)

### <a name="add-the-createemptydataview-method"></a>CreateEmptyDataView() 메서드 추가

`Program.cs`에 다음 메서드를 추가합니다.

[!code-csharp[CreateEmptyDataView](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEmptyDataView)]

`CreateEmptyDataView()`를 통해서는 `IEstimator.Fit()` 메서드의 입력으로 사용될 올바른 스키마를 사용하여 빈 데이터 뷰 개체를 생성합니다.

### <a name="create-the-detectspike-method"></a>DetectSpike() 메서드 만들기

`DetectSpike()` 메서드는 다음 작업을 수행합니다.

* 평가자에서 변환을 만듭니다.
* 판매 기록 데이터를 기준으로 급증을 검색합니다.
* 결과를 표시합니다.

1. 다음 코드를 사용하여 `Main()` 메서드 바로 뒤에 `DetectSpike()` 메서드를 만듭니다.

    ```csharp
    static void DetectSpike(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. [IidSpikeEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidSpikeEstimator)를 사용하여 급증 검색에 대한 모델을 학습합니다. 다음 코드를 사용하여 `DetectSpike()` 메서드에 추가합니다.

    [!code-csharp[AddSpikeTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddSpikeTrainer)]

1. `DetectSpike()` 메서드에서 다음 코드 줄로 다음을 추가하여 급증 검색 변환을 만듭니다.

    [!code-csharp[TrainModel1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel1)]

1. 다음 코드 줄을 추가하여 `productSales` 데이터를 `DetectSpike()` 메서드에서 다음 줄로 변환합니다.

    [!code-csharp[TransformData1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData1)]

    이전 코드에서는 [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) 메서드를 사용하여 여러 데이터 세트 입력 행에 대해 예측합니다.

1. `transformedData`를 다음 코드로 [CreateEnumerable()](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable%2A) 메서드를 사용하여 쉽게 표시하도록 강력한 형식의 `IEnumerable`로 변환합니다.

    [!code-csharp[CreateEnumerable1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable1)]

1. 다음 <xref:System.Console.WriteLine?displayProperty=nameWithType> 코드를 사용하여 표시 헤더 줄을 만듭니다.

    [!code-csharp[DisplayHeader1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader1)]

    급증 검색 결과에서 다음 정보를 표시합니다.

    * `Alert` - 지정된 데이터 요소에 대한 급증 경고를 나타냅니다.
    * `Score` - 데이터 세트에서 지정된 데이터 요소에 대한 `ProductSales` 값입니다.
    * `P-Value` "P"는 확률을 나타냅니다. P 값이 0에 가까울수록 데이터 포인트가 변칙일 가능성이 높습니다.

1. 다음 코드를 사용하여 `predictions` `IEnumerable`을 반복하고 결과를 표시합니다.

    [!code-csharp[DisplayResults1](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults1)]

1. `Main()` 메서드의 `DetectSpike()` 메서드에 호출을 추가합니다.

    [!code-csharp[CallDetectSpike](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectSpike)]

## <a name="spike-detection-results"></a>급증 검색 결과

다음과 같은 결과가 나타나야 합니다. 처리 중 메시지가 표시됩니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 일부 메시지는 다음 결과에서 제거되었습니다.

```console
Detect temporary changes in pattern
=============== Training the model ===============
=============== End of training process ===============
Alert   Score   P-Value
0       271.00  0.50
0       150.90  0.00
0       188.10  0.41
0       124.30  0.13
0       185.30  0.47
0       173.50  0.47
0       236.80  0.19
0       229.50  0.27
0       197.80  0.48
0       127.90  0.13
1       341.50  0.00 <-- Spike detected
0       190.90  0.48
0       199.30  0.48
0       154.50  0.24
0       215.10  0.42
0       278.30  0.19
0       196.40  0.43
0       292.00  0.17
0       231.00  0.45
0       308.60  0.18
0       294.90  0.19
1       426.60  0.00 <-- Spike detected
0       269.50  0.47
0       347.30  0.21
0       344.70  0.27
0       445.40  0.06
0       320.90  0.49
0       444.30  0.12
0       406.30  0.29
0       442.40  0.21
1       580.50  0.00 <-- Spike detected
0       412.60  0.45
1       687.00  0.01 <-- Spike detected
0       480.30  0.40
0       586.30  0.20
0       651.90  0.14
```

## <a name="change-point-detection"></a>변화점 검색

`Change points`은 수치 변화 및 추세와 같은 값의 시계열 이벤트 스트림 분산에서 지속적인 변화입니다. 이러한 지속적인 변화는 `spikes`보다 훨씬 오래 지속되며 심각한 이벤트를 나타낼 수 있습니다. `Change points`는 보통 육안으로는 보이지 않지만, 다음 메서드에서와 같은 접근법을 사용하여 데이터에서 검색할 수 있습니다.  다음 이미지는 변화점 검색의 예입니다.

![ChangePointDetection](./media/sales-anomaly-detection/ChangePointDetection.png)

### <a name="create-the-detectchangepoint-method"></a>DetectChangepoint() 메서드 만들기

`DetectChangepoint()` 메서드는 다음 작업을 실행합니다.

* 평가자에서 변환을 만듭니다.
* 판매 내역 데이터에 기반하여 변화점을 검색합니다.
* 결과를 표시합니다.

1. 다음 코드를 사용하여 `Main()` 메서드 바로 뒤에 `DetectChangepoint()` 메서드를 만듭니다.

    ```csharp
    static void DetectChangepoint(MLContext mlContext, int docSize, IDataView productSales)
    {

    }
    ```

1. 다음 코드를 사용하여 `DetectChangepoint()` 메서드에 [iidChangePointEstimator](xref:Microsoft.ML.Transforms.TimeSeries.IidChangePointEstimator)를 만듭니다.

    [!code-csharp[AddChangepointTrainer](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#AddChangepointTrainer)]

1. 이전에 수행한 방식대로 `DetectChangePoint()` 메서드에 다음 코드 줄을 추가하여 평가자에서 변환을 만듭니다.

    [!code-csharp[TrainModel2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TrainModel2)]

1. `Transform()` 메서드로 `DetectChangePoint()`에 다음 코드를 추가하여 데이터를 변환합니다.

    [!code-csharp[TransformData2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#TransformData2)]

1. 이전에 했던 것처럼, `transformedData`를 다음 코드로 `CreateEnumerable()` 메서드를 사용하여 쉽게 표시하도록 강력한 형식의 `IEnumerable`로 변환합니다.

    [!code-csharp[CreateEnumerable2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CreateEnumerable2)]

1. `DetectChangePoint()` 메서드에 아래 코드를 사용하여 표시 헤더를 다음 줄로 만듭니다.

    [!code-csharp[DisplayHeader2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayHeader2)]

    변화점 검색 결과에서 다음 정보를 표시합니다.

    * `Alert` - 지정된 데이터 요소에 대한 변화점 경고를 나타냅니다.
    * `Score` - 데이터 세트에서 지정된 데이터 요소에 대한 `ProductSales` 값입니다.
    * `P-Value` "P"는 확률을 나타냅니다. P 값이 0에 가까울수록 데이터 포인트가 변칙일 가능성이 높습니다.
    * `Martingale value`는 P 값의 시퀀스에 기반하여 데이터 요소의 “이상한” 정도를 식별하는 데 사용됩니다.

1. 다음 코드를 사용하여 `predictions` `IEnumerable`을 반복하고 결과를 표시합니다.

    [!code-csharp[DisplayResults2](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#DisplayResults2)]

1. `Main()` 메서드의 `DetectChangepoint()` 메서드에 다음 호출을 추가합니다.

    [!code-csharp[CallDetectChangepoint](~/samples/machine-learning/tutorials/ProductSalesAnomalyDetection/Program.cs#CallDetectChangepoint)]

## <a name="change-point-detection-results"></a>변화점 검색 결과

다음과 같은 결과가 나타나야 합니다. 처리 중 메시지가 표시됩니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 일부 메시지는 다음 결과에서 제거되었습니다.

```console
Detect Persistent changes in pattern
=============== Training the model Using Change Point Detection Algorithm===============
=============== End of training process ===============
Alert   Score   P-Value Martingale value
0       271.00  0.50    0.00
0       150.90  0.00    2.33
0       188.10  0.41    2.80
0       124.30  0.13    9.16
0       185.30  0.47    9.77
0       173.50  0.47    10.41
0       236.80  0.19    24.46
0       229.50  0.27    42.38
1       197.80  0.48    44.23 <-- alert is on, predicted changepoint
0       127.90  0.13    145.25
0       341.50  0.00    0.01
0       190.90  0.48    0.01
0       199.30  0.48    0.00
0       154.50  0.24    0.00
0       215.10  0.42    0.00
0       278.30  0.19    0.00
0       196.40  0.43    0.00
0       292.00  0.17    0.01
0       231.00  0.45    0.00
0       308.60  0.18    0.00
0       294.90  0.19    0.00
0       426.60  0.00    0.00
0       269.50  0.47    0.00
0       347.30  0.21    0.00
0       344.70  0.27    0.00
0       445.40  0.06    0.02
0       320.90  0.49    0.01
0       444.30  0.12    0.02
0       406.30  0.29    0.01
0       442.40  0.21    0.01
0       580.50  0.00    0.01
0       412.60  0.45    0.01
0       687.00  0.01    0.12
0       480.30  0.40    0.08
0       586.30  0.20    0.03
0       651.90  0.14    0.09
```

지금까지 이제 판매 데이터에서 급증 및 변화점 변칙을 검색하기 위한 기계 학습 모델을 성공적으로 빌드했습니다.

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/ProductSalesAnomalyDetection) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> * 데이터 로드
> * 급증 변칙 검색에 대한 모델 학습
> * 학습된 모델로 급증 변칙 검색
> * 변화 지점 변칙 검색에 대한 모델 학습
> * 학습된 모델로 변화점 변칙 검색

## <a name="next-steps"></a>다음 단계

Machine Learning 샘플 GitHub 리포지토리를 확인하여 전력 소비 변칙 검색 샘플을 살펴보세요.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-samples GitHub 리포지토리](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/AnomalyDetection_PowerMeterReadings)
