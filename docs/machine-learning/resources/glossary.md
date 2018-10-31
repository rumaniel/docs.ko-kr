---
title: 기계 학습 용어집
description: 기계 학습 용어집입니다.
ms.date: 05/31/2018
ms.topic: conceptual
ms.openlocfilehash: 22fcd4d2bdf53efd046cd594af42afe50a853f61
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453205"
---
# <a name="machine-learning-glossary"></a>기계 학습 용어집

다음 목록은 사용자 지정 모델을 빌드할 때 유용한 중요한 기계 학습 용어 모음입니다.

## <a name="accuracy"></a>정확도

[분류](#classification)에서 정확도는 올바르게 분류된 항목 수를 테스트 집합의 총 항목 수로 나눈 값입니다. 범위는 0(가장 덜 정확함)에서 -1(가장 정확함)까지입니다. 정확도는 모델 성능에 대한 평가 메트릭 중 하나입니다. [정밀도](#precision), [재현율](#recall) 및 [F 점수](#f-score)와 함께 고려합니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.Accuracy?displayProperty=nameWithType>.

## <a name="area-under-the-curve-auc"></a>AUC(Area Under the Curve)

[이진 분류](#binary-classification)에서 거짓 긍정 비율(x축)을 기준으로 참 긍정 비율(y축)을 표시하는 곡선 아래의 영역 값을 나타내는 평가 메트릭입니다. 범위는 0.5(최악)에서 1(최상)까지입니다. ROC 곡선(수신기 운용 특성 곡선) 아래 영역이라고도 합니다. 자세한 내용은 Wikipedia에서 [Receiver operating characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)(수신기 운영 특성) 문서를 참조하세요.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.Auc?displayProperty=nameWithType>.

## <a name="binary-classification"></a>이진 분류

[레이블](#label)이 두 클래스 중 하나에만 해당하는 [분류](#classification) 사례입니다. 자세한 내용은 [기계 학습 작업](tasks.md) 항목의 [이진 분류](tasks.md#binary-classification) 섹션을 참조하세요.

## <a name="classification"></a>분류

데이터가 범주를 예측하는 데 사용되는 경우 [감독된 기계 학습](#supervised-machine-learning) 작업을 분류라고 합니다. [이진 분류](#binary-classification)는 두 개의 범주만 예측하는 것을 나타냅니다(예: 이미지를 ‘고양이’ 또는 ‘개’의 그림으로 분류). [다중 클래스 분류](#multiclass-classification)는 여러 범주를 예측하는 것을 나타냅니다(예: 이미지를 개의 특정 품종 그림으로 분류하는 경우).

## <a name="coefficient-of-determination"></a>결정 계수

[회귀](#regression)에서 데이터가 모델에 얼마나 잘 맞는지를 나타내는 평가 메트릭입니다. 범위는 0에서 1까지입니다. 값 0은 데이터가 무작위이거나 모델에 맞지 않음을 의미합니다. 값 1은 모델이 데이터와 정확히 일치함을 의미합니다. 이를 r<sup>2</sup>, R<sup> 2</sup> 또는 r 제곱이라고 합니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.RegressionMetrics.RSquared?displayProperty=nameWithType>.

## <a name="feature"></a>기능

측정 중인 현상의 측정 가능한 속성입니다(일반적으로 숫자(double) 값). 다양한 기능을 **기능 벡터**라고 하며 일반적으로 `double[]`로 저장됩니다. 기능은 측정 중인 현상의 중요한 특성을 정의합니다. 자세한 내용은 Wikipedia에서 [Feature](https://en.wikipedia.org/wiki/Feature_(machine_learning))(기능) 문서를 참조하세요.

## <a name="feature-engineering"></a>기능 엔지니어링

기능 엔지니어링은 [기능](#feature) 집합을 정의하고 사용 가능한 현상 데이터에서 기능 벡터를 생성하는(기능 추출) 소프트웨어를 개발하는 프로세스입니다. 자세한 내용은 Wikipedia에서 [Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering)(기능 엔지니어링) 문서를 참조하세요.

## <a name="f-score"></a>F 점수

[분류](#classification)에서 [정밀도](#precision) 및 [재현율](#recall)을 균형을 맞추는 평가 메트릭입니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.F1Score?displayProperty=nameWithType>.

## <a name="hyperparameter"></a>하이퍼 매개 변수

기계 학습 알고리즘의 매개 변수입니다. 예로는 의사 결정 포리스트에서 학습할 트리 수 또는 그라데이션 하강 알고리즘의 단계 크기가 있습니다. ‘하이퍼 매개 변수’의 값은 모델 학습 전에 설정되고 예측 함수의 매개 변수(예: 의사 결정 트리의 비교 지점 또는 선형 회귀 모델의 가중치)를 찾는 프로세스를 관리합니다. 자세한 내용은 Wikipedia에서 [Hyperparameter](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning))(하이퍼 매개 변수) 문서를 참조하세요.

## <a name="label"></a>레이블

기계 학습 모델로 예측되는 요소입니다. 예를 들어 개의 품종 또는 미래 재고 가격이 있습니다.

## <a name="log-loss"></a>로그 손실

[분류](#classification)에서 분류자의 정확도를 분류하는 평가 메트릭입니다. 로그 손실이 작을수록 분류자의 정확도가 높아집니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.LogLoss?displayProperty=nameWithType>.

## <a name="mean-absolute-error-mae"></a>MAE(절대 평균 오차)

[회귀](#regression)에서 모든 모델 오차의 평균을 나타내는 평가 메트릭입니다. 여기서 모델 오차는 예측된 [레이블](#label) 값과 올바른 레이블 값 사이의 거리입니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.RegressionMetrics.L1?displayProperty=nameWithType>.

## <a name="model"></a>모델

일반적으로 예측 함수에 대한 매개 변수입니다. 예를 들어 선형 회귀 모델의 가중치 또는 의사 결정 트리의 분할 지점이 있습니다. ML.NET에서 모델에는 도메인 개체의 [레이블](#label)을 예측하는 데 필요한 모든 정보가 포함됩니다(예: 이미지 또는 텍스트). 이는 ML.NET 모델에 예측 함수의 매개 변수뿐만 아니라 필요한 기능화 단계가 포함됨을 의미합니다.

## <a name="multiclass-classification"></a>다중 클래스 분류

[레이블](#label)이 세 개 이상의 클래스 중 하나인 [분류](#classification) 사례입니다. 자세한 내용은 [다중 클래스 작업](tasks.md) 항목의 [이진 분류](tasks.md#multiclass-classification) 섹션을 참조하세요.

## <a name="n-gram"></a>N-gram

텍스트 데이터에 대한 기능 추출 체계: N 단어 시퀀스가 [기능](#feature) 값으로 바뀝니다.

## <a name="numerical-feature-vector"></a>숫자 기능 벡터

숫자 값만으로 구성된 [기능](#feature) 벡터입니다. 이는 `double[]`과 유사합니다.

## <a name="pipeline"></a>파이프라인

데이터 집합에 모델을 맞추는 데 필요한 모든 작업입니다. 파이프라인은 데이터 가져오기, 변환, 기능화 및 학습 단계로 구성됩니다. 파이프라인은 학습된 후 모델로 바뀝니다.

## <a name="precision"></a>전체 자릿수

[분류](#classification)에서 클래스의 정밀도는 해당 클래스에 속하는 것으로 올바르게 예측된 항목 수를 클래스에 속하는 것으로 예측된 총 항목 수로 나눈 값입니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.NegativePrecision?displayProperty=nameWithType>, <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.PositivePrecision?displayProperty=nameWithType>.

## <a name="recall"></a>재현율

[분류](#classification)에서 클래스의 재현율은 해당 클래스에 속하는 것으로 올바르게 예측된 항목 수를 실제로 클래스에 속하는 총 항목 수로 나눈 값입니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.NegativeRecall?displayProperty=nameWithType>, <xref:Microsoft.ML.Legacy.Models.BinaryClassificationMetrics.PositiveRecall?displayProperty=nameWithType>.

## <a name="regression"></a>재발

출력이 실제 값(예: double)인 [감독된 기계 학습](#supervised-machine-learning) 작업입니다. 예로는 재고 가격 예측이 있습니다. 자세한 내용은 [다중 클래스 작업](tasks.md) 항목의 [회귀](tasks.md#regression) 섹션을 참조하세요.

## <a name="relative-absolute-error"></a>상대 절대 오차

[회귀](#regression)에서 모든 절대 오차의 합계를 올바른 [레이블](#label) 값과 모든 올바른 레이블 값의 평균 간 거리의 합계로 나눈 값을 나타내는 평가 메트릭입니다.

## <a name="relative-squared-error"></a>상대 제곱 오차

[회귀](#regression)에서 모든 절대 제곱 오차의 합계를 올바른 [레이블](#label) 값과 모든 올바른 레이블 값의 평균 간 거리 제곱의 합계로 나눈 값을 나타내는 평가 메트릭입니다.

## <a name="root-of-mean-squared-error-rmse"></a>RMSE(평균 제곱 오차의 제곱근)

[회귀](#regression)에서 오차 제곱 평균의 제곱근인 평가 메트릭입니다.

관련 ML.NET API: <xref:Microsoft.ML.Legacy.Models.RegressionMetrics.Rms?displayProperty=nameWithType>.

## <a name="supervised-machine-learning"></a>감독된 기계 학습

원하는 모델이 아직 확인되지 않은 데이터에 대한 레이블을 예측하는 기계 학습의 서브클래스입니다. 예로는 분류, 회귀 및 구조화된 예측이 있습니다. 자세한 내용은 Wikipedia에서 [Supervised learning](https://en.wikipedia.org/wiki/Supervised_learning)(감독된 학습) 문서를 참조하세요.

## <a name="training"></a>학습

지정된 학습 데이터 집합에 대한 [모델](#model)을 식별하는 프로세스입니다. 선형 모델의 경우 가중치를 찾는 방법입니다. 트리의 경우 분할 지점을 식별하는 작업이 포함됩니다.

## <a name="transform"></a>변형

데이터를 변환하는 [파이프라인](#pipeline) 구성 요소입니다. 예를 들어 텍스트에서 숫자의 벡터까지입니다.

## <a name="unsupervised-machine-learning"></a>감독되지 않는 기계 학습

원하는 모델이 데이터에서 숨겨진(또는 잠재적) 구조를 찾는 기계 학습의 서브클래스입니다. 예로는 클러스터링, 항목 모델링 및 차원 감소가 있습니다. 자세한 내용은 Wikipedia에서 [Unsupervised learning](https://en.wikipedia.org/wiki/Unsupervised_learning)(감독되지 않는 학습) 문서를 참조하세요.
