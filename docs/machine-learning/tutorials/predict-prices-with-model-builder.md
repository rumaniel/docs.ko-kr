---
title: '자습서: 모델 작성기와 함께 회귀를 사용하여 가격 예측'
description: 이 자습서에서는 ML.NET 모델 작성기를 사용하여 가격(특히, 뉴욕 시 택시 요금)을 예측하기 위한 회귀 모델을 빌드하는 방법에 대해 설명합니다.
author: luisquintanilla
ms.author: luquinta
ms.date: 10/08/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: a851bf3c405d15243bc1457b8c3dff815d072ebe
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180280"
---
# <a name="tutorial-predict-prices-using-regression-with-model-builder"></a>자습서: 모델 작성기와 함께 회귀를 사용하여 가격 예측

ML.NET 모델 작성기 빌드를 사용하여 가격을 예측하기 위한 회귀 모델을 빌드하는 방법을 알아봅니다.  이 자습서에서 개발하는 .NET 콘솔 앱은 뉴욕의 과거 택시 요금 데이터를 기반으로 택시 요금을 예측합니다.

모델 작성기 가격 예측 템플릿은 숫자 예측 값이 필요한 모든 시나리오에 사용할 수 있습니다. 예제 시나리오에는 집값 예측, 수요 예측 및 판매 예측 등이 있습니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> - 데이터 준비 및 이해
> - 시나리오 선택
> - 데이터 로드
> - 모델 학습
> - 모델 평가
> - 예측에 모델 사용

> [!NOTE]
> 모델 작성기는 현재 미리 보기로 제공됩니다.

## <a name="pre-requisites"></a>필수 구성 요소

필수 구성 요소 및 설치 지침 목록을 보려면 [모델 작성기 설치 가이드](../how-to-guides/install-model-builder.md)를 방문하세요.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

1. "TaxiFarePrediction"이라는 **.NET Core 콘솔 애플리케이션**을 만듭니다.

## <a name="prepare-and-understand-the-data"></a>데이터 준비 및 이해

1. 프로젝트에 *Data*라는 디렉터리를 만들어 데이터 세트 파일을 저장합니다.

1. 기계 학습 모델을 교육하고 평가하는 데 사용되는 데이터 세트는 원래 NYC TLC 택시 여행 데이터 세트에서 가져온 것입니다.

    1. 데이터 세트를 다운로드하려면 [taxi-fare-train.csv 다운로드 링크](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/taxi-fare-train.csv)로 이동합니다.

    1. 페이지가 로드되면 페이지의 아무 곳이나 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 저장**을 선택합니다.

    1. **다른 이름으로 저장 대화 상자**를 사용하여 이전 단계에서 만든 *Data* 폴더에 파일을 저장합니다.

1. **솔루션 탐색기**에서 *taxi-fare-train.csv* 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

`taxi-fare-train.csv` 데이터 세트의 각 행에는 택시에서 수행한 주행에 대한 세부 정보가 포함되어 있습니다.

1. **taxi-fare-train.csv** 데이터 세트 열기

    제공된 데이터 집합에는 다음과 같은 열이 포함되어 있습니다.

    - **vendor_id:** 택시 공급업체의 ID가 기능입니다.
    - **rate_code:** 택시 이동의 요금 유형이 기능입니다.
    - **passenger_count:** 이동하는 승객 수가 기능입니다.
    - **trip_time_in_secs:** 이동에 걸린 시간입니다. 이동을 완료하기 전에 이동 요금을 예측하려고 합니다. 해당 시간에는 이동이 얼마나 길지 알지 못합니다. 따라서 이동 시간은 기능이 아니며 모델에서 이 열을 제외합니다.
    - **trip_distance:** 이동 거리가 기능입니다.
    - **payment_type:** 결제 방법(현금 또는 신용 카드)이 기능입니다.
    - **fare_amount:** 지급한 총 택시 요금이 레이블입니다.

`label`은 예측할 열입니다. 회귀 작업을 수행할 때 목표는 숫자 값을 예측하는 것입니다. 이 가격 예측 시나리오에서는 택시 승차 비용이 예측됩니다. 따라서 **fare_amount**는 레이블입니다. 식별된 `features`는 `label` 예측을 위해 모델에 제공하는 입력입니다. 이 경우에 **trip_time_in_secs**를 제외한 나머지 열은 요금을 예측하는 기능 또는 입력으로 사용됩니다.

## <a name="choose-a-scenario"></a>시나리오 선택

모델을 학습하려면 모델 작성기에서 제공하는 사용 가능한 기계 학습 시나리오 목록에서 선택해야 합니다. 이 경우에 시나리오는 `Price Prediction`입니다.

1. **솔루션 탐색기**에서 *TaxiFarePrediction* 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Machine Learning**을 선택합니다.
1. 모델 작성기 도구의 시나리오 단계에서 *가격 예측* 시나리오를 선택합니다.

## <a name="load-the-data"></a>데이터 로드

모델 작성기는 SQL Server 데이터베이스 또는 로컬 파일 csv 또는 tsv 형식의 두 가지 소스에서 데이터를 허용합니다.

1. 모델 작성기 도구의 데이터 단계의 데이터 원본 드롭다운에서 *파일*을 선택합니다.
1. *파일 선택* 텍스트 상자 옆의 있는 단추를 선택하고 파일 탐색기를 사용하여 *Data* 디렉터리에서 *taxi-fare-test.csv*를 찾아서 선택합니다.
1. *예측할 열(레이블)* 드롭다운에서 *fare_amount*를 선택하고 모델 작성기 도구의 학습 단계로 이동합니다.
1. *입력 열(기능)*  드롭다운을 확장하고 *trip_time_in_secs* 열을 선택 취소하여 학습 동안 기능으로서 제외합니다.

## <a name="train-the-model"></a>모델 학습

이 자습서에서 가격 예측 모델을 학습하는 데 사용되는 기계 학습 작업은 회귀입니다. 모델 학습 프로세스 중에 모델 작성기는 다른 회귀 알고리즘 및 설정을 통해 개별 모델을 학습하여 데이터 세트에 가장 적합한 모델을 찾습니다.

모델을 학습하는 데 필요한 시간은 데이터 양에 비례합니다. 모델 작성기는 데이터 소스의 크기에 따라 **학습 시간(초)** 의 기본값을 자동으로 선택합니다.

1. 더 긴 학습 시간을 원하지 않는다면 *학습 시간(초)* 의 기본값을 그대로 둡니다.
2. *학습 시작*을 선택합니다.

학습 프로세스 전체에서 진행률 데이터는 학습 단계의 `Progress` 섹션에 표시됩니다.

- 상태는 학습 프로세스의 완료 상태를 표시합니다.
- 가장 높은 정확도는 모델 작성기가 현재까지 찾은 최고 성능 모델의 정확도를 표시합니다. 더 높은 정확도는 테스트 데이터에서 모델이 더 정확하게 예측된다는 것을 의미합니다.
- 최상의 알고리즘은 모델 작성기가 현재까지 찾은 최고 성능 알고리즘의 이름을 표시합니다.
- 마지막 알고리즘은 모델 작성기가 가장 최근에 학습하기 위해 사용한 알고리즘의 이름을 표시합니다.

학습이 완료되면 평가 단계로 이동합니다.

## <a name="evaluate-the-model"></a>모델 평가

학습 단계의 결과는 최상의 성능을 가진 하나의 모델이 됩니다. 모델 작성기 도구의 평가 단계인 출력 섹션에는 *최상의 모델* 항목에서 가장 성능이 좋은 모델에서 사용되는 알고리즘과 *최상의 모델 품질(RSquared)* 의 메트릭이 포함됩니다. 또한 상위 5개 모델 및 해당 메트릭을 포함하는 요약 테이블입니다.

정확도 메트릭에 만족하지 않는 경우 모델 정확도를 개선하기 위한 몇 가지 쉬운 방법은 모델을 학습하거나 더 많은 데이터를 사용하기 위한 시간을 늘리는 것입니다. 그렇지 않으면 코드 단계로 이동합니다.

## <a name="add-the-code-to-make-predictions"></a>코드를 추가하여 예측하기

학습 프로세스의 결과로 두 개의 프로젝트가 만들어질 수 있습니다.

- TaxiFarePredictionML.ConsoleApp: 모델 학습 및 샘플 소비 코드가 포함된 .NET Core 콘솔 애플리케이션입니다.
- TaxiFarePredictionML.Model: 입력 및 출력 모델 데이터의 스키마를 정의하는 데이터 모델, 학습 중 가장 성능이 뛰어난 모델의 저장된 버전, 예측을 위한 `ConsumeModel`이라는 도우미 클래스를 포함하는 .NET Standard 클래스 라이브러리입니다.

1. 모델 작성기 도구의 코드 단계에서 **프로젝트 추가**를 선택하여 자동 생성된 프로젝트를 솔루션에 추가합니다.
1. *TaxiFarePrediction* 프로젝트에서 *Program.cs* 파일을 엽니다.
1. *TaxiFarePredictionML.Model* 프로젝트를 참조하도록 다음 using 문을 추가합니다.

    ```csharp
    using System;
    using TaxiFarePredictionML.Model;
    ```

1. 모델을 사용하여 새 데이터에 대해 예측을 수행하려면 `Main` 메서드 내부에 `ModelInput` 클래스의 새 인스턴스를 만듭니다. 요금 금액은 입력에 포함되지 않습니다. 모델에서 해당 금액을 예측하기 때문입니다. 

    ```csharp
    // Create sample data
    ModelInput input = new ModelInput()
    {
        Vendor_id = "CMT",
        Rate_code = 1,
        Passenger_count = 1,
        Trip_distance = 3.8f,
        Payment_type = "CRD"
    };
    ```

1. `ConsumeModel` 클래스의 `Predict` 메서드를 사용합니다. `Predict` 메서드는 학습된 모델을 로드하고 모델에 대한 [`PredictionEngine`](xref:Microsoft.ML.PredictionEngine%602)을 만든 후 새 데이터에 대해 예측하는 데 사용합니다. 

    ```csharp
    // Make prediction
    ModelOutput prediction = ConsumeModel.Predict(input);

    // Print Prediction
    Console.WriteLine($"Predicted Fare: {prediction.Score}");
    Console.ReadKey();
    ```

1. 애플리케이션을 실행합니다.

    프로그램에서 생성된 출력은 아래 코드 조각과 유사해야 합니다.

    ```bash
    Predicted Fare: 14.96086
    ```

생성된 프로젝트를 나중에 다른 솔루션 내에서 참조해야 하는 경우 `C:\Users\%USERNAME%\AppData\Local\Temp\MLVSTools` 디렉터리 내에서 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
>
> - 데이터 준비 및 이해
> - 시나리오 선택
> - 데이터 로드
> - 모델 학습
> - 모델 평가
> - 예측에 모델 사용

### <a name="additional-resources"></a>추가 리소스

이 자습서에서 언급한 항목에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [모델 작성기 시나리오](../automate-training-with-model-builder.md#scenarios)
- [재발](../resources/glossary.md#regression)
- [회귀 모델 메트릭](../resources/metrics.md#metrics-for-regression)
- [NYC TLC 택시 여행 데이터 세트](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)
