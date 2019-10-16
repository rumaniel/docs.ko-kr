---
title: '#define - C# 참조'
ms.custom: seodec18
ms.date: 06/30/2018
f1_keywords:
- '#define'
helpviewer_keywords:
- '#define directive [C#]'
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
ms.openlocfilehash: d207c96621564acd8070c9d5f618f43a6d8f15a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924596"
---
# <a name="define-c-reference"></a>#define(C# 참조)
`#define`을 사용하여 기호를 정의합니다. 기호를 [#if](./preprocessor-if.md) 지시문에 전달되는 식으로 사용하는 경우 식이 다음 예제와 같이 `true`로 평가됩니다.  
 
 ```csharp
 #define DEBUG
 ```
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> C 및 C++에서 일반적으로 수행하듯이 `#define` 지시문을 사용하여 상수 값을 선언할 수 없습니다. C#의 상수는 클래스 또는 구조체의 정적 멤버로 가장 잘 정의됩니다. 이러한 상수가 여러 개 있는 경우 상수를 포함할 별도의 "Constants" 클래스를 만드는 것이 좋습니다.  
  
 기호를 사용하여 컴파일 조건을 지정할 수 있습니다. [#if](./preprocessor-if.md) 또는 [#elif](./preprocessor-elif.md)를 사용하여 기호를 테스트할 수 있습니다. <xref:System.Diagnostics.ConditionalAttribute>를 사용하여 조건부 컴파일을 수행할 수도 있습니다.  
  
 기호를 정의할 수 있지만 기호에 값을 할당할 수는 없습니다. `#define` 지시문은 파일에서 전처리기 지시문이 아닌 명령을 사용하기 전에 나와야 합니다.  
  
 [-define](../compiler-options/define-compiler-option.md) 컴파일러 옵션으로 기호를 정의할 수도 있습니다. [#undef](./preprocessor-undef.md)로 기호 정의를 해제할 수 있습니다.  
  
 `-define` 또는 `#define`으로 정의하는 기호는 동일한 이름의 변수와 충돌하지 않습니다. 즉, 변수 이름이 전처리기 지시문에 전달되지 않아야 하며, 전처리기 지시문을 통해서만 기호를 평가할 수 있습니다.  
  
 `#define`을 사용하여 만든 기호의 범위는 기호가 정의된 파일입니다.  
  
 다음 예제와 같이, `#define` 지시문을 파일 맨 위에 배치해야 합니다.  
  
```csharp  
#define DEBUG  
//#define TRACE  
#undef TRACE  
  
using System;  
  
public class TestDefine  
{  
    static void Main()  
    {  
#if (DEBUG)  
        Console.WriteLine("Debugging is enabled.");  
#endif  
  
#if (TRACE)  
     Console.WriteLine("Tracing is enabled.");  
#endif  
    }  
}  
// Output:  
// Debugging is enabled.  
```  
  
 기호 정의를 해제하는 방법의 예는 [#undef](./preprocessor-undef.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 전처리기 지시문](./index.md)
- [const](../keywords/const.md)
- [방법: 추적 및 디버그를 사용한 조건부 컴파일](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
- [#undef](./preprocessor-undef.md)
- [#if](./preprocessor-if.md)
