---
title: ML.NET 방법 가이드
description: 사용자 지정 AI 솔루션 생성 및 .NET 애플리케이션에 Machine Learning 통합을 지원하는 특정 작업을 수행하는 방법에 대해 알아보세요.
ms.custom: seodec18
ms.date: 03/01/2019
ms.openlocfilehash: c16adf6bf85aec1aef51751c6d4fe8c7f0f3c9f4
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645039"
---
# <a name="net-machine-learning-how-to-guides"></a>.NET 기계 학습 방법 가이드 

ML.NET 가이드의 방법 섹션에서 일반적인 질문에 대한 빠른 답변을 찾을 수 있습니다. 경우에 따라 문서를 쉽게 찾을 수 있도록 여러 섹션에 나타날 수 있습니다.

## <a name="load-the-data"></a>데이터 로드

* [기계 학습 처리를 위해 CSV 파일에서 많은 열을 포함하는 데이터를 로드합니다.](load-data-from-mult-column-csv-ml-net.md)

* [기계 학습 처리를 위해 여러 파일에서 데이터를 로드합니다.](load-data-from-multiple-files-ml-net.md)

* [기계 학습 처리를 위해 텍스트 파일에서 데이터를 로드합니다.](load-data-from-text-file-ml-net.md)

### <a name="prepare-the-data"></a>데이터 준비

* [데이터 처리에 사용할 학습 데이터를 노멀라이저로 전처리합니다.](normalizers-preprocess-data-ml-net.md)

## <a name="train-the-model"></a>모델 학습

* [텍스트 파일에 포함되지 않은 데이터를 사용하여 기계 학습 모델을 학습합니다.](load-non-file-training-data-ml-net.md)

* [교차 유효성 검사를 사용하여 기계 학습 모델을 학습합니다.](train-cross-validation-ml-net.md)

* [ML.NET을 사용해서 회귀 모델을 학습하여 값을 예측합니다.](train-regression-model-ml-net.md)

### <a name="evaluate-the-model-quality"></a>모델 품질 평가

* [메트릭을 계산하여 모델 품질을 평가합니다.](verify-model-quality-ml-net.md)

### <a name="model-explainability"></a>모델 설명 가능성

* [순열 기능 중요도를 사용하여 모델의 기능 중요도를 판별합니다.](determine-global-feature-importance-in-model.md)

* [모델 설명을 위해 일반화된 추가 모델 및 도형 함수를 사용합니다.](use-gams-for-model-explainability.md)

### <a name="feature-engineering"></a>기능 엔지니어링

* [범주 데이터에 모델 학습용 기능 엔지니어링을 적용합니다.](train-model-categorical-ml-net.md)

* [ML.NET을 사용하여 텍스트 데이터에 모델 학습용 기능 엔지니어링을 적용합니다.](train-model-textual-ml-net.md)

## <a name="run"></a>실행

* [ML.NET 파이프라인을 처리하는 동안 중간 데이터 값을 검사합니다.](inspect-intermediate-data-ml-net.md)

* [앱에서 학습된 기계 학습 모델을 운용합니다.](consuming-model-ml-net.md)

* [PredictionFunction을 사용하여 한 번에 하나씩 예측을 수행합니다.](single-predict-model-ml-net.md)

## <a name="probabilistic-infernet"></a>확률(Infer.NET)

* [Infer.NET 및 확률적 프로그래밍을 사용하여 게임 대전 목록 앱을 만듭니다.](matchup-app-infer-net.md)
