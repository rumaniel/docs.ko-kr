---
title: '방법: 코드 섹션 축소 및 숨기기 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
ms.openlocfilehash: 4f11982cc0aa7654c1e456fb15d918a68bc4791b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054115"
---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>방법: 코드 섹션 축소 및 숨기기 (Visual Basic)

`#Region` 지시문을 사용 하면 Visual Basic 파일에서 코드 섹션을 축소 하 고 숨길 수 있습니다. 지시문 `#Region` 을 사용 하면 Visual Studio 코드 편집기를 사용할 때 확장 하거나 축소할 수 있는 코드 블록을 지정할 수 있습니다. 코드를 선택적으로 숨기는 기능을 통해 파일을 보다 쉽게 관리 하 고 읽을 수 있습니다. 자세한 내용은 [개요](/visualstudio/ide/outlining)를 참조하세요.

`#Region`지시문은와 같은 코드 블록 의미 `#If...#End If`체계를 지원 합니다. 즉, 한 블록에서 시작 하 여 다른 블록에서 끝날 수 없습니다. start 및 end는 동일한 블록에 있어야 합니다. `#Region`지시문은 함수 내에서 지원 되지 않습니다.

## <a name="to-collapse-and-hide-a-section-of-code"></a>코드 섹션을 축소 하 고 숨기려면

다음 예제와 같이 `#Region` 및 `#End Region` 문 사이에 코드 섹션을 놓습니다.

[!code-vb[VbVbalrConditionalComp#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConditionalComp/VB/Class1.vb#6)]

블록 `#Region` 은 코드 파일에서 여러 번 사용할 수 있습니다. 따라서 사용자는 프로시저 및 클래스의 고유한 블록을 정의 하 여 축소할 수 있습니다. `#Region`블록은 다른 `#Region` 블록 내에 중첩 될 수도 있습니다.

> [!NOTE]
> 코드를 숨기면 문이 컴파일되지 않으며 문에 영향을 `#If...#End If` 주지 않습니다.

## <a name="see-also"></a>참고자료

- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [#Region 지시문](../../../visual-basic/language-reference/directives/region-directive.md)
- [#If...Then...#Else 지시문](../../../visual-basic/language-reference/directives/if-then-else-directives.md)
- [개요](/visualstudio/ide/outlining)
