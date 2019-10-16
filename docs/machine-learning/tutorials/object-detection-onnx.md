---
title: '자습서: ONNX 및 ML.NET를 통한 딥 러닝을 사용하여 개체 검색'
description: 이 자습서에서는 ML.NET에서 미리 학습된 ONNX 딥 러닝 학습 모델을 사용하여 이미지에서 개체를 검색하는 방법을 보여줍니다.
author: luisquintanilla
ms.author: luquinta
ms.date: 08/27/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 4856608e2c944c3a0fee65a328076bf1581f3d2a
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332631"
---
# <a name="tutorial-detect-objects-using-onnx-in-mlnet"></a>자습서: ML.NET에서 ONNX를 사용하여 개체 검색

ML.NET에서 미리 학습된 ONNX 모델을 사용하여 이미지에서 개체를 검색하는 방법을 알아봅니다.

개체 검색 모델을 처음부터 학습시키려면 수백만 개의 매개 변수, 다량의 레이블 지정 학습 데이터 및 많은 양의 컴퓨팅 리소스(수백 시간의 GPU 시간)를 설정해야 합니다. 미리 학습된 모델을 사용하면 학습 프로세스를 바로 수행할 수 있습니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> - 문제 이해
> - ONNX의 개념과 ML.NET에서 작동하는 방식에 대해 알아보기
> - 모델 이해
> - 미리 학습된 모델 다시 사용
> - 로드된 모델을 사용하여 개체 검색

## <a name="pre-requisites"></a>필수 구성 요소

- “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017).
- [Microsoft.ML NuGet 패키지](https://www.nuget.org/packages/Microsoft.ML/)
- [Microsoft.ML.ImageAnalytics NuGet 패키지](https://www.nuget.org/packages/Microsoft.ML.ImageAnalytics/)
- [Microsoft.ML.OnnxTransformer NuGet 패키지](https://www.nuget.org/packages/Microsoft.ML.OnnxTransformer/)
- [Tiny YOLOv2 미리 학습된 모델](https://github.com/onnx/models/tree/master/tiny_yolov2)
- [Netron](https://github.com/lutzroeder/netron)(선택 사항)

## <a name="onnx-object-detection-sample-overview"></a>ONNX 개체 검색 샘플 개요

이 샘플에서는 미리 학습된 딥 러닝 ONNX 모델을 사용하여 이미지 내에서 개체를 검색하는 .NET core 콘솔 애플리케이션을 만듭니다. 이 샘플의 코드는 GitHub의 [dotnet/machinelearning-samples repository](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx)에서 찾을 수 있습니다.

## <a name="what-is-object-detection"></a>개체 검색의 개념

개체 검색은 컴퓨터 비전 문제입니다. 개체 검색은 이미지 분류와 밀접하게 관련된 반면, 보다 세부적인 규모에서 이미지 분류를 수행합니다. 개체 검색에서는 이미지에서 엔터티 찾기 _및_ 분류를 둘 다 수행합니다. 이미지에 서로 다른 유형의 개체가 여러 개 포함되어 있는 경우 개체 검색을 사용합니다.

![왼쪽에는 한 강아지의 이미지 분류를 표시하고, 오른쪽에는 한 강아지의 그룹 개체 분류를 보여 주는 병렬 이미지](./media/object-detection-onnx/img-classification-obj-detection.PNG)

개체 검색의 몇 가지 사용 사례는 다음과 같습니다.

- 자동 주행 자동차
- Robotics
- 얼굴 감지
- 작업 영역 안전성
- 개체 수 계산
- 활동 인식

## <a name="select-a-deep-learning-model"></a>딥 러닝 모델 선택

딥 러닝은 기계 학습의 하위 집합입니다. 딥 러닝 모델을 학습시키려면 많은 양의 데이터가 필요합니다. 데이터의 패턴은 일련의 계층으로 표시됩니다. 데이터의 관계는 가중치를 포함하는 계층 간의 연결로 인코딩됩니다. 가중치가 높을수록 관계가 강해집니다. 이러한 일련의 계층 및 연결을 통칭하여 인공신경망이라고 합니다. 네트워크에 있는 계층이 많을수록 “심층 강화”되어, 심층 신경망으로 만듭니다.

신경망의 유형은 여러 가지가 있습니다. 가장 일반적으로 MLP(Multi-Layered Perceptron), CNN(Convolutional Neural Network) 및 RNN(Recurrent Neural Network)이 있습니다. 가장 기본적인 유형은 일련의 입력을 출력 집합에 매핑하는 MLP입니다. 이 신경망은 데이터에 공간 또는 시간 구성 요소가 없는 경우에 유용합니다. CNN은 나선형 계층을 사용하여 데이터에 포함된 공간 정보를 처리합니다. CNN의 좋은 사용 사례는 이미지의 영역에 기능이 있는지 검색하는 이미지 처리입니다(예: 이미지의 중심에 코가 있나요?). 마지막으로 RNN은 상태 또는 메모리의 지속성을 입력으로 사용할 수 있도록 허용합니다. RNN은 순차 순서와 이벤트 컨텍스트가 중요한 시계열 분석에 사용됩니다.

### <a name="understand-the-model"></a>모델 이해

개체 검색은 이미지 처리 작업입니다. 따라서 이 문제를 해결하도록 학습된 대부분의 딥 러닝 모델은 CNN입니다. 이 자습서에서 사용되는 모델은 백서에 설명된 YOLOv2 모델의 축소 버전인 Tiny YOLOv2 모델입니다. [“YOLO9000: Better, Faster, Stronger” by Redmon and Fadhari](https://arxiv.org/pdf/1612.08242.pdf). Tiny YOLOv2는 Pascal VOC 데이터 세트에서 학습되며 20개의 서로 다른 개체 클래스를 예측할 수 있는 15개의 계층으로 구성됩니다. Tiny YOLOv2는 소스 YOLOv2 모델의 축소된 버전이며, 속도와 정확도가 서로 절충됩니다. Netron과 같은 도구를 사용하여 모델을 구성하는 다양한 계층을 시각화할 수 있습니다. 모델을 검사하면 신경망을 구성하는 모든 계층 간에 연결 매핑이 일시 중단됩니다. 여기서 각 계층에는 각 입력/출력의 차원과 함께 계층 이름이 포함됩니다. 모델의 입력 및 출력을 설명하는 데 사용하는 데이터 구조를 텐서(tensor)라고 합니다. 텐서는 N 차원에 데이터를 저장하는 컨테이너로 간주할 수 있습니다. Tiny YOLOv2의 경우 입력 계층의 이름은 `image`이고 `3 x 416 x 416` 차원의 텐서가 있어야 합니다. 출력 계층의 이름은 `grid`이고 `125 x 13 x 13` 차원의 출력 텐서를 생성합니다.

![숨겨진 레이어로 분할되는 입력 계층을 표시한 후 출력 계층 표시](./media/object-detection-onnx/netron-model-map.png)

YOLO 모델에서는 `3(RGB) x 416px x 416px` 이미지를 사용합니다. 이 모델에서는 출력을 생성하기 위해 이 입력을 받아 다양한 계층에 전달합니다. 출력은 입력 이미지를 `13 x 13` 그리드로 나누며, 그리드의 각 셀은 `125` 값으로 구성됩니다.

### <a name="what-is-an-onnx-model"></a>ONNX 모델의 개념

ONNX(Open Neural Network Exchange)는 AI 모델의 오픈 소스 형식입니다. ONNX에서는 프레임워크 간의 상호 운용성을 지원합니다. 즉, PyTorch와 같이 널리 사용되는 여러 기계 학습 프레임워크 중 하나에서 모델을 학습시키고, ONNX 형식으로 변환하며, ML.NET과 같은 다른 프레임워크에서 ONNX 모델을 사용할 수 있습니다. 자세히 알아보려면 [ONNX 웹 사이트](https://onnx.ai/)를 방문하세요.

![ONNX 지원 형식을 ONNX로 가져온 다음, 다른 ONNX 지원 형식에서 사용](./media/object-detection-onnx/onnx-frameworks.png)

미리 학습된 Tiny YOLOv2 모델은 계층과 해당 계층의 학습된 패턴을 직렬화하여 표시하는 ONNX 형식으로 저장됩니다. ML.NET에서 ONNX와의 상호 운용성은 [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) 및 [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) NuGet 패키지를 통해 달성합니다. [`ImageAnalytics`](xref:Microsoft.ML.Transforms.Image) 패키지에는 이미지를 받아 예측이나 학습 파이프라인의 입력으로 사용할 수 있는 숫자 값으로 인코딩하는 일련의 변환이 포함되어 있습니다. [`OnnxTransformer`](xref:Microsoft.ML.Transforms.Onnx.OnnxTransformer) 패키지에서는 ONNX Runtime을 사용하여 ONNX 모델을 로드하고 제공된 입력을 기반으로 예측하는 데 사용합니다.

![ONNX 파일에서 ONNX 런타임으로, 마지막으로 C# 애플리케이션으로의 데이터 흐름 표시](./media/object-detection-onnx/onnx-ml-net-integration.png)

## <a name="set-up-the-net-core-project"></a>.NET Core 프로젝트 설정

이제 ONNX의 개념과 Tiny YOLOv2의 작동 원리를 대략적으로 파악했으므로 이제 애플리케이션을 빌드하겠습니다.

### <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

1. “ObjectDetection”이라는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

1. **Microsoft.ML NuGet 패키지**를 설치합니다.

    - 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.
    - 패키지 소스로 “nuget.org”를 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색합니다.
    - **설치** 단추를 선택합니다.
    - **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.
    - **Microsoft.ML.ImageAnalytics** 및 **Microsoft.ML.OnnxTransformer**에 대해 이 단계를 반복합니다.

### <a name="prepare-your-data-and-pre-trained-model"></a>데이터 및 미리 학습된 모델 준비

1. [프로젝트 자산 디렉터리 zip 파일](https://github.com/dotnet/machinelearning-samples/raw/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/assets.zip)을 다운로드하고 압축을 풉니다.

1. `assets` 디렉터리를 *ObjectDetection* 프로젝트 디렉터리에 복사합니다. 이 디렉터리 및 해당 하위 디렉터리에는 이 자습서에 필요한 이미지 파일이 포함되어 있습니다(다음 단계에서 다운로드 및 추가하는 Tiny YOLOv2 모델 제외).

1. [ONNX Model Zoo](https://github.com/onnx/models/tree/master/vision/object_detection_segmentation/tiny_yolov2)에서 [Tiny YOLOv2 모델](https://onnxzoo.blob.core.windows.net/models/opset_8/tiny_yolov2/tiny_yolov2.tar.gz)을 다운로드하고 압축을 풉니다.

    명령 프롬프트를 열고 다음 명령을 입력합니다.

    ```shell
    tar -xvzf tiny_yolov2.tar.gz
    ```

1. 방금 압축을 푼 디렉터리에서 *ObjectDetection* 프로젝트 `assets\Model` 디렉터리로 추출된 `model.onnx` 파일을 복사하고 이름을 `TinyYolo2_model.onnx`로 변경합니다. 이 디렉터리에는 이 자습서에 필요한 모델이 포함되어 있습니다.

1. 솔루션 탐색기에서 자산 디렉터리 및 하위 디렉터리의 각 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

*Program.cs* 파일을 열고 다음 추가 `using` 문을 파일의 맨 위에 추가합니다.

[!code-csharp [ProgramUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L1-L7)]

다음으로 다양한 자산의 경로를 정의합니다.

1. 먼저 `GetAbsolutePath` 메서드를 `Program` 클래스의 `Main` 메서드 아래 추가합니다.

    [!code-csharp [GetAbsolutePath](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L66-L74)]

1. 그런 다음, `Main` 메서드 내에서 자산의 위치를 저장하는 필드를 만듭니다.

    [!code-csharp [AssetDefinition](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L17-L21)]

프로젝트에 새 디렉터리를 추가하여 입력 데이터 및 예측 클래스를 저장합니다.

**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. 새 폴더가 솔루션 탐색기에 표시되면 이름을 “DataStructures”로 표시합니다.

새로 만든 *DataStructures* 디렉터리에 입력 데이터 클래스를 만듭니다.

1. **솔루션 탐색기**에서 *DataStructures* 디렉터리를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *ImageNetData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *ImageNetData.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *ImageNetData.cs*의 맨 위에 추가합니다.

    [!code-csharp [ImageNetDataUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetData.cs#L1-L4)]

    기존 클래스 정의를 제거하고 `ImageNetData` 클래스에 대한 다음 코드를 *ImageNetData.cs* 파일에 추가합니다.

    [!code-csharp [ImageNetDataClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetData.cs#L8-L23)]

    `ImageNetData`는 입력 이미지 데이터 클래스이며 다음 <xref:System.String> 필드를 포함합니다.

    - `ImagePath`에는 이미지가 저장되는 경로가 포함되어 있습니다.
    - `Label`에는 파일 이름이 포함되어 있습니다.

    또한 `ImageNetData`에는 지정된 `imageFolder` 경로에 저장된 여러 이미지 파일을 로드하여 `ImageNetData` 개체의 컬렉션으로 반환하는 `ReadFromFile` 메서드가 포함되어 있습니다.

*DataStructures* 디렉터리에 예측 클래스를 만듭니다.

1. **솔루션 탐색기**에서 *DataStructures* 디렉터리를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *ImageNetPrediction.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *ImageNetPrediction.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *ImageNetPrediction.cs*의 맨 위에 추가합니다.

    [!code-csharp [ImageNetPredictionUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetPrediction.cs#L1)]

    기존 클래스 정의를 제거하고 `ImageNetPrediction` 클래스에 대한 다음 코드를 *ImageNetPrediction.cs* 파일에 추가합니다.

    [!code-csharp [ImageNetPredictionClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/DataStructures/ImageNetPrediction.cs#L5-L9)]

    `ImageNetPrediction`은 예측 데이터 클래스이며 다음 `float[]` 필드를 포함합니다.

    - `PredictedLabel`에는 이미지에서 검색된 각 경계 상자의 크기, 개체 점수 및 클래스 확률이 포함되어 있습니다.

### <a name="initialize-variables-in-main"></a>Main에서 변수 초기화

[MLContext 클래스](xref:Microsoft.ML.MLContext)는 모든 ML.NET 작업의 시작점이며, `mlContext`를 초기화하면 모델 생성 워크플로 개체 간에 공유할 수 있는 새 ML.NET 환경이 생성됩니다. 개념적으로 Entity Framework의 `DBContext`와 유사합니다.

`outputFolder` 필드 아래 *Program.cs*의 `Main` 메서드에 다음 줄을 추가하여 `MLContext`의 새로운 인스턴스로 `mlContext` 변수를 초기화합니다.

[!code-csharp [InitMLContext](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L24)]

## <a name="create-a-parser-to-post-process-model-outputs"></a>파서를 만들어 모델 출력 후처리

모델은 이미지를 `13 x 13` 그리드로 나눕니다. 여기서 각 그리드 셀은 `32px x 32px`입니다. 각 그리드 셀에는 5개의 잠재적 개체 경계 상자가 포함되어 있습니다. 경계 상자에는 25개의 요소가 있습니다.

![왼쪽에 모눈 샘플, 오른쪽에 경계 상자 샘플 표시](./media/object-detection-onnx/model-output-description.png)

- `x` 연결된 그리드 셀을 기준으로 하는 경계 상자 중심의 x 위치입니다.
- `y` 연결된 그리드 셀을 기준으로 하는 경계 상자 중심의 y 위치입니다.
- `w` 경계 상자의 너비입니다.
- `h` 경계 상자의 높이입니다.
- `o` 경계 상자 내에 개체가 있는 신뢰도 값입니다(개체성 점수라고도 함).
- `p1-p20` 모델에서 예측하는 20개 클래스 각각의 클래스 확률입니다.

각각 5개의 경계 상자를 설명하는 총 25개의 요소는 각 그리드 셀에 포함된 125개의 요소를 구성합니다.

미리 학습된 ONNX 모델에서 생성한 출력은 `125 x 13 x 13` 크기의 텐서 요소를 나타내는 `21125` 길이의 부동 소수점 배열입니다. 모델에서 생성한 예측을 텐서로 변환하려면 몇 가지 후처리 작업이 필요합니다. 이렇게 하려면 출력을 구문 분석하는 데 도움이 되는 클래스 집합을 만드세요.

프로젝트에 새 디렉터리를 추가하여 파서 클래스 집합을 구성합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. 새 폴더가 솔루션 탐색기에 표시되면 이름을 “YoloParser”로 표시합니다.

### <a name="create-bounding-boxes-and-dimensions"></a>경계 상자 및 차원 만들기

모델의 데이터 출력에는 이미지 내 개체의 경계 상자에 대한 좌표와 크기가 포함됩니다. 차원의 기본 클래스를 만듭니다.

1. **솔루션 탐색기**에서 *YoloParser* 디렉터리를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *DimensionsBase.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *DimensionsBase.cs* 파일이 코드 편집기에서 열립니다. 모든 `using` 문과 기존 클래스 정의를 제거합니다.

    `DimensionsBase` 클래스의 다음 코드를 *DimensionsBase.cs* 파일에 추가합니다.

    [!code-csharp [DimensionsBaseClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/DimensionsBase.cs#L3-L9)]

    `DimensionsBase`에는 다음 `float` 필드가 있습니다.

    - `X`에는 x축의 개체 위치가 포함되어 있습니다.
    - `Y`에는 y축의 개체 위치가 포함되어 있습니다.
    - `Height`에는 개체의 높이가 포함되어 있습니다.
    - `Width`에는 개체의 너비가 포함되어 있습니다.

다음으로 경계 상자의 클래스를 만듭니다.

1. **솔루션 탐색기**에서 *YoloParser* 디렉터리를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *YoloBoundingBox.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *YoloBoundingBox.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *YoloBoundingBox.cs*의 맨 위에 추가합니다.

    [!code-csharp [YoloBoundingBoxUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L1)]

    각 경계 상자의 크기를 포함하도록 기존 클래스 정의 바로 위에 `DimensionsBase` 클래스에서 상속하는 `BoundingBoxDimensions`라는 새 클래스 정의를 추가합니다.

    [!code-csharp [BoundingBoxDimClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L5)]

    기존 `YoloBoundingBox` 클래스 정의를 제거하고 `YoloBoundingBox` 클래스의 다음 코드를 *YoloBoundingBox.cs* 파일에 추가합니다.

    [!code-csharp [YoloBoundingBoxClass](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloBoundingBox.cs#L7-L21)]

    `YoloBoundingBox`에는 다음 필드가 있습니다.

    - `Dimensions`에는 경계 상자의 크기가 포함되어 있습니다.
    - `Label`에는 경계 상자 내에서 검색된 개체의 클래스가 포함되어 있습니다.
    - `Confidence`에는 클래스의 신뢰도가 포함되어 있습니다.
    - `Rect`에는 경계 상자 크기의 사각형 표현이 포함되어 있습니다.
    - `BoxColor`에는 이미지를 그리는 데 사용되는 각 클래스와 관련된 색이 포함되어 있습니다.

### <a name="create-the-parser"></a>파서 만들기

이제 차원 및 경계 상자의 클래스가 생성되므로, 파서를 만들 때입니다.

1. **솔루션 탐색기**에서 *YoloParser* 디렉터리를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *YoloOutputParser.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *YoloOutputParser.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *YoloOutputParser.cs*의 맨 위에 추가합니다.

    [!code-csharp [YoloParserUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L1-L4)]

    기존 `YoloOutputParser` 클래스 정의 내에서 이미지에 있는 각 셀의 크기를 포함하는 중첩된 클래스를 추가합니다. `YoloOutputParser` 클래스 정의의 맨 위에 있는 `DimensionsBase` 클래스에서 상속하는 `CellDimensions` 클래스의 다음 코드를 추가합니다.

    [!code-csharp [YoloParserUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L10)]

1. `YoloOutputParser` 클래스 정의 내에 다음 상수와 필드를 추가합니다.

    [!code-csharp [ParserVarDefinitions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L12-L21)]

    - `ROW_COUNT`는 그리드에서 이미지가 나뉘는 행의 수입니다.
    - `COL_COUNT`는 그리드에서 이미지가 나뉘는 열의 수입니다.
    - `CHANNEL_COUNT`는 그리드의 한 셀에 포함된 총 값입니다.
    - `BOXES_PER_CELL`은 셀의 경계 상자 수이며,
    - `BOX_INFO_FEATURE_COUNT`는 상자에 포함된 기능 수입니다(x, y, 높이, 너비, 신뢰도).
    - `CLASS_COUNT`는 각 경계 상자에 포함된 클래스 예측 수입니다.
    - `CELL_WIDTH`는 이미지 그리드에 있는 한 셀의 너비입니다.
    - `CELL_HEIGHT`는 이미지 그리드에 있는 한 셀의 높이입니다.
    - `channelStride`는 그리드에서 현재 셀의 시작 위치입니다.

    모델은 점수라고도 하는 예측을 생성할 때 `416px x 416px` 입력 이미지를 `13 x 13` 크기의 셀 그리드로 나눕니다. 포함된 각 셀은 `32px x 32px`입니다. 각 셀에는 각각 5개의 기능(x, y, 너비, 높이, 신뢰도)을 포함하는 5개의 경계 상자가 있습니다. 또한 각 경계 상자에는 각 클래스의 확률이 포함되며, 이 경우에는 20입니다. 따라서 각 셀에는 125개의 정보(5개의 기능 + 20개의 클래스 확률)가 포함됩니다.

`channelStride` 아래에 5개의 경계 상자 모두에 대한 고정 목록을 만듭니다.

[!code-csharp [ParserAnchors](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L23-L26)]

앵커는 경계 상자의 미리 정의된 높이 및 너비 비율입니다. 모델에서 검색한 대부분의 개체 또는 클래스는 비율이 서로 비슷합니다. 따라서 경계 상자를 만들 때 유용합니다. 경계 상자를 예측하는 대신 미리 정의된 차원의 오프셋을 계산하므로 경계 상자를 예측하는 데 필요한 계산이 줄어듭니다. 일반적으로 이러한 고정 비율은 사용된 데이터 세트를 기반으로 계산합니다. 이 경우 데이터 세트가 알려져 있고 값이 미리 컴퓨팅되었기 때문에 앵커는 하드 코딩할 수 있습니다.

그런 다음 모델에서 예측할 레이블 또는 클래스를 정의합니다. 이 모델은 원래 YOLOv2 모델에서 예측한 총 클래스 수의 하위 집합인 20개의 클래스를 예측합니다.

`anchors` 아래에 레이블 목록을 추가합니다.

[!code-csharp [ParserLabels](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L28-L34)]

각 클래스와 관련된 색이 있습니다. `labels` 아래에 클래스 색을 할당합니다.

[!code-csharp [ParserColors](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L36-L59)]

### <a name="create-helper-functions"></a>도우미 함수 만들기

후처리 단계와 관련된 일련의 단계가 있습니다. 이를 지원하려면 몇 가지 도우미 메서드를 사용할 수 있습니다.

파서에서 사용하는 도우미 메서드는 다음과 같습니다.

- `Sigmoid`는 0에서 1 사이의 숫자를 출력하는 sigmoid 함수를 적용합니다.
- `Softmax`는 입력 벡터를 확률 분포로 정규화합니다.
- `GetOffset`은 1차원 모델 출력의 요소를 `125 x 13 x 13` 텐서의 해당 위치에 매핑합니다.
- `ExtractBoundingBoxes`는 모델 출력의 `GetOffset` 메서드를 사용하여 경계 상자 차원을 추출합니다.
- `GetConfidence`는 모델에서 개체를 발견한 확률을 나타내는 신뢰도 값을 추출하고 `Sigmoid` 함수를 사용하여 백분율로 전환합니다.
- `MapBoundingBoxToCell`은 경계 상자 차원을 사용하여 이미지 내의 해당 셀에 매핑합니다.
- `ExtractClasses`는 `GetOffset` 메서드를 사용하여 모델 출력에서 경계 상자의 클래스 예측을 추출한 다음 `Softmax` 메서드를 사용하여 확률 분포로 전환합니다.
- `GetTopResult`는 확률이 가장 높은 예측 클래스 목록에서 클래스를 선택합니다.
- `IntersectionOverUnion`은 낮은 확률의 겹치는 경계 상자를 필터링합니다.

모든 도우미 메서드 코드를 `classColors` 목록 아래 추가합니다.

[!code-csharp [ParserHelperMethods](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L61-L151)]

모든 도우미 메서드를 정의하고 나면 이제 이 메서드를 사용하여 모델 출력을 처리해야 합니다.

`IntersectionOverUnion` 메서드 아래에서 `ParseOutputs` 메서드를 만들어 모델에서 생성한 출력을 처리합니다.

```csharp
public IList<YoloBoundingBox> ParseOutputs(float[] yoloModelOutputs, float threshold = .3F)
{

}
```

목록을 만들어 경계 상자를 저장하고 `ParseOutputs` 메서드 내에 변수를 정의합니다.

[!code-csharp [BBoxList](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L155)]

각 이미지는 `13 x 13` 셀의 그리드로 나뉩니다. 각 셀에는 5개의 경계 상자가 포함되어 있습니다. `boxes` 변수 아래에 각 셀의 모든 상자를 처리하는 코드를 추가합니다.

```csharp
for (int row = 0; row < ROW_COUNT; row++)
{
    for (int column = 0; column < COL_COUNT; column++)
    {
        for (int box = 0; box < BOXES_PER_CELL; box++)
        {

        }
    }
}
```

1차원 모델 출력에서 현재 상자의 시작 위치를 가장 안쪽의 루프에서 계산합니다.

[!code-csharp [ChannelDef](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L163)]

바로 아래에서 `ExtractBoundingBoxDimensions` 메서드를 사용하여 현재 경계 상자의 크기를 가져옵니다.

[!code-csharp [GetBBoxDims](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L165)]

그런 다음 `GetConfidence` 메서드를 사용하여 현재 경계 상자의 신뢰도를 가져옵니다.

[!code-csharp [GetConfidence](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L167)]

그런 다음 `MapBoundingBoxToCell` 메서드를 사용하여 현재 경계 상자를 처리 중인 현재 셀에 매핑합니다.

[!code-csharp [MapBoundingBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L169)]

추가 처리를 수행하기 전에 신뢰도 값이 제공된 임계값보다 큰지 확인합니다. 그렇지 않은 경우 다음 경계 상자를 처리합니다.

[!code-csharp [CheckThreshold1](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L171-L172)]

그렇지 않으면 출력을 계속 처리합니다. 다음 단계에서는 `ExtractClasses` 메서드를 사용하여 현재 경계 상자에 대해 예측된 클래스의 확률 분포를 얻습니다.

[!code-csharp [ExtractClasses](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L174)]

그런 다음 `GetTopResult` 메서드를 사용하여 현재 상자의 확률이 가장 높은 클래스 값과 색인을 가져오고 해당 점수를 계산합니다.

[!code-csharp [GetTopResult](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L176-L177)]

`topScore`를 사용하여 지정된 임계값을 초과하는 경계 상자만 유지합니다.

[!code-csharp [CheckThreshold2](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L179-L180)]

마지막으로 현재 경계 상자가 임계값을 초과하는 경우 새 `BoundingBox` 개체를 만들어 `boxes` 목록에 추가합니다.

[!code-csharp [AddBBoxToList](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L182-L194)]

이미지의 모든 셀을 처리한 후 `boxes` 목록을 반환합니다. `ParseOutputs` 메서드의 가장 바깥쪽 for 루프 아래에 다음 return 문을 추가합니다.

[!code-csharp [ReturnBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L198)]

### <a name="filter-overlapping-boxes"></a>겹치는 상자 필터

모델 출력에서 신뢰도가 높은 모든 경계 상자를 추출했으므로 추가 필터링을 수행하여 겹치는 이미지를 제거해야 합니다. `ParseOutputs` 메서드 아래 `FilterBoundingBoxes`라는 메서드를 추가합니다.

```csharp
public IList<YoloBoundingBox> FilterBoundingBoxes(IList<YoloBoundingBox> boxes, int limit, float threshold)
{

}
```

`FilterBoundingBoxes` 메서드 내에서 검색된 상자의 크기와 같은 배열을 만들고 모든 슬롯을 활성 또는 처리할 준비 완료로 표시하여 시작합니다.

[!code-csharp [InitActiveSlots](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L203-L207)]

그런 다음, 경계 상자를 포함하는 목록을 신뢰도에 따라 내림차순으로 정렬합니다.

[!code-csharp [SortBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L209-L211)]

그런 다음 필터링된 결과를 저장할 목록을 만듭니다.

[!code-csharp [InitFilterResult](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L213)]

각 경계 상자를 반복하여 각 경계 상자에 대한 처리를 시작합니다.

```csharp
for (int i = 0; i < boxes.Count; i++)
{

}
```

이 for 루프 내에서 현재 경계 상자를 처리할 수 있는지 확인합니다.

```csharp
if (isActiveBoxes[i])
{

}
```

그런 경우 경계 상자를 결과 목록에 추가합니다. 결과가 추출할 상자의 지정된 한도를 초과하면 루프를 중단합니다. If-문 내에 다음 코드를 추가합니다.

[!code-csharp [AddFirstBBoxToResults](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L219-L223)]

처리할 수 없으면 인접한 경계 상자를 확인합니다. 상자 제한 검사 아래에 다음 코드를 추가합니다.

```csharp
for (var j = i + 1; j < boxes.Count; j++)
{

}
```

첫 번째 상자와 같이 인접한 상자가 활성 상태이거나 처리할 준비가 된 경우 `IntersectionOverUnion` 메서드를 사용하여 첫 번째 상자와 두 번째 상자가 지정된 임계값을 초과하는지 확인합니다. 가장 안쪽에 있는 for 루프에 다음 코드를 추가합니다.

[!code-csharp [IOUBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L227-L239)]

인접 경계 상자를 확인하는 가장 안쪽의 for 루프 외부에서 처리할 나머지 경계 상자가 있는지 확인합니다. 그렇지 않은 경우 외부 for 루프를 중단합니다.

[!code-csharp [CheckActiveSlots](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L242-L243)]

마지막으로 `FilterBoundingBoxes` 메서드의 초기 for 루프 외부에서 다음 결과를 반환합니다.

[!code-csharp [ReturnFilteredBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/YoloParser/YoloOutputParser.cs#L246)]

잘하셨습니다. 이제 채점을 위해 모델과 함께 이 코드를 사용합니다.

## <a name="use-the-model-for-scoring"></a>모델을 사용하여 채점

후처리와 마찬가지로 채점 단계에는 몇 가지 단계가 있습니다. 이 작업을 지원하기 위해 채점 로직을 포함하는 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.
1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *OnnxModelScorer.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *OnnxModelScorer.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *OnnxModelScorer.cs*의 위에 추가합니다.

    [!code-csharp [ScorerUsings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L1-L7)]

    `OnnxModelScorer` 클래스 정의에 다음 변수를 추가합니다.

    [!code-csharp [InitScorerVars](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L13-L17)]

    바로 아래에서 이전에 정의된 변수를 초기화할 `OnnxModelScorer` 클래스의 생성자를 만듭니다.

    [!code-csharp [ScorerCtor](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L19-L24)]

    생성자를 만들었으면 이미지 및 모델 설정과 관련된 변수를 포함하는 두 개의 구조체를 정의합니다. `ImageNetSettings`라는 구조체를 만들어 예상 높이와 너비를 모델의 입력으로 포함시킵니다.

    [!code-csharp [ImageNetSettingStruct](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L26-L30)]

    그런 다음 모델의 입력 및 출력 계층 이름을 포함하는 `TinyYoloModelSettings`라는 또 다른 구조체를 만듭니다. 모델의 입력 및 출력 계층 이름을 시각화하려면 [Netron](https://github.com/lutzroeder/netron)과 같은 도구를 사용할 수 있습니다.

    [!code-csharp [YoloSettingsStruct](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L32-L43)]

    다음으로 채점에 사용되는 첫 번째 메서드 집합을 만듭니다. `OnnxModelScorer` 클래스 내부에 `LoadModel` 메서드를 만듭니다.

    ```csharp
    private ITransformer LoadModel(string modelLocation)
    {

    }
    ```

    `LoadModel` 메서드 내에서 로깅을 위해 다음 코드를 추가합니다.

    [!code-csharp [LoadModelLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L47-L49)]

    ML.NET 파이프라인은 [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) 메서드가 호출될 때 작동할 데이터 스키마를 알아야 합니다. 이 경우 학습과 비슷한 프로세스가 사용됩니다. 그러나 실제 학습이 발생하지 않기 때문에 빈 [ `IDataView` ](xref:Microsoft.ML.IDataView)를 사용할 수 있습니다. 빈 목록에서 파이프라인의 새로운 [`IDataView`](xref:Microsoft.ML.IDataView)를 만듭니다.

    [!code-csharp [LoadEmptyIDV](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L52)]

    그런 다음 파이프라인을 정의합니다. 파이프라인은 4개의 변환으로 구성됩니다.

    - [`LoadImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages*)에서는 이미지를 비트맵으로 로드합니다.
    - [`ResizeImages`](xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages*)는 지정된 크기로 이미지의 크기를 조정합니다(이 경우 `416 x 416`).
    - [`ExtractPixels`](xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels*)는 이미지의 픽셀 표현을 비트맵에서 숫자 벡터로 변경합니다.
    - [`ApplyOnnxModel`](xref:Microsoft.ML.OnnxCatalog.ApplyOnnxModel*)는 ONNX 모델을 로드하고 제공된 데이터를 채점하는 데 사용합니다.

    `data` 변수 아래에 `LoadModel` 메서드의 파이프라인을 정의합니다.

    [!code-csharp [ScoringPipeline](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L55-L58)]

    이제 채점을 위해 모델을 인스턴스화해야 합니다. 파이프라인에서 [`Fit`](xref:Microsoft.ML.IEstimator%601.Fit*) 메서드를 호출하고 추가 처리를 위해 반환합니다.

    [!code-csharp [FitReturnModel](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L61-L63)]

모델을 로드한 후에는 모델을 사용하여 예측할 수 있습니다. 이 프로세스를 용이하게 하려면 `LoadModel` 메서드 아래 `PredictDataUsingModel`라는 메서드를 만듭니다.

```csharp
private IEnumerable<float[]> PredictDataUsingModel(IDataView testData, ITransformer model)
{

}
```

`PredictDataUsingModel`내에서 로깅을 위해 다음 코드를 추가합니다.

[!code-csharp [PredictDataLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L68-L71)]

그런 다음 [`Transform`](xref:Microsoft.ML.ITransformer.Transform*) 메서드를 사용하여 데이터를 채점합니다.

[!code-csharp [ScoreImages](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L73)]

예측된 확률을 추출하고 추가 처리를 위해 반환합니다.

[!code-csharp [ReturnModelOutput](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L75-L77)]

이제 두 단계가 모두 설정되었으므로 단일 메서드로 결합합니다. `PredictDataUsingModel` 메서드 아래 `Score`라는 새 메서드를 추가합니다.

[!code-csharp [ScoreMethod](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/OnnxModelScorer.cs#L80-L85)]

거의 완료되었습니다! 이제 모두 사용할 수 있습니다.

## <a name="detect-objects"></a>개체 검색

이제 모든 설치가 완료되었으므로 일부 개체를 검색해 보겠습니다. 먼저 *Program.cs* 클래스에서 채점자 및 파서에 대한 참조를 추가합니다.

[!code-csharp [ReferenceScorerParser](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L8-L9)]

### <a name="score-and-parse-model-outputs"></a>채점 및 구문 분석 모델 출력

*Program.cs* 클래스의 `Main` 메서드에서 try-catch 문을 추가합니다.

```csharp
try
{

}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

`try` 블록에서 개체 검색 로직을 구현하기 시작합니다. 먼저 데이터를 [`IDataView`](xref:Microsoft.ML.IDataView)에 로드합니다.

[!code-csharp [LoadData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L29-L30)]

그런 다음 `OnnxModelScorer`의 인스턴스를 만들고 이를 사용하여 로드된 데이터를 채점합니다.

[!code-csharp [ScoreData](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L33-L36)]

이제 후처리 단계가 진행됩니다. `YoloOutputParser`의 인스턴스를 만들고 이를 사용하여 모델 출력을 처리합니다.

[!code-csharp [ParsePredictions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L39-L44)]

모델 출력을 처리하고 나면 이미지에 경계 상자를 그릴 차례입니다.

### <a name="visualize-predictions"></a>예측 시각화

모델에서 이미지를 채점하고 출력이 처리되고 나면 이미지에 경계 상자를 그려야 합니다. 그렇게 하려면 `DrawBoundingBox` 메서드를 *Program.cs*의 `GetAbsolutePath` 메서드 아래 추가합니다.

```csharp
private static void DrawBoundingBox(string inputImageLocation, string outputImageLocation, string imageName, IList<YoloBoundingBox> filteredBoundingBoxes)
{

}
```

먼저 이미지를 로드하고 `DrawBoundingBox` 메서드에서 높이 및 너비 차원을 가져옵니다.

[!code-csharp [LoadImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L78-L81)]

그런 다음 모델에서 검색한 각 경계 상자를 반복하는 for-each 루프를 만듭니다.

```csharp
foreach (var box in filteredBoundingBoxes)
{

}
```

for-each 루프 내에서 경계 상자의 크기를 가져옵니다.

[!code-csharp [GetBBoxDimensions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L86-L89)]

경계 상자의 크기는 `416 x 416`의 모델 입력에 해당하므로 경계 상자 크기를 이미지의 실제 크기와 일치하도록 조정합니다.

[!code-csharp [ScaleImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L92-L95)]

그런 다음 각 경계 상자 위에 표시될 텍스트의 템플릿을 정의합니다. 텍스트에는 각 경계 상자 내의 개체 클래스와 신뢰도가 포함됩니다.

[!code-csharp [DefineBBoxText](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L98)]

이미지를 그리려면 [`Graphics`](xref:System.Drawing.Graphics) 개체로 변환하세요.

```csharp
using (Graphics thumbnailGraphic = Graphics.FromImage(image))
{

}
```

`using` 코드 블록에서 그래픽의 [`Graphics`](xref:System.Drawing.Graphics) 개체 설정을 조정합니다.

[!code-csharp [TuneGraphicSettings](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L102-L104)]

그런 다음 텍스트 및 경계 상자의 글꼴 및 색 옵션을 설정합니다.

[!code-csharp [SetColorOptions](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L106-L114)]

[`FillRectangle`](xref:System.Drawing.Graphics.FillRectangle*) 메서드를 사용하여 텍스트를 포함하도록 경계 상자 위에 직사각형을 만들어 채웁니다. 그러면 텍스트가 대비되어 가독성을 높이는 데 도움이 됩니다.

[!code-csharp [DrawTextBackground](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L117)]

그런 다음 [`DrawString`](xref:System.Drawing.Graphics.DrawString*) 및 [`DrawRectangle`](xref:System.Drawing.Graphics.DrawRectangle*) 메서드를 사용하여 이미지에 텍스트와 경계 상자를 그립니다.

[!code-csharp [DrawClassAndBBox](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L118-L121)]

for-each 루프 외부에서 `outputDirectory`에 이미지를 저장하는 코드를 추가합니다.

[!code-csharp [SaveImage](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L125-L130)]

런타임 시 애플리케이션이 예상대로 예측하는지에 대한 추가 피드백을 위해 `LogDetectedObjects` 메서드를 *Program.cs* 파일의 `DrawBoundingBox` 메서드 아래 추가하여 검색된 개체를 콘솔에 출력합니다.

[!code-csharp [LogOutputs](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L133-L143)]

이제 예측에서 시각적 피드백을 만드는 도우미 메서드가 있으므로 채점된 각 이미지를 반복하는 for 루프를 추가합니다.

```csharp
for (var i = 0; i < images.Count(); i++)
{

}
```

for 루프 내에서 이미지 파일의 이름과 연결된 경계 상자를 가져옵니다.

[!code-csharp [GetImageFileName](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L49-L50)]

그런 다음 `DrawBoundingBox` 메서드를 사용하여 이미지에 경계 상자를 그립니다.

[!code-csharp [DrawBBoxes](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L52)]

마지막으로 `LogDetectedObjects` 메서드를 사용하여 예측을 콘솔에 출력합니다.

[!code-csharp [LogPredictionsOutput](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L54)]

try-catch 문 다음에 프로세스 실행이 완료되었음을 나타내는 추가 로직을 추가합니다.

[!code-csharp [EndProcessLog](~/machinelearning-samples/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx/ObjectDetectionConsoleApp/Program.cs#L62-L63)]

정말 간단하죠.

## <a name="results"></a>결과

이전 단계를 수행한 후 콘솔 앱을 실행합니다(Ctrl+F5). 다음 출력과 같은 결과가 나타나야 합니다. 경고 또는 처리 메시지가 표시될 수 있지만, 이해하기 쉽도록 이러한 메시지는 다음 결과에서 제거되었습니다.

```console
=====Identify the objects in the images=====

.....The objects in the image image1.jpg are detected as below....
car and its Confidence score: 0.9697262
car and its Confidence score: 0.6674225
person and its Confidence score: 0.5226039
car and its Confidence score: 0.5224892
car and its Confidence score: 0.4675332

.....The objects in the image image2.jpg are detected as below....
cat and its Confidence score: 0.6461141
cat and its Confidence score: 0.6400049

.....The objects in the image image3.jpg are detected as below....
chair and its Confidence score: 0.840578
chair and its Confidence score: 0.796363
diningtable and its Confidence score: 0.6056048
diningtable and its Confidence score: 0.3737402

.....The objects in the image image4.jpg are detected as below....
dog and its Confidence score: 0.7608147
person and its Confidence score: 0.6321323
dog and its Confidence score: 0.5967442
person and its Confidence score: 0.5730394
person and its Confidence score: 0.5551759

========= End of Process..Hit any Key ========
```

경계 상자가 있는 이미지를 보려면 `assets/images/output/` 디렉터리로 이동합니다. 다음은 처리된 이미지 중 하나의 샘플입니다.

![처리된 거실 이미지 샘플](./media/object-detection-onnx/image3.jpg)

지금까지 이제 ML.NET에서 미리 학습된 `ONNX` 모델을 다시 사용하여 개체 검색을 위한 기계 학습 모델을 성공적으로 빌드했습니다.

[dotnet/samples](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/getting-started/DeepLearning_ObjectDetection_Onnx) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - 문제 이해
> - ONNX의 개념과 ML.NET에서 작동하는 방식에 대해 알아보기
> - 모델 이해
> - 미리 학습된 모델 다시 사용
> - 로드된 모델을 사용하여 개체 검색

기계 학습 샘플 GitHub 리포지토리를 확인하여 확장된 개체 검색 샘플을 살펴보세요.
> [!div class="nextstepaction"]
> [dotnet/machinelearning-samples GitHub 리포지토리](https://github.com/dotnet/machinelearning-samples/tree/master/samples/csharp/end-to-end-apps/DeepLearning_ObjectDetection_Onnx)
