---
title: 참조 반환 값 (Visual Basic)
ms.date: 04/28/2017
helpviewer_keywords:
- variables [Visual Basic]
- ref return values [Visual Basic]
- ref returns [Visual Basic]
ms.assetid: 5ef0cc69-eb3a-4a67-92a2-78585f223cb5
ms.openlocfilehash: ba649c4beaf3ec70a8c118f823fe8f25651a05a7
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198304"
---
# <a name="support-for-reference-return-values-visual-basic"></a>참조 반환 값 (Visual Basic)에 대 한 지원

부터 C# 7.0에는 C# 언어 지원 *반환 값을 참조*합니다. 참조 반환 값을 이해 하는 한 가지 방법은 이들이 반대 메서드에 참조로 전달 되는 인수입니다. 참조로 전달 되는 인수 수정 되 면 변경 내용이 호출자에 변수의 값에 반영 됩니다. 호출자에 게 참조 반환 값을 제공 하는 메서드를, 호출자가 참조 반환 값에 대 한 수정 호출된 된 메서드의 데이터에 반영 됩니다.

Visual Basic 참조를 사용 하 여 만든 메서드에 값 돌아가게 없지만 참조 반환 값을 사용할 수 있습니다 수는 허용 하지 않습니다. 즉, 참조 반환 값을 사용 하 여 메서드를 호출 하 고 해당 반환 값을 수정할 수 있습니다 및 참조 반환 값을 변경 하는 호출된 된 메서드의 데이터에 반영 됩니다.

## <a name="modifying-the-ref-return-value-directly"></a>참조 반환 값을 직접 수정

항상 실패 하 고 없는 하는 방법에 대 한 `ByRef` 매개 변수를 직접 참조 반환 값을 수정할 수 있습니다. 참조 반환 값을 반환 하는 식에 새 값을 할당 하 여이 작업을 수행 합니다. 

다음 C# 예제에서는 정의 `NumericValue.IncrementValue` 메서드 내부 값을 증가 시키고 참조로 반환 하는 값을 반환 합니다. 

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/ref-returns1.cs)]

참조 값이 다음 Visual Basic 예제에서는 호출자가 수정 후 반환 합니다. 한 줄으로 된 `NumericValue.IncrementValue` 메서드 호출 메서드에 값을 할당 하지 않습니다. 대신, 메서드에 의해 반환 되는 참조 반환 값을 할당 합니다.

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/use-ref-returns1.vb)]

## <a name="using-a-helper-method"></a>도우미 메서드를 사용 하 여

다른 경우에 메서드 호출의 참조 반환 값을 직접 수정 항상 바람직하지 않을 합니다. 예를 들어 문자열을 반환 하는 검색 메서드를 찾을 수 없습니다 항상 일치 하는 합니다. 이 경우 검색에 성공 하는 경우에 참조 반환 값을 수정 하려고 합니다.

다음 C# 예제에서는이 시나리오를 보여 줍니다. 정의 `Sentence` 로 작성 된 클래스 C# 포함을 `FindNext` 메서드는 지정된 된 부분 문자열을 사용 하 여 시작 하는 문장 내에서 다음 단어를 찾습니다. 문자열은 참조 반환 값으로 반환되며, 메서드에 참조로 전달된 `Boolean` 변수는 검색에 성공했는지 여부를 나타냅니다. 참조 반환 값이 나타냅니다는 호출자가 읽을 수 없습니다만 반환 되는 값입니다. 자신이 수정할 수 있으며 해당 수정에서 내부적으로 포함 된 데이터에 반영 됩니다는 `Sentence` 클래스입니다.

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

참조를 직접 수정 반환 값이 경우은 하지 않습니다, 신뢰할 수 있는 일치 항목을 찾을 문장의 첫 번째 단어를 반환 하는 메서드 호출이 실패할 수 있습니다. 이 경우 호출자가 문장의 첫 번째 단어를 실수로 수정 합니다. 이 반환 하는 호출자에 의해 차단 될 수 있습니다는 `null` (또는 `Nothing` Visual basic에서). 이 경우 값이 문자열을 수정 하려고 하지만 `Nothing` throw를 <xref:System.NullReferenceException>입니다. 반환 하는 호출자에 의해 차단 될 수 있습니다 하는 경우 <xref:System.String.Empty?displayProperty=nameWithType>를 호출자에 게 값인 문자열 변수 정의 필요 하지만 <xref:System.String.Empty?displayProperty=nameWithType>합니다. 수정 된 문자열에서 저장 된 문장에 대 한 단어 아무런 관계가 있으므로 자체 수정 없는 용도로 호출자에 게 해당 문자열을 수정할 수, 하는 동안 사용 되는 `Sentence` 클래스입니다.

이 시나리오를 처리 하는 가장 좋은 방법은 도우미 메서드에 대 한 참조에서 참조 반환 값을 전달 하는 경우 도우미 메서드는 다음 논리를 확인 하는지 여부를 메서드 호출에 성공한 경우 수정 하려면 참조 반환 값을 포함 합니다. 다음 예제에서는 가능한 구현을 제공합니다.

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

## <a name="see-also"></a>참고자료

[값 및 참조로 인수 전달](passing-arguments-by-value-and-by-reference.md)   
[Visual Basic의 프로시저](index.md)   


