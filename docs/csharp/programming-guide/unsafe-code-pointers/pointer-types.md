---
title: 포인터 형식 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 04/20/2018
helpviewer_keywords:
- unsafe code [C#], pointers
- pointers [C#]
ms.openlocfilehash: 4d0801cd81e00c84be278b44730058798b0acfa9
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588199"
---
# <a name="pointer-types-c-programming-guide"></a>포인터 형식(C# 프로그래밍 가이드)

안전하지 않은 컨텍스트에서는 형식이 포인터 형식, 값 형식 또는 참조 형식이 될 수 있습니다. 포인터 형식 선언은 다음 형식 중 하나를 사용합니다.

``` csharp
type* identifier;
void* identifier; //allowed but not recommended
```

포인터 형식에서 `*` 앞에 지정된 형식을 **참조 형식**이라고 합니다. [비관리형 형식](../../language-reference/builtin-types/unmanaged-types.md)만 참조 형식일 수 있습니다.

포인터 형식은 [개체](../../language-reference/keywords/object.md)에서 상속되지 않으며 포인터 형식과 `object`는 서로 변환되지 않습니다. 또한 boxing과 unboxing은 포인터를 지원하지 않습니다. 그러나 다른 포인터 형식 간의 변환 및 포인터 형식과 정수 형식 사이의 변환은 허용됩니다.

동일한 선언에서 여러 포인터를 선언하는 경우 별표(*)는 기본 형식에만 함께 사용되고 각 포인터 이름의 접두사로는 사용되지 않습니다. 예:

```csharp
int* p1, p2, p3;   // Ok
int *p1, *p2, *p3;   // Invalid in C#
```

개체 참조는 포인터가 해당 개체 참조를 가리키는 경우에도 가비지 수집될 수 있으므로 포인터는 참조나 참조가 들어 있는 [구조체](../../language-reference/keywords/struct.md)를 가리킬 수 없습니다. 가비지 수집기는 포인터 형식에서 개체를 가리키는지 여부를 추적하지 않습니다.

`myType*` 형식의 포인터 변수 값은 `myType` 형식의 변수 주소입니다. 다음은 포인터 형식 선언의 예제입니다.

|예|설명|
|-------------|-----------------|
|`int* p`|`p`는 정수에 대한 포인터입니다.|
|`int** p`|`p`는 정수에 대한 포인터를 가리키는 포인터입니다.|
|`int*[] p`|`p`는 정수에 대한 포인터의 1차원 배열입니다.|
|`char* p`|`p`는 문자에 대한 포인터입니다.|
|`void* p`|`p`는 알 수 없는 형식에 대한 포인터입니다.|

포인터 간접 참조 연산자 *를 사용하면 포인터 변수가 가리키는 위치의 내용에 액세스할 수 있습니다. 예를 들어, 다음 선언을 참조하십시오.

```csharp
int* myVariable;
```

여기서 `*myVariable` 식은 `int`에 포함된 주소에 있는 `myVariable` 변수를 가리킵니다.

[fixed 문](../../language-reference/keywords/fixed-statement.md) 및 [포인터 변환](./pointer-conversions.md) 항목에 포인터에 대한 몇 가지 예제가 나와 있습니다. 다음 예제는 `unsafe` 키워드 및 `fixed` 문을 사용하고 정수 포인터를 증분하는 방법을 보여줍니다.  이 코드를 실행하려면 콘솔 애플리케이션의 주 함수에 붙여 넣습니다. 이러한 예제는 [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) 컴파일러 옵션 집합으로 컴파일되어야 합니다.

[!code-csharp[Using pointer types](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#5)]

`void*` 형식의 포인터에는 간접 참조 연산자를 적용할 수 없습니다. 그러나 캐스트를 사용하여 void 포인터를 다른 포인터 형식으로 변환하거나 반대로 변환할 수 있습니다.

포인터는 `null`일 수 있습니다. null 포인터에 간접 참조 연산자를 적용할 때 발생하는 동작은 구현에 따라 다릅니다.

메서드 사이에 포인터를 전달하면 정의되지 않은 동작이 발생할 수 있습니다. `in`, `out` 또는 `ref` 매개 변수를 통해, 또는 함수 결과로 지역 변수에 포인터를 반환하는 메서드를 고려합니다. fixed 블록에서 포인터가 설정되면 이 포인터가 가리키는 변수의 고정 상태가 해제될 수 있습니다.

다음 표에서는 안전하지 않은 컨텍스트에서 포인터에 대해 수행할 수 있는 연산자와 문을 보여 줍니다.

|연산자/문|기능|
|-------------------------|---------|
|`*`|포인터 간접 참조를 수행합니다.|
|`->`|포인터를 통해 구조체 멤버에 액세스합니다.|
|`[]`|포인터를 인덱싱합니다.|
|`&`|변수 주소를 가져옵니다.|
|`++` 및 `--`|포인터를 증가 및 감소시킵니다.|
|`+` 및 `-`|포인터 연산을 수행합니다.|
|`==`, `!=`, `<`, `>`, `<=` 및 `>=`|포인터를 비교합니다.|
|[`stackalloc` 연산자](../../language-reference/operators/stackalloc.md)|스택에 메모리를 할당합니다.|
|[`fixed` statement](../../language-reference/keywords/fixed-statement.md)|해당 주소를 찾을 수 있도록 임시로 변수를 고정합니다.|

포인터에 관련 연산자에 대한 자세한 내용은 [포인터 관련 연산자](../../language-reference/operators/pointer-related-operators.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [포인터 형식](~/_csharplang/spec/unsafe-code.md#pointer-types) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [안전하지 않은 코드 및 포인터](index.md)
- [포인터 변환](pointer-conversions.md)
- [유형](../../language-reference/keywords/types.md)
- [unsafe](../../language-reference/keywords/unsafe.md)
