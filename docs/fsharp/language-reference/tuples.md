---
title: 튜플
description: 다른 형식의 명명 F# 되지 않은 정렬 된 값의 그룹인 튜플에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 7a15d7e0c6c9b42118dd75066f02cbb2e05335fc
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630232"
---
# <a name="tuples"></a>튜플

*튜플은* 다른 형식의 명명 되지 않은 정렬 된 값을 그룹화 한 것입니다.  튜플은 참조 형식 또는 구조체 일 수 있습니다.

## <a name="syntax"></a>구문

```fsharp
(element, ... , element)
struct(element, ... ,element )
```

## <a name="remarks"></a>설명

위의 구문에서 각 *요소* 는 유효한 F# 식일 수 있습니다.

## <a name="examples"></a>예

튜플의 예로는 같거나 다른 형식의 쌍, 삼중 쌍 등이 있습니다. 다음 코드에서는 몇 가지 예를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L6-L21)]

## <a name="obtaining-individual-values"></a>개별 값 가져오기

다음 코드와 같이 패턴 일치를 사용 하 여 튜플 요소의 이름에 액세스 하 고 해당 이름을 할당할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L27-L29)]

바인딩을 통해 `match` `let` 식 외부의 패턴 일치를 통해 튜플을 분해할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L34-L37)]

또는 튜플에서 함수에 대 한 입력으로 일치를 패턴으로 지정할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L43-L47)]

튜플의 요소가 하나만 필요한 경우에는 필요 하지 않은 값에 대 한 새 이름을 만드는 것을 방지 하기 위해 와일드 카드 문자 (밑줄)를 사용할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L53-L54)]

참조 튜플에 있는 요소를 구조체 튜플로 복사 하는 것도 간단 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L62-L66)]

`fst` 함수와`snd` (참조 튜플을 해당)는 각각 튜플의 첫 번째 및 두 번째 요소를 반환 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L72-L73)]

삼중의 세 번째 요소를 반환 하는 기본 제공 함수는 없지만 다음과 같이 간단 하 게 작성할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L78-L78)]

일반적으로 패턴 일치를 사용 하 여 개별 튜플 요소에 액세스 하는 것이 좋습니다.

## <a name="using-tuples"></a>튜플 사용

튜플은 다음 예제와 같이 함수에서 여러 값을 반환 하는 편리한 방법을 제공 합니다. 이 예에서는 정수 나누기를 수행 하 고 작업의 반올림 된 결과를 튜플 쌍의 첫 번째 멤버로 반환 하 고 나머지는 쌍의 두 번째 멤버로 반환 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L83-L86)]

일반적인 함수 구문에서 암시 하는 함수 인수의 암시적 currying을 방지 하려는 경우 튜플을 함수 인수로 사용할 수도 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L88-L88)]

함수 `let sum a b = a + b` 를 정의 하기 위한 일반적인 구문을 사용 하면 다음 코드와 같이 함수의 첫 번째 인수에 대 한 부분 응용 프로그램용 함수를 정의할 수 있습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/basic-examples.fsx#L90-L94)]

튜플을 매개 변수로 사용 하면 currying가 사용 되지 않습니다. 자세한 내용은 [함수](./functions/index.md)에서 "인수 부분 적용"을 참조 하세요.

## <a name="names-of-tuple-types"></a>튜플 형식의 이름

튜플 형식의 이름을 작성 하는 경우 `*` 기호를 사용 하 여 요소를 구분 합니다. `int` ,`float` 및`(10, 10.0, "ten")`와 같이로구성된튜플의경우형식은다음과같이작성됩니다.`string`

```fsharp
int * float * string
```

## <a name="interoperation-with-c-tuples"></a>튜플을 사용 C# 하 여 상호 운용

C#7.0는 언어에 튜플을 도입 했습니다.  의 C# 튜플은 구조체 이며의 F#구조체 튜플에 해당 합니다.  와 C#상호 운용 해야 하는 경우 구조체 튜플을 사용 해야 합니다.

이렇게 하는 것이 쉽습니다.  예를 들어 튜플을 C# 클래스에 전달한 다음 그 결과를 사용 해야 한다고 가정 합니다.

```csharp
namespace CSharpTupleInterop
{
    public static class Example
    {
        public static (int, int) AddOneToXAndY((int x, int y) a) =>
            (a.x + 1, a.y + 1);
    }
}
```

그런 다음 F# 코드에서 구조체 튜플을 매개 변수로 전달 하 고 결과를 구조체 튜플로 사용할 수 있습니다.

```fsharp
open TupleInterop

let struct (newX, newY) = Example.AddOneToXAndY(struct (1, 2))
// newX is now 2, and newY is now 3
```

### <a name="converting-between-reference-tuples-and-struct-tuples"></a>참조 튜플 및 구조체 튜플 간 변환

참조 튜플 및 구조체 튜플의 기본 표현은 완전히 다르므로 암시적으로 변환할 수 없습니다.  즉, 다음과 같은 코드는 컴파일되지 않습니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/interop.fsx#L5-L12)]

하나의 튜플에 패턴 일치를 사용 하 고 구성 요소를 사용 하 여 다른 튜플을 생성 해야 합니다.  예를 들어:

[!code-fsharp[Main](~/samples/snippets/fsharp/tuples/interop.fsx#L18-L22)]

## <a name="compiled-form-of-reference-tuples"></a>참조 튜플의 컴파일된 형태

이 섹션에서는 컴파일될 때 튜플의 형태에 대해 설명 합니다.  .NET Framework 3.5를 대상으로 하지 않는 한이 정보는 읽을 필요가 없습니다.

튜플은 인자 수에서 오버 로드 된 여러 제네릭 형식 `System.Tuple`중 하나의 개체 또는 형식 매개 변수의 수로 컴파일됩니다. 튜플 형식은 C# 또는 Visual Basic 같은 다른 언어에서 볼 때 또는 F# 구문을 인식 하지 않는 도구를 사용 하는 경우이 형식으로 표시 됩니다. `Tuple` 형식은 .NET Framework 4에서 도입 되었습니다. .NET Framework의 이전 버전을 대상으로 하는 경우 컴파일러는 F# 핵심 라이브러리의 2.0 [버전에서 사용](https://msdn.microsoft.com/library/5ac7953d-acdc-4a58-bfb7-c1f6406c0fa3) 하는 system.string 버전을 사용 합니다. 이 라이브러리의 형식은 .NET Framework의 2.0, 3.0 및 3.5 버전을 대상으로 하는 응용 프로그램에만 사용 됩니다. 유형 전달은 .NET Framework 2.0 및 .NET Framework 4 F# 구성 요소 간의 이진 호환성을 보장 하는 데 사용 됩니다.

### <a name="compiled-form-of-struct-tuples"></a>구조체 튜플의 컴파일된 형태

구조체 튜플 (예: `struct (x, y)`)은 기본적으로 참조 튜플과 다릅니다.  이러한 매개 변수는 인자 <xref:System.ValueTuple> 수로 오버 로드 된 형식 또는 형식 매개 변수 수로 컴파일됩니다.  7\.0 튜플 및 [Visual Basic 2017 튜플](../../visual-basic/programming-guide/language-features/data-types/tuples.md)및 상호 운용 양방향으로와 동일 합니다. [ C# ](../../csharp/tuples.md)

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
- [F# 형식](fsharp-types.md)
