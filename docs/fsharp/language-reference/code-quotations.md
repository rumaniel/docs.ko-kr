---
title: 코드 인용
description: 프로그래밍 방식 F# 으로 F# 코드 식을 생성 하 고 사용할 수 있도록 하는 언어 기능인 코드 인용에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: c6ec0078c685a6452f49edd289b01491dd62e3db
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630422"
---
# <a name="code-quotations"></a>코드 인용

> [!NOTE]
> API 참조 링크를 통해 MSDN으로 이동됩니다.  docs.microsoft.com API 참조가 완전하지 않습니다.

이 항목에서는 프로그래밍 방식으로 F# 코드 식을 생성 하 고 사용할 수 있도록 하는 언어 기능인 *코드 인용*에 대해 설명 합니다. 이 기능을 사용 하면 코드를 나타내는 F# 추상 구문 트리를 생성할 수 있습니다. 그런 다음 응용 프로그램의 필요에 따라 추상 구문 트리를 트래버스 하 고 처리할 수 있습니다. 예를 들어 트리를 사용 하 여 코드를 F# 생성 하거나 다른 언어로 코드를 생성할 수 있습니다.

## <a name="quoted-expressions"></a>따옴표 붙은 식

*따옴표 붙은 식은* 프로그램의 F# 일부로 컴파일되지 않고 F# 식을 나타내는 개체로 컴파일되는 방식으로 구분 되는 코드의 식입니다 (예: 다음 두 가지 방법 중 하나를 사용 하 여 따옴표 붙은 식을 표시할 수 있습니다. 형식 정보를 사용 하거나 형식 정보를 포함 하지 않습니다. 형식 정보를 포함 하려는 경우 기호 `<@` `@>` 를 사용 하 여 따옴표 붙은 식을 구분 합니다. 형식 정보가 필요 하지 않은 경우에는 기호와 `<@@` `@@>`를 사용 합니다. 다음 코드는 형식화 된 및 형식화 되지 않은 따옴표를 보여 줍니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet501.fs)]

형식 정보를 포함 하지 않는 경우에는 긴 식 트리를 더 빠르게 트래버스할 수 있습니다. 형식화 된 기호로 묶은 식의 결과 형식은입니다. 여기서 형식 `Expr<'T>`매개 변수는 F# 컴파일러의 형식 유추 알고리즘에 의해 결정 된 식의 형식입니다. 형식 정보 없이 코드 따옴표를 사용 하는 경우 따옴표 붙은 식의 형식은 제네릭이 아닌 형식 [Expr](https://msdn.microsoft.com/library/ed6a2caf-69d4-45c2-ab97-e9b3be9bce65)입니다. 형식화된 클래스에대해 [Raw](https://msdn.microsoft.com/library/47fb94f1-e77f-4c68-aabc-2b0ba40d59c2) 속성을 호출하여 `Expr`형식화되지 않은 개체`Expr`를 가져올 수 있습니다.

따옴표로 묶은 식을 사용 하지 않고 F# `Expr` 클래스에서 프로그래밍 방식으로 식 개체를 생성할 수 있도록 하는 다양 한 정적 메서드가 있습니다.

코드 인용에는 전체 식이 포함 되어야 합니다. 예를 들어 바인딩의 경우 바인딩 이름 및 바인딩을 사용 하는 추가 식의 정의가 모두 필요 합니다. `let` 자세한 구문에서 `in` 키워드 뒤에 오는 식입니다. 모듈의 최상위 수준에서이는 모듈의 다음 식일 뿐 아니라 따옴표 안에 명시적으로 필요 합니다.

따라서 다음 식은 유효 하지 않습니다.

```fsharp
// Not valid:
// <@ let f x = x + 1 @>
```

그러나 다음 식은 유효 합니다.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet502.fs)]

따옴표를 F# 계산 하려면 [따옴표 계산기를 사용 해야 합니다. F# ](https://github.com/fsprojects/FSharp.Quotations.Evaluator) 식 개체를 평가 하 고 실행 F# 하는 기능을 지원 합니다.

## <a name="expr-type"></a>Expr 형식

`Expr` 형식의 인스턴스는 F# 식을 나타냅니다. 제네릭 형식과 제네릭이 `Expr` 아닌 형식은 모두 F# 라이브러리 설명서에 설명 되어 있습니다. 자세한 내용은 [Fsharp.core 네임 스페이스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.quotations-namespace-%5bfsharp%5d) 및 [인용구 클래스](https://msdn.microsoft.com/visualfsharpdocs/conceptual/quotations.expr-class-%5bfsharp%5d)를 참조 하세요.

## <a name="splicing-operators"></a>스플라이스 연산자

스플라이스를 사용 하면 프로그래밍 방식으로 또는 다른 코드 인용에서 만든 식과 리터럴 코드 따옴표를 결합할 수 있습니다. 및 연산자를 사용 하 여 코드 인용 F# 에 식 개체를 추가할 수 있습니다. `%%` `%` `%` 연산자를 사용 하 여 형식화 된 식 개체를 형식화 된 따옴표로 삽입 합니다. 연산자를 `%%` 사용 하 여 형식화 되지 않은 식 개체를 형식화 되지 않은 따옴표로 삽입 합니다. 두 연산자는 단항 전위 연산자입니다. 따라서가 `expr` 형식의 `Expr`형식화 되지 않은 식인 경우에는 다음 코드를 사용할 수 있습니다.

```fsharp
<@@ 1 + %%expr @@>
```

가 형식의 `expr` `Expr<int>`형식화 된 인용 인 경우 다음 코드는 유효 합니다.

```fsharp
<@ 1 + %expr @>
```

## <a name="example"></a>예제

### <a name="description"></a>Description

다음 예제에서는 코드 인용을 사용 하 여 코드를 F# 식 개체에 넣은 다음 식을 나타내는 F# 코드를 인쇄 하는 방법을 보여 줍니다. 식 개체 `println` ( `print` 형식`Expr`)를 친숙 한 형식으로 표시 하는 재귀 함수를 포함 하는 함수가 정의 되었습니다. F# [Fsharp.core](https://msdn.microsoft.com/library/093944a9-c752-403a-8983-5fcd5dbf92a4) 및 [fsharp.core](https://msdn.microsoft.com/library/d2434a6e-ae7b-4f3d-b567-c162938bc9cd) 모듈에는 식 개체를 분석 하는 데 사용할 수 있는 여러 가지 활성 패턴이 있습니다. 이 예에는 F# 식에 나타날 수 있는 가능한 모든 패턴이 포함 되지 않습니다. 인식할 수 없는 모든 패턴은 와일드 카드 패턴 (`_`)에 대 한 일치를 트리거하고 `ToString` 메서드를 사용 하 여 렌더링 됩니다 `Expr` .이 메서드를 사용 하면 해당 형식에서 일치 식에 추가할 활성 패턴을 알 수 있습니다.

### <a name="code"></a>코드

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet601.fs)]

### <a name="output"></a>출력

```fsharp
fun (x:System.Int32) -> x + 1
a + 1
let f = fun (x:System.Int32) -> x + 10 in f 10
```

## <a name="example"></a>예제

### <a name="description"></a>Description

[Exprshape.rebuildshapecombination 모듈](https://msdn.microsoft.com/library/7685150e-2432-4d39-9338-57292eff18de) 의 세 가지 활성 패턴을 사용 하 여 활성 패턴이 적을수록 식 트리를 트래버스할 수도 있습니다. 이러한 활성 패턴은 트리를 트래버스 하려고 하지만 대부분의 노드에 모든 정보가 필요 하지 않은 경우에 유용할 수 있습니다. F# 이러한 패턴을 사용 하는 경우 식은 변수가 변수인 경우 `ShapeVar` , `ShapeLambda` 식이 람다 식인 경우 또는 `ShapeCombination` 식이 다른 것 인 경우에는 다음 세 가지 패턴 중 하 나와 일치 합니다. 이전 코드 예제와 같이 활성 패턴을 사용 하 여 식 트리를 트래버스하는 경우에는 더 많은 패턴을 사용 하 여 가능한 F# 모든 식 형식을 처리 해야 합니다. 그러면 코드가 더 복잡해 집니다. 자세한 내용은 [exprshape.rebuildshapecombination. ShapeVar&#124;&#124;ShapeLambda ShapeCombination Active Pattern](https://msdn.microsoft.com/visualfsharpdocs/conceptual/exprshape.shapevarhshapelambdahshapecombination-active-pattern-%5bfsharp%5d)을 참조 하십시오.

다음 코드 예제는 보다 복잡 한 순회를 위한 기준으로 사용할 수 있습니다. 이 코드에서는 함수 호출를 `add`포함 하는 식에 대해 식 트리가 생성 됩니다. [SpecificCall](https://msdn.microsoft.com/library/05a77b21-20fe-4b9a-8e07-aa999538198d) 활성 패턴은 식 트리에서에 대 `add` 한 호출을 검색 하는 데 사용 됩니다. 이 활성 패턴은 호출의 인수를 `exprList` 값에 할당 합니다. 이 경우에는 두 개만 있으므로이를 끌어올 수 있으며 함수는 인수에서 재귀적으로 호출 됩니다. 결과는 splice 연산자 ( `mul` `%%`)를 사용 하 여에 대 한 호출을 나타내는 코드 따옴표로 삽입 됩니다. 이전 `println` 예제의 함수는 결과를 표시 하는 데 사용 됩니다.

다른 활성 패턴 분기의 코드는 동일한 식 트리를 다시 생성 하므로 결과 식의 변경 내용만에서 `add` 로 `mul`변경 됩니다.

### <a name="code"></a>코드

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet701.fs)]

### <a name="output"></a>출력

```fsharp
1 + Module1.add(2,Module1.add(3,4))
1 + Module1.mul(2,Module1.mul(3,4))
```

## <a name="see-also"></a>참고자료

- [F# 언어 참조](index.md)
