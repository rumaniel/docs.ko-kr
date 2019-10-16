---
title: 고정 크기 버퍼 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 04/20/2018
helpviewer_keywords:
- fixed size buffers [C#]
- unsafe buffers [C#]
- unsafe code [C#], fixed size buffers
ms.openlocfilehash: 5bfd9f3f559e4780b910a2e5a3430b08a2183ee3
ms.sourcegitcommit: 34593b4d0be779699d38a9949d6aec11561657ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66833500"
---
# <a name="fixed-size-buffers-c-programming-guide"></a>고정 크기 버퍼(C# 프로그래밍 가이드)

C#에서는 [fixed](../../language-reference/keywords/fixed-statement.md) 문을 사용하여 데이터 구조에 고정 크기 배열이 있는 버퍼를 만들 수 있습니다. 고정 크기 버퍼는 다른 언어 또는 플랫폼에서 데이터 원본과 interop하는 메서드를 작성하는 경우에 유용합니다. 고정 배열은 일반 구조체 멤버에 허용되는 특성이나 한정자를 사용할 수 있습니다. 배열 형식이 `bool`, `byte`, `char`, `short`, `int`, `long`, `sbyte`, `ushort`, `uint`, `ulong`, `float` 또는 `double`이어야 한다는 것이 유일한 제한 사항입니다.

```csharp
private fixed char name[30];
```

## <a name="remarks"></a>설명

안전한 코드에서 배열을 포함하는 C# 구조체는 배열 요소를 포함하지 않습니다. 대신 구조체에 요소에 대한 참조가 포함되어 있습니다. [unsafe](../../language-reference/keywords/unsafe.md) 코드 블록에서 사용될 경우 [struct](../../language-reference/keywords/struct.md)에 고정 크기 배열을 포함할 수 있습니다.

다음 `struct`은 8바이트 크기입니다. `pathName` 배열은 참조입니다.

[!code-csharp[Struct with embedded array](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#6)]

`struct`은 안전하지 않은 코드에 포함된 배열을 포함할 수 있습니다. 다음 예제에서 `fixedBuffer` 배열은 고정 크기입니다. `fixed` 명령문을 사용하여 첫 번째 요소에 대한 포인터를 설정합니다. 이 포인터를 통해 배열의 요소에 액세스합니다. `fixed` 명령문은 `fixedBuffer`의 인스턴스 필드를 메모리의 특정 위치에 고정합니다.

[!code-csharp[Struct with embedded inline array](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#7)]

128개 요소 `char` 배열의 크기는 256바이트입니다. 고정 크기 [char](../../language-reference/keywords/char.md) 버퍼는 인코딩에 관계없이 항상 문자당 2바이트를 사용합니다. 이는 char 버퍼가 `CharSet = CharSet.Auto` 또는 `CharSet = CharSet.Ansi`를 사용하는 API 메서드 또는 구조체로 마샬링되는 경우에도 마찬가지입니다. 자세한 내용은 <xref:System.Runtime.InteropServices.CharSet>을 참조하세요.

앞의 예제에서는 C# 7.3부터 사용할 수 있으며 고정하지 않은 `fixed` 필드에 액세스하는 방법을 보여 줍니다.

또 다른 일반적인 고정 크기 배열은 [bool](../../language-reference/keywords/bool.md) 배열입니다. `bool` 배열의 요소 크기는 항상 1바이트입니다. `bool` 배열은 비트 배열이나 버퍼를 만드는 데 적합하지 않습니다.

> [!NOTE]
> [stackalloc](../../language-reference/operators/stackalloc.md)를 사용하여 만든 메모리를 제외하고 C# 컴파일러와 CLR(공용 언어 런타임)에서 보안 버퍼 오버런 검사를 수행하지 않습니다. 모든 안전하지 않은 코드와 마찬가지로 주의해야 합니다.

안전하지 않은 버퍼는 다음과 같은 측면에서 일반 배열과 다릅니다.

- 안전하지 않은 버퍼는 안전하지 않은 컨텍스트에서만 사용할 수 있습니다.
- 안전하지 않은 버퍼는 항상 벡터 또는 1차원 배열입니다.
- 배열의 선언에는 `char id[8]`와 같이 개수가 포함되어야 합니다. `char id[]`을 사용할 수 없습니다.
- 안전하지 않은 버퍼는 안전하지 않은 컨텍스트에서 구조체의 인스턴스 필드만 될 수 있습니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [안전하지 않은 코드 및 포인터](index.md)
- [fixed 문](../../language-reference/keywords/fixed-statement.md)
- [상호 운용성](../interop/index.md)
