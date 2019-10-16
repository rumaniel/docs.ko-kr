---
title: 모델 작성기란 무엇이며 어떻게 작동하나요?
description: ML.NET 모델 작성기를 사용하여 기계 학습 모델을 자동으로 학습하는 방법
author: natke
ms.date: 08/07/2019
ms.custom: overview
ms.openlocfilehash: 77b5e75fede1a4aa93eadcf7e21591d82f565cab
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929478"
---
# <a name="what-is-model-builder-and-how-does-it-work"></a>모델 작성기란 무엇이며 어떻게 작동하나요?

ML.NET 모델 작성기는 사용자 지정 기계 학습 모델을 빌드, 학습 및 배포하기 위한 직관적인 그래픽 Visual Studio 확장 기능입니다.

모델 작성기는 AutoML(자동 기계 학습)을 사용하여 다양한 기계 학습 알고리즘과 설정을 탐색하여 시나리오에 가장 적합한 것을 찾아냅니다.

모델 작성기를 사용하기 위해 기계 학습 전문 지식이 필요하지 않습니다. 필요한 것은 약간의 데이터와 해결해야 할 문제뿐입니다. 모델 작성기는 .NET 애플리케이션에 모델을 추가하는 코드를 생성합니다.

![모델 작성기 Visual Studio 확장 사용자 인터페이스 애니메이션](media/ml-dotnet-model-builder.gif)

> [!NOTE]
> 모델 작성기는 현재 미리 보기로 제공됩니다.

## <a name="scenarios"></a>시나리오

애플리케이션에 대한 기계 학습 모델을 생성하기 위해 모델 작성기에 다양한 시나리오를 가져올 수 있습니다.

시나리오는 데이터를 사용하여 수행할 예측 유형에 대한 설명입니다. 예:

- 과거 판매 데이터를 기반으로 향후 제품 판매량 예측
- 고객 리뷰에 따라 감정을 긍정 또는 부정으로 분류
- 은행 트랜잭션이 사기인지 여부를 검색
- 고객 피드백 문제를 회사의 올바른 팀에 전달

## <a name="choose-a-model-type"></a>모델 형식을 선택합니다.

모델 작성기에서는 기계 학습 모델 형식을 선택해야 합니다. 모델 형식은 수행하려는 예측의 정렬에 따라 다릅니다.

숫자를 예측하는 시나리오의 경우 기계 학습 모델 형식을 `regression`이라고 합니다.

범주를 예측하는 시나리오의 경우 모델 형식은 `classification`입니다. 두 가지 형식의 분류가 있습니다.

- 두 개의 범주만 있는 경우: `binary classification`.
- 세 개 이상의 범주가 있는 경우: `multiclass classification`.

### <a name="which-model-type-is-right-for-me"></a>내게 적합한 모델 형식은 무엇인가요?

#### <a name="predict-a-category-when-there-are-only-two-categories"></a>범주 예측(두 개의 범주만 있는 경우)

이진 분류는 데이터를 두 범주(예/아니요, 통과/실패, 참/거짓 긍정/부정)로 분류하는 데 사용됩니다.

![사기 탐지, 위험 완화 및 애플리케이션 심사를 포함한 이진 분류의 예를 보여 주는 다이어그램](media/binary-classification-examples.png)

감정 분석은 고객 피드백에 대한 긍정 또는 부정 감정을 예측하는 데 사용될 수 있습니다. 이진 분류 모델 형식의 예입니다.

시나리오에서 두 범주로 분류해야 하는 경우, 이 템플릿을 사용자 고유의 데이터 세트와 함께 사용할 수 있습니다.

#### <a name="predict-a-category-when-there-are-three-or-more-categories"></a>범주 예측(세 개 이상의 범주가 있는 경우)

다중 클래스 분류는 데이터를 세 개 이상의 클래스로 분류하는 데 사용될 수 있습니다. 

![문서 및 제품 분류, 지원 티켓 라우팅 및 고객 이슈 우선 순위 지정을 포함한 다중 클래스 분류의 예](media/multiclass-classification-examples.png)

문제 분류는 문제 제목 및 설명을 사용하여 고객 피드백(예: GitHub) 문제를 분류하는 데 사용될 수 있습니다. 다중 클래스 분류 모델 형식의 예입니다.

데이터를 세 가지 이상의 범주로 분류하려는 경우 시나리오에 대한 문제 분류 템플릿을 사용할 수 있습니다.

#### <a name="predict-a-number"></a>숫자 예측

회귀는 숫자를 예측하는 데 사용됩니다.

![가격 예측, 매출 예측 및 예측 유지 관리와 같은 회귀 예를 보여 주는 다이어그램](media/regression-examples.png)

가격 예측은 집의 위치, 크기 및 기타 특성을 통해 집 가격을 예측하는 데 사용할 수 있습니다. 회귀 모델 형식의 예입니다.

사용자 고유의 데이터 세트를 사용하여 숫자 값을 예측하려는 경우 시나리오에 가격 예측 템플릿을 사용할 수 있습니다.

#### <a name="custom-scenario-choose-your-model-type"></a>사용자 지정 시나리오(모델 형식 선택)

사용자 지정 시나리오를 사용하여 모델 형식을 수동으로 선택할 수 있습니다.

## <a name="data"></a>데이터

모델 형식을 선택하면 모델 작성기에서 데이터 세트를 제공하라는 메시지가 표시됩니다. 이 데이터는 시나리오에 가장 적합한 모델을 학습, 평가 및 선택하는 데 사용됩니다.

![모델 작성기 단계를 보여 주는 다이어그램](media/model-builder-steps.png)

### <a name="choose-the-output-to-predict-label"></a>예측할 출력을 선택합니다(레이블).

데이터 세트는 학습 예제의 행과 특성 열을 나열한 표입니다. 각 행에는 다음이 있습니다.

- **레이블**(예측하려는 특성)
- **기능**(레이블을 예측하기 위한 입력으로 사용되는 특성).

주택 가격 예측 시나리오의 경우 다음과 같은 기능을 사용할 수 있습니다.

- 집의 평방 피트
- 침실과 욕실의 수
- 우편 번호

이 레이블은 평방 피트, 침실, 욕실 값 및 우편 번호 행에 대해 기록한 주택 가격입니다.

![크기 객실 우편 번호 및 가격 레이블로 구성된 기능을 갖춘 주택 가격 데이터의 행과 열을 보여주는 표](media/model-builder-data.png)

### <a name="example-datasets"></a>예제 데이터 세트

아직 사용자 고유의 데이터가 없는 경우 다음 데이터 세트 중 하나를 사용해 보세요.

|시나리오|모델 형식|데이터|레이블|기능|
|-|-|-|-|-|
|가격 예측|회귀|[택시 요금 데이터](https://github.com/dotnet/machinelearning-samples/blob/master/datasets/taxi-fare-train.csv)|요금|운행 시간, 거리|
|변칙 검색|이진 분류|[제품 판매 데이터](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)|제품 판매|월|
|정서 분석|이진 분류|[웹 사이트 주석 데이터](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)|레이블(부정적인 감정인 경우 0, 긍정적인 감정인 경우 1)|주석, 연도|
|부정 행위 감지|이진 분류|[신용 카드 데이터](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/BinaryClassification_CreditCardFraudDetection/CreditCardFraudDetection.Trainer/assets/input/creditcardfraud-dataset.zip)|클래스(사기일 경우 1, 그렇지 않으면 0)|수량, V1-V28(익명화된 기능)|
|텍스트 분류|다중 클래스 분류|[GitHub 문제 데이터](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/end-to-end-apps/MulticlassClassification-GitHubLabeler/GitHubLabeler/Data/corefx-issues-train.tsv)|영역|제목, 설명|

## <a name="train"></a>학습

시나리오, 데이터 및 레이블을 선택하면 모델 작성기가 모델을 학습합니다.

### <a name="what-is-training"></a>학습이란?

학습은 모델 작성기가 시나리오에 대한 질문에 대답하는 방법을 모델에 알려주는 자동 프로세스입니다. 학습하면 이전에 없었던 입력 데이터로 예측할 수 있습니다. 예를 들어 주택 가격을 예측하고 새 집이 시장에 나온다면 판매 가격을 예측할 수 있습니다.

모델 작성기는 AutoML(자동 기계학습)을 사용하기 때문에 학습 중에 입력하거나 튜닝할 필요가 없습니다.

## <a name="evaluate"></a>Evaluate

평가는 학습된 모델을 통해 새 테스트 데이터를 사용하여 예측한 다음, 예측이 얼마나 올바른지를 측정하는 프로세스입니다.

모델 작성기는 학습 데이터를 학습 집합과 테스트 집합으로 분할합니다. 학습 데이터(80%)는 모델을 학습하는 데 사용되며, 테스트 데이터(20%)는 모델을 평가하기 위해 보류됩니다. 모델 작성기는 메트릭을 사용하여 모델이 얼마나 효과적인지 측정합니다. 사용되는 특정 메트릭은 모델 형식에 따라 다릅니다. 자세한 내용은 [모델 평가 메트릭](resources/metrics.md)을 참조하세요.

## <a name="improve"></a>개선

모델 성능 점수가 원하는 만큼 좋지 않은 경우 다음을 수행할 수 있습니다.

- 더 긴 시간 동안 학습합니다. 시간이 지날수록 자동화된 기계 학습 엔진은 더 많은 알고리즘과 설정을 시도합니다.

- 더 많은 데이터를 추가합니다. 경우에 따라 데이터의 양이 고품질 기계 학습 모델을 학습하기에 충분하지 않을 수도 있습니다.

- 데이터의 균형을 유지합니다. 분류 작업의 경우 학습 집합이 범주 전반에 걸쳐 균형을 유지하는지 확인합니다. 예를 들어 100개의 학습 예제에 대한 네 개의 클래스가 있고, 90개의 레코드에 두 개의 첫 번째 클래스(tag1 및 tag2)가 사용되지만 다른 두 개 클래스(tag3 및 tag4)가 나머지 10개의 레코드에만 사용되는 경우 균형 있는 데이터가 부족하여 모델이 tag3 또는 tag4를 올바르게 예측하는 데 어려움을 겪을 수 있습니다.

## <a name="code"></a>코드

평가 단계 후 모델 작성기는 모델 파일 및 모델을 애플리케이션에 추가하는 데 사용할 수 있는 코드를 출력합니다. ML.NET 모델은 zip 파일로 저장됩니다. 모델을 로드하고 사용하는 코드는 솔루션에는 새 프로젝트로 추가됩니다. 또한 모델 작성기는 실행 중인 모델을 보기 위해 실행할 수 있는 샘플 콘솔 앱을 추가합니다.

또한 모델 작성기는 모델을 생성하는 데 사용되는 단계를 이해할 수 있도록 모델을 생성하는 코드를 출력합니다. 모델 학습 코드를 사용하여 새 데이터로 모델을 다시 학습할 수도 있습니다.

## <a name="whats-next"></a>새로운 기능

모델 작성기 Visual Studio 확장 [설치](how-to-guides/install-model-builder.md)

[가격 예측 또는 모든 회귀 시나리오](tutorials/predict-prices-with-model-builder.md) 시도
