---
title: 메서드 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- methods [C#]
- C# language, methods
ms.assetid: cc738f07-e8cd-4683-9585-9f40c0667c37
ms.openlocfilehash: 318f51afefd780ed7be0ab8c2a72acb5fcf9db15
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699974"
---
# <a name="methods-c-programming-guide"></a>메서드(C# 프로그래밍 가이드)

메서드는 일련의 문을 포함하는 코드 블록입니다. 프로그램을 통해 메서드를 호출하고 필요한 메서드 인수를 지정하여 문을 실행합니다. C#에서는 실행된 모든 명령이 메서드의 컨텍스트에서 수행됩니다. `Main` 메서드는 모든 C# 애플리케이션의 진입점이고 프로그램이 시작될 때 CLR(공용 언어 런타임)에서 호출됩니다.

> [!NOTE]
> 이 항목에서는 명명된 메서드에 대해 설명합니다. 익명 함수에 대한 자세한 내용은 [익명 함수](../statements-expressions-operators/anonymous-functions.md)를 참조하세요.

## <a name="method-signatures"></a>메서드 시그니처

메서드는 [클래스](../../language-reference/keywords/class.md) 또는 [구조체](../../language-reference/keywords/struct.md) 에서 `public` 또는 `private`등의 액세스 수준, `abstract` 또는 `sealed`등의 선택적 한정자, 반환 값, 메서드 이름 및 메서드 매개 변수를 지정하여 선언합니다. 이들 파트는 함께 메서드 서명을 구성합니다.

> [!NOTE]
> 메서드의 반환 값은 메서드 오버로드를 위한 메서드 서명의 파트가 아닙니다. 그러나 대리자와 대리자가 가리키는 메서드 간의 호환성을 결정할 경우에는 메서드 서명의 파트입니다.

메서드 매개 변수는 괄호로 묶고 쉼표로 구분합니다. 빈 괄호는 메서드에 매개 변수가 필요하지 않음을 나타냅니다. 이 클래스에는 다음 네 개의 메서드가 있습니다.

[!code-csharp[csProgGuideObjects#40](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#40)]

## <a name="method-access"></a>메서드 액세스

개체에 대한 메서드 호출은 필드 액세스와 비슷합니다. 개체 이름 뒤에 마침표, 메서드 이름 및 괄호를 추가합니다. 인수는 괄호 안에 나열되고 쉼표로 구분합니다. `Motorcycle` 클래스의 메서드는 다음 예제와 같이 호출될 수 있습니다.

[!code-csharp[csProgGuideObjects#41](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#41)]

## <a name="method-parameters-vs-arguments"></a>메서드 매개 변수 및 인수

메서드 정의는 필요한 모든 매개 변수의 이름 및 형식을 지정합니다. 호출하는 코드에서 메서드를 호출할 때 해당 코드는 각 매개 변수에 대한 인수라는 구체적인 값을 제공합니다. 인수는 매개 변수 형식과 호환되어야 하지만 호출하는 코드에 사용된 인수 이름(있는 경우)은 메서드에 정의된 명명된 매개 변수와 동일할 필요가 없습니다. 예:

[!code-csharp[csProgGuideObjects#74](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#74)]

## <a name="passing-by-reference-vs-passing-by-value"></a>참조로 전달할 것인지, 아니면 값으로 전달할 것인지 선택

기본적으로 값 형식이 메서드에 전달될 때 개체 자체가 아닌 복사본이 전달됩니다. 따라서 인수에 대한 변경 내용은 호출하는 메서드의 원래 복사본에 영향을 주지 않습니다. ref 키워드를 사용하여 값 형식을 참조로 전달할 수 있습니다. 자세한 내용은 [값 형식 매개 변수 전달](./passing-value-type-parameters.md)을 참조하세요. 기본 제공 값 형식 목록을 보려면 [값 형식 표](../../language-reference/keywords/value-types-table.md)를 참조하세요.

참조 형식의 개체가 메서드에 전달될 때 개체에 대한 참조가 전달됩니다. 즉, 메서드는 개체 자체가 아니라 개체의 위치를 나타내는 인수를 수신합니다. 이 참조를 사용하여 개체의 멤버를 변경하면 개체를 값으로 전달하더라도 변경 내용은 호출하는 메서드의 인수에 반영됩니다.

다음 예제와 같이 `class` 키워드를 사용하여 참조 형식을 만듭니다.

[!code-csharp[csProgGuideObjects#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#42)]

이제 이 형식에 기반을 둔 개체를 메서드에 전달하면 개체에 대한 참조가 전달됩니다. 다음 예제에서는 `SampleRefType` 형식의 개체를 `ModifyObject` 메서드에 전달합니다.

[!code-csharp[csProgGuideObjects#75](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#75)]

이 예제는 인수를 값으로 메서드에 전달한다는 점에서 기본적으로 이전 예제와 같은 작업을 수행합니다. 그러나 참조 형식이 사용되므로 결과가 다릅니다. `ModifyObject` 에서 매개 변수 `value` 의 `obj`필드에 대해 수정한 내용으로 인해 `value` 메서드에서 `rt`인수의 `TestRefType` 필드도 변경됩니다. `TestRefType` 메서드는 출력으로 33을 표시합니다.

참조 형식을 참조 및 값으로 전달하는 방법에 대한 자세한 내용은 [참조-형식 매개 변수 전달](./passing-reference-type-parameters.md) 및 [참조 형식](../../language-reference/keywords/reference-types.md)을 참조하세요.

## <a name="return-values"></a>반환 값

메서드는 호출자에 값을 반환할 수 있습니다. 메서드 이름 앞에 나열된 반환 형식이 `void`가 아니면 메서드는 `return` 키워드를 사용하여 값을 반환할 수 있습니다. `return` 키워드에 이어 반환 형식과 일치하는 값을 포함하는 문은 메서드 호출자에 값을 반환합니다.

호출자에게 값으로 또는 C# 7.0부터 [참조로](ref-returns.md) 값을 반환할 수 있습니다. `ref` 키워드가 메서드 시그니처에 사용되고 각 `return` 키워드 뒤에 오면 값이 호출자에게 참조로 반환됩니다. 예를 들어 다음 메서드 시그니처 및 반환 문은 메서드가 변수 이름 `estDistance`를 호출자에게 참조로 반환함을 나타냅니다.

```csharp
public ref double GetEstimatedDistance()
{
    return ref estDistance;
}
```

`return` 키워드는 메서드 실행을 중지합니다. 반환 형식이 `void`이면 값이 없는 `return` 문을 사용하여 메서드 실행을 중지할 수 있습니다. `return` 키워드를 사용하지 않으면 메서드는 코드 블록 끝에 도달할 때 실행을 중지합니다. `return` 키워드를 사용하여 값을 반환하려면 void가 아닌 반환 값을 포함한 메서드가 필요합니다. 예를 들어 이들 두 메서드에서는 `return` 키워드를 사용하여 정수를 반환합니다.

[!code-csharp[csProgGuideObjects#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#44)]

메서드에서 반환된 값을 사용하려면 호출하는 메서드에서 같은 형식의 값으로 충분한 모든 경우에 메서드 호출 자체를 사용하면 됩니다. 반환 값을 변수에 할당할 수도 있습니다. 예를 들어 다음 두 코드 예제에서는 같은 목표를 달성합니다.

[!code-csharp[csProgGuideObjects#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#45)]

[!code-csharp[csProgGuideObjects#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#46)]

지역 변수(이 경우 `result`)를 사용하여 값을 저장하는 것은 선택 사항입니다. 코드의 가독성에 도움이 될 수 있고 전체 메서드 범위에 대해 인수의 원래 값을 저장해야 할 경우 필요할 수도 있습니다.

메서드에서 참조로 반환된 값을 사용하려면 해당 값을 수정하려는 경우 [참조 지역](ref-returns.md#ref-locals) 변수를 선언해야 합니다. 예를 들어 `Planet.GetEstimatedDistance` 메서드가 <xref:System.Double> 값을 참조로 반환하는 경우 다음과 같은 코드를 사용하여 참조 지역 변수로 정의할 수 있습니다.

```csharp
ref int distance = plant
```

호출하는 함수가 배열을 `M`에 전달한 경우에는 배열 내용을 수정하는 `M` 메서드에서 다차원 배열을 반환할 필요가 없습니다.  좋은 스타일이나 값의 기능 흐름을 위해 `M`의 결과 배열을 반환할 수 있지만, C#에서는 모든 참조 형식을 값으로 전달하고 배열 참조의 값이 배열에 대한 포인터이기 때문에 필요하지 않습니다. 다음 예제와 같이 `M` 메서드의 배열 내용에 대한 변경 사항은 배열에 대한 참조가 있는 모든 코드에서 관찰할 수 있습니다.

```csharp
static void Main(string[] args)
{
    int[,] matrix = new int[2, 2];
    FillMatrix(matrix);
    // matrix is now full of -1
}

public static void FillMatrix(int[,] matrix)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
    {
        for (int j = 0; j < matrix.GetLength(1); j++)
        {
            matrix[i, j] = -1;
        }
    }
}
```

자세한 내용은 [return](../../language-reference/keywords/return.md)을 참조하세요.

## <a name="async-methods"></a>비동기 메서드

비동기 기능을 사용하면 명시적 콜백을 사용하거나 수동으로 여러 메서드 또는 람다 식에 코드를 분할하지 않고도 비동기 메서드를 호출할 수 있습니다.

메서드에 [async](../../language-reference/keywords/async.md) 한정자를 표시하면 메서드에서 [await](../../language-reference/operators/await.md) 연산자를 사용할 수 있습니다. 컨트롤이 비동기 메서드의 await 식에 도달하면 컨트롤이 호출자로 돌아가고 대기 중인 작업이 완료될 때까지 메서드의 진행이 일시 중단됩니다. 작업이 완료되면 메서드가 실행이 다시 시작될 수 있습니다.

> [!NOTE]
> 비동기 메서드는 아직 완료되지 않은 첫 번째 대기된 개체를 검색할 때나 비동기 메서드의 끝에 도달할 때 중에서 먼저 발생하는 시점에 호출자에게 반환됩니다.

비동기 메서드의 반환 형식은 <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task>또는 void일 수 있습니다. void 반환 형식은 기본적으로 void 반환 형식이 필요할 때 이벤트 처리기를 정의하는 데 사용합니다. void를 반환하는 비동기 메서드는 대기할 수 없고 void를 반환하는 메서드의 호출자는 메서드가 throw하는 예외를 catch할 수 없습니다.

다음 예제에서 `DelayAsync` 는 반환 형식이 <xref:System.Threading.Tasks.Task%601>인 비동기 메서드입니다. `DelayAsync` 에는 정수를 반환하는 `return` 문이 포함됩니다. 따라서 `DelayAsync` 의 메서드 선언의 반환 형식은 `Task<int>`여야 합니다. 반환 형식이 `Task<int>`이므로 `await` 의 `DoSomethingAsync` 식 계산에서 다음 문과 같이 정수가 생성됩니다. `int result = await delayTask`.

`startButton_Click` 메서드는 반환 형식이 void인 비동기 메서드의 한 가지 예입니다. `DoSomethingAsync` 는 비동기 메서드이므로 다음 문과 같이 `DoSomethingAsync` 호출에 대한 작업을 기다려야 합니다. `await DoSomethingAsync();`. `startButton_Click` 메서드에 `async` 식이 포함되므로 `await` 한정자를 사용하여 해당 메서드를 정의해야 합니다.

[!code-csharp[csAsyncMethod#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncmethod/cs/mainwindow.xaml.cs#2)]

비동기 메서드는 모든 [ref](../../language-reference/keywords/ref.md) 또는 [out](../../language-reference/keywords/out-parameter-modifier.md) 매개 변수를 선언할 수 없지만, 이러한 매개 변수가 있는 메서드를 호출할 수는 있습니다.

비동기 메서드에 대한 자세한 내용은 [async 및 await를 사용한 비동기 프로그래밍](../concepts/async/index.md), [비동기 프로그램의 제어 흐름](../concepts/async/control-flow-in-async-programs.md) 및 [비동기 반환 형식](../concepts/async/async-return-types.md)을 참조하세요.

## <a name="expression-body-definitions"></a>식 본문 정의

일반적으로 식의 결과와 함께 바로 반환되거나 단일 문이 메서드 본문으로 포함된 메서드 정의가 있습니다. `=>`를 사용하여 해당 메서드를 속성을 정의하기 위한 구문 바로 가기는 다음과 같습니다.

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

메서드가 `void` 를 반환하거나 비동기 메서드이면 메서드 본문은 문 식이어야 합니다(람다에서와 같음). 속성 및 인덱서의 경우 읽기 전용이어야 하며, `get` 접근자 키워드를 사용하지 않습니다.

## <a name="iterators"></a>Iterators

반복기는 배열 목록과 같은 컬렉션에 대해 사용자 지정 반복을 수행합니다. 반복기는 [yield return](../../language-reference/keywords/yield.md) 문을 사용하여 각 요소를 따로따로 반환할 수 있습니다. [yield return](../../language-reference/keywords/yield.md) 문에 도달하면 코드의 현재 위치가 기억됩니다. 다음에 반복기가 호출되면 해당 위치에서 실행이 다시 시작됩니다.

[foreach](../../language-reference/keywords/foreach-in.md) 문을 사용하여 클라이언트 코드에서 반복기를 호출합니다.

반복기의 반환 형식은 <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>또는 <xref:System.Collections.Generic.IEnumerator%601>일 수 있습니다.

자세한 내용은 [반복기](../concepts/iterators.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](index.md)
- [액세스 한정자](access-modifiers.md)
- [정적 클래스 및 정적 클래스 멤버](static-classes-and-static-class-members.md)
- [상속](inheritance.md)
- [추상/봉인된 클래스 및 클래스 멤버](abstract-and-sealed-classes-and-class-members.md)
- [params](../../language-reference/keywords/params.md)
- [return](../../language-reference/keywords/return.md)
- [out](../../language-reference/keywords/out.md)
- [ref](../../language-reference/keywords/ref.md)
- [매개 변수 전달](passing-parameters.md)
