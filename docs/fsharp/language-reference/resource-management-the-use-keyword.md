---
title: '리소스 관리: Use 키워드'
description: 리소스의 초기화 F# 및 해제를 제어할 수 있는 ' use ' 키워드 및 ' using ' 함수에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 5e0838401bee02050343b2f6dcc646a8dc8b4dc0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68627263"
---
# <a name="resource-management-the-use-keyword"></a>리소스 관리: Use 키워드

이 항목에서는 리소스의 `use` 초기화 및 `using` 해제를 제어할 수 있는 키워드 및 함수에 대해 설명 합니다.

## <a name="resources"></a>리소스

*리소스* 라는 용어는 여러 가지 방법으로 사용 됩니다. 예, 리소스는 응용 프로그램에서 사용 하는 데이터 (예: 문자열, 그래픽 등) 일 수 있지만,이 컨텍스트에서 *리소스* 는 그래픽 장치 컨텍스트, 파일 핸들, 네트워크, 데이터베이스 등의 소프트웨어 또는 운영 체제 리소스를 참조 합니다. 연결, 대기 핸들 등의 동시성 개체 등이 있습니다. 응용 프로그램에서 이러한 리소스를 사용 하는 경우 다른 응용 프로그램에 제공 될 수 있도록 운영 체제 또는 다른 리소스 공급자의 리소스를 획득 한 다음 나중에 해당 리소스를 풀에 릴리스 해야 합니다. 응용 프로그램에서 리소스를 공용 풀로 다시 해제 하지 않을 때 문제가 발생 합니다.

## <a name="managing-resources"></a>리소스 관리

응용 프로그램에서 리소스를 효율적이 고 체계적으로 관리 하려면 예측 가능한 방식으로 리소스를 즉시 해제 해야 합니다. .NET Framework는 인터페이스를 `System.IDisposable` 제공 하 여이 작업을 수행 하는 데 도움이 됩니다. 을 구현 `System.IDisposable` 하는 형식에 `System.IDisposable.Dispose` 는 리소스가 올바르게 해제 되는 메서드가 있습니다. 잘 작성 된 응용 프로그램은 `System.IDisposable.Dispose` 제한 된 리소스를 보유 하는 개체가 더 이상 필요 하지 않을 때 즉시 호출 되도록 보장 합니다. 다행히 대부분의 .NET 언어는이를 용이 하 게 하는 F# 지원을 제공 하며, 예외는 아닙니다. Dispose 패턴 `use` 을 지 원하는 두 가지 유용한 언어 구문은 바인딩과 `using` 함수입니다.

## <a name="use-binding"></a>바인딩 사용

키워드의 형식은 `let` 바인딩의 형식과 비슷합니다. `use`

*값* = *식* 사용

`let` 바인딩과 동일한 기능을 제공 하지만 값이 범위를 벗어나면 값 `Dispose` 에 대 한 호출을 추가 합니다. 컴파일러는 값에 null 검사를 삽입 하므로 값이 인 `null`경우에 대 `Dispose` 한 호출이 시도 되지 않습니다.

다음 예제에서는 키워드를 `use` 사용 하 여 파일을 자동으로 닫는 방법을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6301.fs)]

> [!NOTE]
> 계산 식에 `use` 를 사용할 수 있습니다 .이 경우 사용자 지정 된 버전 `use` 의 식이 사용 됩니다. 자세한 내용은 [시퀀스](sequences.md), [비동기 워크플로](asynchronous-workflows.md)및 [계산 식](computation-expressions.md)을 참조 하세요.

## <a name="using-function"></a>using 함수

함수 `using` 는 다음과 같은 형식입니다.

`using`(*expression1*) *함수 또는-람다*

식에서 expression1는 삭제 해야 하는 개체를 만듭니다. `using` *Expression1* (삭제 해야 하는 개체)의 결과는 인수, *값*, *함수 또는 람다*가 됩니다 .이 함수는에 의해 *생성 된 값과 일치 하는 형식에 대해 남아 있는 단일 인수를 필요로 하는 함수입니다. expression1*또는 해당 형식의 인수를 필요로 하는 람다 식입니다. 함수 실행이 끝날 때 런타임은 리소스를 호출 `Dispose` 하 고 해제 합니다 .이 경우 값이이 `null`고, 그렇지 않으면 Dispose에 대 한 호출이 시도 되지 않습니다.

다음 예에서는 람다 식이 `using` 있는 식을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6302.fs)]

다음 예에서는 함수를 `using` 사용 하는 식을 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6303.fs)]

함수는 일부 인수를 이미 적용 한 함수 일 수 있습니다. 다음 코드 예제에서는 이 작업을 보여줍니다. 문자열이 `XYZ`포함 된 파일을 만듭니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6304.fs)]

`using` 함수와`use` 바인딩은 거의 동일한 방식으로 동일한 작업을 수행 합니다. 키워드 `using` 는를 호출 하는 경우 `Dispose` 에 대 한 더 많은 제어를 제공 합니다. 를 `using` `use` `Dispose` 사용 하는 경우은 함수 또는 람다 식의 끝에서 호출 됩니다. 키워드를 사용 하는 경우 포함 하는 코드 블록의 끝에서가 호출 됩니다. `Dispose` 일반적으로 `use` `using` 함수 대신를 사용 하는 것이 좋습니다.

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
