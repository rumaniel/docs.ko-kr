---
title: sizeof 연산자 - C# 참조
ms.custom: seodec18
ms.date: 07/25/2019
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: c455804923f4d0e7cc8f556bb9b9df34b6332d82
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796521"
---
# <a name="sizeof-operator-c-reference"></a>sizeof 연산자(C# 참조)

`sizeof` 연산자는 지정된 형식의 변수에서 사용하는 바이트 수를 반환합니다. `sizeof` 연산자의 인수는 [비관리형 형식](../builtin-types/unmanaged-types.md) 또는 비관리형 형식이 되기 위해 [제한된](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint) 형식 매개 변수의 이름이어야 합니다.

`sizeof` 연산자에 [안전하지 않은](../keywords/unsafe.md) 컨텍스트가 필요합니다. 그러나 아래 표의 식은 컴파일 시간에 해당 상수 값으로 계산되며 안전하지 않은 컨텍스트가 필요하지 않습니다.

|식|상수 값|
|---------|---------------|
|`sizeof(sbyte)`|1|
|`sizeof(byte)`|1|
|`sizeof(short)`|2|
|`sizeof(ushort)`|2|
|`sizeof(int)`|4|
|`sizeof(uint)`|4|
|`sizeof(long)`|8|
|`sizeof(ulong)`|8|
|`sizeof(char)`|2|
|`sizeof(float)`|4|
|`sizeof(double)`|8|
|`sizeof(decimal)`|16|
|`sizeof(bool)`|1|

`sizeof` 연산자의 피연산자가 [열거형](../keywords/enum.md) 형식의 이름인 경우에도 안전하지 않은 컨텍스트를 사용할 필요가 없습니다.

다음 예제에서는 `sizeof` 연산자의 사용법을 보여 줍니다.

[!code-csharp[sizeof examples](~/samples/csharp/language-reference/operators/SizeOfOperator.cs)]

`sizeof` 연산자는 관리되는 메모리의 공용 언어 런타임에서 할당하는 바이트 수를 반환합니다. [구조체](../keywords/struct.md) 형식의 경우 앞의 예제에서 보여 주는 것처럼 해당 값에 안쪽 여백이 포함됩니다. `sizeof` 연산자의 결과는 ‘관리되지 않는’ 메모리의 형식 크기를 반환하는 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 메서드의 결과와 다를 수 있습니다. 

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [sizeof 연산자](~/_csharplang/spec/unsafe-code.md#the-sizeof-operator) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 연산자](index.md)
- [포인터 관련 연산자](pointer-related-operators.md)
- [포인터 형식](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [메모리 및 범위 관련 형식](../../../standard/memory-and-spans/index.md)
