---
title: 메서드 - C# 가이드
description: 메서드, 메서드 매개 변수 및 메서드 반환 값의 개요
author: rpetrusha
ms.author: ronpet
ms.date: 05/21/2018
ms.assetid: 577a8527-1081-4b36-9b9e-0685b6553c6e
ms.openlocfilehash: b95818e06d37b0e98bf55428ff97dd476f92fac7
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168510"
---
# <a name="methods"></a>메서드

메서드는 일련의 문을 포함하는 코드 블록입니다. 프로그램을 통해 메서드를 호출하고 필요한 메서드 인수를 지정하여 문을 실행합니다. C#에서는 실행된 모든 명령이 메서드의 컨텍스트에서 수행됩니다. `Main` 메서드는 모든 C# 애플리케이션의 진입점이고 프로그램이 시작될 때 CLR(공용 언어 런타임)에서 호출됩니다.

> [!NOTE]
> 이 항목에서는 명명된 메서드에 대해 설명합니다. 익명 함수에 대한 자세한 내용은 [익명 함수](programming-guide/statements-expressions-operators/anonymous-functions.md)를 참조하세요.

이 항목에는 다음과 같은 단원이 포함되어 있습니다.

- [메서드 시그니처](#signatures)
- [메서드 호출](#invocation)
- [상속 및 재정의된 메서드](#inherited)
- [매개 변수 전달](#passing)
  - [값으로 매개 변수 전달](#byval)
  - [참조로 매개 변수 전달](#byref)
  - [매개 변수 배열](#paramarray)
- [선택적 매개 변수 및 인수](#optional)
- [반환 값](#return)
- [확장 메서드](#extension)
- [비동기 메서드](#async)
- [식 본문 멤버](#expr)
- [반복기](#iterators)

<a name="signatures"></a>

## <a name="method-signatures"></a>메서드 시그니처

메서드는 다음을 지정하여 `class` 또는 `struct`에서 선언됩니다.

- `public` 또는 `private`와 같은 선택적 액세스 수준입니다. 기본값은 `private`입니다.
- `abstract` 또는 `sealed`와 같은 선택적 한정자입니다.
- 반환 값 또는 메서드에 반환 값이 없는 경우 `void`입니다.
- 메서드 이름입니다.
- 메서드 매개 변수입니다. 메서드 매개 변수는 괄호로 묶고 쉼표로 구분합니다. 빈 괄호는 메서드에 매개 변수가 필요하지 않음을 나타냅니다.

이러한 부분이 결합되어 메서드 시그니처를 구성합니다.

> [!NOTE]
> 메서드의 반환 값은 메서드 오버로드를 위한 메서드 서명의 부분이 아닙니다. 그러나 대리자와 대리자가 가리키는 메서드 간의 호환성을 결정할 경우에는 메서드 서명의 부분입니다.

다음 예제에서는 다섯 개의 메서드를 포함하는 `Motorcycle`이라는 클래스를 정의합니다.

[!code-csharp[csSnippets.Methods#40](../../samples/snippets/csharp/concepts/methods/methods40.cs#40)]

`Motorcycle` 클래스에는 오버로드된 메서드 `Drive`가 있습니다. 두 메서드는 이름이 같지만 해당 매개 변수 형식으로 구별되어야 합니다.

<a name="invocation"></a>

## <a name="method-invocation"></a>메서드 호출

메서드는 *인스턴스* 또는 *정적*일 수 있습니다. 인스턴스 메서드를 호출하려면 개체를 인스턴스화하고 해당 개체에서 메서드를 호출해야 합니다. 인스턴스 메서드는 인스턴스 및 해당 데이터에 대해 작동합니다. 메서드가 속하는 형식의 이름을 참조하여 정적 메서드를 호출합니다. 정적 메서드는 인스턴스 데이터에 대해 작동하지 않습니다. 개체 인스턴스를 통해 정적 메서드를 호출하려고 하면 컴파일러 오류가 생성됩니다.

메서드 호출은 필드 액세스와 비슷합니다. 개체 이름(인스턴스 메서드를 호출하는 경우) 또는 형식 이름(`static` 메서드를 호출하는 경우) 뒤에 마침표, 메서드 이름 및 괄호를 추가합니다. 인수는 괄호 안에 나열되고 쉼표로 구분합니다.

메서드 정의는 필요한 모든 매개 변수의 이름 및 형식을 지정합니다. 호출자는 메서드를 호출할 때 각 매개 변수에 대해 인수라는 구체적인 값을 제공합니다. 인수는 매개 변수 형식과 호환되어야 하지만 인수 이름(호출하는 코드에 사용된 경우)은 메서드에 정의된 명명된 매개 변수와 동일할 필요가 없습니다. 다음 예제에서는 `Square` 메서드에 *i*라는 `int` 형식의 단일 매개 변수가 포함되어 있습니다. 첫 번째 메서드 호출은 `Square` 메서드에 *num*이라는 `int` 형식의 변수를 전달합니다. 두 번째 호출은 숫자 상수, 세 번째 호출은 식을 전달합니다.

[!code-csharp[csSnippets.Methods#74](../../samples/snippets/csharp/concepts/methods/params74.cs#74)]

가장 일반적인 형태의 메서드 호출은 위치 인수를 사용하며, 메서드 매개 변수와 동일한 순서로 인수를 제공합니다. `Motorcycle` 클래스의 메서드는 다음 예제와 같이 호출될 수 있습니다. 예를 들어 `Drive` 메서드 호출에는 메서드 구문의 두 매개 변수에 해당하는 두 개의 인수가 포함되어 있습니다. 첫 번째 인수는 `miles` 매개 변수의 값이 되고, 두 번째 인수는 `speed` 매개 변수의 값이 됩니다.

[!code-csharp[csSnippets.Methods#41](../../samples/snippets/csharp/concepts/methods/methods40.cs#41)]

메서드를 호출할 때 위치 인수 대신 *명명된 인수*를 사용할 수도 있습니다. 명명된 인수를 사용하는 경우 매개 변수 이름 뒤에 콜론(":")과 인수를 지정합니다. 모든 필수 인수가 있기만 하면 메서드의 인수 순서는 중요하지 않습니다. 다음 예제에서는 명명된 인수를 사용하여 `TestMotorcycle.Drive` 메서드를 호출합니다. 이 예제에서는 명명된 인수가 메서드의 매개 변수 목록과 반대 순서로 전달됩니다.

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/named1.cs#45)]

위치 인수와 명명된 인수 둘 다를 사용하여 메서드를 호출할 수 있습니다. 그러나 위치 인수는 명명된 인수 다음에 올 수 없습니다. 다음 예제에서는 위치 인수 하나와 명명된 인수 하나를 사용하여 이전 예제의 `TestMotorcycle.Drive` 메서드를 호출합니다.

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/named2.cs#46)]

<a name="inherited"></a>

## <a name="inherited-and-overridden-methods"></a>상속 및 재정의된 메서드

형식은 해당 형식에서 명시적으로 정의된 멤버 외에도 기본 클래스에서 정의된 멤버를 상속합니다. 관리되는 형식 시스템의 모든 형식이 직접 또는 간접적으로 <xref:System.Object> 클래스에서 상속하므로 모든 형식은 <xref:System.Object.Equals(System.Object)>, <xref:System.Object.GetType> 및 <xref:System.Object.ToString>과 같은 해당 멤버를 상속합니다. 다음 예제에서는 `Person` 클래스를 정의하고, 두 개의 `Person` 개체를 인스턴스화하고, `Person.Equals` 메서드를 호출하여 두 개체가 같은지 여부를 확인합니다. 그러나 `Equals` 메서드는 `Person` 클래스에서 정의되지 않고 <xref:System.Object>에서 상속됩니다.

[!code-csharp[csSnippets.Methods#104](../../samples/snippets/csharp/concepts/methods/inherited1.cs#104)]

형식은 `override` 키워드를 사용하고 재정의된 메서드에 대한 구현을 제공하여 상속된 멤버를 재정의할 수 있습니다. 메서드 시그니처는 재정의된 메서드의 시그니처와 같아야 합니다. 다음 예제는 <xref:System.Object.Equals(System.Object)> 메서드를 재정의한다는 점을 제외하고 이전 예제와 비슷합니다. 또한 두 메서드가 일치하는 결과를 제공하기 때문에 <xref:System.Object.GetHashCode> 메서드를 재정의합니다.

[!code-csharp[csSnippets.Methods#105](../../samples/snippets/csharp/concepts/methods/overridden1.cs#105)]

<a name="passing"></a>

## <a name="passing-parameters"></a>매개 변수 전달

C#의 형식은 *값 형식* 또는 *참조 형식*입니다. 기본 제공 값 형식 목록을 보려면 [형식 및 변수](./tour-of-csharp/types-and-variables.md)를 참조하세요. 기본적으로, 값 형식과 참조 형식은 둘 다 값으로 메서드에 전달됩니다.

<a name="byval"></a>

### <a name="passing-parameters-by-value"></a>값으로 매개 변수 전달

값 형식이 값으로 메서드에 전달되는 경우 개체 자체가 아니라 개체의 복사본이 메서드에 전달됩니다. 따라서 제어가 호출자로 반환될 때 호출된 메서드의 개체 변경 내용은 원래 개체에 영향을 주지 않습니다.

다음 예제에서는 값 형식을 값으로 메서드에 전달하며, 호출된 메서드는 값 형식의 값을 변경하려고 합니다. 값 형식인 `int` 형식의 변수를 정의하고, 해당 값을 20으로 초기화한 다음 `ModifyValue`라는 메서드에 전달하면 이 메서드가 변수의 값을 30으로 변경합니다. 그러나 메서드가 반환될 때는 변수의 값이 변경되지 않습니다.

[!code-csharp[csSnippets.Methods#10](../../samples/snippets/csharp/concepts/methods/byvalue10.cs#10)]

참조 형식의 개체가 메서드에 값으로 전달되는 경우 개체에 대한 참조가 값으로 전달됩니다. 즉, 메서드는 개체 자체가 아니라 개체의 위치를 나타내는 인수를 수신합니다. 이 참조를 사용하여 개체의 멤버를 변경하는 경우 제어가 호출하는 메서드로 반환될 때 변경 내용이 개체에 반영됩니다. 그러나 메서드에 전달되는 개체를 바꾸면 제어가 호출자로 반환될 때 원래 개체에 영향을 주지 않습니다.

다음 예제에서는 `SampleRefType`이라는 클래스(참조 형식)를 정의합니다. `SampleRefType` 개체를 인스턴스화하고, 해당 `value` 필드에 44를 할당한 다음 개체를 `ModifyObject` 메서드에 전달합니다. 이 예제는 인수를 값으로 메서드에 전달한다는 점에서 기본적으로 이전 예제와 같은 작업을 수행합니다. 그러나 참조 형식이 사용되므로 결과가 다릅니다. 예제의 출력과 같이 `ModifyObject`에서 `obj.value` 필드에 대해 수정한 내용으로 인해 `Main` 메서드에서 `rt` 인수의 `value` 필드도 33으로 변경됩니다.

[!code-csharp[csSnippets.Methods#42](../../samples/snippets/csharp/concepts/methods/byvalue42.cs#42)]

<a name="byref"></a>

### <a name="passing-parameters-by-reference"></a>참조로 매개 변수 전달

메서드의 인수 값을 변경하고 제어가 호출하는 메서드로 반환될 때 해당 변경 내용을 반영하려는 경우 참조로 매개 변수를 전달합니다. 참조로 매개 변수를 전달하려면 [`ref`](language-reference/keywords/ref.md) 또는 [`out`](language-reference/keywords/out-parameter-modifier.md) 키워드를 사용합니다. 복사를 방지하지만 여전히 [`in`](language-reference/keywords/in-parameter-modifier.md) 키워드를 사용하여 수정을 방지하도록 참조로 값을 전달할 수도 있습니다.

다음 예제는 값이 참조로 `ModifyValue` 메서드에 전달된다는 점을 제외하고 이전 예제와 동일합니다. `ModifyValue` 메서드에서 매개 변수의 값을 수정하면 제어가 호출자로 반환될 때 값의 변경 내용이 반영됩니다.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/byref106.cs#106)]

by ref 매개 변수를 사용하는 일반적인 패턴은 변수 값의 교환을 포함합니다. 두 개의 변수를 참조로 메서드에 전달하고 메서드가 해당 내용을 바꿉니다. 다음 예제에서는 정수 값을 바꿉니다.

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/swap107.cs#107)]

참조 형식 매개 변수를 전달하면 해당 개별 요소 또는 필드의 값이 아니라 참조 자체의 값을 변경할 수 있습니다.

<a name="paramarray"></a>

### <a name="parameter-arrays"></a>매개 변수 배열

경우에 따라 메서드의 인수 개수를 정확하게 지정하라는 요구 사항은 제한적입니다. `params` 키워드를 사용하여 매개 변수를 매개 변수 배열로 지정하면 가변 개수의 인수로 메서드를 호출할 수 있습니다. `params` 키워드로 태그가 지정된 매개 변수는 배열 형식이어야 하며, 메서드의 매개 변수 목록에서 마지막 매개 변수여야 합니다.

그러면 호출자가 다음 세 가지 방법 중 하나로 메서드를 호출할 수 있습니다.

- 원하는 개수의 요소를 포함하는 적절한 형식의 배열 전달
- 적절한 형식의 개별 인수가 포함된 쉼표로 구분된 목록을 메서드에 전달
- 매개 변수 배열에 인수 제공 안 함

다음 예제에서는 매개 변수 배열의 모든 모음을 반환하는 `GetVowels` 메서드를 정의합니다. `Main` 메서드는 해당 메서드를 호출하는 세 가지 방법을 모두 보여 줍니다. 호출자가 `params` 한정자를 포함하는 매개 변수의 인수를 제공할 필요는 없습니다. 이 경우 매개 변수는 `null`입니다.

[!code-csharp[csSnippets.Methods#75](~/samples/snippets/csharp/concepts/methods/params75.cs#75)]

<a name="optional"></a>

## <a name="optional-parameters-and-arguments"></a>선택적 매개 변수 및 인수

메서드 정의에서 해당 매개 변수를 필수 또는 선택 사항으로 지정할 수 있습니다. 기본적으로 매개 변수는 필수입니다. 선택적 매개 변수는 메서드 정의에 매개 변수의 기본값을 포함하여 지정됩니다. 메서드를 호출할 때 선택적 매개 변수에 대한 인수가 제공되지 않은 경우 기본값이 대신 사용됩니다.

다음 종류의 식 중 하나로 매개 변수의 기본값을 할당해야 합니다.

- 리터럴 문자열이나 숫자와 같은 상수
- `new ValType` 형태의 식. 여기서 `ValType`은 값 형식입니다. 이 경우 형식의 실제 멤버가 아닌 값 형식의 매개 변수가 없는 암시적 생성자가 호출됩니다.
- `default(ValType)` 형태의 식. 여기서 `ValType`은 값 형식입니다.

메서드에 필수 및 선택적 매개 변수가 둘 다 포함된 경우 선택적 매개 변수는 매개 변수 목록의 끝에서 모든 필수 매개 변수 다음에 정의됩니다.

다음 예제에서는 필수 매개 변수 하나와 선택적 매개 변수 두 개가 있는 `ExampleMethod` 메서드를 정의합니다.

[!code-csharp[csSnippets.Methods#21](../../samples/snippets/csharp/concepts/methods/optional1.cs#21)]

여러 선택적 인수가 있는 메서드를 위치 인수로 호출하는 경우 호출자가 첫 번째 매개 변수부터 인수가 제공되는 마지막 매개 변수까지 모든 선택적 매개 변수에 대한 인수를 제공해야 합니다. 예를 들어 `ExampleMethod` 메서드에서 호출자가 `description` 매개 변수에 대한 인수를 제공하는 경우 `optionalInt` 매개 변수에 대한 인수도 제공해야 합니다. `opt.ExampleMethod(2, 2, "Addition of 2 and 2");`는 유효한 메서드 호출이고, `opt.ExampleMethod(2, , "Addition of 2 and 0");`은 "인수가 없습니다." 컴파일러 오류를 생성합니다.

명명된 인수 또는 위치 인수와 명명된 인수의 조합을 사용하여 메서드를 호출하는 경우 호출자는 메서드 호출에서 마지막 위치 인수 뒤에 오는 모든 인수를 생략할 수 있습니다.

다음 예제에서는 `ExampleMethod` 메서드를 세 번 호출합니다.  처음 두 메서드 호출은 위치 인수를 사용합니다. 첫 번째 호출은 선택적 인수를 둘 다 생략하고, 두 번째 호출은 마지막 인수를 생략합니다. 세 번째 메서드 호출은 필수 매개 변수에 대한 위치 인수를 제공하지만 `optionalInt` 인수를 생략하고 명명된 인수를 사용하여 `description` 매개 변수에 값을 제공합니다.

[!code-csharp[csSnippets.Methods#22](../../samples/snippets/csharp/concepts/methods/optional1.cs#22)]

선택적 매개 변수를 사용하면 *오버로드 확인* 또는 C# 컴파일러가 메서드 호출에서 호출해야 하는 특정 오버로드를 확인하는 방법이 다음과 같이 영향을 받습니다.

- 메서드, 인덱서 또는 생성자는 해당 매개 변수가 각각 선택 사항이거나 이름 또는 위치로 호출하는 문의 단일 인수에 해당하고 이 인수를 매개 변수의 형식으로 변환할 수 있는 경우 실행 후보가 됩니다.
- 둘 이상의 인증서가 있으면 기본 설정 변환에 대한 오버로드 확인 규칙이 명시적으로 지정된 인수에 적용됩니다. 선택적 매개 변수에 대해 생략된 인수는 무시됩니다.
- 두 후보가 똑같이 정상이라고 판단되는 경우 기본적으로 호출에서 인수가 생략된 선택적 매개 변수가 없는 후보가 설정됩니다. 이는 매개 변수가 적은 후보에 대한 오버로드 확인에서 일반적인 기본 설정의 결과입니다.

<a name="return"></a>

## <a name="return-values"></a>반환 값

메서드는 호출자에 값을 반환할 수 있습니다. 메서드 이름 앞에 나열된 반환 형식이 `void`가 아니면 메서드는 `return` 키워드를 사용하여 값을 반환할 수 있습니다. `return` 키워드에 이어 반환 형식과 일치하는 변수, 상수 또는 식을 포함하는 문은 메서드 호출자에 값을 반환합니다. `return` 키워드를 사용하여 값을 반환하려면 void가 아닌 반환 값을 포함한 메서드가 필요합니다. `return` 키워드는 메서드 실행을 중지합니다.

반환 형식이 `void`이면 값이 없는 `return` 문을 사용하여 메서드 실행을 중지할 수 있습니다. `return` 키워드를 사용하지 않으면 메서드는 코드 블록 끝에 도달할 때 실행을 중지합니다.

예를 들어 이들 두 메서드에서는 `return` 키워드를 사용하여 정수를 반환합니다.

[!code-csharp[csSnippets.Methods#44](../../samples/snippets/csharp/concepts/methods/return44.cs#44)]

메서드에서 반환된 값을 사용하려면 호출하는 메서드에서 같은 형식의 값으로 충분한 모든 경우에 메서드 호출 자체를 사용하면 됩니다. 반환 값을 변수에 할당할 수도 있습니다. 예를 들어 다음 두 코드 예제에서는 같은 목표를 달성합니다.

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/return44.cs#45)]

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/return44.cs#46)]

지역 변수(이 경우 `result`)를 사용하여 값을 저장하는 것은 선택 사항입니다. 코드의 가독성에 도움이 될 수 있고 전체 메서드 범위에 대해 인수의 원래 값을 저장해야 할 경우 필요할 수도 있습니다.

메서드에서 둘 이상의 값을 반환하려는 경우도 있습니다. C# 7.0부터 *튜플 형식* 및 *튜플 리터럴*을 사용하면 이 작업을 쉽게 수행할 수 있습니다. 튜플 형식은 튜플 요소의 데이터 형식을 정의합니다. 튜플 리터럴은 반환된 튜플의 실제 값을 제공합니다. 다음 예제에서 `(string, string, string, int)`는 `GetPersonalInfo` 메서드에서 반환되는 튜플 형식을 정의합니다. `(per.FirstName, per.MiddleName, per.LastName, per.Age)` 식은 튜플 리터럴입니다. 메서드는 `PersonInfo` 개체와 함께 이름, 중간 이름 및 성을 반환합니다.

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

호출자는 반환된 튜플을 코드에서 다음과 같이 사용할 수 있습니다.

```csharp
var person = GetPersonalInfo("111111111")
Console.WriteLine("{person.Item1} {person.Item3}: age = {person.Item4}");
```

튜플 형식 정의의 튜플 요소에 이름을 할당할 수도 있습니다. 다음 예제에서는 명명된 요소를 사용하는 `GetPersonalInfo` 메서드의 대체 버전을 보여 줍니다.

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

`GetPersonInfo` 메서드에 대한 이전 호출을 다음과 같이 수정할 수 있습니다.

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine("{person.FName} {person.LName}: age = {person.Age}");
```

메서드에 배열이 인수로 전달되고 메서드가 개별 요소의 값을 수정하는 경우 값의 스타일 또는 기능 흐름 개선을 위해 메서드에서 배열을 반환하도록 선택할 수도 있지만 필수는 아닙니다.  이는 C#에서 모든 참조 형식을 값으로 전달하고 배열 참조의 값이 배열에 대한 포인터이기 때문입니다. 다음 예제에서는 `DoubleValues` 메서드에서 수행한 `values` 배열 내용의 변경 사항을 배열에 대한 참조가 있는 모든 코드에서 관찰할 수 있습니다.

[!code-csharp[csSnippets.Methods#101](../../samples/snippets/csharp/concepts/methods/returnarray1.cs#101)]

<a name="extension"></a>

## <a name="extension-methods"></a>확장 메서드

일반적으로 기존 형식에 메서드를 추가하는 방법에는 다음 두 가지가 있습니다.

- 해당 형식에 대한 소스 코드를 수정합니다. 물론, 형식의 소스 코드를 소유하지 않은 경우에는 이 작업을 수행할 수 없습니다. 이는 메서드를 지원하기 위해 전용 데이터 필드를 추가하는 경우에도 주요 변경 내용이 됩니다.
- 파생 클래스에서 새 메서드를 정의합니다. 구조체, 열거형 등의 다른 형식에 대해 상속을 사용하여 이러한 방식으로 메서드를 추가할 수는 없습니다. 봉인 클래스에 메서드를 "추가"하는 데 사용할 수도 없습니다.

확장 메서드를 사용하면 형식 자체를 수정하거나 상속된 형식에서 새 메서드를 구현하지 않고 기존 형식에 메서드를 "추가"할 수 있습니다. 또한 확장 메서드는 확장하는 형식과 동일한 어셈블리에 있지 않아도 됩니다. 형식의 정의된 멤버인 것처럼 확장 메서드를 호출합니다.

자세한 내용은 [확장 메서드](programming-guide/classes-and-structs/extension-methods.md)를 참조하세요.

<a name="async"></a>

## <a name="async-methods"></a>비동기 메서드

비동기 기능을 사용하면 명시적 콜백을 사용하거나 수동으로 여러 메서드 또는 람다 식에 코드를 분할하지 않고도 비동기 메서드를 호출할 수 있습니다.

메서드에 [async](language-reference/keywords/async.md) 한정자를 표시하면 메서드에서 [await](language-reference/operators/await.md) 연산자를 사용할 수 있습니다. 제어가 비동기 메서드의 `await` 식에 도달하면 대기된 작업이 완료되지 않은 경우 제어가 호출자로 반환되고, 대기된 작업이 완료될 때까지 `await` 키워드가 있는 메서드의 진행이 일시 중단됩니다. 작업이 완료되면 메서드가 실행이 다시 시작될 수 있습니다.

> [!NOTE]
> 비동기 메서드는 아직 완료되지 않은 첫 번째 대기된 개체를 검색할 때나 비동기 메서드의 끝에 도달할 때 중에서 먼저 발생하는 시점에 호출자에게 반환됩니다.

비동기 메서드의 반환 형식은 <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task> 또는 `void`일 수 있습니다. `void` 반환 형식은 기본적으로 `void` 반환 형식이 필요할 때 이벤트 처리기를 정의하는 데 사용됩니다. `void`를 반환하는 비동기 메서드는 대기할 수 없고 void를 반환하는 메서드의 호출자는 메서드가 throw하는 예외를 catch할 수 없습니다. C# 7.0부터 비동기 메서드에는 [작업과 유사한 반환 형식](./whats-new/csharp-7.md#generalized-async-return-types)이 있을 수 있습니다.

다음 예제에서 `DelayAsync`는 정수를 반환하는 return 문을 포함하는 비동기 메서드입니다. 비동기 메서드이기 때문에 해당 메서드 선언의 반환 형식은 `Task<int>`여야 합니다. 반환 형식이 `Task<int>`이므로 `DoSomethingAsync`의 `await` 식 계산에서 다음 `int result = await delayTask` 문과 같이 정수가 생성됩니다.

[!code-csharp[csSnippets.Methods#102](../../samples/snippets/csharp/concepts/methods/async1.cs#102)]

비동기 메서드는 모든 [in](language-reference/keywords/in-parameter-modifier.md), [ref](language-reference/keywords/ref.md) 또는 [out](language-reference/keywords/out-parameter-modifier.md) 매개 변수를 선언할 수 없지만, 이러한 매개 변수가 있는 메서드를 호출할 수는 있습니다.

 비동기 메서드에 대한 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](async.md), [비동기 프로그램의 제어 흐름](programming-guide/concepts/async/control-flow-in-async-programs.md) 및 [비동기 반환 형식](programming-guide/concepts/async/async-return-types.md)을 참조하세요.

<a name="expr"></a>

## <a name="expression-bodied-members"></a>식 본문 멤버

일반적으로 식의 결과와 함께 바로 반환되거나 단일 문이 메서드 본문으로 포함된 메서드 정의가 있습니다.  `=>`를 사용하여 해당 메서드를 속성을 정의하기 위한 구문 바로 가기는 다음과 같습니다.

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

메서드가 `void`를 반환하거나 비동기 메서드이면 메서드 본문은 문 식이어야 합니다(람다에서와 같음).  속성 및 인덱서의 경우 읽기 전용이어야 하며, `get` 접근자 키워드를 사용하지 않습니다.

<a name="iterators"></a>

## <a name="iterators"></a>반복기

반복기는 배열 목록과 같은 컬렉션에 대해 사용자 지정 반복을 수행합니다. 반복기는 [yield return](language-reference/keywords/yield.md) 문을 사용하여 각 요소를 한 번에 하나씩 반환합니다. `yield return` 문에 도달하면 호출자가 시퀀스의 다음 요소를 요청할 수 있도록 현재 위치가 기억됩니다.

반복기의 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>또는 <xref:System.Collections.Generic.IEnumerator%601>일 수 있습니다.

자세한 내용은 [반복기](programming-guide/concepts/iterators.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [액세스 한정자](language-reference/keywords/access-modifiers.md)
- [정적 클래스 및 정적 클래스 멤버](programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [상속](programming-guide/classes-and-structs/inheritance.md)
- [추상/봉인된 클래스 및 클래스 멤버](programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [params](language-reference/keywords/params.md)
- [out](language-reference/keywords/out-parameter-modifier.md)
- [ref](language-reference/keywords/ref.md)
- [in](language-reference/keywords/in-parameter-modifier.md)
- [매개 변수 전달](programming-guide/classes-and-structs/passing-parameters.md)
