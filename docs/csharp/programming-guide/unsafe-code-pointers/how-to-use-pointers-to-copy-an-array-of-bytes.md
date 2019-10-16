---
title: '방법: 포인터를 사용하여 바이트 배열 복사 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 04/20/2018
helpviewer_keywords:
- byte arrays [C#]
- arrays [C#], byte
- pointers [C#], to copy bytes
ms.openlocfilehash: d174f51fa1709a70b98473a4dbbad89b9c62c22a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54640305"
---
# <a name="how-to-use-pointers-to-copy-an-array-of-bytes--c-programming-guide"></a>방법: 포인터를 사용하여 바이트 배열 복사(C# 프로그래밍 가이드)

다음 예제에서는 포인터를 사용하여 배열 간에 바이트를 복사합니다.

이 예제에서는 `Copy` 메서드에서 포인터를 사용할 수 있도록 하는 [unsafe](../../language-reference/keywords/unsafe.md) 키워드를 사용합니다. [fixed](../../language-reference/keywords/fixed-statement.md) 문은 소스 및 대상 배열에 대한 포인터를 선언하는 데 사용됩니다. `fixed` 명령문은 소스 및 대상 배열의 위치가 메모리에 *고정*되므로 가비지 수집에 의해 이동되지 않습니다. `fixed` 블록이 완료되면 배열에 대한 메모리 블록이 고정 해제됩니다. 이 예제의 `Copy` 메서드는 `unsafe` 키워드를 사용하기 때문에 [-unsafe](../../language-reference/compiler-options/unsafe-compiler-option.md) 컴파일러 옵션으로 컴파일해야 합니다.

이 예제에서는 두 번째 관리되지 않는 포인터보다는 인덱스를 사용하여 두 배열의 요소에 액세스합니다. `pSource` 및 `pTarget` 포인터의 선언은 배열을 고정합니다. 이 기능은 C# 7.3부터 사용할 수 있습니다.

## <a name="example"></a>예제

[!code-csharp[Struct with embedded inline array](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#8)]

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [안전하지 않은 코드 및 포인터](index.md)
- [-unsafe(C# 컴파일러 옵션)](../../language-reference/compiler-options/unsafe-compiler-option.md)
- [가비지 수집](../../../standard/garbage-collection/index.md)
