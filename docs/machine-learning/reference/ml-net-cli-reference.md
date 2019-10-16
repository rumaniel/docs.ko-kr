---
title: ML.NET CLI 도구의 auto-train 명령
description: ML.NET CLI 도구의 auto-train 명령에 대한 개요, 샘플 및 참조입니다.
ms.date: 04/16/2019
ms.custom: ''
ms.openlocfilehash: 8363a16ab5e793e715131ac37283106517850439
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929196"
---
# <a name="the-auto-train-command-in-mlnet-cli"></a>ML.NET CLI의 'auto-train' 명령

> [!NOTE]
> 이 항목은 현재 미리 보기 중인 ML.NET CLI 및 ML.NET AutoML에 대해 다루며, 자료는 변경될 수 있습니다.

`auto-train` 명령은 ML.NET CLI 도구에서 제공하는 주 명령입니다. 이 명령을 사용하면 좋은 품질의 ML.NET 모델(연속된 모델 .zip 파일)과 해당 모델을 실행/채점할 예제 C# 코드를 생성할 수 있습니다. 또한, 사용자가 일반화된 “최적 모델”에 사용 중인 알고리즘과 설정을 살펴볼 수 있도록 해당 모델을 생성/학습할 C# 코드도 생성됩니다.

직접 코딩하지 않고 자체 데이터 세트에서 이러한 자산을 생성할 수 있으므로, 이미 ML.NET을 알고 있는 경우에도 생산성이 개선됩니다.

현재 ML.NET CLI에서 지원하는 ML 작업은 다음과 같습니다.

- `binary-classification`
- `multiclass-classification`
- `regression`

- 이후: 기타 기계 학습 작업, 예:
  - `recommendation`
  - `anomaly-detection`
  - `clustering`

명령 프롬프트에서 사용 예제:

```console
> mlnet auto-train --task regression --dataset "cars.csv" --label-column-name price
```

`mlnet auto-train` 명령은 다음 자산을 생성합니다.

- 사용 준비가 된 Serialize된 모델 .zip("최적 모델")
- 해당 생성된 모델을 실행/채점할 C# 코드(해당 모델으로 최종 사용자 앱에서 예측하기 위한)
- 해당 모델(학습 목적)을 생성하기 위해 사용한 학습 코드가 포함된 C# 코드

처음 두 개의 자산은 생성된 ML 모델로 예측을 수행하기 위해 최종 사용자 앱(ASP.NET Core 웹앱, 서비스, 데스크톱 앱 등)에서 직접 사용할 수 있습니다.

세 번째 자산 학습 코드는 생성된 모델을 학습하기 위해 CLI에서 사용한 ML.NET API 코드를 보여주므로, CLI 및 ML.NET AutoML 엔진에서 선택한 특정 트레이너/알고리즘과 하이퍼 매개 변수를 살펴볼 수 있습니다.

## <a name="the-auto-train-command-uses-the-automl-engine"></a>'auto-train' 명령은 AutoML 엔진을 사용합니다.

CLI는 ML.NET AutoML 엔진(NuGet 패키지)을 사용하여 아래 다이어그램에 표시된 대로 최적 품질 모델을 인텔리전트하게 검색합니다.

![이미지](./media/ml-net-automl-working-diagram.png "ML.NET CLI 내에서 작동하는 AutoML 엔진")

auto-train 명령으로 ML.NET CLI 도구를 실행하면 이 도구가 다양한 알고리즘과 구성 조합으로 많은 반복을 시도하는 것을 보게 됩니다.

## <a name="reference-for-auto-train-command"></a>'auto-train' 명령에 대한 참조

## <a name="examples"></a>예제

이진 분류 문제에 가장 간단한 CLI 명령(AutoML은 제공된 데이터에서 대부분의 구성을 추론해야 함):

```console
> mlnet auto-train --task binary-classification --dataset "customer-feedback.tsv" --label-column-name Sentiment
```

회귀 문제에 대한 다른 간단한 CLI 명령:

``` console
> mlnet auto-train --task regression --dataset "cars.csv" --label-column-name Price
```

학습 데이터 세트, 테스트 데이터 세트 및 추가 사용자 지정 명시적 인수로 이진 분류 모델을 만들고 학습합니다.

```console
> mlnet auto-train --task binary-classification --dataset "/MyDataSets/Population-Training.csv" --test-dataset "/MyDataSets/Population-Test.csv" --label-column-name "InsuranceRisk" --cache on --max-exploration-time 600
```

## <a name="name"></a>name

`mlnet auto-train` - 제공된 데이터 세트에 따라 여러 모델(‘n’ 반복)을 학습하고 최종적으로 최적 모델을 선택한 후 Serialize된 .zip 파일로 저장하고 채점 및 학습을 위해 관련된 C# 코드를 생성합니다.

## <a name="synopsis"></a>개요

```console
> mlnet auto-train

--task | --mltask | -T <value>

--dataset | -d <value>

[
 [--validation-dataset | -v <value>]
  --test-dataset | -t <value>
]

--label-column-name | -n <value>
|
--label-column-index | -i <value>

[--ignore-columns | -I <value>]

[--has-header | -h <value>]

[--max-exploration-time | -x <value>]

[--verbosity | -V <value>]

[--cache | -c <value>]

[--name | -N <value>]

[--output-path | -o <value>]

[--help | -h]

```

잘못된 입력 옵션을 사용할 경우 CLI 도구는 유효한 입력 목록과 해당 인수가 누락되었음을 설명하는 오류 메시지를 표시합니다(해당하는 경우).

## <a name="options"></a>옵션

 ----------------------------------------------------------

`--task | --mltask | -T`(문자열)

해결할 ML 문제를 제공하는 단일 문자열입니다. 예를 들어, 다음 작업 중 하나(CLI는 결과적으로 AutoML에서 지원되는 모든 작업을 지원함):

- `regression` - 숫자 값을 예측하기 위해 ML 모델을 사용할지 선택합니다.
- `binary-classification` - ML 모델 결과에 두 개의 가능한 범주 부울 값(0 또는 1)이 있는지 선택합니다.
- `multiclass-classification` - ML 모델 결과에 여러 개의 가능한 범주 값이 있는지 선택합니다.

이후 릴리스에서는 `recommendations`, `clustering` 및 `ranking` 등의 추가적인 ML 작업 및 시나리오가 지원됩니다.

 이 인수에는 단 하나의 ML 작업만 제공되어야 합니다.

 ----------------------------------------------------------

`--dataset | -d`(문자열)

이 인수는 다음 옵션 중 하나에 대한 파일 경로를 제공합니다.

- *A: 전체 데이터 세트 파일:* 이 옵션을 사용하고 사용자가 `--test-dataset` 및 `--validation-dataset`를 제공하지 않는다면 교차 유효성 검사(k-fold 등) 또는 자동화된 데이터 분할 접근법은 모델의 유효성 검사를 위해 내부적으로 사용됩니다. 이 경우에 사용자는 데이터 세트 파일 경로를 제공해야 합니다.

- *B: 학습 데이터 세트 파일:* 또한 사용자가 모델 유효성 검사에 데이터 세트를 제공하고 있다면(`--test-dataset` 및 옵션으로 `--validation-dataset`) `--dataset` 인수는 “학습 데이터 세트”만 있음을 의미합니다. 예를 들어, 모델 품질의 유효성을 검사하고 정확도 메트릭을 획득하기 위해 80% - 20% 접근법을 사용할 경우 “학습 데이터 세트”는 데이터의 80%, “테스트 데이터 세트”는 데이터의 20%를 차지하게 됩니다.

----------------------------------------------------------

`--test-dataset | -t`(문자열)

테스트 데이터 세트 파일을 가리키는 파일 경로(예: 정확도 메트릭을 획득하기 위해 정규 유효성 검사 수행 시 80% - 20% 접근법을 사용하는 경우)

`--test-dataset`를 사용한다면 `--dataset`도 필요합니다.

--유효성 검사-데이터 세트가 사용되지 않을 경우 `--test-dataset` 인수는 옵션입니다. 이 경우, 사용자는 세 개의 인수를 사용해야 합니다.

----------------------------------------------------------

`--validation-dataset | -v`(문자열)

유효성 검사 데이터 세트 파일을 가리키는 파일 경로입니다. 어떠한 경우에도 유효성 검사 데이터 세트는 옵션입니다.

`validation dataset`를 사용할 경우 동작은 다음과 같아야 합니다.

- `test-dataset` 및 `--dataset` 인수도 필요합니다.

- `validation-dataset` 데이터 세트는 모델 선택에 대한 예측 오류를 예상하기 위해 사용됩니다.

- `test-dataset`는 최종 선택된 모델의 일반화 오류를 평가하는 데 사용됩니다. 이상적으로, 테스트 세트는 “자격 증명 모음”에 보관되어야 하며 데이터 분석이 끝날 때만 꺼내야 합니다.

기본적으로 `validation dataset` 및 `test dataset`를 사용할 경우 유효성 검사 단계는 다음 두 부분으로 나뉩니다.

1. 첫 번째 부분에서는 모델을 살펴 보고 유효성 검사 데이터(=유효성 검사)를 사용하는 가장 효과적인 접근법을 선택합니다.
2. 그런 다음, 선택한 접근법의 정확도를 추정합니다(=테스트).

따라서 데이터는 80/10/10 또는 75/15/10으로 분리될 수 있습니다. 예:

- `training-dataset` 파일에는 데이터의 75%가 있어야 합니다.
- `validation-dataset` 파일에는 데이터의 15%가 있어야 합니다.
- `test-dataset` 파일에는 데이터의 10%가 있어야 합니다.

어떠한 경우에도 이러한 백분율은 이미 분할된 파일을 제공할 CLI를 사용하는 사용자가 결정합니다.

----------------------------------------------------------

`--label-column-name | -n`(문자열)

이 인수를 사용하면 특정 목표/대상 열(예측하려는 변수)은 데이터 세트의 헤더에서 지정된 열 이름을 사용하여 지정할 수 있습니다.

이 인수는 *분류 문제* 등의 감독된 ML 작업에만 사용됩니다. *클러스터링* 등의 감독되지 않은 ML 작업에는 사용할 수 없습니다.

----------------------------------------------------------

`--label-column-index | -i`(int)

이 인수를 사용하면 특정 목표/대상 열(예측하려는 변수)은 데이터 세트 파일에서 열의 숫자 인덱스(열 인덱스 값은 1에서 시작)를 사용하여 지정할 수 있습니다.

*참고:* 또한 사용자가 `--label-column-name`을 사용하고 있는 경우 `--label-column-name`도 사용되는 것입니다.

이 인수는 *분류 문제* 등의 감독된 ML 작업에만 사용됩니다. *클러스터링* 등의 감독되지 않은 ML 작업에는 사용할 수 없습니다.

----------------------------------------------------------

`--ignore-columns | -I`(문자열)

이 인수를 사용하면 훈련 프로세스에서 로드되어 사용되지 않도록 데이터 세트 파일에서 기존 열을 무시할 수 있습니다.

무시하려는 열 이름을 지정합니다. ', '(공백이 있는 쉼표) 또는 ' '(공백)을 사용하여 여러 열 이름을 구분합니다. 공백이 있는 열 이름에 큰따옴표를 사용할 수 있습니다(예: "logged in").

예제:

`--ignore-columns email, address, id, logged_in`

----------------------------------------------------------

`--has-header | -h`(bool)

데이터 세트 파일에 헤더 행이 있는지 지정합니다.
가능한 값은 다음과 같습니다.

- `true`
- `false`

사용자가 이 인수를 지정하지 않은 경우 기본 값은 `true`입니다.

`--label-column-name` 인수를 사용하려면 데이터 세트 파일에 헤더가 있고 `--has-header`가 `true`로 설정되어 있어야 합니다(기본값).

----------------------------------------------------------

`--max-exploration-time | -x`(문자열)

기본적으로, 최대 검색 시간은 30분입니다.

이 인수는 프로세스에서 여러 트레이너와 구성을 검색하는 최대 시간(초 단위)을 설정합니다. 단일 반복에 지정된 시간이 너무 짧을 경우(예를 들어 2초) 구성된 값이 초과될 수 있습니다. 이 경우에 실제 시간은 단일 반복에서 하나의 모델 구성을 생성하는 데 필요한 시간입니다.

반복에 필요한 시간은 데이터 세트의 크기에 따라 다를 수 있습니다.

----------------------------------------------------------

`--cache | -c`(문자열)

캐싱을 사용할 경우 전체 학습 데이터 세트는 메모리에 로드됩니다.

중소 규모의 데이터 세트의 경우, 캐시를 사용하면 학습 성능을 크게 개선할 수 있습니다. 즉, 캐시를 사용하지 않을 때보다 학습 시간을 단축할 수 있습니다.

단, 대규모 데이터 세트의 경우 메모리에 모든 데이터를 로드하면 메모리가 부족해져 좋지 않은 영향을 끼칠 수 있습니다. 대규모 데이터 세트 파일로 학습하고 캐시를 사용하지 않을 경우 ML.NET은 학습하는 동안 더 많은 데이터를 로드해야 할 때 드라이브에서 데이터 청크를 스트리밍하게 됩니다.

다음 값을 지정할 수 있습니다.

`on`: 학습 시 캐시를 사용하도록 강제 적용합니다.
`off`: 학습 시 캐시를 사용하지 않도록 강제 적용합니다.
`auto`: AutoML 추론에 따라 캐시는 사용되거나 사용되지 않습니다. 일반적으로, 중/소 규모의 데이터 세트는 캐시를 사용하고 대규모 데이터 세트는 사용자가 `auto` 선택을 사용할 경우 캐시를 사용하지 않습니다.

`--cache` 매개 변수를 지정하지 않는다면 캐시 `auto` 구성이 기본적으로 사용됩니다.

----------------------------------------------------------

`--name | -N`(문자열)

생성된 출력 프로젝트 또는 솔루션의 이름입니다. 지정된 이름이 없을 경우 `sample-{mltask}`이 사용됩니다.

ML.NET 모델 파일(.ZIP 파일)도 같은 이름을 갖게 됩니다.

----------------------------------------------------------

`--output-path | -o`(문자열)

생성된 출력을 저장할 루트 위치/폴더입니다. 기본값은 현재 디렉터리입니다.

----------------------------------------------------------

`--verbosity | -V`(문자열)

표준 출력의 자세한 정도를 설정합니다.

허용된 값은 다음과 같습니다.

- `q[uiet]`
- `m[inimal]`(기본값)
- `diag[nostic]`(로깅 정보 수준)

기본적으로, CLI 도구는 작동 중인지 그리고, 가능하면 남은 시간 또는 완료된 시간 비율을 언급하는 등, 일부 최소 피드백(최소)을 표시해야 합니다.

----------------------------------------------------------

`-h|--help`

각 명령의 매개 변수에 대한 설명과 함께 명령에 대한 도움말을 출력합니다.

----------------------------------------------------------

## <a name="see-also"></a>참고 항목

- [ML.NET CLI 도구 설치 방법](../how-to-guides/install-ml-net-cli.md)
- [ML.NET CLI로 모델 학습 자동화](../automate-training-with-cli.md)
- [자습서: ML.NET CLI를 사용하여 이진 분류자 자동 생성](../tutorials/mlnet-cli.md)
- [ML.NET CLI의 원격 분석](../resources/ml-net-cli-telemetry.md)
