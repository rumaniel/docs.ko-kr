---
title: 데이터 변환
description: ML.NET에서 지원되는 기능 엔지니어링 구성 요소를 탐색합니다.
author: natke
ms.author: nakersha
ms.date: 04/02/2019
ms.openlocfilehash: 25da3cceb3c9090661b34254ed240207aaf3b9d7
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929251"
---
# <a name="data-transformations"></a>데이터 변환

데이터 변환은 다음 작업에 사용됩니다.

- 모델 학습을 위한 데이터 준비
- TensorFlow 또는 ONNX 형식으로 가져온 모델 적용
- 모델을 통해 전달된 후 데이터 사후 처리

이 가이드의 변환은 [IEstimator](xref:Microsoft.ML.IEstimator%601) 인터페이스를 구현하는 클래스를 반환합니다. 데이터 변환은 함께 연결될 수 있습니다. 두 변환은 각각 연결된 참조 설명서에 지정된 특정 형식 및 형태의 데이터를 예측하고 생성합니다.

일부 데이터 변환의 경우 해당 매개 변수를 계산하려면 학습 데이터가 필요합니다. 예를 들어 <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> 변환기는 `Fit()` 작업 중에 학습 데이터의 평균 및 분산을 계산하고 해당 매개 변수를 `Transform()` 작업에서 사용합니다. 

다른 데이터 변환에는 학습 데이터가 필요하지 않습니다. 예를 들어 <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale*> 변환은 `Fit()` 작업 중에 학습 데이터를 확인하지 않고 `Transform()` 작업을 수행할 수 있습니다.

## <a name="column-mapping-and-grouping"></a>열 매핑 및 그룹화

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.TransformExtensionsCatalog.Concatenate%2A> | 새 출력 열에 하나 이상의 입력 열 연결 |
| <xref:Microsoft.ML.TransformExtensionsCatalog.CopyColumns%2A> | 하나 이상의 입력 열 복사 및 이름 바꾸기 |
| <xref:Microsoft.ML.TransformExtensionsCatalog.DropColumns%2A> | 하나 이상의 입력 열 삭제 |
| <xref:Microsoft.ML.TransformExtensionsCatalog.SelectColumns%2A> | 입력 데이터에서 유지할 하나 이상의 열 선택 |

## <a name="normalization-and-scaling"></a>정규화 및 크기 조정

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMeanVariance%2A> | 학습 데이터의 평균을 빼고 학습 데이터의 차이로 나누기 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLogMeanVariance%2A> | 학습 데이터의 로그를 기반으로 정규화 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeLpNorm%2A> | [lp-norm](https://en.wikipedia.org/wiki/Lp_space#The_p-norm_in_finite_dimensions)으로 입력 벡터 크기 조정. 여기서 p는 1, 2 또는 무한대입니다. 기본값 l2(유클리드 거리)로 설정 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeGlobalContrast%2A> | 행 데이터의 평균을 빼서 행에 있는 각 값의 크기를 조정하고, 표준 편차 또는 l2-norm(행 데이터)으로 나누고, 구성 가능한 배율(기본값 2) 곱하기 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning%2A> | bin 인덱스에 입력 값을 할당하고 bin 수로 나누어 0과 1 사이 float 값을 생성합니다. bin 경계는 여러 bin에 학습 데이터를 균등하게 분배하도록 계산됨 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeSupervisedBinning%2A> | 레이블 열에 대한 상관 관계에 따라 bin에 입력 값 할당 |
| <xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax%2A> | 학습 데이터에서 최솟값과 최댓값의 차이로 입력 크기 조정 |

## <a name="conversions-between-data-types"></a>데이터 형식 간 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.ConvertType%2A> | 입력 열 형식을 새 형식으로 변환 |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValue*> | 제공된 매핑 사전을 기반으로 키(범주)에 값 매핑 |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey*> | 입력 데이터에서 매핑을 만들어 키(범주)에 값 매핑 |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToValue*> | 키를 다시 원래 값으로 변환 |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapKeyToVector*> | 키를 다시 원래 값의 벡터로 변환 |
| <xref:Microsoft.ML.ConversionsCatalog.MapKeyToBinaryVector*> | 키를 다시 원래 값의 이진 벡터로 변환 |
| <xref:Microsoft.ML.ConversionsExtensionsCatalog.Hash*> | 입력 열에서 값 해시 |

## <a name="text-transformations"></a>텍스트 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.TextCatalog.FeaturizeText*> | 텍스트 열을 정규화된 ngrams 및 char-grams 수의 float 배열로 변환 | 
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoWords*> | 하나 이상의 텍스트 열을 개별 단어로 분할 |
| <xref:Microsoft.ML.TextCatalog.TokenizeIntoCharactersAsKeys*> | 토픽 세트에서 하나 이상의 텍스트 열을 개별 문자 float로 분할 |
| <xref:Microsoft.ML.TextCatalog.NormalizeText*> | 대/소문자 변경, 분음 부호, 문장 부호 및 숫자 제거 |
| <xref:Microsoft.ML.TextCatalog.ProduceNgrams*> | 텍스트 열을 ngrams 개수 모음(연속 단어의 시퀀스)으로 변환|
| <xref:Microsoft.ML.TextCatalog.ProduceWordBags*> | 텍스트 열을 ngrams 벡터 개수 모음으로 변환 |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedNgrams*> | 텍스트 열을 해시된 ngram 개수 벡터로 변환 |
| <xref:Microsoft.ML.TextCatalog.ProduceHashedWordBags*> | 텍스트 열을 해시된 ngram 개수 모음으로 변환 |
| <xref:Microsoft.ML.TextCatalog.RemoveDefaultStopWords*>  | 입력 열에서 지정된 언어의 기본 중지 단어 제거 |
| <xref:Microsoft.ML.TextCatalog.RemoveStopWords*> | 입력 열에서 지정된 중지 단어 제거 |
| <xref:Microsoft.ML.TextCatalog.LatentDirichletAllocation*> | 토픽 세트에서 문서(float 벡터로 표시됨)를 float 벡터로 변환 |
| <xref:Microsoft.ML.TextCatalog.ApplyWordEmbedding*> | 미리 학습된 모델을 사용하여 텍스트 토큰의 벡터를 문장 벡터로 변환 |

## <a name="image-transformations"></a>이미지 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToGrayscale*> | 이미지를 회색조로 변환 |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ConvertToImage*> | 픽셀의 벡터를 <xref:Microsoft.ML.Transforms.Image.ImageDataViewType>으로 변환 |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ExtractPixels*> | 입력 이미지의 벡터를 숫자의 벡터로 변환 |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.LoadImages*> | 폴더에서 메모리로 이미지 로드 |
| <xref:Microsoft.ML.ImageEstimatorsCatalog.ResizeImages*> | 이미지 크기 조정 |
| <xref:Microsoft.ML.OnnxCatalog.DnnFeaturizeImage*> | 미리 학습된 심층 신경망(DNN) 모델을 적용하여 입력 이미지를 기능 벡터로 변환 |

## <a name="categorical-data-transformations"></a>범주별 데이터 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*> | 하나 이상의 텍스트 열을 [원 핫(one-hot)](https://en.wikipedia.org/wiki/One-hot) 인코딩된 벡터로 변환 |
| <xref:Microsoft.ML.CategoricalCatalog.OneHotHashEncoding*> | 하나 이상의 텍스트 열을 해시 기반 원 핫(one-hot) 인코딩된 벡터로 변환 |

## <a name="time-series-data-transformations"></a>시계열 데이터 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectAnomalyBySrCnn*> | SR(Spectral Residual) 알고리즘을 사용하여 입력 시계열 데이터에서 변칙 검색 |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectChangePointBySsa*> | 단일 스펙트럼 분석(SSA)을 사용하여 시계열 데이터에서 변경점 검색 |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectIidChangePoint*> | 적응 커널 밀도 예측 및 마팅게일(martingale) 점수를 사용하여 개별적으로 동일하게 배포된(IID) 시계열 데이터에서 변경점 검색 |
| <xref:Microsoft.ML.TimeSeriesCatalog.ForecastBySsa*> | 단일 스펙트럼 분석(SSA)을 사용하여 시계열 데이터 예측 |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectSpikeBySsa*> | 단일 스펙트럼 분석(SSA)을 사용하여 시계열 데이터에서 급증 검색 |
| <xref:Microsoft.ML.TimeSeriesCatalog.DetectIidSpike*> | 적응 커널 밀도 예측 및 마팅게일(martingale) 점수를 사용하여 개별적으로 동일하게 배포된(IID) 시계열 데이터에서 급증 검색 |

## <a name="missing-values"></a>누락 값

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.ExtensionsCatalog.IndicateMissingValues*> | 새 부울 출력 열 만들기. 이 열의 값은 입력 열의 값이 누락된 경우 true입니다. |
| <xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*> | 새 출력 열 만들기. 이 열의 값은 입력 열에 값이 없는 경우 기본값으로 설정되고, 이외의 경우에는 해당 값으로 설정됩니다. |

## <a name="feature-selection"></a>기능 선택

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnCount*> | 기본값이 아닌 값이 임계값보다 큰 기능 선택 |
| <xref:Microsoft.ML.FeatureSelectionCatalog.SelectFeaturesBasedOnMutualInformation*> | 레이블 열의 데이터가 종속성이 가장 높은 기능 선택 |

## <a name="feature-transformations"></a>기능 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.KernelExpansionCatalog.ApproximatedKernelMap*> | 기능을 선형 알고리즘의 입력으로 사용할 수 있도록 내부 제품에서 커널 함수에 가까운 낮은 차원 기능 영역에 각 입력 벡터를 매핑 |
| <xref:Microsoft.ML.PcaCatalog.ProjectToPrincipalComponents*> | 보안 주체 구성 요소 분석 알고리즘을 적용하여 입력 기능 벡터의 차원 줄이기 |

## <a name="explainability-transformations"></a>설명 가능성 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.ExplainabilityCatalog.CalculateFeatureContribution*> | 기능 벡터의 각 요소에 대한 기여 점수 계산 |

## <a name="calibration-transformations"></a>보정 변환

| 변형 | 정의 |
| --- | --- |
|<xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Platt%28System.String%2CSystem.String%2CSystem.String%29> | 학습 데이터를 사용하여 추정한 매개 변수가 있는 로지스틱 회귀 분석을 사용하여 이진 분류자 원시 점수를 클래스 확률로 변환 |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Platt%28System.Double%2CSystem.Double%2CSystem.String%29> | 고정 매개 변수가 있는 로지스틱 회귀 분석을 사용하여 이진 분류자 원시 점수를 클래스 확률로 변환 |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Naive*> | Bin에 점수를 할당하고 bin 간 분포를 기준으로 확률을 계산하여 이진 분류자 원시 점수를 클래스 확률로 변환 |
| <xref:Microsoft.ML.BinaryClassificationCatalog.CalibratorsCatalog.Isotonic*> | 점수를 bin에 할당하여 이진 분류자 원시 점수를 클래스 확률로 변환합니다. 여기서 경계 위치와 bin 크기는 학습 데이터를 사용하여 추정함  |

## <a name="deep-learning-transformations"></a>딥 러닝 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.OnnxCatalog.ApplyOnnxModel*> | 가져온 ONNX 모델을 사용하여 입력 데이터 변환 |
| <xref:Microsoft.ML.TensorflowCatalog.LoadTensorFlowModel*> | 가져온 TensorFlow 모델을 사용하여 입력 데이터 변환 |

## <a name="custom-transformations"></a>사용자 지정 변환

| 변형 | 정의 |
| --- | --- |
| <xref:Microsoft.ML.CustomMappingCatalog.CustomMapping*> | 사용자 정의 매핑을 사용하여 기존 열을 새 열로 변환 |
