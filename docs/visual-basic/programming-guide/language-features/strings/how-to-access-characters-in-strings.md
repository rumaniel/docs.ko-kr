---
title: '방법: Visual Basic의 문자열에서 문자 액세스'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], accessing characters
- characters [Visual Basic], accessing in strings
ms.assetid: 02c5206c-ffab-494d-b648-3b2ea358dc34
ms.openlocfilehash: 840a769b0bb322ef7b878a312437c5ec200ab074
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62054031"
---
# <a name="how-to-access-characters-in-strings-in-visual-basic"></a>방법: Visual Basic의 문자열에서 문자 액세스
이 예제를 사용 하는 방법에 설명 합니다 <xref:System.String.Chars%2A> 속성에 액세스 하는 문자열의 지정된 된 위치에 있는 문자가 있습니다.  
  
## <a name="example"></a>예제  
 경우에 따라 문자열 내에서 해당 문자의 위치 및 문자열의 문자에 대 한 데이터가 있어야 유용 합니다. 문자열을 문자 배열로 생각할 수 있습니다 (`Char` 인스턴스);를 통해 해당 문자의 인덱스를 참조 하 여 특정 문자를 검색할 수 있습니다는 <xref:System.String.Chars%2A> 속성입니다.  
  
 [!code-vb[VbVbalrStrings#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#49)]  
  
 합니다 `index` 의 매개 변수는 <xref:System.String.Chars%2A> 속성은 0부터 시작 합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 <xref:System.String.Chars%2A> 속성이 지정된 된 위치에 문자를 반환 합니다. 그러나 둘 이상의 문자로 일부 유니코드 문자를 나타낼 수 있습니다. 유니코드 문자를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 문자 배열을 문자열로 변환할](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md)합니다.  
  
 합니다 <xref:System.String.Chars%2A> 속성을 <xref:System.IndexOutOfRangeException> 예외 경우는 `index` 매개 변수는 문자열의 길이 보다 크거나이 0 보다 작은 경우 또는  
  
## <a name="see-also"></a>참고자료

- <xref:System.String.Chars%2A>
- [방법: 문자열을 문자 배열로 변환](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md)
- [Visual Basic에서 문자열 및 기타 데이터 형식 사이에 변환](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)
- [문자열](../../../../visual-basic/programming-guide/language-features/strings/index.md)
