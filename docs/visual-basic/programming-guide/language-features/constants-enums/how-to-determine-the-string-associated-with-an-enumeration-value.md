---
title: '방법: 열거형 값 (Visual Basic)를 사용 하 여 연결 문자열 확인'
ms.date: 07/20/2015
helpviewer_keywords:
- enumerations [Visual Basic]
- strings [Visual Basic], enumeration values
- values [Visual Basic], enumeration members
ms.assetid: 9253e7c8-579c-49a2-8f26-392b20ea99eb
ms.openlocfilehash: 25c55c14507c67b9bdd8606cb85afd55f9a748fa
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610539"
---
# <a name="how-to-determine-the-string-associated-with-an-enumeration-value-visual-basic"></a>방법: 열거형 값 (Visual Basic)를 사용 하 여 연결 문자열 확인
합니다 <xref:System.Enum.GetValues%2A> 고 <xref:System.Enum.GetNames%2A> 메서드를 사용 하는 문자열과 열거형 멤버와 연결 된 값을 확인할 수 있습니다.  
  
### <a name="to-determine-the-string-associated-with-an-enumeration"></a>열거형을 사용 하 여 연결 된 문자열을 확인 하려면  
  
- 사용 된 <xref:System.Enum.GetNames%2A> 열거형 멤버와 연결 된 문자열을 검색 하는 방법입니다. 이 예제에서는 열거형 선언 `flavorEnum`를 사용 하 여는 <xref:System.Enum.GetNames%2A> 각 멤버와 연결 된 문자열을 표시 하는 방법입니다.  
  
     [!code-vb[VbEnumsTask#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Enum.GetValues%2A>
- <xref:System.Enum.GetNames%2A>
- <xref:System.Enum>
- [방법: 열거형 선언](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [방법: 열거형 멤버 참조](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [열거형 및 이름 한정](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [방법: Visual Basic에서 열거형 반복](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [열거형을 사용하는 경우](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)
