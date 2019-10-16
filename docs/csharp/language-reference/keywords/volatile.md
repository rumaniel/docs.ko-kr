---
title: volatile - C# 참조
ms.custom: seodec18
ms.date: 10/24/2018
f1_keywords:
- volatile_CSharpKeyword
- volatile
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
ms.openlocfilehash: 7200432780cb5a65bc5420b41c5dbd2e27a2c01f
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633092"
---
# <a name="volatile-c-reference"></a>volatile(C# 참조)

`volatile` 키워드는 동시에 실행되는 여러 스레드에 의해 필드가 수정될 수 있음을 나타냅니다. 컴파일러, 런타임 시스템 및 하드웨어는 성능상의 이유로 메모리 위치에 대한 읽기 및 쓰기를 다시 정렬할 수 있습니다. `volatile`로 선언된 필드에는 이러한 최적화가 적용되지 않습니다. `volatile` 한정자를 추가하면 모든 스레드가 수행된 순서대로 다른 스레드가 휘발성 쓰기를 수행합니다. 모든 실행 스레드에서처럼 휘발성 쓰기의 단일 순서가 모두 보장되는 것은 아닙니다.

`volatile` 키워드는 다음 형식의 필드에 적용될 수 있습니다.

- 참조 형식.
- 포인터 형식(안전하지 않은 컨텍스트에서). 포인터 자체는 volatile이 될 수 있지만, 포인터가 가리키는 개체는 volatile이 될 수 없습니다. 즉, "pointer to volatile"을 선언할 수 없습니다.
- `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `char`, `float` 및 `bool`와 같은 단순 형식.
- 기본 형식 `byte`, `sbyte`, `short`, `ushort`, `int` 또는 `uint` 중 하나가 있는 `enum` 형식.
- 참조 형식으로 알려진 제네릭 형식 매개 변수.
- <xref:System.IntPtr>와 <xref:System.UIntPtr>을 참조하세요.

`double` 및 `long`을 포함한 기타 형식은 해당 형식의 필드에 대한 읽기 및 쓰기가 원자성임을 보장할 수 없기 때문에 `volatile`로 표시될 수 없습니다. 이러한 형식의 필드에 대한 다중 스레드 액세스를 보호하려면 <xref:System.Threading.Interlocked> 클래스 멤버를 사용하거나 [`lock`](lock-statement.md) 문을 통해 액세스를 보호합니다.

`volatile` 키워드는 `class` 또는 `struct`의 필드에만 적용할 수 있습니다. 지역 변수는 `volatile`로 선언할 수 없습니다.

## <a name="example"></a>예제

다음 예제에서는 공용 필드 변수를 `volatile`로 선언하는 방법을 보여 줍니다.

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Declaration)]

다음 예제에서는 보조 또는 작업자 스레드를 만들어 기본 스레드와 병렬로 처리하는 데 사용하는 방법을 보여줍니다. 다중 스레딩에 대한 자세한 내용은 [관리되는 스레딩](../../../standard/threading/index.md)을 참조하세요.

[!code-csharp[declareVolatile](~/samples/snippets/csharp/language-reference/keywords/volatile/Program.cs#Volatile)]

`_shouldStop`의 선언에 `volatile` 한정자를 추가하면 항상 동일한 결과가 표시됩니다(앞의 코드에 표시된 것과 유사함). 그러나 `_shouldStop` 멤버의 해당 한정자가 없으면 동작을 예측할 수 없습니다. `DoWork` 메서드가 멤버 액세스를 최적화할 수 있으므로 부실 데이터를 읽게 됩니다. 다중 스레드 프로그래밍의 특성으로 인해 부실 읽기 수는 예측할 수 없습니다. 프로그램의 실행에 따라 약간 다른 결과가 생성됩니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 언어 사양: volatile 키워드](../../../../_csharplang/spec/classes.md#volatile-fields)
- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [한정자](modifiers.md)
- [lock 문](lock-statement.md)
- <xref:System.Threading.Interlocked>
