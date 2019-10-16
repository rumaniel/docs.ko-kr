---
title: '방법: Visual Basic에서 열거형 반복'
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [Visual Basic], iterating
- enumerations [Visual Basic], iterating
- ListBox control [Windows Forms], populating from an enumeration
ms.assetid: e5aa10eb-cfcd-4a3b-8e76-f06b8f2002be
ms.openlocfilehash: c3fd7e6f7e8e4fcabf279975f7ffc2d848679396
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645243"
---
# <a name="how-to-iterate-through-an-enumeration-in-visual-basic"></a>방법: Visual Basic에서 열거형 반복
열거형은 관련된 상수 집합으로 작업하고 이름과 상수 값을 연결하는 편리한 방법을 제공합니다. 열거자를 반복 하려면 이동할 수 있습니다. 사용 하 여 배열에는 <xref:System.Enum.GetValues%2A> 메서드. 사용 하 여 열거형을 반복할 수도 있습니다는 `For...Each` 문을 사용 하 여는 <xref:System.Enum.GetNames%2A> 또는 <xref:System.Enum.GetValues%2A> 문자열 또는 숫자 값을 추출 하는 방법입니다.  
  
### <a name="to-iterate-through-an-enumeration"></a>열거형 반복  
  
- 배열을 선언 하 고 열거를 사용 하 여 변환할는 <xref:System.Enum.GetValues%2A> 배열으로 전달 하기 전에 메서드는 다른 변수입니다. 다음 예제에서는 열거형의 각 멤버 <xref:Microsoft.VisualBasic.FirstDayOfWeek> 열거형 반복으로 합니다.  
  
     [!code-vb[VbEnumsTask#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#7)]  
  
## <a name="see-also"></a>참고자료

- [열거형 개요](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [방법: 열거형 값과 연결 된 문자열 확인](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
