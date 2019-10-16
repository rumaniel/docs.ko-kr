---
title: 식별자 이름
description: C# 프로그래밍 언어에서 올바른 식별자 이름에 대한 규칙을 알아봅니다.
ms.date: 08/21/2018
ms.openlocfilehash: f8a27ddae0437ed037b59f76d60dc7e420ddc2eb
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589347"
---
# <a name="identifier-names"></a>식별자 이름

**식별자**는 형식(클래스, 인터페이스, 구조체, 대리자 또는 열거형), 멤버, 변수 또는 네임스페이스에 할당하는 이름입니다. 유효한 식별자는 다음 규칙을 따라야 합니다.

- 식별자는 문자 또는 `_`로 시작해야 합니다.
- 식별자에는 유니코드 문자, 10진수 문자, 유니코드 연결 문자, 유니코드 조합 문자 또는 유니코드 형식 문자가 포함될 수 있습니다. 유니코드 범주에 대한 자세한 내용은 [유니코드 범주 데이터베이스](https://www.unicode.org/reports/tr44/)를 참조하세요.
식별자의 `@` 접두사를 사용하여 C# 키워드와 일치하는 식별자를 선언할 수 있습니다. `@`는 식별자 이름의 일부가 아닙니다. 예를 들어 `@if`는 `if`라는 식별자를 선언합니다. 이러한 [verbatim 식별자](../../language-reference/tokens/verbatim.md)는 주로 다른 언어로 선언된 식별자와의 상호 운용성을 위한 것입니다.

유효한 식별자의 전체 정의는 [C# 언어 사양의 식별자 항목](../../../../_csharplang/spec/lexical-structure.md#identifiers)을 참조하세요.

## <a name="naming-conventions"></a>명명 규칙

규칙 외에도 .NET API 전체에서 사용되는 여러 식별자 [명명 규칙](../../../standard/design-guidelines/naming-guidelines.md)이 있습니다. 규칙에 따라 C# 프로그램은 형식 이름, 네임스페이스 및 모든 공용 멤버에 `PascalCase`를 사용합니다. 또한, 다음 규칙이 일반적입니다.

- 인터페이스 이름은 대문자 `I`로 시작합니다.
- 특성 유형은 `Attribute` 단어로 끝납니다.
- 열거형 형식은 플래그가 아닌 경우에는 단수 명사를 사용하고 플래그인 경우에는 복수 명사를 사용합니다.
- 식별자에는 두 개의 연속 `_` 문자가 없어야 합니다. 이러한 이름은 컴파일러 생성 식별자용으로 예약되어 있습니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [C# 프로그램 내부](./index.md)
- [C# 참조](../../language-reference/index.md)
- [클래스](../classes-and-structs/classes.md)
- [구조체](../classes-and-structs/structs.md)
- [네임스페이스](../namespaces/index.md)
- [인터페이스](../interfaces/index.md)
- [대리자](../delegates/index.md)
