---
title: '자습서: 미리 학습된 TensorFlow 모델에서 ML.NET 이미지 분류 모델 생성'
description: 기존 TensorFlow 모델에서 새로운 ML.NET 이미지 분류 모델로 정보를 전이하는 방법을 알아봅니다. TensorFlow 모델은 이미지를 천 개 범주로 분류하도록 학습되었습니다. ML.NET 모델은 전이 학습을 사용하여 이미지를 좀 더 광범위한 범주로 분류합니다.
ms.date: 09/30/2019
ms.topic: tutorial
ms.custom: mvc, title-hack-0612
author: natke
ms.author: nakersha
ms.openlocfilehash: 8ae966330ca85722c72c92e26363d99c7d9de3e7
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698645"
---
# <a name="tutorial-generate-an-mlnet-image-classification-model-from-a-pre-trained-tensorflow-model"></a>자습서: 미리 학습된 TensorFlow 모델에서 ML.NET 이미지 분류 모델 생성

기존 TensorFlow 모델에서 새로운 ML.NET 이미지 분류 모델로 정보를 전이하는 방법을 알아봅니다.

TensorFlow 모델은 이미지를 천 개 범주로 분류하도록 학습되었습니다. ML.NET 모델은 파이프라인에서 TensorFlow 모델의 일부를 사용하여 이미지를 3개 범주로 분류하는 모델을 학습합니다.

[이미지 분류](https://en.wikipedia.org/wiki/Outline_of_object_recognition) 모델을 처음부터 학습시키려면 수백만 개의 매개 변수, 많은 레이블 지정 학습 데이터 및 많은 양의 컴퓨팅 리소스(수백 시간의 GPU 시간)를 설정해야 합니다. 사용자 지정 모델을 처음부터 학습시키는 것만큼 효과적이지는 않지만, 전이 학습을 사용하면 수천 개 이미지 및 수백만 개 레이블 지정 이미지를 사용하여 이 프로세스를 간소화하고 사용자 지정 모델을 매우 빠르게 빌드할 수 있습니다(GPU가 없는 머신에서는 1시간 안에 가능). 이 자습서에서는 해당 프로세스를 좀 더 축소하여 12개의 학습 이미지만 사용합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> * 문제 이해
> * 미리 학습된 TensorFlow 모델을 ML.NET 파이프라인에 통합
> * ML.NET 모델 학습 및 평가
> * 테스트 이미지 분류

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다. 기본적으로 이 자습서의 .NET 프로젝트 구성은 .NET Core 2.2를 대상으로 합니다.

## <a name="what-is-transfer-learning"></a>전이 학습이란?

전이 학습은 한 가지 문제를 해결한 후 관련이 있지만 다른 문제에 적용하면서 얻은 정보를 사용하는 프로세스입니다.

이 자습서에서는 이미지를 천 개의 범주로 분류하도록 학습된 TensorFlow 모델의 일부를 3개 범주로 이미지를 분류하는 ML.NET 모델에서 사용합니다.

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).

* Microsoft.ML 1.3.1 Nuget 패키지
* Microsoft.ML.ImageAnalytics 1.3.1 Nuget 패키지
* Microsoft.ML.TensorFlow 1.3.1 Nuget 패키지

* [자습서 자산 디렉터리 .ZIP 파일](https://download.microsoft.com/download/0/E/5/0E5E0136-21CE-4C66-AC18-9917DED8A4AD/image-classifier-assets.zip)

* [InceptionV1 기계 학습 모델](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)

## <a name="select-the-right-machine-learning-task"></a>적절한 기계 학습 작업 선택

### <a name="deep-learning"></a>딥러닝

[딥 러닝](https://en.wikipedia.org/wiki/Deep_learning)은 Computer Vision 및 음성 인식 같은 혁신적인 영역인 기계 학습의 하위 집합입니다.

딥 러닝 모델은 여러 학습 계층이 포함된 대규모 [레이블 지정 데이터](https://en.wikipedia.org/wiki/Labeled_data) 및 [신경망](https://en.wikipedia.org/wiki/Artificial_neural_network) 세트를 사용하여 학습됩니다. 딥 러닝

* Computer Vision 같은 일부 작업에서 더 효과적으로 작동합니다.
* 상당한 양의 학습 데이터가 필요합니다.

이미지 분류는 다음과 같은 범주로 이미지를 자동으로 분류할 수 있는 일반적인 기계 학습 작업입니다.

* 이미지에서 사람 얼굴을 인식하는지 여부.
* 고양이 및 개 인식.

 또는 다음 이미지와 같이 이미지가 음식, 장난감 또는 어플라이언스인지 확인:

![피자 이미지](./media/image-classification/220px-Pepperoni_pizza.jpg)
![테디 베어 이미지](./media/image-classification/119px-Nalle_-_a_small_brown_teddy_bear.jpg)
![토스터 이미지](./media/image-classification/193px-Broodrooster.jpg)

>[!Note]
> 앞의 이미지는 Wikimedia Commons에 속하고 다음 특성을 사용합니다.
>
> * “220px-Pepperoni_pizza.jpg” 공용 도메인, https://commons.wikimedia.org/w/index.php?curid=79505,
> * “119px-Nalle_-_a_small_brown_teddy_bear.jpg” 작성자: [Jonik](https://commons.wikimedia.org/wiki/User:Jonik) - 직접 사진 촬영, CC BY-SA 2.0, https://commons.wikimedia.org/w/index.php?curid=48166.
> * “193px-Broodrooster.jpg” 작성자: [M.Minderhoud](https://nl.wikipedia.org/wiki/Gebruiker:Michiel1972) - 직접 작업, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=27403

`Inception model`은 이미지를 천 개의 범주로 분류하도록 학습되지만, 이 자습서에서는 더 작은 범주 세트 및 해당 범주로만 이미지를 분류해야 합니다. `transfer learning`의 `transfer` 부분을 입력합니다. 이미지를 인식하고 사용자 지정 이미지 분류자의 제한된 새 범주로 분류하는 `Inception model`의 기능을 전이할 수 있습니다.

* 음식
* 장난감
* 어플라이언스

이 자습서에서는 `ImageNet` 데이터 세트에 대해 학습된 인기 있는 이미지 인식 모델인 TensorFlow [개시 모델](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip) 심층 학습 모델을 사용합니다. TensorFlow 모델은 전체 이미지를 “Umbrella”, “Jersey” 및 “Dishwasher” 등의 천 개 클래스로 분류합니다.

`Inception model`은 수천 개의 이미지를 기반으로 미리 학습되었으므로 이미지 식별에 필요한 [이미지 기능](https://en.wikipedia.org/wiki/Feature_(computer_vision))을 내부적으로 포함합니다. 모델에서 이러한 내부 이미지 기능을 활용하여 훨씬 더 적은 수의 클래스를 새 모델에 학습시킬 수 있습니다.

다음 다이어그램과 같이 .NET Core 또는 .NET Framework 애플리케이션에서 ML.NET NuGet 패키지에 대한 참조를 추가합니다. 기본적으로 ML.NET은 기존 학습된 `TensorFlow` 모델 파일을 로드하는 코드를 작성하는 데 사용할 수 있는 네이티브 `TensorFlow` 라이브러리를 포함하고 참조합니다.

![TensorFlow 변환 ML.NET 아키텍처 다이어그램](./media/image-classification/tensorflow-mlnet.png)

### <a name="multiclass-classification"></a>다중 클래스 분류

TensorFlow 개시 모델을 사용하여 기존 기계 학습 알고리즘에 대한 입력으로 적합한 기능을 추출한 후에 ML.NET [다중 클래스 분류자](../resources/tasks.md#multiclass-classification)를 추가합니다.

이 경우에 사용되는 특정 트레이너는 [다항 로지스틱 회귀 알고리즘](https://en.wikipedia.org/wiki/Multinomial_logistic_regression)입니다.

이 트레이너가 구현하는 알고리즘은 이미지 데이터에 심층 학습 모델이 작동하는 경우에 해당하는 많은 기능을 사용할 때 발생하는 문제에 잘 작동합니다.

### <a name="data"></a>데이터

두 개의 데이터 소스인 `.tsv` 파일 및 이미지 파일이 있습니다.  `tags.tsv` 파일에는 두 개의 열이 있습니다. 첫 번째 열은 `ImagePath`로 정의되고 두 번째 열은 이미지에 해당하는 `Label`입니다. 다음 예제 파일에는 머리글 행이 없고 다음과 같이 표시됩니다.

<!-- markdownlint-disable MD010 -->
```tsv
broccoli.jpg    food
pizza.jpg   food
pizza2.jpg  food
teddy2.jpg  toy
teddy3.jpg  toy
teddy4.jpg  toy
toaster.jpg appliance
toaster2.png    appliance
```
<!-- markdownlint-enable MD010 -->

학습 및 테스트 이미지는 zip 파일로 다운로드할 수 있는 자산 폴더에 있습니다. 이 이미지는 Wikimedia Commons에 속합니다.
> *[Wikimedia Commons](https://commons.wikimedia.org/w/index.php?title=Main_Page&oldid=313158208), 무료 미디어 리포지토리.* 2018년 10월 17일 10시 48분 검색된 위치: https://commons.wikimedia.org/wiki/Pizza https://commons.wikimedia.org/wiki/Toaster https://commons.wikimedia.org/wiki/Teddy_bear

## <a name="setup"></a>설정

### <a name="create-a-project"></a>프로젝트 만들기

1. "TransferLearningTF"라는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

1. **Microsoft.ML NuGet 패키지**를 설치합니다.

    * 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
    * 패키지 소스로 “nuget.org”를 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색합니다.
    * **버전** 드롭다운을 클릭하고, 목록에서 **1.3.1** 패키지를 선택하고, **설치** 단추를 선택합니다.
    * **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택합니다.
    * 나열된 패키지 라이선스 조건에 동의하면 **라이선스 수락** 대화 상자에서 **동의함** 단추를 선택합니다.
    * **Microsoft.ML.ImageAnalytics v1.3.1** 및 **Microsoft.ML.TensorFlow v1.3.1**에 대해 이 단계를 반복합니다.

### <a name="download-assets"></a>자산 다운로드

1. [프로젝트 자산 디렉터리 zip 파일](https://download.microsoft.com/download/0/E/5/0E5E0136-21CE-4C66-AC18-9917DED8A4AD/image-classifier-assets.zip)을 다운로드하고 압축을 풉니다.

1. `assets` 디렉터리를 *TransferLearningTF* 프로젝트 디렉터리에 복사합니다. 이 디렉터리 및 해당 하위 디렉터리에는 이 자습서에 필요한 데이터 및 지원 파일이 포함되어 있습니다(다음 단계에서 다운로드 및 추가하는 Inception 모델 제외).

1. [Inception 모델](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)을 다운로드하고 압축을 풉니다.

1. 방금 *TransferLearningTF* 프로젝트 `assets/inputs-train/inception` 디렉터리에 압축을 푼 `inception5h` 디렉터리의 콘텐츠를 복사합니다. 이 디렉터리에는 다음 이미지와 같이 이 자습서에 필요한 모델 및 추가 지원 파일이 포함되어 있습니다.

   ![Inception 디렉터리 콘텐츠](./media/image-classification/inception-files.png)

1. 솔루션 탐색기에서 자산 디렉터리 및 하위 디렉터리의 각 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

1. *Program.cs* 파일 맨 위에 다음 추가 `using` 문을 추가합니다.

    [!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#AddUsings)]

1. `Main` 메서드 바로 위의 줄에 다음 코드를 추가하여 해당 자산 경로를 지정합니다.

    [!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DeclareGlobalVariables)]

1. 입력 데이터 및 예측에 대한 클래스를 만듭니다.

    [!code-csharp[DeclareImageData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DeclareImageData)]

    `ImageData`는 입력 이미지 데이터 클래스이며 다음 <xref:System.String> 필드를 포함합니다.

    * `ImagePath`에는 이미지 파일 이름이 포함됩니다.
    * `Label`에는 이미지 레이블의 값이 포함됩니다.

1. `ImagePrediction`의 새 클래스를 프로젝트에 추가합니다.

    [!code-csharp[DeclareImagePrediction](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DeclareImagePrediction)]

    `ImagePrediction`은 이미지 예측 클래스이며 다음 필드를 포함합니다.

    * `Score`에는 지정된 이미지 분류를 위한 신뢰율이 포함됩니다.
    * `PredictedLabelValue`에는 예측된 이미지 분류 레이블의 값이 포함됩니다.

    `ImagePrediction`은 모델이 학습된 후 예측에 사용되는 클래스입니다. 이 클래스에는 이미지 경로의 `string`(`ImagePath`)이 포함됩니다. `Label`은 모델을 다시 사용하고 학습시키는 데 사용됩니다. `PredictedLabelValue`은 예측 및 평가 중에 사용됩니다. 평가를 위해 학습 데이터가 있는 입력, 예측 값 및 모델이 사용됩니다.

### <a name="initialize-variables-in-main"></a>Main에서 변수 초기화

1. `MLContext`의 새 인스턴스를 사용하여 `mlContext` 변수를 초기화합니다.  `Main` 메서드에서 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 바꿉니다.

    [!code-csharp[CreateMLContext](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CreateMLContext)]

    [MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작점이며, `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

### <a name="create-a-struct-for-inception-model-parameters"></a>개시 모델 매개 변수에 대한 구조체 만들기

1. 개시 모델에는 전달해야 하는 여러 가지 매개 변수가 있습니다. `Main()` 메서드 바로 뒤에서 다음 코드를 사용하여 매개 변수 값을 친숙한 이름에 매핑하는 구조체를 만듭니다.

    [!code-csharp[InceptionSettings](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#InceptionSettings)]

### <a name="create-a-display-utility-method"></a>표시 유틸리티 메서드 만들기

이미지 데이터와 관련 예측을 여러 번 표시하므로 표시 유틸리티 메서드를 만들어 이미지 및 예측 결과 표시를 처리합니다.

1. 다음 코드를 사용하여 `InceptionSettings` 구조체 바로 뒤에 `DisplayResults()` 메서드를 만듭니다.

    ```csharp
    private static void DisplayResults(IEnumerable<ImagePrediction> imagePredictionData)
    {

    }
    ```

1. 다음과 같이 `DisplayResults` 메서드의 본문을 채웁니다.

    [!code-csharp[DisplayPredictions](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayPredictions)]

### <a name="create-a-tsv-file-utility-method"></a>.tsv 파일 유틸리티 메서드 만들기

1. 다음 코드를 사용하여 `DisplayResults()` 메서드 바로 뒤에 `ReadFromTsv()` 메서드를 만듭니다.

    ```csharp
    public static IEnumerable<ImageData> ReadFromTsv(string file, string folder)
    {

    }
    ```

1. 다음과 같이 `ReadFromTsv` 메서드의 본문을 채웁니다.

    [!code-csharp[ReadFromTsv](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ReadFromTsv)]

    이 코드는 `tags.tsv` 파일을 구문 분석하여 `ImagePath` 속성의 이미지 파일 이름에 파일 경로를 추가하고 로드한 다음, `Label`을 `ImageData` 개체로 로드합니다.

### <a name="create-a-method-to-make-a-prediction"></a>예측을 수행하는 메서드 만들기

1. 다음 코드를 사용하여 `DisplayResults()` 메서드 바로 앞에 `ClassifySingleImage()` 메서드를 만듭니다.

    ```csharp
    public static void ClassifySingleImage(MLContext mlContext, ITransformer model)
    {

    }
    ```

1. 단일 `ImagePath`의 정규화된 경로 및 이미지 파일 이름을 포함하는 `ImageData` 개체를 만듭니다. `ClassifySingleImage()` 메서드의 다음 줄로 아래 코드를 추가합니다.

    [!code-csharp[LoadImageData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadImageData)]

1. `ClassifySingleImage` 메서드에서 다음 코드를 그 다음 줄로 추가하여 단일 예측을 수행합니다.

    [!code-csharp[PredictSingle](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#PredictSingle)]

    예측을 가져오려면 [Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) 메서드를 사용합니다. [PredictionEngine](xref:Microsoft.ML.PredictionEngine%602)은 데이터의 단일 인스턴스에 대한 예측을 수행할 수 있는 편리한 API입니다. [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)은 스레드로부터 안전하지 않습니다. 단일 스레드 또는 프로토타입 환경에서 사용할 수 있습니다. 프로덕션 환경에서 성능 및 스레드 보안을 개선하려면 `PredictionEnginePool` 서비스를 사용합니다. 이 서비스는 애플리케이션 전체에서 사용할 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602) 개체의 [`ObjectPool`](xref:Microsoft.Extensions.ObjectPool.ObjectPool%601)을 만듭니다. [ASP.NET Core 웹 API에서 `PredictionEnginePool`을 사용하는 방법](https://docs.microsoft.com/en-us/dotnet/machine-learning/how-to-guides/serve-model-web-api-ml-net#register-predictionenginepool-for-use-in-the-application)에 대한 자세한 내용은 이 가이드를 참조하세요.

    > [!NOTE]
    > `PredictionEnginePool` 서비스 확장은 현재 미리 보기 상태입니다.

1. 예측 결과를 `ClassifySingleImage()` 메서드의 다음 코드 줄로 표시합니다.

   [!code-csharp[DisplayPrediction](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayPrediction)]

## <a name="construct-the-mlnet-model-pipeline"></a>ML.NET 모델 파이프라인 생성

ML.NET 모델 파이프라인은 추정기의 체인입니다. 파이프라인 생성 중에는 실행이 발생하지 않습니다. 추정기 개체가 만들어졌지만 실행되지 않습니다.

1. 모델을 생성하는 메서드 추가

    이 메서드는 자습서의 핵심입니다. 모델에 대한 파이프라인을 만들고 파이프라인을 학습하여 ML.NET 모델을 생성합니다. 또한 확인되지 않은 이전 테스트 데이터를 기준으로 모델을 평가합니다.

    다음 코드를 사용하여 `InceptionSettings` 구조체 바로 뒤 및 `DisplayResults()` 메서드 바로 앞에 `GenerateModel()` 메서드를 만듭니다.

    ```csharp
    public static ITransformer GenerateModel(MLContext mlContext)
    {

    }
    ```

1. 추정기를 추가하여 이미지 데이터에서 픽셀을 로드하고, 크기를 조정하고, 추출합니다.

    [!code-csharp[ImageTransforms](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ImageTransforms)]

    이미지 데이터를 TensorFlow 모델에 필요한 형식으로 처리해야 합니다. 이 경우, 이미지는 메모리에 로드되고 일관된 크기로 조정되며 픽셀이 숫자 벡터로 추출됩니다.

1. 추정기를 추가하여 TensorFlow 모델을 로드하고 점수를 계산합니다.

    [!code-csharp[ScoreTensorFlowModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ScoreTensorFlowModel)]

    파이프라인의 이 단계는 TensorFlow 모델을 메모리로 로드한 다음, TensorFlow 모델 네트워크를 통해 픽셀 값의 벡터를 처리합니다. 심층 학습 모델에 입력을 적용하고 모델을 사용하여 출력을 생성하는 것을 **점수 매기기**라고 합니다. 모델을 전체적으로 사용하는 경우 점수를 매기기 위해 유추 또는 예측을 수행됩니다. 

    이 경우에는 유추를 수행하는 계층인 마지막 계층을 제외한 모든 TensorFlow 모델을 사용합니다. 마지막에서 두 번째 계층의 출력은 `softmax_2_preactivation`이 레이블로 지정됩니다. 이 계층의 출력은 사실상 원래 입력 이미지의 특징을 나타내는 기능 벡터입니다.

    TensorFlow 모델에서 생성된 이 기능 벡터는 ML.NET 학습 알고리즘에 대한 입력으로 사용됩니다.

1. 학습 데이터의 문자열 레이블을 정수 키 값에 매핑하는 추정기를 추가합니다.

    [!code-csharp[MapValueToKey](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#MapValueToKey)]

    다음에 추가된 ML.NET 트레이너에서는 해당 레이블이 임의 문자열이 아닌 `key` 형식 이어야 합니다. 키는 문자열 값에 일대일로 매핑되는 숫자입니다.

1. 다음과 같이 ML.NET 학습 알고리즘을 추가합니다.

    [!code-csharp[AddTrainer](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#AddTrainer)]

1. 예측 키 값을 문자열에 다시 매핑하는 추정기를 추가합니다.

    [!code-csharp[MapKeyToValue](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#MapKeyToValue)]

## <a name="train-the-model"></a>모델 학습

1. [LoadFromTextFile](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile(Microsoft.ML.DataOperationsCatalog,System.String,Microsoft.ML.Data.TextLoader.Options)) 래퍼를 사용하여 학습 데이터를 로드합니다. `GenerateModel()` 메서드에 아래 코드를 다음 줄로 추가합니다.

    [!code-csharp[LoadData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadData "Load the data")]

    ML.NET의 데이터는 [IDataView 클래스](xref:Microsoft.ML.IDataView)로 표시됩니다. `IDataView`는 표 형식 데이터(숫자 및 텍스트)를 유연하고 효율적으로 설명하는 방법입니다. 데이터를 텍스트 파일 또는 실시간(예: SQL 데이터베이스 또는 로그 파일)에서 `IDataView` 개체로 로드할 수 있습니다.

1. 위에 로드된 데이터로 모델을 학습시킵니다.

    [!code-csharp[TrainModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#TrainModel)]

    `Fit()` 메서드는 학습 데이터 세트를 파이프라인에 적용하여 모델을 학습시킵니다.

## <a name="evaluate-the-accuracy-of-the-model"></a>모델의 정확도 평가

1. `GenerateModel` 메서드의 다음 줄에 다음 코드를 추가하여 테스트 데이터를 로드하고 변환합니다.

    [!code-csharp[LoadAndTransformTestData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadAndTransformTestData "Load and transform test data")]

    모델을 평가하는 데 사용할 수 있는 몇 가지 샘플 이미지가 있습니다. 학습 데이터와 마찬가지로, 이러한 이미지도 모델에서 변환할 수 있도록 `IDataView`로 로드해야 합니다.
   
1. `GenerateModel()` 메서드에 다음 코드를 추가하여 모델을 평가합니다.

    [!code-csharp[Evaluate](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#Evaluate)]

    예측 세트가 있으면 [Evaluate()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A) 메서드가 다음을 수행합니다.

    * 모델을 평가합니다(예측 값을 테스트 데이터 세트 `labels`와 비교).
    * 모델 성능 메트릭을 반환합니다.

1. 모델 정확도 메트릭 표시

    다음 코드를 사용하여 메트릭을 표시하고, 결과를 공유한 다음, 작업을 수행합니다.

    [!code-csharp[DisplayMetrics](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayMetrics)]

    이미지 분류를 위해 다음 메트릭이 평가됩니다.

    * `Log-loss` - [로그 손실](../resources/glossary.md#log-loss)을 참조하세요. 로그 손실을 가능한 한 0에 가깝게 합니다.
    * `Per class Log-loss`. 클래스별 로그 손실을 가능한 한 0에 가깝게 합니다.

1. 다음 코드를 추가하여 학습된 모델을 다음 줄로 반환합니다.

    [!code-csharp[SaveModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ReturnModel)]

## <a name="run-the-application"></a>애플리케이션을 실행합니다.

1. MLContext 클래스를 만든 후 `Main` 메서드에서 `GenerateModel` 호출을 추가합니다.

    [!code-csharp[CallGenerateModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallGenerateModel)]

1. `ClassifySingleImage()` 메서드 호출을 `Main` 메서드의 다음 코드 줄로 추가합니다.

    [!code-csharp[CallClassifySingleImage](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallClassifySingleImage)]

1. 콘솔 앱을 실행합니다(Ctrl+F5). 다음 출력과 같은 결과가 나타나야 합니다.  경고 또는 처리 메시지가 표시될 수 있지만, 이해하기 쉽도록 이러한 메시지는 다음 결과에서 제거되었습니다.

    ```console
    =============== Training classification model ===============
    Image: broccoli.jpg predicted as: food with score: 0.976743
    Image: pizza.jpg predicted as: food with score: 0.9751652
    Image: pizza2.jpg predicted as: food with score: 0.9660203
    Image: teddy2.jpg predicted as: toy with score: 0.9748783
    Image: teddy3.jpg predicted as: toy with score: 0.9829691
    Image: teddy4.jpg predicted as: toy with score: 0.9868168
    Image: toaster.jpg predicted as: appliance with score: 0.9769174
    Image: toaster2.png predicted as: appliance with score: 0.9800823
    =============== Classification metrics ===============
    LogLoss is: 0.0228266745633507
    PerClassLogLoss is: 0.0277501705149937 , 0.0186303530571291 , 0.0217359128952187
    =============== Making single image classification ===============
    Image: toaster3.jpg predicted as: appliance with score: 0.9625379

    C:\Program Files\dotnet\dotnet.exe (process 4304) exited with code 0.
    Press any key to close this window . . .
    ```

지금까지 이제 ML.NET에서 `TensorFlow` 모델에 전이 학습을 적용하여 이미지 분류를 위한 기계 학습 모델을 성공적으로 빌드했습니다.

[dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> * 문제 이해
> * 미리 학습된 TensorFlow 모델을 ML.NET 파이프라인에 통합
> * ML.NET 모델 학습 및 평가
> * 테스트 이미지 분류

기계 학습 샘플 GitHub 리포지토리를 확인하여 확장된 이미지 분류 샘플을 살펴보세요.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-samples GitHub 리포지토리](https://github.com/dotnet/machinelearning-samples/)
