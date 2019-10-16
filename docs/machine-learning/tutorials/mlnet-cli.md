---
title: ML.NET CLI를 사용하여 감정 분석
description: 샘플 데이터 세트에서 ML 모델 및 관련된 C# 모드를 자동으로 생성
author: cesardl
ms.author: cesardl
ms.date: 04/24/2019
ms.custom: mvc
ms.topic: tutorial
ms.openlocfilehash: 5b3b0af5b46774beff9fb7a2a86c37e5399c0dd2
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957397"
---
# <a name="analyze-sentiment-using-the-mlnet-cli"></a>ML.NET CLI를 사용하여 감정 분석

ML.NET CLI를 사용하여 ML.NET 모델 및 기본 C# 코드를 자동으로 생성하는 방법을 알아봅니다. 구현하려는 기계 학습 작업과 데이터 세트를 제공하고 CLI는 AutoML 엔진을 사용하여 이진 모델뿐만 아니라 모델 생성 및 배포 소스 코드를 만듭니다.

이 자습서에서는 다음 단계를 수행합니다.
> [!div class="checklist"]
>
> - 선택된 기계 학습 작업에 사용할 데이터 준비
> - CLI에서 'mlnet auto-train' 명령 실행
> - 품질 메트릭 결과 검토
> - 생성된 C# 코드를 이해하여 애플리케이션에서 모델 사용
> - 모델 학습에 사용된 생성된 C# 코드 검색

> [!NOTE]
> 이 항목은 현재 미리 보기 중인 ML.NET CLI 도구를 참조하며 자료는 변경될 수 있습니다. 자세한 내용은 [ML.NET](https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet) 페이지를 참조하세요.

ML.NET CLI는 ML.NET의 일부이며, ML.NET 학습 시 .NET 개발자를 위해 ML.NET을 “자유롭게”하여 시작할 때 사용자가 처음부터 코딩할 필요가 없게 하는 것이 기본 목표입니다.

어떤 명령-프롬프트(Windows, Mac 또는 Linux)에서도 ML.NET CLI를 실행하여 사용자가 제공하는 학습 데이터 세트에 기반하여 좋은 품질의 ML.NET 모델 및 소스 코드를 생성할 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

- [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.2) 이상
- (옵션) [Visual Studio 2017 또는 2019](https://visualstudio.microsoft.com/vs/)
- [ML.NET CLI](../how-to-guides/install-ml-net-cli.md)

Visual Studio 또는 `dotnet run`(.NET Core CLI)으로 생성된 C# 코드를 실행할 수 있습니다.

## <a name="prepare-your-data"></a>데이터 준비

이진 분류 기계 학습 작업인 ‘감정 분석’ 시나리오에 사용한 기존 데이터 세트를 사용하려고 합니다. 유사한 방식으로 자체 데이터 세트를 사용할 수 있으며 사용자를 위한 모델과 코드가 생성됩니다.

1. [The UCI Sentiment Labeled Sentences dataset zip 파일(다음 참고에서 인용 내용 참조)](https://archive.ics.uci.edu/ml/machine-learning-databases/00331/sentiment%20labelled%20sentences.zip)을 다운로드하고 사용자가 선택한 폴더에 압축을 풉니다.

    > [!NOTE]
    > 이 자습서의 데이터 세트에서는 다음 데이터 세트를 사용합니다. 'From Group to Individual Labels using Deep Features', Kotzias et al,. KDD 2015)에서 제공되고 UCI Machine Learning Repository(Dua, D. 및 Karra Taniskidou, E. (2017))에서 호스트됩니다. UCI Machine Learning Repository[http://archive.ics.uci.edu/ml ]. Irvine, CA: University of California, School of Information and Computer Science.

2. `yelp_labelled.txt` 파일을 이전에 만든 폴더(예: `/cli-test`)에 복사합니다.

3. 기본 설정된 명령 프롬프트를 열고 데이터 세트 파일을 복사한 폴더로 이동합니다. 예:

    ```console
    > cd /cli-test
    ```

    Visual Studio Code 등의 텍스트 편집기를 사용하여 `yelp_labelled.txt` 데이터 세트 파일을 열고 검색할 수 있습니다. 다음과 같은 구조를 볼 수 있습니다.

    - 파일에는 헤더가 없습니다. 열의 인덱스를 사용하게 됩니다.

    - 단 두 개의 열이 있습니다.

        | 텍스트(열 인덱스 0) | 레이블(열 인덱스 1)|
        |--------------------------|-------|
        | 와우... 여기가 좋았습니다. | 1 |
        | 크러스트가 좋지 않습니다. | 0 |
        | 맛있지는 않고 식감도 좋지 않습니다. | 0 |
        | ...더 많은 텍스트 행... | ...(1 또는 0)... |

    편집기에서 데이터 세트 파일을 닫습니다.

    이제 ‘감정 분석’ 시나리오에 CLI를 사용할 준비가 되었습니다.

    > [!NOTE]
    > 이 자습서를 마친 후에는 *'이진 분류', '다중 클래스 분류' 및 '회귀'* ) 등 ML.NET CLI Preview에서 현재 지원되는 ML 작업에 사용할 준비가 되었다면 자체 데이터 세트로 시도해 볼 수도 있습니다.

## <a name="run-the-mlnet-auto-train-command"></a>'mlnet auto-train' 명령 실행

1. 다음 ML.NET CLI 명령을 실행합니다.

    ```console
    > mlnet auto-train --task binary-classification --dataset "yelp_labelled.txt" --label-column-index 1 --has-header false --max-exploration-time 10
    ```

    이 명령은 **`mlnet auto-train` 명령**을 사용합니다.
    - **`binary-classification`** 유형의 **ML 작업**
    - 학습 및 테스트 데이터 세트로 **데이터 세트 파일 `yelp_labelled.txt`** 사용(내부적으로 CLI는 교차 유효성 검증을 사용하거나, 하나는 학습, 그리고 하나는 테스트용으로 두 개의 데이터 세트로 분할함)
    - 여기서 예측하려는 **목표/대상 열**(일반적으로 **'레이블'** )은 **인덱스 1이 있는 열**(즉, 인덱스가 0 기반이므로 두 번째 열)임
    - 이 특정 데이터 세트 파일에는 헤더가 없으므로 열 이름으로 **파일 헤더를 사용하지 않음**
    - 실험의 **목표 검색 시간**은 **10초**임

    CLI의 출력은 다음과 같이 보입니다.

    <!-- markdownlint-disable MD023 MD025 -->

    # <a name="windowstabwindows"></a>[Windows](#tab/windows)

    ![PowerShell에서의 ML.NET CLI auto-train](./media/mlnet-cli/mlnet-auto-train-binary-classification-powershell.gif)

    # <a name="macos-bashtabmacosbash"></a>[macOS Bash](#tab/macosbash)

    ![PowerShell에서의 ML.NET CLI auto-train](./media/mlnet-cli/mlnet-auto-train-binary-classification-bash.gif)

    이 특정 사례에서는 단 10초만에, 그리고 제공된 소규모의 데이터 세트를 사용하여 CLI 도구는 아주 적은 반복을 실행할 수 있었습니다. 즉, 다른 내부 데이터 변형과 알고리즘의 하이퍼 매개 변수로 다른 조합의 알고리즘/구성에 기반하여 여러 차례 학습했음을 의미합니다. 

    마지막으로, 10초만에 발견된 “최적 품질” 모델은 어떠한 특정 구성으로 특별한 트레이너/알고리즘을 사용하는 모델입니다. 검색 시간에 따라 명령은 다른 결과를 생성할 수 있습니다. 선택은 표시된 다중 메트릭(예: `Accuracy`)에 기반합니다.

    **모델의 품질 메트릭 이해**

    이진 분류 모델을 평가하는 첫 번째 그리고 가장 쉬운 메트릭은 이해하기 간단한 정확도입니다. "정확도는 테스트 데이터 세트 사용 시 올바른 예측의 비율입니다.” 100%(1.00)에 가까울 수록 좋습니다.

    단, 정확도 메트릭으로 측정하는 것으로 충분하지 않은, 특히 테스트 데이터 세트에서 레이블(이 경우에는 0과 1)의 균형이 맞지 않는 경우가 그렇습니다.

    다른 모델을 평가하는 데 사용하는 정확도, AUC, AUCPR, F1-점수 등의 **메트릭에 대한 보다 자세한 정보**와 추가 메트릭은 [ML.NET 메트릭 이해](../resources/metrics.md)를 참조하세요.

    > [!NOTE]
    > 이 매우 동일한 데이터 세트를 사용해 보고 `--max-exploration-time`에 몇 분을 지정하여(예를 들어, 3분은 180초) 이 데이터 세트에 대한 다른 학습 파이프라인 구성(매우 작음, 1000개 행)에 더 나은 “최적 모델”을 찾게 됩니다. 
        
    더 큰 데이터 세트를 목표로 하는 “프로덕션 준비 모델”인 “최적/좋은 품질”의 모델을 찾기 위해서는 데이터 세트의 크기에 따라 일반적으로 훨씬 더 많은 검색 시간을 지정하는 CLI로 실험해 봐야 합니다. 사실 대부분의 경우, 특히 데이터 세트의 행과 열이 큰 경우에는 몇 시간의 검색 시간이 필요할 수 있습니다. 

1. 이전 명령 실행으로 다음 자산을 생성했습니다.

    - 사용 준비가 된 Serialize된 모델 .zip("최적 모델") 
    - 해당 생성된 모델을 실행/채점할 C# 코드(해당 모델으로 최종 사용자 앱에서 예측하기 위한)
    - 이 모델을 생성하는 데 사용한 C# 학습 코드(학습 목적)
    - 하이퍼 매개 변수 및 데이터 변형 조합으로 시도한 각 알고리즘에 대한 구체적인 세부 정보가 있는 검색된 모든 반복이 있는 로그 파일 

    처음 두 자산(.ZIP 파일 모델과 해당 모델을 실행하기 위한 C# 코드)은 생성된 ML 모델로 예측을 수행하기 위해 최종 사용자 앱(ASP.NET Core 웹앱, 서비스, 데스크톱 앱 등)에서 직접 사용할 수 있습니다.

    세 번째 자산인 학습 코드는 사용자에게 생성된 모델을 학습하기 위해 CLI에서 사용한 ML.NET API 코드를 표시하므로, 사용자는 CLI에서 선택한 특정 트레이너/알고리즘 및 하이퍼 매개 변수를 살펴볼 수 있습니다.

이러한 열거된 자산은 자습서의 다음 단계에 설명되어 있습니다.

## <a name="explore-the-generated-c-code-to-use-for-running-the-model-to-make-predictions"></a>예측을 수행하기 위해 모델 실행에 사용할 생성된 C# 코드 검색

1. Visual Studio(2017 또는 2019)에서, 원래 대상 폴더(자습서에서 `/cli-test`로 이름이 지정된) 내의 `SampleBinaryClassification` 폴더에 생성된 솔루션을 엽니다. 다음과 유사한 솔루션이 보입니다.

    > [!NOTE]
    > 자습서에서는 Visual Studio를 사용하도록 제안하고 있지만 텍스트 편집기를 사용하여, 생성된 C# 코드(두 개의 프로젝트)를 검색하고 macOS, Linux 또는 Windows 머신에서 `dotnet CLI`로 생성된 콘솔 앱을 실행할 수도 있습니다.

    ![CLI로 생성된 VS 솔루션](./media/mlnet-cli/generated-csharp-solution-detailed.png)

    - Serialize된 ML 모델(.zip 파일)과 데이터 클래스(데이터 모델)를 포함한 생성된 **클래스 라이브러리**는 클래스 라이브러리를 직접 참조하거나(원한다면 코드를 이동하여) 최종 사용자 애플리케이션에서 직접 사용할 수 있습니다.
    - 생성된 **콘솔 앱**에는 사용자가 검토해야 하는 실행 코드가 있습니다. 그런 다음, 사용자가 예측하려는 최종 사용자 애플리케이션으로 해당 단순 코드(단 몇 개의 줄)를 이동하여 ‘채점 코드’(예측하기 위해 ML 모델을 실행하는 코드)를 재사용합니다. 

1. 클래스 라이브러리 프로젝트에서 **ModelInput.cs** 및 **ModelOutput.cs** 클래스 파일을 엽니다. 이러한 클래스는 데이터를 보유하기 위해 사용하는 ‘데이터 클래스’ 또는 POCO 클래스임을 알게 됩니다. '상용구 코드’지만 데이터 세트에 수십 또는 수백 개의 열이 있는 경우 생성하는 것이 유용합니다. 
    - `ModelInput` 클래스는 데이터 세트에서 데이터를 읽을 때 사용됩니다. 
    - `ModelOutput` 클래스는 예측 결과(예측 데이터)를 가져오는 데 사용됩니다.

1. Program.cs 파일을 열고 코드를 검색합니다. 단 몇 개의 줄로 모델을 실행하고 단순 예측을 수행할 수 있습니다.

    ```csharp
    static void Main(string[] args)
    {
        MLContext mlContext = new MLContext();

        // Training code used by ML.NET CLI and AutoML to generate the model
        //ModelBuilder.CreateModel();

        ITransformer mlModel = mlContext.Model.Load(MODEL_FILEPATH, out DataViewSchema inputSchema);
        var predEngine = mlContext.Model.CreatePredictionEngine<ModelInput, ModelOutput>(mlModel);

        // Create sample data to do a single prediction with it 
        ModelInput sampleData = CreateSingleDataSample(mlContext, DATA_FILEPATH);

        // Try a single prediction
        ModelOutput predictionResult = predEngine.Predict(sampleData);

        Console.WriteLine($"Single Prediction --> Actual value: {sampleData.Label} | Predicted value: {predictionResult.Prediction}");
    }
    ```

- 코드의 첫 번째 줄은 ML.NET 코드를 실행할 때마다 필요한 `MLContext` 개체를 만듭니다. 

- 코드의 두 번째 줄은 CLI 도구를 통해 사용자를 위해 이미 학습되어 모델의 Serialize된 .ZIP 파일에 저장되었으므로 모델을 학습할 필요가 없어 주석 처리되었습니다. 하지만 CLI를 통해 *"모델이 학습된 방식"* 을 보고 싶다면 이 줄의 주석 처리를 해제하고 특정 ML 모델에 사용된 학습 코드를 실행/디버깅할 수 있습니다.

- 코드의 세 번째 줄에서는 해당 모델 .ZIP 파일에 대한 경로를 제공하여 `mlContext.Model.Load()` API로 Serialize된 모델 .ZIP 파일에서 모델을 로드합니다.

- 코드의 네 번째 줄에서는 `mlContext.Model.CreatePredictionEngine<TSrc,TDst>(ITransformer mlModel)` API를 사용하여 `PredictionEngine` 개체를 로드하고 생성합니다. 단일 데이터 샘플(이 경우에는 감정을 예측하기 위한 단일 텍스트 조각)을 대상으로 예측하려고 할 때마다 `PredictionEngine` 개체가 필요합니다.

- 코드의 다섯 번째 줄은 함수 `CreateSingleDataSample()`을 호출하여 예측에 사용할 *단일 샘플 데이터*를 만듭니다. CLI 도구는 어떤 종류의 샘플 데이터를 사용할지 알지 못하므로, 이 함수 내에 데이터 세트의 첫 번째 행을 로드합니다. 하지만 이러한 경우를 위해 이 함수를 구현하는 이 유사한 코드를 업데이트하여 `CreateSingleDataSample()` 함수의 최신 구현 대신 자체의 ‘하드 코드된’ 데이터를 만들 수도 있습니다.

    ```csharp
    private static ModelInput CreateSingleDataSample()
    {
        ModelInput sampleForPrediction = new ModelInput() { Col0 = "The ML.NET CLI is great for getting started. Very cool!", Label = true };
        return sampleForPrediction;
    }
    ```

1. 데이터 세트의 첫 번째 행에서 로드된 원래 샘플 데이터를 사용하거나 자체 사용자 지정 하드 코드된 샘플 데이터를 제공하여 프로젝트를 실행합니다. 다음과 견줄만한 예측을 해야 합니다.

    # <a name="windowstabwindows"></a>[Windows](#tab/windows)

    F5 키를 눌러(실행 단추) Visual Studio에서 콘솔 앱을 실행합니다.

    ![PowerShell에서의 ML.NET CLI auto-train](./media/mlnet-cli/sample-cli-prediction-execution.png))

    # <a name="macos-bashtabmacosbash"></a>[macOS Bash](#tab/macosbash)

    명령 프롬프트에서 다음 명령을 입력하여 콘솔 앱을 실행합니다.

     ```bash
     > cd SampleBinaryClassification
     > cd SampleBinaryClassification.ConsoleApp

     > dotnet run
     ```

    ![PowerShell에서의 ML.NET CLI auto-train](./media/mlnet-cli/sample-cli-prediction-execution-bash.png))

    ---

1. 하드 코드된 샘플 데이터를 다른 감정의 다른 문장으로 변경해 보고 모델이 긍정 또는 부정적인 감정을 예측하는 방식을 살펴 봅니다. 

## <a name="infuse-your-end-user-applications-with-ml-model-predictions"></a>최종 사용자 애플리케이션에 ML 모델 예측 입력

유사한 ‘ML 모델 채점 코드’를 사용하여 최종 사용자 애플리케이션에서 모델을 실행하고 예측을 수행할 수 있습니다. 

예를 들어 이 코드를 **WPF** 및 **WinForms** 등의 Windows 데스크톱 애플리케이션으로 직접 이동하고 콘솔 앱에서 실행된 것과 동일한 방식으로 모델을 실행할 수 있습니다.

그러나 ML 모델을 실행하기 위해 이러한 코드 줄을 구현하는 방식은 최적화되어야 하며(즉, 모델 .zip 파일을 캐싱하고 한 번 로드), 특히 다음 섹션에서 설명된 대로 웹 애플리케이션 또는 분산 서비스와 같이 애플리케이션이 확장 가능해야 하는 경우에는 모든 요청마다 만드는 대신, 싱글톤 개체가 있어야 합니다.

### <a name="running-mlnet-models-in-scalable-aspnet-core-web-apps-and-services-multi-threaded-apps"></a>확장 가능한 ASP.NET Core 웹앱 및 서비스(다중 스레드 앱)에서 ML.NET 모델 실행

모델 개체(모델의 .zip 파일에서 로드한 `ITransformer`) 및 `PredictionEngine` 개체 만들기는 특히 확장 가능한 웹앱과 분산 서비스에서 실행할 경우 최적화되어야 합니다. 첫 번째 경우, 모델 개체(`ITransformer`)에서 최적화는 간단합니다. `ITransformer` 개체는 스레드로부터 안전하므로, 한 번에 모델을 로드할 수 있도록 싱글톤 또는 정적 개체로 해당 개체를 캐싱할 수 있습니다.

두 번째 개체, `PredictionEngine` 개체의 경우 `PredictionEngine` 개체가 스레드로부터 안전하지 않아 이 개체를 ASP.NET Core 앱에서 싱글톤 또는 정적 개체로 인스턴스화할 수 없으므로 쉽지 않습니다. 이 스레드로부터 안전한, 그리고 확장성 문제는 [블로그 게시물](https://devblogs.microsoft.com/cesardelatorre/how-to-optimize-and-run-ml-net-models-on-scalable-asp-net-core-webapis-or-web-apps/)에서 자세히 다루고 있습니다. 

그러나 블로그 게시물에 설명된 것보다 훨씬 쉽습니다. 사용자를 위해 보다 단순한 접근법에 노력을 기울였으며 애플리케이션 DI 서비스(종속성 주입 서비스)에서 등록하여 ASP.NET Core 앱 및 서비스에서 쉽게 사용한 다음, 사용자 코드에서 직접 사용할 수 있는 괜찮은 **'.NET Core 통합 패키지'** 를 만들었습니다. 다음 자습서와 수행 예제를 확인하세요.

- [자습서: ASP.NET Core 웹앱 및 WebAPI에서 ML.NET 모델 실행](https://aka.ms/mlnet-tutorial-netcoreintegrationpkg)
- [샘플: ASP.NET Core WebAPI의 확장 가능한 ML.NET 모델](https://aka.ms/mlnet-sample-netcoreintegrationpkg)

## <a name="explore-the-generated-c-code-that-was-used-to-train-the-best-quality-model"></a>“최적 품질” 모델을 학습하기 위해 사용한 생성된 C# 코드 검색 

보다 고급의 학습 목적을 위해 생성된 모델을 학습하기 위해 CLI 도구에서 사용한 생성된 C# 코드를 검색할 수도 있습니다.

이 ‘학습 모델 코드’는 현재 이름이 `ModelBuilder`인 생성된 사용자 지정 클래스에 생성되어 있으므로, 이 학습 코드를 살펴볼 수 있습니다.

무엇보다도 이 특별한 시나리오(감정 분석 모델)의 경우 다음 자습서에 설명된 코드와 생성된 학습 코드를 비교할 수도 있습니다.

- 비교: [자습서: 감정 분석 이진 분류 시나리오에서 ML.NET 사용](sentiment-analysis.md)

CLI 도구를 통해 생성된 코드와 자습서에서 선택된 알고리즘 및 파이프라인 구성을 비교하는 것이 흥미롭습니다. 더 나은 모델을 찾기 위해 반복하고 검색하는 데 소요된 시간에 따라, 선택된 알고리즘은 특정 하이퍼 매개 변수 및 파이프라인 구성과 함께 다를 수 있습니다.

## <a name="see-also"></a>참고 항목

- [ML.NET CLI로 모델 학습 자동화](../automate-training-with-cli.md)
- [자습서: ASP.NET Core 웹앱 및 WebAPI에서 ML.NET 모델 실행](https://aka.ms/mlnet-tutorial-netcoreintegrationpkg)
- [샘플: ASP.NET Core WebAPI의 확장 가능한 ML.NET 모델](https://aka.ms/mlnet-sample-netcoreintegrationpkg)
- [ML.NET CLI auto-train 명령 참조 가이드](../reference/ml-net-cli-reference.md) 
- [ML.NET CLI(명령줄 인터페이스) 도구를 설치하는 방법](../how-to-guides/install-ml-net-cli.md)
- [ML.NET CLI의 원격 분석](../resources/ml-net-cli-telemetry.md)

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - 선택한 ML 작업(해결할 문제)에 사용할 데이터 준비
> - CLI 도구에서 'mlnet auto-train' 명령 실행
> - 품질 메트릭 결과 검토
> - 모델을 실행하기 위해 생성된 C# 코드(최종 사용자 앱에서 사용할 코드) 이해
> - “최적 품질” 모델(학습 목적)을 학습하기 위해 사용한 생성된 C# 코드 검색

> [!div class="nextstepaction"]
> [ML.NET CLI로 모델 학습 자동화](../automate-training-with-cli.md)
