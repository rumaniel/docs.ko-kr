---
title: '#if 전처리기 지시문 - C# 참조'
ms.custom: seodec18
ms.date: 06/30/2018
f1_keywords:
- '#if'
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
ms.openlocfilehash: d0297094fbb8098b706cb8c6338fa123afc0753b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605694"
---
# <a name="if-c-reference"></a>#if(C# 참조)

C# 컴파일러는 `#if` 지시문과 [#endif](preprocessor-endif.md) 지시문이 차례로 확인되면 지정된 기호가 정의되어 있어야 지시문 사이의 코드를 컴파일합니다. C 및 C++와 달리, 기호에 숫자 값을 할당할 수 없습니다. C#의 #if 문은 부울이고 기호가 정의되었는지 여부만 테스트합니다. 예:

```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

[==](../operators/equality-operators.md#equality-operator-)(같음) 및 [!=](../operators/equality-operators.md#inequality-operator-)(같지 않음) 연산자는 [true](../keywords/true-literal.md) 또는 [false](../keywords/false-literal.md)를 테스트할 때만 사용할 수 있습니다. true가 반환되면 기호가 정의된 것입니다. `#if DEBUG` 문의 의미는 `#if (DEBUG == true)`와 같습니다. [&&](../operators/boolean-logical-operators.md#conditional-logical-and-operator-)(및), [&#124;&#124;](../operators/boolean-logical-operators.md#conditional-logical-or-operator-)(또는), [!](../operators/boolean-logical-operators.md#logical-negation-operator-)(아님) 연산자를 사용하면 여러 기호가 정의되었는지 여부를 평가할 수 있습니다. 기호와 연산자를 괄호로 묶을 수도 있습니다.

## <a name="remarks"></a>설명

`#if`를 [#else](preprocessor-else.md), [#elif](preprocessor-elif.md), [#endif](preprocessor-endif.md), [#define](preprocessor-define.md) 및 [#undef](preprocessor-undef.md) 지시문과 함께 사용하면 하나 이상의 기호 유무에 따라 코드를 포함하거나 제거할 수 있습니다. 따라서 코드를 디버그 빌드용으로 컴파일하거나 특정 구성용으로 컴파일할 때 유용할 수 있습니다.

`#if` 지시문으로 시작되는 조건부 지시문은 `#endif` 지시문을 사용하여 명시적으로 종료해야 합니다.

`#define`을 사용하여 기호를 정의할 수 있습니다. 그러면 `#if` 지시문으로 전달되는 식으로 해당 기호를 사용하는 경우 식이 `true`로 평가됩니다.

[-define](../compiler-options/define-compiler-option.md) 컴파일러 옵션으로 기호를 정의할 수도 있습니다. [#undef](preprocessor-undef.md)로 기호 정의를 해제할 수 있습니다.

`-define` 또는 `#define`으로 정의하는 기호는 동일한 이름의 변수와 충돌하지 않습니다. 즉, 변수 이름이 전처리기 지시문에 전달되지 않아야 하며 전처리기 지시문을 통해서만 기호를 평가할 수 있습니다.

`#define`을 사용하여 만든 기호의 범위는 해당 기호가 정의된 파일입니다.

빌드 시스템은 여러 [대상 프레임워크](../../../standard/frameworks.md)를 나타내는 미리 정의된 전처리기 기호도 인식합니다. 둘 이상의 .NET 구현 또는 버전을 대상으로 지정할 수 있는 애플리케이션을 만들 때 유용합니다.

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

기타 미리 정의된 기호에는 DEBUG와 TRACE 상수가 있습니다. `#define`을 사용하여 프로젝트에 설정된 값을 재정의할 수 있습니다. 예를 들어 DEBUG 기호는 빌드 구성 특성(“디버그” 또는 “릴리스” 모드)에 따라 자동으로 설정됩니다.

## <a name="examples"></a>예제

다음 예제에서는 파일에 MYTEST 기호를 정의한 다음 MYTEST 및 DEBUG 기호의 값을 테스트하는 방법을 보여 줍니다. 이 예제의 출력은 디버그 구성 모드에서 프로젝트를 빌드했는지, 릴리스 구성 모드에서 프로젝트를 빌드했는지에 따라 다릅니다.

```csharp
#define MYTEST
using System;
public class MyClass
{
    static void Main()
    {
#if (DEBUG && !MYTEST)
        Console.WriteLine("DEBUG is defined");
#elif (!DEBUG && MYTEST)
        Console.WriteLine("MYTEST is defined");
#elif (DEBUG && MYTEST)
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else
        Console.WriteLine("DEBUG and MYTEST are not defined");
#endif
    }
}
```

다음 예제에서는 가능한 경우 새 API를 사용할 수 있도록 여러 대상 프레임워크에 대해 테스트하는 방법을 보여 줍니다.

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        WebClient _client = new WebClient();
#else
        HttpClient _client = new HttpClient();
#endif
    }
    //...
}
```

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 전처리기 지시문](index.md)
- [방법: 추적 및 디버그를 사용한 조건부 컴파일](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
