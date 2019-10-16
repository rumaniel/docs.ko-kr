---
title: ML.NET 알고리즘을 선택하는 방법
description: 기계 학습 모델에 사용할 ML.NET 알고리즘을 선택하는 방법에 대해 살펴봅니다.
author: natke
ms.topic: overview
ms.date: 06/05/2019
ms.openlocfilehash: dfea21908258e6eb0b696de7affe1b03cff5cb3b
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972082"
---
# <a name="how-to-choose-an-mlnet-algorithm"></a>ML.NET 알고리즘을 선택하는 방법

각 [ML.NET 작업](resources/tasks.md)에는 선택할 수 있는 여러 학습 알고리즘이 있습니다. 선택할 알고리즘은 사용자가 해결하려고 하는 문제, 데이터 특징, 사용 가능한 컴퓨팅 및 스토리지 리소스에 따라 좌우됩니다. 기계 학습 모델을 학습하는 것은 반복적인 프로세스입니다. 가장 적합한 것을 찾기 위해 여러 알고리즘을 시도해봐야 합니다.

알고리즘은 **기능**에서 작동합니다. 기능은 입력 데이터에서 계산된 숫자 값으로, 기계 학습 알고리즘에 최적의 입력입니다. 하나 이상의 [데이터 변형](resources/transforms.md)을 사용하여 원시 입력 데이터를 기능을 변환합니다. 예를 들어, 텍스트 데이터는 단어 수와 단어 조합 수 세트로 변환됩니다. 데이터 변형을 사용하여 기능이 원시 데이터 형식에서 추출된 후에는 **기능화**되었다고 합니다. 기능화된 텍스트 또는 기능화된 이미지 데이터를 예로 들 수 있습니다.

## <a name="trainer--algorithm--task"></a>트레이너 = 알고리즘 + 작업

알고리즘은 **모델**을 생성하기 위해 실행하는 수학입니다. 다른 알고리즘은 다른 특징의 모델을 생성합니다. 

ML.NET을 사용하여 동일한 알고리즘을 다른 작업에 적용할 수 있습니다. 예를 들어 확률적 이중 좌표 상승법(Stochastic Descent Coordinated Ascent)을 이진 분류, 다중 클래스 분류 및 회귀에 사용할 수 있습니다. 차이점은 작업에 맞추기 위해 알고리즘의 출력이 해석되는 방식에 있습니다. 

각 알고리즘/작업 조합에 대해 ML.NET은 학습 알고리즘을 실행하고 해석을 수행하는 구성 요소를 제공합니다. 이러한 구성 요소를 트레이너라고 합니다. 예를 들어 <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer>는 **회귀** 작업에 적용된 **StochasticDualCoordinatedAscent** 알고리즘을 사용합니다.

## <a name="linear-algorithms"></a>선형 알고리즘

선형 알고리즘은 입력 데이터의 선형 조합과 **가중치** 세트로부터 **점수**를 계산하는 모델을 생성합니다. 가중치는 학습 중 추정된 모델의 매개 변수입니다.

선형 알고리즘은 [선형적으로 분리 가능한](https://en.wikipedia.org/wiki/Linear_separability) 기능에 잘 작동합니다.

선형 알고리즘으로 학습하기 전에 기능을 정규화해야 합니다. 이를 통해 하나의 기능이 다른 기능에 비해 결과에 더 많은 영향을 끼치지 않게 해줍니다.

일반적으로 선형 알고리즘은 확장 가능하고 빠르며 학습하기 쉽고 예측이 편리합니다. 기능의 수와 대략적으로 학습 데이터 세트의 크기로 규모가 조정됩니다.

선형 알고리즘은 학습 데이터에 여러 개의 통로를 만듭니다. 데이터 세트가 메모리에 적합할 경우 트레이너를 추가하기 전에 ML.NET 파이프라인에 [캐시 검사점](xref:Microsoft.ML.LearningPipelineExtensions.AppendCacheCheckpoint*)을 추가하면 학습을 보다 빨리 실행할 수 있습니다.

**선형 트레이너**

|알고리즘|속성|트레이너|
|---------|----------|--------|
|평균 퍼셉트론(Averaged perceptron)|텍스트 분류에 최적|<xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer>|
|확률적 이중 좌표 상승|좋은 기본 성능에는 튜닝이 필요하지 않음|<xref:Microsoft.ML.Trainers.SdcaLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedBinaryTrainer> <xref:Microsoft.ML.Trainers.SdcaMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaNonCalibratedMulticlassTrainer> <xref:Microsoft.ML.Trainers.SdcaRegressionTrainer>|
|L-BFGS|기능 수가 클 경우에 사용합니다. 로지스틱 회귀 학습 통계를 생성하지만 AveragedPerceptronTrainer처럼 규모 조정은 안 됩니다.|<xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer> <xref:Microsoft.ML.Trainers.LbfgsMaximumEntropyMulticlassTrainer> <xref:Microsoft.ML.Trainers.LbfgsPoissonRegressionTrainer>|
|기호 확률적 경사 하강법(Symbolic stochastic gradient descent)|가장 빠르고 가장 정확한 선형 이진 분류 트레이너입니다. 다수의 프로세서에 맞게 규모 조정이 가능합니다.|<xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer>|

## <a name="decision-tree-algorithms"></a>의사결정 트리 알고리즘

의사결정 트리 알고리즘은 일련의 의사결정을 포함한 모델을 생성합니다(데이터 값을 통해 효과적으로 흐름 차트).

이 유형의 알고리즘을 사용하기 위해 기능이 선형적으로 구분 가능해야 할 필요는 없습니다. 그리고 기능 벡터의 개별 값이 의사결정 프로세스에서 독립적으로 사용되므로 기능을 일반화할 필요가 없습니다.

의사결정 트리 알고리즘은 일반적으로 매우 정확합니다.

일반화 가법 모델(Generalized Additive Model, GAM)을 제외한 세 모델은 기능 수가 클 경우 설명 가능성이 부족할 수 있습니다.

의사결정 트리 알고리즘은 더 많은 리소스를 사용하며 선형 알고리즘처럼 규모 조정은 안 됩니다. 이 알고리즘은 메모리에 적합할 수 있는 데이터 세트에서 잘 작용합니다.

부스팅된 의사결정 트리는 작은 트리의 모음으로, 각 트리는 입력 데이터를 채점하고 더 나은 점수를 얻을 수 있도록 이 점수를 다음 트리에 계속 전달하며 모음의 각 트리는 이전 트리에서 개선됩니다.

**의사결정 트리 트레이너**

|알고리즘|속성|트레이너|
|---------|----------|--------|
|가벼운 경사 부스팅 머신(Light gradient boosted machine, LGBM)|이진 분류 트리 트레이너 중 가장 빠르고 정확하며 튜닝 성능이 뛰어납니다.|<xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmMulticlassTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRegressionTrainer> <xref:Microsoft.ML.Trainers.LightGbm.LightGbmRankingTrainer>|
|빠른 트리(Fast tree)|기능화된 이미지 데이터에 사용합니다. 불균형된 데이터에 유연하며 튜닝 성능이 뛰어납니다. | <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRegressionTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeTweedieTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastTreeRankingTrainer>|
|빠른 포레스트(Fast forest)|노이즈가 많은 데이터와 잘 작동합니다.|<xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.FastForestRegressionTrainer>|
|일반화된 가법 모델(Generalized additive model, GAM)|트리 알고리즘과 잘 작동하지만 설명 가능성이 우선인 문제에 최적입니다.|<xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer> <xref:Microsoft.ML.Trainers.FastTree.GamRegressionTrainer>|

## <a name="matrix-factorization"></a>행렬 인수 분해(Matrix factorization）

|속성|트레이너|
|----------|--------|
|데이터 세트가 큰 분산된 범주 데이터에 최적입니다.|<xref:Microsoft.ML.Trainers.FieldAwareFactorizationMachineTrainer>|

## <a name="meta-algorithms"></a>메타 알고리즘

이진 트레이너에서 다중 클래스 트레이너를 만드는 트레이너입니다. <xref:Microsoft.ML.Trainers.AveragedPerceptronTrainer>, <xref:Microsoft.ML.Trainers.LbfgsLogisticRegressionBinaryTrainer>, <xref:Microsoft.ML.Trainers.SymbolicSgdLogisticRegressionBinaryTrainer>, <xref:Microsoft.ML.Trainers.LightGbm.LightGbmBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.FastTreeBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.FastForestBinaryTrainer>, <xref:Microsoft.ML.Trainers.FastTree.GamBinaryTrainer>에 사용합니다.

|알고리즘|속성|트레이너|
|---------|----------|--------|
|One-Vs-One|이 다중 클래스 분류자는 각 클래스에 대해 하나의 이진 분류자를 학습하여 해당 클래스를 다른 모든 클래스와 구별합니다. 범주화할 클래스 수에 따라 규모 조정이 제한적입니다.|[OneVersusAllTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.OneVersusAllTrainer) |
|쌍별 결합(Pairwise coupling)|이 다중 클래스 분류자는 각 쌍의 클래스에서 이진 분류 알고리즘을 학습합니다. 두 클래스의 각 조합을 학습해야 하므로 클래스 수에 따라 규모 조정이 제한적입니다.|[PairwiseCouplingTrainer\<BinaryClassificationTrainer>](xref:Microsoft.ML.Trainers.PairwiseCouplingTrainer)|

## <a name="k-means"></a>K-평균(K-means)

|속성|트레이너|
|----------|--------|
|클러스터링에 사용|<xref:Microsoft.ML.Trainers.KMeansTrainer>|

## <a name="principal-component-analysis"></a>주성분 분석(Principal component analysis)

|속성|트레이너|
|----------|--------|
|변칙 검색에 사용|<xref:Microsoft.ML.Trainers.RandomizedPcaTrainer>|

## <a name="naive-bayes"></a>이브 베이즈(Naive Bayes)

|속성|트레이너|
|----------|--------|
|기능이 독립적이고 학습 데이터 세트가 작을 때 이 다중 클래스 분류 트레이너를 사용합니다.|<xref:Microsoft.ML.Trainers.NaiveBayesMulticlassTrainer>|

## <a name="prior-trainer"></a>사전 트레이너(Prior Trainer）

|속성|트레이너|
|----------|--------|
|다른 트레이너의 성과를 기준치로 삼기 위해 이 이진 분류 트레이너를 사용합니다. 효과를 발휘하려면 다른 트레이너의 메트릭이 사전 트레이너보다 더 좋아야 합니다. |<xref:Microsoft.ML.Trainers.PriorTrainer>|
