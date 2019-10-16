---
title: 기본 제공 참조 형식 - C# 참조
description: 선언하는 데 사용할 수 있는 C# 키워드가 있는 참조 형식에 대해 알아봅니다.
ms.date: 06/25/2019
f1_keywords:
- object_CSharpKeyword
- object
- delegate_CSharpKeyword
- delegate
- dynamic_CSharpKeyword
- string
- string_CSharpKeyword
helpviewer_keywords:
- object keyword [C#]
- delegate keyword [C#]
- function pointers [C#]
- dynamic [C#]
- dynamic keyword [C#]
- strings [C#], reference
- '@ string literal'
- string literals [C#]
- string keyword [C#]
ms.openlocfilehash: a5a32fa0a98cda37d7f599b20ef2b507cadd730c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69604206"
---
# <a name="built-in-reference-types-c-reference"></a>기본 제공 참조 형식(C# 참조)

C#에는 여러 가지 기본 제공 참조 형식이 있습니다. .NET 라이브러리의 형식에 대한 동의어인 키워드 또는 연산자를 가지고 있습니다. 

## <a name="the-object-type"></a>개체 유형

`object` 형식은 .NET에서 <xref:System.Object?displayProperty=nameWithType>의 별칭입니다. C#의 통합 형식 시스템에서 사용자 정의 및 미리 정의된 참조 형식과 값 형식을 비롯한 모든 형식은 직접 또는 간접적으로 <xref:System.Object?displayProperty=nameWithType>에서 상속합니다. `object` 형식의 변수에 모든 형식의 값을 할당할 수 있습니다. 모든 `object` 변수는 리터럴 `null`을 사용하여 기본값으로 할당할 수 있습니다. 값 형식의 변수가 개체로 변환된 경우 *boxed*라고 합니다. 형식 개체의 변수가 값 형식으로 변환된 경우 *unboxed*라고 합니다. 자세한 내용은 [boxing 및 unboxing](../../programming-guide/types/boxing-and-unboxing.md)을 참조하세요. 

## <a name="the-string-type"></a>문자열 유형

`string` 형식은 0자 이상의 유니코드 문자 시퀀스를 나타냅니다. `string`는 .NET에서 <xref:System.String?displayProperty=nameWithType>의 별칭입니다.

`string`은 참조 형식이지만 [같음 연산자 `==` 및 `!=`](../operators/equality-operators.md#string-equality)는 참조가 아니라 `string` 개체의 값을 비교하도록 정의됩니다. 이 때문에 좀 더 직관적으로 문자열이 같은지 테스트할 수 있습니다. 예:

```csharp-interactive
string a = "hello";
string b = "h";
// Append to contents of 'b'
b += "ello";
Console.WriteLine(a == b);
Console.WriteLine(object.ReferenceEquals(a, b));
```

이 코드는 "True"를 표시한 다음 "False"를 표시하며, 이는 문자열의 내용이 동일하지만 `a`와 `b`는 동일한 문자열 인스턴스를 가리키지 않기 때문입니다.

[+ 연산자](../operators/addition-operator.md#string-concatenation)는 문자열을 연결합니다.

```csharp
string a = "good " + "morning";
```

이 경우 "good morning"이 포함된 문자열 개체가 생성됩니다.

문자열은 *변경할 수 없습니다*. 구문상 가능한 것처럼 보여도 개체를 만든 후에는 문자열 개체의 내용을 변경할 수 없습니다. 예를 들어 이 코드를 작성하면 컴파일러는 실제로 새 문자 시퀀스를 보유할 새 문자열 개체를 만들고, 새 개체가 `b`에 할당됩니다. `b`에 할당된 메모리(문자열 "h"가 포함된 경우)는 가비지 수집에 적합합니다.

```csharp
string b = "h";
b += "ello";
```

`[]` [연산자](../operators/member-access-operators.md#indexer-operator-)는 `string`의 개별 문자에 대한 읽기 전용 액세스에 사용할 수 있습니다. 유효한 값은 `0`에서 시작되며 `string`의 길이보다 작아야 합니다.

```csharp
string str = "test";
char x = str[2];  // x = 's';
```

비슷한 방식으로 `[]` 연산자도 `string`의 각 문자를 반복하는 데 사용할 수 있습니다.

```csharp-interactive
string str = "test";

for (int i = 0; i < str.Length; i++)
{
  Console.Write(str[i] + " ");
}
// Output: t e s t
``` 

문자열 리터럴은 `string` 형식이며, quoted 및 `@`-quoted의 두 가지 형식으로 작성될 수 있습니다. 따옴표가 있는 문자열 리터럴은 큰따옴표(")로 묶여 있습니다.

```csharp
"good morning"  // a string literal
```

문자열 리터럴에는 모든 문자 리터럴이 포함될 수 있습니다. 이스케이프 시퀀스가 포함됩니다. 다음 예제에서는 이스케이프 시퀀스 `\\`를 백슬래시에 사용하고, `\u0066`을 f에 사용하고, `\n`을 줄 바꿈에 사용합니다.

```csharp-interactive
string a = "\\\u0066\n F";
Console.WriteLine(a);
\\ Output:
\\ \f
\\  F
```

> [!NOTE]
> 이스케이프 코드 `\udddd`(여기서 `dddd`는 4자리 숫자)는 유니코드 문자 U+`dddd`를 나타냅니다. 8자리 유니코드 이스케이프 코드 `\Udddddddd`도 인식됩니다.

[축자 문자열 리터럴](../tokens/verbatim.md)은 `@`로 시작하며 큰따옴표로 묶여 있습니다. 예:

```csharp
@"good morning"  // a string literal
```

축자 문자열의 장점은 이스케이프 시퀀스가 처리되지 *않으므로*, 정규화된 Windows 파일 이름 등을 쉽게 쓸 수 있다는 것입니다.

```csharp
@"c:\Docs\Source\a.txt"  // rather than "c:\\Docs\\Source\\a.txt"
```

@-quoted 문자열에 큰따옴표를 포함하려면 큰따옴표로 묶습니다.

```csharp
@"""Ahoy!"" cried the captain." // "Ahoy!" cried the captain.
```

## <a name="the-delegate-type"></a>대리자 형식

delegate 형식의 선언은 메서드 시그니처와 유사합니다. 반환 값이 있으며 모든 형식의 매개 변수를 개수에 관계없이 사용할 수 있습니다.

```csharp
public delegate void MessageDelegate(string message);
public delegate int AnotherDelegate(MyType m, long num);
```

.NET에서 `System.Action` 및 `System.Func` 유형은 많은 일반 대리자에 대한 일반적인 정의를 제공합니다. 새 사용자 지정 대리자 형식을 정의할 필요가 없습니다. 대신 제공된 제네릭 형식의 인스턴스화를 만들 수 있습니다.

`delegate`는 명명된 메서드나 무명 메서드를 캡슐화하는 데 사용할 수 있는 참조 형식입니다. 대리자는 C++의 함수 포인터와 비슷하지만 형식 안전성과 보안성을 제공한다는 점이 다릅니다. 대리자 적용에 대해서는 [대리자](../../programming-guide/delegates/index.md) 및 [제네릭 대리자](../../programming-guide/generics/generic-delegates.md)를 참조하세요. 대리자는 [이벤트](../../programming-guide/events/index.md)의 기반이 됩니다. 대리자는 명명된 메서드나 무명 메서드와 연결하여 인스턴스화할 수 있습니다.

대리자는 호환되는 반환 형식 및 입력 매개 변수가 있는 메서드나 람다 식을 사용하여 인스턴스화해야 합니다. 메서드 시그니처에서 허용되는 가변성 수준에 대한 자세한 내용은 [대리자의 가변성](../../programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)을 참조하세요. 무명 메서드에서 사용하기 위해 메서드에 연결할 대리자와 코드를 함께 선언합니다. 

## <a name="the-dynamic-type"></a>동적 형식

`dynamic` 유형은 변수 및 해당 멤버에 대한 참조 사용이 컴파일 파일 형식 검사를 바이패스함을 나타냅니다. 대신, 이러한 작업은 런타임에 확인됩니다. `dynamic` 형식은 Office Automation API와 같은 COM API, IronPython 라이브러리 등의 동적 API 및 HTML DOM(문서 개체 모델)에 대한 액세스를 간소화합니다.

`dynamic` 형식은 대부분의 상황에서 `object` 형식처럼 동작합니다. 특히 null이 아닌 모든 식은 `dynamic` 형식으로 변환될 수 있습니다. `dynamic` 유형의 식을 포함하는 작업은 컴파일러에서 확인되거나 형식이 검사되지 않았다는 점에서 `dynamic` 유형은 `object`와 다릅니다. 컴파일러는 작업에 대한 정보를 패키지하며, 나중에 해당 정보는 런타임에 작업을 평가하는 데 사용됩니다. 이 과정에서 `dynamic` 형식의 변수는 `object` 형식의 변수로 컴파일됩니다. 따라서 `dynamic` 형식은 컴파일 시간에만 존재하고 런타임에는 존재하지 않습니다.

다음 예제에서는 `dynamic` 형식의 변수와 `object` 형식의 변수를 비교합니다. 컴파일 시간에 각 변수의 형식을 확인하려면 `WriteLine` 문의 `dyn` 또는 `obj` 위에 마우스 포인터를 놓습니다. IntelliSense를 사용할 수 있는 편집기로 다음 코드를 복사합니다. IntelliSense는 `dyn`에 대해 **dynamic**을 표시하고 `obj`에 대해 **object**를 표시합니다.

[!code-csharp[csrefKeywordsTypes#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic1.cs#21)]

<xref:System.Console.WriteLine%2A> 문은 `dyn` 및 `obj`의 런타임 형식을 표시합니다. 이 시점에는 둘 다 동일한 형식인 정수입니다. 다음 출력이 생성됩니다.

```console
System.Int32
System.Int32
```

컴파일 시간에 `dyn` 및 `obj` 간의 차이를 보려면 앞의 예제에서 선언과 `WriteLine` 문 사이에 다음 두 줄을 추가합니다.

```csharp
dyn = dyn + 3;
obj = obj + 3;
```

 `obj + 3` 식에 정수와 개체를 추가하려는 시도와 관련해서 컴파일러 오류가 보고됩니다. 하지만 `dyn + 3`에 대한 오류는 보고되지 않습니다. `dyn`의 형식이 `dynamic`이기 때문에 `dyn`을 포함하는 식은 컴파일 시간에 확인되지 않습니다.

다음 예제에서는 여러 선언에 `dynamic`을 사용합니다. 또한 `Main` 메서드는 컴파일 시간 형식 검사를 런타임 형식 검사와 비교합니다.

[!code-csharp[csrefKeywordsTypes#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/dynamic2.cs#25)]

### <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 키워드](../keywords/index.md)
- [이벤트](../../programming-guide/events/index.md)
- [dynamic 형식 사용](../../programming-guide/types/using-type-dynamic.md)
- [문자열 사용에 대한 모범 사례](../../../standard/base-types/best-practices-strings.md)
- [기본적인 문자열 작업](../../../standard/base-types/basic-string-operations.md)
- [새 문자열 만들기](../../../standard/base-types/creating-new.md)
- [형식 테스트 및 캐스트 연산자](../operators/type-testing-and-cast.md)
- [방법: 패턴 일치, as 및 is 연산자를 사용하여 안전하게 캐스트](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)
- [연습: 동적 개체 만들기 및 사용](../../programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
- <xref:System.Object?displayProperty=nameWithType>
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.Dynamic.DynamicObject?displayProperty=nameWithType>
