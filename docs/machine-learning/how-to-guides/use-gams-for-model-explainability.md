---
title: 모델 설명을 위해 일반화된 추가 모델 및 도형 함수 사용
description: ML.NET에서 모델 설명을 위해 일반화된 추가 모델 및 형상 함수 사용
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: c58cf823007196c35da093fab7423c1e40ba1158
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855607"
---
# <a name="use-generalized-additive-models-and-shape-functions-for-model-explainability-in-mlnet"></a>ML.NET에서 모델 설명을 위해 일반화된 추가 모델 및 형상 함수 사용

> [!NOTE]
> 이 항목은 현재 미리 보기로 제공되는 ML.NET을 참조하며, 자료는 변경될 수 있습니다. 자세한 내용은 [ML.NET](https://dotnet.microsoft.com/apps/machinelearning-ai/ml-dotnet) 페이지를 참조하세요.

이 방법과 관련 샘플에서는 현재 **ML.NET 버전 0.10**을 사용하고 있습니다. 자세한 내용은 [dotnet/machinelearning GitHub 리포지토리](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)에서 릴리스 정보를 참조하세요.

기계 학습 모델을 만들 때는 예측을 수행하기에 부족한 경우가 많습니다. 기계 학습 개발자, 의사 결정자 및 모델의 영향을 받는 사람이 기계 학습 모델의 의사 결정 방법 및 성과에 도움이 되는 기능을 이해해야 합니다. **GAM(일반화된 추가 모델)** 은 기계 학습 개발자가 다른 사람이 쉽게 해석할 수 있는 고용량 모델을 만들 수 있도록 돕기 위해 Microsoft 내부에서 모델 설명에 사용됩니다.

GAM은 항이 단일 변수의 “형상 함수”라는 비선형 모델인 선형 모델을 나타내는 **해석 가능 모델** 클래스입니다. 선형 모델이므로 간단하게 해석되지만, 모델이 단일 가중치 대신 기능의 함수를 학습하기 때문에 단순 선형 모델보다 복잡한 관계를 모델링할 수 있습니다. 결과로 생성된 GAM 추정기에는 학습 세트에 대한 평균 예측을 나타내는 절편항과 평균 예측의 편차를 나타내는 형상 함수가 있습니다. 형상 함수는 기능의 다양한 값에 대한 모델의 응답을 확인하기 위해 눈으로 검사하고, 코드 예제의 끝에 생성된 다음 그래프처럼 시각화할 수 있습니다. ML.NET의 GAM 학습자는 비모수 형상 함수를 학습하기 위해 단순 그래디언트 부스팅 트리(예: 트리 스텀프)를 사용하여 구현되었으며, Lou, Caruana 및 Gehrke에 의해 [지능형 분류 및 회귀 모델](https://www.cs.cornell.edu/~yinlou/papers/lou-kdd12.pdf)에 설명된 방법을 기반으로 합니다.

```csharp
// Train the Generalized Additive Model
var fitPipeline = pipeline.Fit(data);
var gamModel = fitPipeline.LastTransformer.Model;

// The intercept for Generalize Additive Models represent the average prediction for the training data
var intercept = gamModel.Intercept;
Console.WriteLine($"Average predicted cost: {intercept:0.00}");

// Get the column names from the training set
var columnNames = data.Schema.AsEnumerable()
    .Select(column => column.Name) // Get the column names
    .Where(name => name != "MedianHomeValue") // Drop the Label
    .ToArray();

// Get the index of a variable from the training data
var myFeatureIndex = columnNames.ToList().FindIndex(str => str.Equals("MyFeature"));

// The shape functions represent the deviation from the average prediction as a function of the feature value
// It is represented by a discrete set of bins
// First, get the array of bin upper bounds from the model for this feature
var myFeatureBins = gamModel.GetBinUpperBounds(myFeatureIndex);
// Then get the array of bin weights; these are the effect size for each bin
var myFeatureWeights = gamModel.GetBinEffects(myFeatureIndex);

// Write out the shape function for the feature (see the following figure for what this looks like)
for (int i = 0; i < myFeatureBins.Length; i++)
{
    Console.WriteLine($"x < {myFeatureBins[i]:0.00} => {myFeatureWeights[i]:0.000}");
}
```

![일반화된 추가 모델 형상 함수 그래프](./media/use-gams-for-model-explainability/gam-shape-function-graph.png)

GAM 모델을 학습시키고 결과를 검사 및 해석하는 방법에 대한 샘플은 [dotnet/machinelearning GitHub 리포지토리](https://github.com/dotnet/machinelearning/blob/master/docs/samples/Microsoft.ML.Samples/Dynamic/GeneralizedAdditiveModels.cs)를 참조하세요.
