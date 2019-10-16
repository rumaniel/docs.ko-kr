---
title: '방법: 코드에서 문 분리 및 결합 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb._
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores [Visual Basic], in code
- statements [Visual Basic], line continuation in
- line breaks [Visual Basic], in code
- line-continuation character [Visual Basic]
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
ms.openlocfilehash: a0a77b161d81271a4cb7eecf2982a287debee6a5
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991720"
---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>방법: 코드에서 문 분리 및 결합 (Visual Basic)

코드를 작성할 때 코드 편집기에서 가로로 스크롤해야 하는 긴 문을 만들 수 있습니다. 이는 코드가 실행 되는 방식에는 영향을 주지 않지만 사용자 또는 다른 사용자가 모니터에 표시 되는 코드를 읽을 수 있도록 하는 것이 어렵습니다. 이 경우 단일 long 문을 여러 줄로 나누는 것이 좋습니다.

## <a name="to-break-a-single-statement-into-multiple-lines"></a>단일 문을 여러 줄로 분할 하려면

줄 연속 문자를 사용 합니다 .이 문자는 줄을`_`나눌 지점에서 밑줄 ()입니다. 밑줄 바로 앞에는 공백이 오고 바로 뒤에 줄 종결자 (캐리지 리턴)가와 야 합니다 (버전 16.0부터). 주석 뒤에 캐리지 리턴이와 야 합니다.

  > [!NOTE]
  > 경우에 따라 줄 연속 문자를 생략 하는 경우 Visual Basic 컴파일러는 다음 코드 줄에서 문을 암시적으로 계속 합니다. 줄 연속 문자를 생략할 수 있는 구문 요소 목록은 [문의](../../../visual-basic/programming-guide/language-features/statements.md)"암시적 줄 연속"을 참조 하세요.

  다음 예제에서 문은 줄 연속 문자를 사용 하 여 마지막 줄을 제외한 4 개의 줄로 구분 됩니다.

  [!code-vb[VbVbcnConventions#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#20)]

  이 시퀀스를 사용 하면 온라인 및 인쇄 시 코드를 더 쉽게 읽을 수 있습니다.

  줄 연속 문자는 줄에서 마지막 문자 여야 합니다. 동일한 줄에서 다른 작업을 수행할 수 없습니다.

  줄 연속 문자를 사용할 수 있는 위치에 대 한 몇 가지 제한이 있습니다. 예를 들어 인수 이름 중간에 사용할 수 없습니다. 줄 연속 문자를 사용 하 여 인수 목록을 나눌 수 있지만 인수의 개별 이름은 그대로 유지 되어야 합니다.

  줄 연속 문자를 사용 하 여 주석을 계속할 수 없습니다. 컴파일러는 특별 한 의미를 위해 주석의 문자를 검사 하지 않습니다. 여러 줄로 된 주석을 보려면 각 줄에서 주석 기호 (`'`)를 반복 합니다.

 각 문을 별도의 줄에 배치 하는 것이 좋습니다. Visual Basic을 사용 하면 여러 문을 같은 줄에 배치할 수도 있습니다.

## <a name="to-place-multiple-statements-on-the-same-line"></a>같은 줄에 여러 문을 추가 하려면

다음 예제와 같이 문을 콜론 (`:`)으로 구분 합니다.

  [!code-vb[VbVbcnConventions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#10)]

## <a name="see-also"></a>참고자료

- [프로그램 구조 및 코드 규칙](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [문(C++)](../../../visual-basic/programming-guide/language-features/statements.md)
