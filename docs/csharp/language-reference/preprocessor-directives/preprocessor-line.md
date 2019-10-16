---
title: '#line - C# 참조'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- '#line'
helpviewer_keywords:
- '#line directive [C#]'
ms.assetid: 6439e525-5dd5-4acb-b8ea-efabb32ff95b
ms.openlocfilehash: b4ac4fd3277fb53251e87321500d1b8007458037
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608529"
---
# <a name="line-c-reference"></a>#line(C# 참조)

`#line`을 사용하면 오류 및 경고에 대한 컴파일러의 줄 번호 매기기 및 파일 이름 출력(선택 사항)을 수정할 수 있습니다.

다음 예제에서는 줄 번호와 관련된 두 개의 경고를 보고하는 방법을 보여 줍니다. `#line 200` 지시문은 다음 줄 번호를 강제로 200(기본값은 #6임)으로 설정하며, 다음 `#line` 지시문까지 파일 이름이 “Special”로 보고됩니다. `#line default` 지시문은 줄 번호 매기기를 기본 번호 매기기로 되돌립니다. 이 경우 이전 지시문을 통해 번호가 다시 매겨진 줄이 계산됩니다.

```csharp
class MainClass
{
    static void Main()
    {
#line 200 "Special"
        int i;
        int j;
#line default
        char c;
        float f;
#line hidden // numbering not affected
        string s;
        double d;
    }
}
```

컴파일은 다음 출력을 생성합니다.

```console
Special(200,13): warning CS0168: The variable 'i' is declared but never used
Special(201,13): warning CS0168: The variable 'j' is declared but never used
MainClass.cs(9,14): warning CS0168: The variable 'c' is declared but never used
MainClass.cs(10,15): warning CS0168: The variable 'f' is declared but never used
MainClass.cs(12,16): warning CS0168: The variable 's' is declared but never used
MainClass.cs(13,16): warning CS0168: The variable 'd' is declared but never used
```

## <a name="remarks"></a>설명

`#line` 지시문은 빌드 프로세스의 자동화된 중간 단계에서 사용할 수 있습니다. 예를 들어 원래 소스 코드 파일에서 줄이 제거되었지만 여전히 컴파일러에서 파일의 원래 줄 번호 매기기에 따라 출력을 생성하려는 경우, 줄을 제거한 다음 `#line`을 사용하여 원래 줄 번호 매기기를 시뮬레이트할 수 있습니다.

`#line hidden` 지시문은 개발자가 코드를 단계별로 실행할 때 `#line hidden`과 다음 `#line` 지시문(다른 `#line hidden` 지시문이 아니라고 가정) 사이에 있는 모든 줄이 프로시저 단위로 실행되도록 디버거에서 연속되는 줄을 숨깁니다. 이 옵션을 사용하여 ASP.NET이 사용자 정의 코드와 컴퓨터에서 생성된 코드를 구분하도록 할 수도 있습니다. ASP.NET이 이 기능의 주 소비자지만 기능을 사용할 소스 생성기가 늘어날 가능성이 큽니다.

`#line hidden` 지시문은 오류 보고의 파일 이름이나 줄 번호에는 영향을 주지 않습니다. 즉, 숨겨진 블록에서 오류가 발생할 경우 컴파일러는 오류의 현재 파일 이름과 줄 번호를 보고합니다.

`#line filename` 지시문은 컴파일러 출력에 표시하려는 파일 이름을 지정합니다. 기본적으로 소스 코드 파일의 실제 이름이 사용됩니다. 파일 이름은 큰따옴표(“ ”)로 묶어야 하고 줄 번호 뒤에 와야 합니다.

소스 코드 파일에 `#line` 지시문을 개수와 관계없이 포함할 수 있습니다.

## <a name="example-1"></a>예제 1

다음 예제에서는 디버거가 코드의 숨겨진 줄을 어떻게 무시하는지를 보여 줍니다. 예제를 실행하면 세 줄의 텍스트가 표시됩니다. 그러나 예제와 같이 중단점을 설정하고 F10 키를 눌러 코드를 단계별로 실행할 경우 디버거는 숨겨진 줄을 무시합니다. 숨겨진 줄에 중단점을 설정한 경우에도 디버거가 무시합니다.

```csharp
// preprocessor_linehidden.cs
using System;
class MainClass
{
    static void Main()
    {
        Console.WriteLine("Normal line #1."); // Set break point here.
#line hidden
        Console.WriteLine("Hidden line.");
#line default
        Console.WriteLine("Normal line #2.");
    }
}
```

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 전처리기 지시문](./index.md)
