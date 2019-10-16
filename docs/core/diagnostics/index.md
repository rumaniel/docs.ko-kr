---
title: 진단 도구 개요 - .NET Core
description: .NET Core 애플리케이션을 진단하는 데 사용할 수 있는 도구 및 기술에 대한 개요입니다.
author: sdmaclea
ms.author: stmaclea
ms.date: 10/14/2019
ms.topic: overview
ms.openlocfilehash: c0a45a1bfe866ad42890db576b5dd5098b1dbc3d
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318339"
---
# <a name="what-diagnostic-tools-are-available-in-net-core"></a>.NET Core에서 사용할 수 있는 진단 도구는 무엇인가요?

소프트웨어가 항상 예상한 대로 작동하지는 않지만 .NET Core에는 이러한 문제를 빠르고 효과적으로 진단할 수 있는 도구 및 API가 있습니다.

이 문서는 필요한 다양한 도구를 찾는 데 도움이 됩니다.

## <a name="managed-debuggers"></a>관리형 디버거

[관리형 디버거](managed-debuggers.md)를 사용하여 프로그램과 상호 작용할 수 있습니다. 일시 중지, 증분 실행, 검사 및 다시 시작은 코드 동작에 대한 인사이트를 제공합니다. 디버거는 쉽게 재현될 수 있는 기능 문제를 진단하는 데 사용되는 첫 번째 선택 옵션입니다.

## <a name="logging-and-tracing"></a>로깅 및 추적

[로깅 및 추적](logging-tracing.md)은 관련된 기술입니다. 계측 코드를 참조하여 로그 파일을 만듭니다. 파일에는 프로그램에서 수행하는 작업에 대한 세부 정보가 기록됩니다. 해당 세부 정보를 사용하여 가장 복잡한 문제를 진단할 수 있습니다. 타임스탬프와 결합할 경우 이러한 기술은 성능 조사에도 유용합니다.

## <a name="unit-testing"></a>단위 테스트

[유닛 테스트](../testing/index.md)는 고품질 소프트웨어의 연속 통합 및 배포를 위한 핵심 구성 요소입니다. 단위 테스트는 항목을 중단할 때 조기 경고를 제공하도록 설계되었습니다.

## <a name="net-core-dotnet-diagnostic-global-tools"></a>.NET Core dotnet 진단 전역 도구

### <a name="dotnet-counters"></a>dotnet-counters

[dotnet-counters](dotnet-counters.md)는 1단계 상태 모니터링 및 성능 조사를 위한 성능 모니터링 도구입니다. <xref:System.Diagnostics.Tracing.EventCounter>API를 통해 게시된 성능 카운터 값을 관찰합니다. 예를 들어 .NET Core 애플리케이션에서 throw되는 CPU 사용량 또는 예외 발생률과 같은 항목을 신속하게 모니터링할 수 있습니다.

### <a name="dotnet-dump"></a>dotnet-dump

[dotnet dump](dotnet-dump.md) 도구는 네이티브 디버거 없이 Windows 및 Linux 코어 덤프를 수집하 고 분석하는 방법입니다.

### <a name="dotnet-trace"></a>dotnet-trace

.NET Core에는 진단 데이터가 노출되는 `EventPipe`라고 하는 기능이 포함되어 있습니다. [dotnet-trace](dotnet-trace.md) 도구를 사용하면 앱에서 흥미로운 프로파일링 데이터를 사용하여 앱 속도가 느려지는 근본 원인이 되는 시나리오를 찾는 데 도움이 될 수 있습니다.
