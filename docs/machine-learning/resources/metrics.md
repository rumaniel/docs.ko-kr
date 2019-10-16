---
title: ML.NET 메트릭
description: ML.NET 모델의 성능을 평가하기 위해 사용한 메트릭 이해
ms.date: 04/29/2019
author: natke
ms.openlocfilehash: 45176902a195906e7b5cffd24fc9da839406ad9d
ms.sourcegitcommit: 52e588dc2ee74d484cd07ac60076be25cbf777ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67410525"
---
# <a name="model-evaluation-metrics-in-mlnet"></a>ML.NET에서 모델 평가 메트릭

## <a name="metrics-for-binary-classification"></a>이진 분류용 메트릭

| 메트릭   |      설명      |  살펴볼 항목 |
|-----------|-----------------------|-----------|
| **정확도(Accuracy)** |  [정확도](https://en.wikipedia.org/wiki/Accuracy_and_precision#In_binary_classification)는 테스트 데이터 세트 사용 시 올바른 예측의 비율입니다. 총 입력 샘플 수 대비 올바른 예측 수의 비율입니다. 각 클래스에 유사한 수의 샘플이 속해 있는 경우에만 제대로 작동합니다.| **1.00에 가까울 수록 좋습니다**. 하지만 정확하게 1.00은 문제(일반적으로 레이블/대상 누출, 오버피팅 또는 학습 데이터 테스트)를 나타냅니다. 테스트 데이터의 균형이 맞지 않은 경우(대부분 인스턴스가 클래스 중 하나에 속해 있는 경우) 데이터 세트가 아주 작거나 점수가 0.00 또는 1.00에 근접하면 정확도는 실제로 분류자의 유효성을 포착하지 못하므로 추가 메트릭을 확인해야 합니다. |
| **AUC** |    [aucROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) 또는 *곡선 아래의 영역*: 참 긍정 비율과 거짓 긍정 비율을 스윕하여 생성된 곡선 아래의 영역을 측정하는 것입니다.  |   **1.00에 가까울 수록 좋습니다**. 0\.50보다 큰 모델은 수용 가능하며 AUC가 0.50 또는 미만인 모델은 가치가 없습니다. |
| **AUCPR** | [aucPR](https://www.coursera.org/lecture/ml-classification/precision-recall-curve-rENu8) 또는 *정밀도-리콜 곡선의 아래의 영역*: 클래스의 균형이 매우 좋지 않을 때(상당히 기울어진 데이터 세트) 예측 성공에 대한 의미 있는 측정값입니다. |  **1.00에 가까울 수록 좋습니다**. 1\.00에 가까운 고득점은 분류자가 정확한 결과(높은 정밀도)를 반환할 뿐만 아니라 대다수가 모두 긍정 결과(높은 재현율)를 반환하고 있음을 보여줍니다. |
| **F1-점수(F1-score)** | *balanced F-score 또는 F-measure*라고도 하는 [F1 점수](https://en.wikipedia.org/wiki/F1_score)는 정밀도와 재현율의 조화 평균입니다. F1 점수는 정밀도(Precision)와 재현율(Recall) 간 균형을 찾으려고 할 때 유용합니다.| **1.00에 가까울 수록 좋습니다**.  F1 점수에서 가장 높은 값은 1.00이고 가장 낮은 점수는 0.00으로, 분류자의 정밀도를 알려줍니다. |

이진 분류 메트릭에 대한 자세한 내용은 다음 메트릭 문서를 참조하세요.

- [정확도, 정밀도, 재현율 또는 F1?](https://towardsdatascience.com/accuracy-precision-recall-or-f1-331fb37c5cb9)
- [이진 분류 메트릭 클래스](xref:Microsoft.ML.Data.BinaryClassificationMetrics)
- [정밀도-재현율과 ROC 곡선 간의 관계](http://pages.cs.wisc.edu/~jdavis/davisgoadrichcamera2.pdf)

## <a name="metrics-for-multi-class-classification"></a>다중 클래스 분류용 메트릭

| 메트릭   |      설명      |  살펴볼 항목 |
|-----------|-----------------------|-----------|
| **Micro-정확도** |  [Micro 평균 정확도](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.MicroAccuracy)는 모든 클래스의 기여도를 집계하여 평균 메트릭을 컴퓨팅합니다. 정확하게 예측된 인스턴스의 일부분으로서, Micro-평균은 클래스 멤버 자격을 고려하지 않습니다. 기본적으로, 모든 샘플-클래스 쌍은 정확도 메트릭에 동일기하게 기여합니다. | **1.00에 가까울 수록 좋습니다**. 다중 클래스 분류 작업에서는 클래스 불균형이 있을 것으로 의심되는 경우(예: 다른 클래스의 예보다 한 클래스의 예가 훨씬 많을 수 있음) Macro-정확도보다 Micro-정확도가 더 낫습니다.|
| **Macro-정확도** | [Macro-평균 정확도](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.MacroAccuracy)는 클래스 수준에서는 평균 정확도입니다. 각 클래스에 대한 정확도가 계산되고 Macro-정확도는 이러한 정확도의 평균입니다. 기본적으로, 모든 클래스는 정확도 메트릭에 동일하게 기여합니다. 소수 클래스는 큰 클래스와 같은 가중치를 부여받습니다. Macro-평균 메트릭은 데이터 세트에 포함된 클래스의 인스턴스 수가 얼마나 많던지 상관없이 각 클래스에 동일한 가중치를 부여합니다. |  **1.00에 가까울 수록 좋습니다**.  각 클래스에 대해 독립적으로 메트릭을 계산한 다음, 평균을 냅니다(따라서 모든 클래스를 동일하게 처리). |
| **로그 손실**| [로그 손실](http://wiki.fast.ai/index.php/Log_Loss)은 분류 모델의 성과를 측정합니다. 여기에서 예측 입력은 0.00과 1.00 사이의 확률 값입니다. 로그 손실은 예측된 확률이 실제 레이블에서 나뉘면서 증가합니다. | **0.00에 가까울 수록 좋습니다**. 완벽한 모델은 로그 손실이 0.00이 됩니다. 기계 학습 모델의 목표는 이 값을 최소화하는 것입니다.|
| **로그 손실 감소(Log-Loss Reduction)** | [로그 손실 감소](xref:Microsoft.ML.Data.MulticlassClassificationMetrics.LogLossReduction)는 임의 예측에 대한 분류자의 이점으로 해석할 수 있습니다.| **-inf ~1.00의 범위입니다. 여기서 1.00은 완벽한 예측이고 0.00은 평균 예측을 나타냅니다**. 예를 들어 값이 0.20이라면 “정확한 예측의 확률이 임의 추측보다 20% 나음”으로 해석할 수 있습니다.|

Micro-정확도는 일반적으로 ML 예측의 비즈니스 요구 사항과 더 잘 맞습니다. 다중 클래스 분류 작업의 품질을 선택하기 위해 단일 메트릭을 선택하려는 경우 일반적으로 micro-정확도여야 합니다.

예를 들어, 지원 티켓 분류 작업: (들어오는 티켓을 지원 팀에 매핑)

- Micro-정확도 - 들어오는 티켓이 올바른 팀으로 분류되는 빈도
- Macro-정확도 - 평균 팀의 경우 들어오는 티켓이 해당 팀에 정확한 빈도

Macro-정확도는 이 예에서 작은 팀에 가중치를 초과 부과합니다. 여기서 작은 팀은 매년 10개의 티켓을 받고, 큰 팀은 매년 1만 개의 티켓을 받습니다. 이 경우에 Micro-정확도는 “내 티켓 라우팅 프로세스를 자동화하여 회사가 절감할 수 있는 시간/비용 정도”라는 비즈니스 요구 사항과 상관 관계가 더 좋습니다.

다중 클래스 분류 메트릭에 대한 더 자세한 내용은 다음 문서를 참조하세요.

- [정밀도, 재현율 및 F 점수의 Micro-및 Macro-평균](http://rushdishams.blogspot.com/2011/08/micro-and-macro-average-of-precision.html)
- [불균형 데이터 세트를 사용한 다중 클래스 분류](https://towardsdatascience.com/machine-learning-multiclass-classification-with-imbalanced-data-set-29f6a177c1a)

## <a name="metrics-for-regression"></a>회귀용 메트릭

| 메트릭   |      설명      |  살펴볼 항목 |
|-----------|-----------------------|-----------|
| **R-제곱(R-Squared)** |  [R-제곱(R2)](https://en.wikipedia.org/wiki/Coefficient_of_determination) 또는 *결정 계수*는 -inf와 1.00 사이의 값으로 모델의 예측력을 나타냅니다. 1.00은 완벽한 적합도를 의미하며, 적합도는 임의적으로 나쁠 수 있으므로 점수는 음수가 될 수 있습니다. 점수 0.00은 모델이 레이블의 예상 값을 추측하고 있음을 의미합니다. R2는 실제 테스트 데이터 값이 예측 값에 근접한 정도를 측정합니다. | **1.00에 가까울 수록 품질이 좋습니다**. 단, 낮은 R-제곱 값(예: 0.50)이 사용자의 시나리오에 완전히 정상이거나 충분히 좋을 수 있으며 높은 R-제곱 값이 항상 좋고 의심스러운 것이 아닌 경우가 있습니다. |
| **절대-손실(Absolute-loss)** |  [절대 손실](https://en.wikipedia.org/wiki/Mean_absolute_error) 또는 *평균 절대 오차(MAE)* 는 예측이 실제 결과에 근접한 정도를 측정합니다. 모든 모델 오차의 평균이며, 여기서 모델 오차는 예측된 레이블 값과 올바른 레이블 값 사이의 절대 거리입니다. 이 예측 오차는 테스트 데이터 세트의 각 레코드에 대해 계산됩니다. 마지막으로, 평균 값은 모든 기록된 절대 오차에 대해 계산됩니다.| **0.00에 가까울 수록 품질이 좋습니다**. 절대 평균 오차는 측정 중인 데이터와 동일한 척도를 사용합니다(특정 범위로 정규화되지 않은). 절대-손실, 제곱근-손실 및 RMS 손실은 레이블 값 분산이 유사한 데이터 세트 또는 동일한 데이터 세트의 모델 간에 비교하기 위해서만 사용할 수 있습니다. |
| **제곱-손실(Squared-loss)** |  [제곱-손실](https://en.wikipedia.org/wiki/Mean_squared_error) 또는 *평균 제곱 오차(MSE)* (또는 *평균 제곱근 편차(MSD))* 는 회귀선이 테스트 데이터 값 세트와 근접한 정도를 알려줍니다. 점에서 회귀선까지의 거리(이러한 거리가 오차 E임)를 측정한 후 제곱하여 계산합니다. 제곱은 큰 차이에 더 많은 가중치를 부여합니다. | 항상 음수가 아니며 **값이 0.00에 가까울 수록 더 좋습니다**. 데이터에 따라 평균 제곱근 오차의 아주 작은 값을 가져오는 것이 불가능할 수 있습니다.|
| **RMS-손실(RMS-loss)** |  [RMS-손실](https://en.wikipedia.org/wiki/Root-mean-square_deviation) 또는 *평균 제곱 오차(Root Mean Square Error, RMSE)* (또는 *평균 제곱 편차(Root Mean Square Deviation, RMSD*))는 모델에서 예측한 값과 모델링하려는 환경에서 실제 관찰된 값 사이의 차이를 측정합니다. RMS-손실은 제곱 손실의 제곱근이며 큰 차이에 더 많은 가중치를 부여함으로써 절대-손실과 유사하게, 레이블과 단위가 동일합니다. 평균 제곱 오차는 실험적 결과를 검증하기 위해 일반적으로 기후학, 예측 및 회귀 분석에 사용됩니다. | 항상 음수가 아니며 **값이 0.00에 가까울 수록 더 좋습니다**. RMSD는 척도 종속적이므로, 데이터 세트 간이 아니라 특정 데이터 세트에 대해 다양한 모델의 예측 오차를 비교하기 위한 정확도 측도입니다.|

회귀 메트릭에 대한 자세한 내용은 다음 문서를 참조하세요.

- [회귀 분석: R-제곱을 해석하고 적합성(Goodness-of-Fit)을 평가하려면 어떻게 하나요?](https://blog.minitab.com/blog/adventures-in-statistics-2/regression-analysis-how-do-i-interpret-r-squared-and-assess-the-goodness-of-fit)
- [회귀 분석에서 R-제곱을 해석하는 방법](https://statisticsbyjim.com/regression/interpret-r-squared-regression)
- [R-제곱 정의](https://www.investopedia.com/terms/r/r-squared.asp)
- [평균 제곱 오차 정의](https://www.statisticshowto.datasciencecentral.com/mean-squared-error/)
- [평균 제곱 오차 및 평균 제곱근 오차의 정의](https://www.vernier.com/til/1014/)
