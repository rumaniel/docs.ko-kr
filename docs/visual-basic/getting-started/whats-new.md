---
title: Visual Basic의 새로운 기능
ms.date: 10/24/2018
f1_keywords:
- VB.StartPage.WhatsNew
helpviewer_keywords:
- new features, Visual Basic
- what's new [Visual Basic]
- Visual Basic, what's new
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
ms.openlocfilehash: d286cc811c87f2d45d5a9e6d4e8acd9c430ff346
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835256"
---
# <a name="whats-new-for-visual-basic"></a>Visual Basic의 새로운 기능

이 항목에는 각 Visual Basic 버전의 주요 기능 이름과 최신 Visual Basic 버전의 새로운 기능 및 향상된 기능에 대한 자세한 설명이 정리되어 있습니다.

## <a name="current-version"></a>현재 버전

Visual Basic 16.0 / Visual Studio 2019 버전 16.0  
새 기능은 [Visual Basic 16.0](#visual-basic-160)을 참조하세요.

## <a name="previous-versions"></a>이전 버전

Visual Basic 15.8 / Visual Studio 2017 버전 15.8 새 기능에 대해서는 [Visual Basic 15.8](#visual-basic-158)을 참조하세요.

Visual Basic 15.5 / Visual Studio 2017 Version 15.5 새 기능에 대해서는 [Visual Basic 15.5](#visual-basic-155)를 참조하세요.

Visual Basic 15.3 / Visual Studio 2017 Version 15.3 새 기능에 대해서는 [Visual Basic 15.3](#visual-basic-153)을 참조하세요.

Visual Basic 2017 / Visual Studio 2017 새 기능에 대해서는 [Visual Basic 2017](#visual-basic-2017)을 참조하세요.

Visual Basic / Visual Studio 2015 새 기능에 대해서는 [Visual Basic 14](#visual-basic-14)를 참조하세요.

Visual Basic / Visual Studio 2013 .NET 컴파일러 플랫폼(“Roslyn”)의 기술 미리 보기

Visual Basic / Visual Studio 2012 `Async` 및 `await` 키워드, 반복기, 호출자 정보 특성

Visual Basic, Visual Studio 2010 자동으로 구현된 속성, 컬렉션 이니셜라이저, 암시적 줄 연속, 동적, 제네릭 공변성(Covariance)/반공변성(Contravariance), 전역 네임스페이스 액세스

Visual Basic / Visual Studio 2008 LINQ(통합 언어 쿼리), XML 리터럴, 지역 형식 유추, 개체 이니셜라이저, 익명 형식, 확장 메서드, 로컬 `var` 형식 유추, 람다 식, `if` 연산자, 부분 메서드(Partial Method), nullable 값 형식

Visual Basic / Visual Studio 2005 `My` 형식 및 도우미 형식(앱, 컴퓨터, 파일 시스템, 네트워크에 액세스)

Visual Basic / Visual Studio .NET 2003 비트 시프트 연산자, 루프 변수 선언

Visual Basic / Visual Studio .NET 2002 Visual Basic .NET의 첫 번째 릴리스

## <a name="visual-basic-160"></a>Visual Basic 16.0
Visual Basic 16.0은 .NET Core에 더 많은 Visual Basic 런타임 기능(microsoft.visualbasic.dll)을 제공하는 데 초점을 맞추며, .NET Core에 초점을 맞춘 Visual Basic의 첫 번째 버전입니다. Visual Basic 런타임의 많은 부분은 WinForms에 종속되며, 이후 버전의 Visual Basic에 추가될 예정입니다. 

**문 내의 더 많은 위치에서 주석 허용** Visual Basic 15.8 및 이전 버전에서는 빈 줄, 문의 끝 또는 암시적 줄 연속이 허용되는 문 내의 특정 위치에서만 주석이 허용됩니다. Visual Basic 16.0부터 명시적 줄 연속 뒤와 공백 다음 밑줄로 시작하는 줄의 문 내에서도 주석이 허용됩니다.

```vb
Public Sub Main()
    cmd.CommandText = ' Comment is allowed here without _
        "SELECT * FROM Titles JOIN Publishers " _ ' This is a comment
        & "ON Publishers.PubId = Titles.PubID " _
 _ ' This is a comment on a line without code
        & "WHERE Publishers.State = 'CA'"
End Sub
```

## <a name="visual-basic-158"></a>Visual Basic 15.8

**최적화된 부동 소수점-정수 변환**

이전 버전의 Visual Basic에서 [Double](../language-reference/data-types/double-data-type.md) 및 [Single](../language-reference/data-types/single-data-type.md) 값을 정수로 변환하면 성능이 상대적으로 떨어졌습니다. Visual Basic 15.8은 다음 메서드 중 하나에 의해 반환된 값을 [내장 Visual Basic 정수 변환 함수](../language-reference/functions/type-conversion-functions.md)(CByte, CShort, CInt, CLng, CSByte, CUShort, CUInt, CULng) 중 하나에 전달하거나, [Option Strict](../language-reference/statements/option-strict-statement.md)가 `Off`로 설정된 경우 다음 메서드 중 하나로 반환되는 값이 암시적으로 정수 형식으로 캐스팅될 때 정수에 대한 부동 소수점 변환의 성능을 크게 향상시킵니다.

- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Single)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Single)?displayProperty=nameWithType>
- <xref:System.Math.Ceiling(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Floor(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Round(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Truncate(System.Double)?displayProperty=nameWithType>

이렇게 최적화하면 다량의 정수 형식 변환을 수행하는 코드의 경우 코드 실행 속도가 최대 2배까지 더 빨라집니다. 다음 예제에서는 이 최적화에 영향을 받는 몇 가지 간단한 메서드 호출을 보여줍니다.

```vb
Dim s As Single = 173.7619
Dim d As Double = s

Dim i1 As Integer = CInt(Fix(s))               ' Result: 173
Dim b1 As Byte = CByte(Int(d))                 ' Result: 173
Dim s1 AS Short = CShort(Math.Truncate(s))     ' Result: 173
Dim i2 As Integer = CInt(Math.Ceiling(d))      ' Result: 174
Dim i3 As Integer = CInt(Math.Round(s))        ' Result: 174

```

부동 소수점 값을 반올림하는 것이 아니라 잘린다는 점에 유의하세요.

## <a name="visual-basic-155"></a>Visual Basic 15.5

[뒤에 오지 않는 명명된 인수](../programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md#mixing-arguments-by-position-and-by-name)

Visual Basic 15.3 및 이전 버전에서 메서드 호출이 위치 및 이름별 인수를 포함하는 경우 위치 인수는 명명된 인수 앞에 와야 했습니다. Visual Basic 15.5부터 위치 및 명명된 인수는 마지막 위치 인수까지 모든 인수가 올바른 위치에 있는 한 순서에 관계 없이 나타날 수 있습니다. 이는 명명된 인수가 코드를 더 쉽게 읽을 수 있도록 사용되는 경우 특히 유용합니다.

예를 들어 다음 메서드 호출은 명명된 인수 사이에 두 개의 위치 인수를 갖습니다. 명명된 인수는 값 19가 나이를 나타낸다는 것을 명백하게 합니다.

```vb
StudentInfo.Display("Mary", age:=19, #9/21/1998#)
```

[`Private Protected` 멤버 액세스 한정자](../language-reference/modifiers/private-protected.md)

이 새 키워드 조합은 포함하는 클래스의 모든 멤버를 통해 액세스하고 포함하는 클래스에서 파생된 형식(해당 형식이 포함하는 어셈블리에 있는 경우에만)을 통해 액세스할 수 있는 멤버를 정의합니다. 구조체를 상속할 수 없으므로 `Private Protected`는 클래스의 멤버에만 적용할 수 있습니다.

**선행 16진수/이진/8진수 구분 기호**

Visual Basic 2017은 숫자 구분 기호로 밑줄 문자(`_`)에 대한 지원을 추가했습니다. Visual Basic 15.5부터 접두사와 16 진수, 이진 또는 8진수 숫자 사이의 선행 구분 기호로 밑줄 문자를 사용할 수 있습니다. 다음 예제에서는 선행 숫자 구분 기호를 사용하여 16진수 숫자로 3,271,948,384를 정의합니다.

```vb
Dim number As Integer = &H_C305_F860
```

선행 구분 기호로 밑줄 문자를 사용하려면 Visual Basic 프로젝트(\*.vbproj) 파일에 다음 요소를 추가해야 합니다.

```xml
<PropertyGroup>
  <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

## <a name="visual-basic-153"></a>Visual Basic 15.3

[**명명된 튜플 유추**](../programming-guide/language-features/data-types/tuples.md#inferred-tuple-element-names)

변수에서 튜플 요소의 값을 할당할 때 Visual Basic는 해당 변수 이름에서 튜플 요소의 이름을 유추합니다. 튜블 요소의 이름을 명시적으로 지정할 필요가 없습니다. 다음 예제에서는 유추를 사용하여 세 개의 명명된 요소, `state`, `stateName` 및 `capital`로 튜플을 만듭니다.

[!code-vb[Inferred tuple names](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

**추가 컴파일러 스위치**

이제 Visual Basic 명령줄 컴파일러는 참조 어셈블리의 출력을 제어하기 위해 [ **-refout**](../reference/command-line-compiler/refout-compiler-option.md) 및 [ **-refonly**](../reference/command-line-compiler/refonly-compiler-option.md) 컴파일러 옵션을 지원합니다. **-refout**는 참조 어셈블리의 출력 디렉터리를 정의하고 **-refonly**는 참조 어셈블리만 컴파일로 출력되도록 지정합니다.

## <a name="visual-basic-2017"></a>Visual Basic 2017

[**튜플**](../programming-guide/language-features/data-types/tuples.md)

튜플은 단일 메서드 호출에서 여러 값을 반환하는 데 주로 사용되는 간단한 데이터 구조입니다. 일반적으로 하나의 메서드에서 여러 값을 반환하려면 다음 중 하나를 수행해야 합니다.

- 사용자 지정 형식(`Class` 또는 `Structure`)을 정의합니다. 이는 대규모 솔루션입니다.

- 메서드에서 값을 반환하는 것 외에도 `ByRef` 매개 변수를 하나 이상 정의합니다.

Visual Basic의 튜플 지원을 사용하면 튜플을 신속하게 정의하고, 필요에 따라 해당 값에 의미 체계 이름을 할당하고, 해당 값을 빠르게 검색할 수 있습니다. 다음 예제에서는 <xref:System.Int32.TryParse%2A> 메서드 호출을 래핑하고 튜플을 반환합니다.

[!code-vb[Tuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

그런 다음 메서드를 호출하고 반환된 튜플을 코드에서 다음과 같이 처리할 수 있습니다.

[!code-vb[ReturnTuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

**이진 리터럴 및 자릿수 구분 기호**

`&B` 또는 `&b` 접두사를 사용하여 이진 리터럴을 정의할 수 있습니다. 또한 밑줄 문자 `_`를 자릿수 구분 기호로 사용하여 가독성을 향상할 수 있습니다. 다음 예제에서는 두 기능을 모두 사용하여 `Byte` 값을 할당하고 10진수, 16진수, 이진수로 표시합니다.

[!code-vb[Binary](../../../samples/snippets/visualbasic/getting-started/bin-example.vb#1)]

자세한 내용은 [바이트](../language-reference/data-types/byte-data-type.md#literal-assignments), [정수](../language-reference/data-types/integer-data-type.md#literal-assignments), [Long](../language-reference/data-types/long-data-type.md#literal-assignments), [Short](../language-reference/data-types/short-data-type.md#literal-assignments), [SByte](../language-reference/data-types/sbyte-data-type.md#literal-assignments), [UInteger](../language-reference/data-types/uinteger-data-type.md#literal-assignments), [ULong](../language-reference/data-types/ulong-data-type.md#literal-assignments) 및 [UShort](../language-reference/data-types/ushort-data-type.md#literal-assignments) 데이터 형식의 "리터럴 할당" 섹션을 참조하세요.

[**C# 참조 반환 값 지원**](../programming-guide/language-features/procedures/ref-return-values.md)

C# 7.0부터 C#에서 참조 반환 값을 지원합니다. 즉, 호출하는 메서드가 참조로 반환된 값을 받을 때 참조 값을 변경할 수 있습니다. Visual Basic에서 참조 반환 값이 있는 메서드를 작성할 수는 없지만 참조 반환 값을 사용하고 수정할 수 있습니다.

예를 들어 C#으로 작성된 다음 `Sentence` 클래스에는 문장 내에서 지정한 하위 문자열로 시작하는 다음 단어를 찾는 `FindNext` 메서드가 포함되어 있습니다. 문자열은 참조 반환 값으로 반환되며, 메서드에 참조로 전달된 `Boolean` 변수는 검색에 성공했는지 여부를 나타냅니다. 즉, 호출자는 반환된 값을 읽을 수 있을 뿐만 아니라 수정할 수도 있으며, 수정 내용이 `Sentence` 클래스에 반영됩니다.

[!code-csharp[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

가장 간단한 형태로, 문장에서 찾은 단어를 코드에서 다음과 같이 수정할 수 있습니다. 메서드 대신 메서드가 반환하는 식, 즉 참조 반환 값에 값을 할당합니다.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#1)]

그러나 이 코드의 문제는 일치 항목이 없을 경우 메서드가 첫 번째 단어를 반환한다는 것입니다. 이 예제에서는 `Boolean` 인수의 값을 검사하여 일치 항목이 있는지 확인하지 않으므로 일치 항목이 없을 경우 첫 번째 단어를 수정합니다. 다음 예제에서는 일치 항목이 없을 경우 첫 번째 단어를 해당 단어로 대체하여 이 문제를 해결합니다.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#2)]

더 나은 해결 방법은 참조 반환 값이 참조로 전달되는 도우미 메서드를 사용하는 것입니다. 그러면 도우미 메서드가 참조로 전달된 인수를 수정할 수 있습니다. 다음 예제에서는 해당 작업을 수행합니다.

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

자세한 내용은 [참조 반환 값](../programming-guide/language-features/procedures/ref-return-values.md)을 참조하세요.

## <a name="visual-basic-14"></a>Visual Basic 14

[Nameof](../../csharp/language-reference/operators/nameof.md)

문자열을 하드 코드하지 않고 오류 메시지에서 사용하기 위해 형식이나 멤버의 정규화되지 않은 문자열 이름을 가져올 수 있습니다.  이 기능을 사용하면 리팩터링할 때 코드를 올바르게 유지할 수 있습니다.  이 기능은 MVC(Model-View-Controller) 링크를 연결하고 속성 변경 이벤트를 발생시키는 데도 유용합니다.

[문자열 보간](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md)

문자열 보간 식을 사용하여 문자열을 생성할 수 있습니다.  보간된 문자열 식은 식이 포함된 템플릿 문자열과 유사합니다.  보간된 문자열은 인수 측면에서 [Composite Formatting](../../standard/base-types/composite-format.md)보다 이해하기 쉽습니다.

[Null 조건부 멤버 액세스 및 인덱싱](../language-reference/operators/null-conditional-operators.md)

멤버 액세스(`?.`) 또는 인덱스(`?[]`) 작업을 수행하기 전에 매우 간단한 구문을 사용하여 null 테스트를 수행할 수 있습니다.  이러한 연산자는 null 검사의 처리를 위해 작성하는 코드의 양을 줄이는 데 도움이 되며 특히 데이터 구조에서 아래로 내려가는 경우에 유용합니다.  왼쪽 피연산자 또는 개체 참조가 null이면 연산에서 null이 반환됩니다.

[다중 선 문자열 리터럴](../../visual-basic/programming-guide/language-features/strings/string-basics.md)

문자열 리터럴에 줄 바꿈 시퀀스가 포함될 수 있습니다.  `<xml><![CDATA[...text with newlines...]]></xml>.Value` 사용과 관련된 이전 작업은 더 이상 필요하지 않습니다.

**설명**

암시적 줄 연속 뒤, 이니셜라이저 식 내부 및 LINQ 식 항 사이에 주석을 입력할 수 있습니다.

**더 효율적인 정규화된 이름 확인**

`Threading.Thread.Sleep(1000)`과 같은 코드가 제공된 경우 이전에는 Visual Basic에서 "Threading" 네임스페이스를 조회하고 System.Threading 및 System.Windows.Threading 간에 모호하다는 사실을 발견한 후 오류를 보고했습니다.  이제 Visual Basic에서는 두 가지 가능한 네임스페이스를 함께 고려합니다.  완성 목록을 표시하는 경우 Visual Studio 편집기에서 두 형식의 멤버가 모두 완성 목록에 나열됩니다.

**연도가 먼저 나오는 날짜 리터럴**

yyyy-mm-dd 형식(`#2015-03-17 16:10 PM#`)의 날짜 리터럴을 사용할 수 있습니다.

**읽기 전용 인터페이스 속성**

읽기/쓰기 속성을 사용하여 읽기 전용 인터페이스 속성을 구현할 수 있습니다.  이러한 인터페이스는 최소 기능을 보장하며 구현 클래스에서 속성이 설정되도록 허용하는 것을 차단하지 않습니다.

[TypeOf \<expr> IsNot \<type>](../../visual-basic/language-reference/operators/typeof-operator.md)

코드를 더 읽기 쉽게 만들기 위해 `IsNot`과 함께 `TypeOf`를 사용할 수 있습니다.

[#Disable Warning \<ID> 및 #Enable Warning \<ID>](../../visual-basic/language-reference/directives/index.md)

소스 파일 내의 영역에 대한 특정 경고를 사용하지 않거나 사용하도록 설정할 수 있습니다.

**XML 문서 주석 향상**

문서 주석을 작성하면 편집기의 효율성을 높이고 매개 변수 이름의 유효성 검사, `crefs`(제네릭, 연산자 등)의 적절한 처리, 색 지정 및 리팩터링에 대한 지원을 제공할 수 있습니다.

[부분 모듈 및 인터페이스 정의](../../visual-basic/language-reference/modifiers/partial.md)

클래스 및 구조체 외에도 부분 모듈과 인터페이스를 선언할 수 있습니다.

[메서드 본문 내의 #Region 지시문](../../visual-basic/language-reference/directives/region-directive.md)

#Region…#End Region 구분 기호를 파일의 원하는 위치, 함수 내부 및 여러 함수 본문을 포괄하여 입력할 수 있습니다.

[Overrides 정의는 암시적으로 overloads임](../../visual-basic/language-reference/modifiers/overrides.md)

`Overrides` 한정자를 정의에 추가하면 일반적인 경우에 더 적은 코드를 입력할 수 있도록 컴파일러에서 암시적으로 `Overloads`를 추가합니다.

**특성 인수에서 허용되는 CObj**

이전에는 컴파일러에서 CObj(...)가 특성 생성에서 사용될 때 상수가 아니라는 오류를 제공했습니다.

**여러 인터페이스의 모호한 메서드 선언 및 사용**

이전에는 다음 코드에서 `IMock`을 선언하거나 `GetDetails`를 호출하지 못하게 하는 오류가 발생했습니다(이러한 항목이 C#에서 선언된 경우).

```vb
Interface ICustomer
  Sub GetDetails(x As Integer)
End Interface

Interface ITime
  Sub GetDetails(x As String)
End Interface

Interface IMock : Inherits ICustomer, ITime
  Overloads Sub GetDetails(x As Char)
End Interface

Interface IMock2 : Inherits ICustomer, ITime
End Interface
```

이제 컴파일러에서 일반 오버로드 확인 규칙을 사용하여 호출하는 데 가장 적합한 `GetDetails`를 선택하며, 샘플에서와 같이 Visual Basic에서 인터페이스 관계를 선언할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [Visual Studio 2017의 새로운 기능](/visualstudio/ide/whats-new-in-visual-studio)
