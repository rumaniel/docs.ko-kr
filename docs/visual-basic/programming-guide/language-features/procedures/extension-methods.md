---
title: 확장 메서드(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.ExtensionMethods
helpviewer_keywords:
- extending data types [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
ms.openlocfilehash: b5ad066fe9ec40d715702ed99537f45b21c558cf
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701048"
---
# <a name="extension-methods-visual-basic"></a>확장 메서드(Visual Basic)

개발자는 확장 메서드를 사용 하 여 새 파생 형식을 만들지 않고 이미 정의 된 데이터 형식에 사용자 지정 기능을 추가할 수 있습니다. 확장 메서드를 사용 하면 기존 형식의 인스턴스 메서드인 것 처럼 호출할 수 있는 메서드를 작성할 수 있습니다.
  
## <a name="remarks"></a>설명

확장 메서드는 `Sub` 프로시저 또는 `Function` 프로시저만 될 수 있습니다. 확장 속성, 필드 또는 이벤트를 정의할 수 없습니다. 모든 확장 메서드는 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 네임 스페이스의 `<Extension>` 확장 특성으로 표시 되어야 하며 [모듈](../../../language-reference/statements/module-statement.md)에서 정의 되어야 합니다. 확장 메서드가 모듈 외부에서 정의 된 경우 Visual Basic 컴파일러는 "모듈 에서만 확장 메서드를 정의할 수 있습니다" 라는 오류 [BC36551](../../../misc/bc36551.md)를 생성 합니다.

확장 메서드 정의의 첫 번째 매개 변수는 메서드가 확장 하는 데이터 형식을 지정 합니다. 메서드가 실행 될 때 첫 번째 매개 변수는 메서드를 호출 하는 데이터 형식의 인스턴스에 바인딩됩니다.

@No__t-0 특성은 Visual Basic [`Module`](../../../language-reference/statements/module-statement.md), [`Sub`](../../../language-reference/statements/sub-statement.md)또는 [`Function`](../../../language-reference/statements/function-statement.md)에만 적용할 수 있습니다. @No__t-0 또는 `Structure`에 적용 하는 경우 Visual Basic 컴파일러는 오류 [BC36550](../../../language-reference/error-messages/extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations.md)를 생성 하 고 "Extension ' 특성은 ' Module ', ' Sub ' 또는 ' Function ' 선언에만 적용할 수 있습니다.

## <a name="example"></a>예제

다음 예에서는 <xref:System.String> 데이터 형식에 대 한 `Print` 확장을 정의 합니다. 메서드는 `Console.WriteLine`을 사용 하 여 문자열을 표시 합니다. @No__t-0 메서드의 매개 변수 `aString`은 메서드가 @no__t 2 클래스를 확장 하도록 설정 합니다.
  
[!code-vb[VbVbalrExtensionMethods#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/StringExtensions.vb#1)]

확장 메서드 정의는-0 @no__t 확장 특성으로 표시 되어 있습니다. 메서드가 정의 되는 모듈을 표시 하는 것은 선택 사항 이지만 각 확장 메서드는로 표시 되어야 합니다. 확장 특성에 액세스 하려면 <xref:System.Runtime.CompilerServices>을 가져와야 합니다.

확장 메서드는 모듈 내 에서만 선언할 수 있습니다. 일반적으로 확장 메서드가 정의 된 모듈은 호출 되는 모듈과 동일한 모듈이 아닙니다. 대신 확장 메서드를 포함 하는 모듈을 가져온 후 범위로 가져와야 합니다. @No__t를 포함 하는 모듈이 범위 내에 있는 경우 인수를 사용 하지 않는 일반 인스턴스 메서드인 것 처럼 메서드를 호출할 수 있습니다 (예: `ToUpper`).

[!code-vb[VbVbalrExtensionMethods#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class1.vb#2)]

다음 예제 `PrintAndPunctuate`은 2 개의 매개 변수로 정의 된 <xref:System.String>에 대 한 확장 이기도 합니다. 첫 번째 매개 변수인 `aString`은 확장 메서드가 <xref:System.String>을 확장 하도록 설정 합니다. 두 번째 매개 변수인 `punc`은 메서드가 호출 될 때 인수로 전달 되는 문장 부호의 문자열입니다. 메서드는 문자열 뒤에 문장 부호를 표시 합니다.

[!code-vb[VbVbalrExtensionMethods#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class2.vb#3)]

@No__t-0에 대 한 문자열 인수를 전송 하 여 메서드를 호출 합니다 (`example.PrintAndPunctuate(".")`).

다음 예에서는 `Print` 및 `PrintAndPunctuate`을 정의 하 고 호출 하는 방법을 보여 줍니다. 확장 특성에 대 한 액세스를 사용 하기 위해 정의 모듈에 <xref:System.Runtime.CompilerServices>을 가져옵니다.


```vb
Imports System.Runtime.CompilerServices

Module StringExtensions

    <Extension()>
    Public Sub Print(aString As String)
        Console.WriteLine(aString)
    End Sub

    <Extension()>
    Public Sub PrintAndPunctuate(aString As String, punc As String)
        Console.WriteLine(aString & punc)
    End Sub
End Module
```

그런 다음 확장 메서드를 범위로 가져오고 호출 합니다.

```vb
Imports ConsoleApplication2.StringExtensions

Module Module1

    Sub Main()
        Dim example As String = "Example string"
        example.Print()

        example = "Hello"
        example.PrintAndPunctuate(".")
        example.PrintAndPunctuate("!!!!")
    End Sub
End Module
```

이러한 메서드 또는 유사한 확장 메서드를 실행 하려면 범위 내에 있어야 합니다. 확장 메서드를 포함 하는 모듈이 범위에 있으면 IntelliSense에 표시 되 고 일반 인스턴스 메서드인 것 처럼 호출 될 수 있습니다.

메서드가 호출 되 면 첫 번째 매개 변수에 대해 인수가 전송 되지 않습니다. 이전 메서드 정의의 매개 변수 `aString`은이를 호출 하는 `String` 인스턴스인 `example`에 바인딩됩니다. 컴파일러는 첫 번째 매개 변수로 전달 된 인수로 `example`을 사용 합니다.

@No__t로 설정 된 개체에 대해 확장 메서드가 호출 되 면 확장 메서드가 실행 됩니다. 이는 일반 인스턴스 메서드에는 적용 되지 않습니다. 확장 메서드에서 `Nothing`을 명시적으로 확인할 수 있습니다.

## <a name="types-that-can-be-extended"></a>확장할 수 있는 형식

다음을 포함 하 여 Visual Basic 매개 변수 목록에서 표현할 수 있는 대부분의 형식에 대 한 확장 메서드를 정의할 수 있습니다.

- 클래스 (참조 형식)
- 구조체 (값 형식)
- 인터페이스
- 대리자
- ByRef 및 ByVal 인수
- 제네릭 메서드 매개 변수
- 배열

첫 번째 매개 변수는 확장 메서드가 확장 하는 데이터 형식을 지정 하므로이 매개 변수는 필수 이며 선택 사항이 될 수 없습니다. 이러한 이유로 `Optional` 매개 변수와 `ParamArray` 매개 변수는 매개 변수 목록의 첫 번째 매개 변수가 될 수 없습니다.

확장 메서드는 런타임에 바인딩에서 고려 되지 않습니다. 다음 예제에서 `anObject.PrintMe()`은 두 번째 @no__t 2 확장 메서드 정의가 삭제 된 경우와 동일한 예외로 <xref:System.MissingMemberException> 예외를 발생 시킵니다.

[!code-vb[VbVbalrExtensionMethods#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class6.vb#9)]

## <a name="best-practices"></a>모범 사례

확장 메서드는 기존 형식을 확장 하는 편리 하 고 강력한 방법을 제공 합니다. 그러나이를 성공적으로 사용 하려면 몇 가지 사항을 고려해 야 합니다. 이러한 고려 사항은 주로 클래스 라이브러리의 작성자에 게 적용 되지만 확장 메서드를 사용 하는 모든 응용 프로그램에 영향을 줄 수 있습니다.

일반적으로 사용자가 소유 하지 않은 형식에 추가 하는 확장 메서드는 사용자가 제어 하는 형식에 추가 된 확장 메서드 보다 취약 합니다. 사용자가 소유 하지 않은 클래스에서 다양 한 작업을 수행 하 여 확장 메서드를 방해할 수 있습니다.

- 호출 하는 문의 인수와 호환 되는 시그니처를 포함 하는 액세스 가능한 인스턴스 멤버가 있고 인수에서 매개 변수에 대 한 축소 변환이 필요 하지 않은 경우, 인스턴스 메서드가 모든 확장 메서드에 대 한 기본 설정에서 사용 됩니다. 따라서 특정 시점에 적절 한 인스턴스 메서드를 클래스에 추가 하면 사용 하는 기존 확장 멤버에 액세스할 수 없게 됩니다.

- 확장 메서드 작성자는 다른 프로그래머가 원래 확장 보다 우선 순위가 높은 충돌 하는 확장 메서드를 작성 하는 것을 방지할 수 없습니다.

- 고유한 네임 스페이스에 확장 메서드를 추가 하 여 견고성을 향상 시킬 수 있습니다. 라이브러리의 소비자는 네임 스페이스를 포함 하거나 제외할 수 있으며, 라이브러리의 나머지 부분과 별도로 네임 스페이스 중에서 선택할 수 있습니다.

- 인터페이스 또는 클래스를 소유 하지 않는 경우에는 클래스를 확장 하는 것 보다 인터페이스를 확장 하는 것이 더 안전 합니다. 인터페이스를 변경 하면 해당 인터페이스를 구현 하는 모든 클래스에 영향을 줍니다. 따라서 작성자는 인터페이스에서 메서드를 추가 하거나 변경할 가능성이 적습니다. 그러나 클래스가 동일한 서명으로 확장 메서드를 사용 하는 두 인터페이스를 구현 하는 경우에는 두 확장 메서드가 모두 표시 되지 않습니다.

- 가능 하면 가장 구체적인 형식을 확장 합니다. 형식 계층에서 다른 많은 형식이 파생 되는 형식을 선택 하는 경우 인스턴스 메서드 또는 다른 확장 메서드를 사용 하 여 사용자가 방해할 수 있는 다른 확장 메서드를 도입할 수 있습니다.

## <a name="extension-methods-instance-methods-and-properties"></a>확장 메서드, 인스턴스 메서드 및 속성

범위 내 인스턴스 메서드에 호출 문의 인수와 호환 되는 시그니처가 있는 경우 해당 인스턴스 메서드는 모든 확장 메서드의 기본 설정에서 선택 됩니다. 인스턴스 메서드는 확장 메서드가 더 잘 일치 하는 경우에도 우선 순위가 높습니다. 다음 예제에서 `ExampleClass`은 `Integer` 형식의 매개 변수 하나를 포함 하는 `ExampleMethod` 이라는 인스턴스 메서드를 포함 합니다. 확장 메서드 `ExampleMethod` `ExampleClass`을 확장 하 고 `Long` 형식의 매개 변수 하나를 포함 합니다.

[!code-vb[VbVbalrExtensionMethods#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class4.vb#4)]

@No__t-1은 `Long`이 고 확장 메서드의 `Long` 매개 변수와만 호환 되기 때문에 다음 코드에서 `ExampleMethod`에 대 한 첫 번째 호출은 확장 메서드를 호출 합니다. @No__t-0에 대 한 두 번째 호출에는 `Integer` 인수 `arg2`가 있으며 인스턴스 메서드를 호출 합니다.

[!code-vb[VbVbalrExtensionMethods#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class4.vb#5)]

이제 두 가지 방법으로 매개 변수의 데이터 형식을 되돌립니다.

[!code-vb[VbVbalrExtensionMethods#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class5.vb#6)]

이번에 `Main`의 코드는 인스턴스 메서드를 두 번 호출 합니다. @No__t-0과 `arg2`은 둘 다 `Long`로 확대 변환 되므로 두 경우 모두 인스턴스 메서드가 확장 메서드 보다 우선적으로 사용 됩니다.

[!code-vb[VbVbalrExtensionMethods#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class5.vb#7)]

따라서 확장 메서드는 기존 인스턴스 메서드를 대체할 수 없습니다. 그러나 확장 메서드의 이름이 인스턴스 메서드와 동일 하지만 서명이 충돌 하지 않는 경우 두 메서드 모두에 액세스할 수 있습니다. 예를 들어, @no__t 클래스에 인수를 사용 하지 않는 `ExampleMethod` 이라는 메서드가 포함 된 경우 다음 코드와 같이 이름이 같지만 시그니처가 다른 확장 메서드를 사용할 수 있습니다.

[!code-vb[VbVbalrExtensionMethods#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Module3.vb#8)]

이 코드의 출력은 다음과 같습니다.

```console
Extension method
Instance method
```

속성을 사용 하는 경우 보다 간단 합니다. 확장 메서드가 확장 하는 클래스의 속성과 이름이 같은 경우 확장 메서드는 표시 되지 않으며 액세스할 수 없습니다.

## <a name="extension-method-precedence"></a>확장 메서드 우선 순위

시그니처가 동일한 두 확장 메서드가 범위에 있고 액세스할 수 있는 경우 우선 순위가 높은 하나는 호출 됩니다. 확장 메서드의 우선 순위는 메서드를 범위로 가져오는 데 사용 되는 메커니즘을 기반으로 합니다. 다음 목록에서는 우선 순위 계층을 최상위에서 최하위로 보여 줍니다.

1. 현재 모듈 내에 정의 된 확장 메서드입니다.

2. 현재 네임 스페이스 또는 부모 네임 스페이스의 데이터 형식 내에 정의 된 확장 메서드로, 하위 네임 스페이스가 부모 네임 스페이스 보다 우선 순위가 높습니다.

3. 현재 파일의 모든 형식 가져오기 안에 정의 된 확장 메서드

4. 현재 파일의 네임 스페이스 가져오기 안에 정의 된 확장 메서드

5. 모든 프로젝트 수준 형식 가져오기 내에 정의 된 확장 메서드

6. 프로젝트 수준 네임 스페이스 가져오기 안에 정의 된 확장 메서드

우선 순위에 의해 모호성을 해결 하지 못하는 경우 정규화 된 이름을 사용 하 여 호출 하는 메서드를 지정할 수 있습니다. 이전 예제의 `Print` 메서드가 `StringExtensions` 이라는 모듈에서 정의 된 경우 정규화 된 이름은 `example.Print()`이 아닌 `StringExtensions.Print(example)`입니다.

## <a name="see-also"></a>참조

- <xref:System.Runtime.CompilerServices>
- <xref:System.Runtime.CompilerServices.ExtensionAttribute>
- [확장명 메서드](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
- [Module 문](../../../language-reference/statements/module-statement.md)
- [프로시저 매개 변수 및 인수](procedure-parameters-and-arguments.md)
- [선택적 매개 변수](optional-parameters.md)
- [매개 변수 배열](parameter-arrays.md)
- [특성 개요](../../concepts/attributes/index.md)
- [Visual Basic 범위](../declared-elements/scope.md)
