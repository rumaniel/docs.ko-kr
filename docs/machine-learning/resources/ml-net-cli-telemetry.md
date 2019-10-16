---
title: ML.NET CLI의 원격 분석 수집
description: 어떤 데이터가 수집되고 수집 기능을 사용하지 않도록 설정하는 방법에 대한 분석을 위해 사용 정보를 수집하는 ML.NET CLI 원격 분석 기능을 살펴봅니다. 또한 Microsoft의 GDPR 규정 준수에 대한 정보와 .NET 라이선스 링크를 확인합니다.
ms.topic: conceptual
ms.date: 09/03/2019
ms.custom: ''
ms.openlocfilehash: 77a24416a8008d36006c293cb174b5a8c2f516b7
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929276"
---
# <a name="telemetry-collection-by-the-mlnet-cli"></a>ML.NET CLI의 원격 분석 수집

[ML.NET CLI](https://aka.ms/mlnet-cli)는 Microsoft에서 사용하기 위해 집계한 익명 사용 데이터를 수집하는 원격 분석 기능을 포함합니다.

## <a name="how-microsoft-uses-the-data"></a>Microsoft가 데이터를 사용하는 방법

제품 팀에서는 ML.NET CLI 원격 분석 데이터를 사용하여 도구의 개선 방법을 이해할 수 있습니다. 예를 들어, 고객이 드물게 특정 기계 학습 작업을 사용할 경우 제품 팀은 그 원인을 조사하고 결과에 따라 기능 개발의 우선 순위를 정할 수 있습니다. ML.NET CLI 원격 분석 분석은 충돌, 코드 예외 같은 문제의 디버깅에도 도움이 됩니다. 

제품 팀은 이 인사이트가 중요하지만 모두가 이런 데이터를 보내고자 하는 것은 아닙니다. [원격 분석을 사용하지 않도록 설정하는 방법을 살펴봅니다.](#opt-out-of-data-collection)

## <a name="scope"></a>범위

`mlnet` 명령은 ML.NET CLI를 시작하지만 명령 자체는 원격 분석을 수집하지 않습니다.

연결된 명령 없이 `mlnet` 명령만 실행할 경우 원격 분석을 *사용할 수 없습니다*. 예:

- `mlnet`
- `mlnet --help`

`mlnet auto-train` 등, [ML.NET CLI 명령](../reference/ml-net-cli-reference.md)을 실행할 때는 원격 분석을 *사용합니다*.

## <a name="opt-out-of-data-collection"></a>데이터 수집 옵트아웃

ML.NET CLI 원격 분석 기능은 기본적으로 사용됩니다.

`MLDOTNET_CLI_TELEMETRY_OPTOUT` 환경 변수를 `1` 또는 `true`로 설정하여 원격 분석 기능을 옵트아웃(opt out)합니다. 이 환경 변수는 ML.NET CLI 도구에 전역적으로 적용됩니다.

## <a name="data-points-collected"></a>데이터 포인트 수집

이 기능은 다음 데이터를 수집합니다.

- `auto-train`과 같이 호출된 명령
- 사용된 명령줄 매개 변수 이름(예: "dataset-name, label-column-name, ml-task, output-path, max-exploration-time, verbosity")
- 해시된 MAC 주소: 컴퓨터에 대한 암호화된(SHA256) 익명 및 고유 ID입니다.
- 호출의 타임스탬프
- 지리적 위치 확인에만 사용되는 8진수 IP 주소 3개(전체 IP 주소 아님)
- 모든 인수/사용된 매개 변수 이름 문자열 등, 고객의 값이 아님
- 해시된 데이터 세트 파일 이름
- 데이터 세트 파일 크기 버킷
- 운영 체제 및 버전
- 작업 매개 변수의 값: 범주 값(예: `regression`, `binary-classification` 및 `multiclass-classification`)
- ML.NET CLI 버전(예: 0.3.27703.4)

데이터는 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 기술을 사용하여 Microsoft 서버로 안전하게 전송되고, 제한된 액세스를 기준으로 보관되고, 안전한 [Azure Storage](https://azure.microsoft.com/services/storage/) 시스템에서 엄격한 보안 제어에 따라 사용됩니다.

### <a name="data-points-not-collected"></a>데이터 포인트 수집 안 함
원격 분석 기능은 다음을 *수집하지 않습니다*.

- 사용자 이름 등의 개인 데이터
- 데이터 세트 파일 이름
- 데이터 세트 파일의 데이터

ML.NET CLI 원격 분석이 중요한 데이터를 수집하고 있는지 또는 데이터가 안전하지 않거나 부적절한 방식으로 처리되고 있는지 의심스러운 경우 조사를 위해 [ML.NET](https://github.com/dotnet/machinelearning) 리포지토리에서 문제를 보고하세요.

## <a name="license"></a>라이선스

ML.NET CLI의 Microsoft 배포는 [Microsoft 소프트웨어 사용 조건: Microsoft .NET 라이브러리](https://aka.ms/dotnet-core-eula)에 따라 라이선스가 부여됩니다. 데이터 수집 및 처리에 대한 자세한 내용은 "Data"라는 섹션을 참조하세요.

## <a name="disclosure"></a>공개

`mlnet auto-train` 같은 [ML.NET CLI 명령](../reference/ml-net-cli-reference.md)을 처음 실행하면 ML.NET CLI 도구가 원격 분석에서 옵트아웃하는 방법을 설명하는 공개 텍스트를 표시합니다. 실행 중인 CLI 버전에 따라 텍스트가 약간 달라질 수 있습니다.

## <a name="see-also"></a>참고 항목

- [ML.NET CLI 참조](../reference/ml-net-cli-reference.md)
- [Microsoft 소프트웨어 사용 조건: Microsoft .NET 라이브러리](https://aka.ms/dotnet-core-eula)
- [Microsoft 프라이버시](https://www.microsoft.com/trustcenter/privacy/)
- [Microsoft 개인정보처리방침](https://privacy.microsoft.com/privacystatement)
