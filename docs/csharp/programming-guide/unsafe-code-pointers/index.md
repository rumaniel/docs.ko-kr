---
title: 안전하지 않은 코드 및 포인터 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- security [C#], type safety
- C# language, unsafe code
- type safety [C#]
- unsafe keyword [C#]
- unsafe code [C#]
- C# language, pointers
- pointers [C#], about pointers
ms.assetid: b0fcca10-a92d-4f2a-835b-b0ccae6739ee
ms.openlocfilehash: 99f0b925a37bff8b6ab1ff46e9ce2f0ea0a38aed
ms.sourcegitcommit: ffd7dd79468a81bbb0d6449f6d65513e050c04c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65959484"
---
# <a name="unsafe-code-and-pointers-c-programming-guide"></a>안전하지 않은 코드 및 포인터 - (C# 프로그래밍 가이드)

형식 안전성 및 보안을 유지하기 위해 C#에서는 포인터 산술 연산을 기본적으로 지원하지 않습니다. 그러나 [unsafe](../../language-reference/keywords/unsafe.md) 키워드를 사용하여 포인터를 사용할 수 있는 안전하지 않은 컨텍스트를 정의할 수 있습니다. 포인터에 대한 자세한 내용은 [포인터 형식](pointer-types.md)을 참조하세요.  
  
> [!NOTE]
> CLR(공용 언어 런타임)에서 안전하지 않은 코드를 확인할 수 없는 코드라고 합니다. C#에 안전하지 않은 코드가 반드시 위험한 것은 아니며, CLR에서 안전을 확인할 수 없는 코드입니다. 그러므로 CLR은 완전히 신뢰할 수 있는 어셈블리에 있는 경우 안전하지 않은 코드만 실행합니다. 안전하지 않은 코드를 사용하는 경우 코드로 인해 보안 위험이나 포인터 오류가 발생하지 않도록 확인해야 합니다.  
  
## <a name="unsafe-code-overview"></a>안전하지 않은 코드 개요

안전하지 않은 코드에는 다음과 같은 속성이 있습니다.

- 메서드, 형식 및 코드 블록은 안전하지 않은 것으로 정의할 수 있습니다.

- 경우에 따라 안전하지 않은 코드는 배열 범위 검사를 제거하여 애플리케이션의 성능을 향상할 수 있습니다.

- 포인터가 필요한 네이티브 함수를 호출하는 경우 안전하지 않은 코드가 필요합니다.

- 안전하지 않은 코드를 사용하면 보안 및 안정성 위험이 발생합니다.

- 안전하지 않은 블록을 포함하는 코드는 [-안전하지 않은](../../language-reference/compiler-options/unsafe-compiler-option.md) 컴파일러 옵션을 사용하여 컴파일해야 합니다.
  
## <a name="related-sections"></a>관련 단원

자세한 내용은 다음을 참조하세요.

- [포인터 형식](pointer-types.md)

- [고정 크기 버퍼](fixed-size-buffers.md)

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [안전하지 않은 코드](~/_csharplang/spec/unsafe-code.md) 토픽을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [unsafe](../../language-reference/keywords/unsafe.md)
