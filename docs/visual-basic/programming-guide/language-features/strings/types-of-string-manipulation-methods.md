---
title: Visual Basic의 문자열 조작 메서드 유형
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], manipulating [Visual Basic]
- string manipulation
ms.assetid: 905055cd-7f50-48fb-9eed-b0995af1dc1f
ms.openlocfilehash: 44eb101ebdfeb316958a659107190ef1fc84df44
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938270"
---
# <a name="types-of-string-manipulation-methods-in-visual-basic"></a>Visual Basic의 문자열 조작 메서드 유형
분석 하 고 문자열을 조작 하는 여러 가지가 있습니다. 메서드 중 일부는 Visual Basic 언어의 일부인 있고에 내재 된 `String` 클래스.  
  
## <a name="visual-basic-language-and-the-net-framework"></a>Visual Basic 언어 및.NET Framework  
 Visual Basic 메서드는 언어의 기본 기능으로 사용 됩니다. 코드에서 자격 증명 없이 사용할 수 있습니다. 다음 예제에서는 일반적인 Visual Basic 문자열 조작 명령 사용 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrStrings#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#44)]  
  
 이 예제는 `Mid` 함수에서 직접 작업을 수행 `aString` 값을 할당 하 고 `bString`입니다.  
  
 Visual Basic 문자열 조작 메서드 목록을 참조 하세요 [문자열 조작 요약](../../../../visual-basic/language-reference/keywords/string-manipulation-summary.md)합니다.  
  
### <a name="shared-methods-and-instance-methods"></a>공유 메서드와 인스턴스 메서드  
 메서드를 사용 하 여 문자열을 조작할 수도 있습니다는 `String` 클래스입니다. 메서드는 방법은 두 가지가 `String`: *공유* 메서드 및 *인스턴스* 메서드.  
  
#### <a name="shared-methods"></a>공유 메서드  
 발생 하는 방법은 공유 메서드는 `String` 클래스 자체와 작동 하도록 해당 클래스의 인스턴스를 필요로 하지 않습니다. 이러한 메서드는 클래스의 이름으로 한정할 수 있습니다 (`String`)의 인스턴스 대신는 `String` 클래스입니다. 예를 들어:  
  
 [!code-vb[VbVbalrStrings#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#45)]  
  
 앞의 예제에는 <xref:System.String.Copy%2A?displayProperty=nameWithType> 메서드는 정적 메서드를 식에 사용 되는 역할은 지정 하 고 결과 값을 할당 `bString`합니다.  
  
#### <a name="instance-methods"></a>인스턴스 메서드  
 인스턴스 메서드는 반면,의 특정 인스턴스에서 stem `String` 및 인스턴스 이름으로 정규화 해야 합니다. 예를 들어:  
  
 [!code-vb[VbVbalrStrings#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#46)]  
  
 이 예제는 <xref:System.String.Substring%2A?displayProperty=nameWithType> 메서드는 인스턴스 메서드입니다 `String` (즉, `aString`). 작업 수행 `aString` 해당 값을 할당 하 고 `bString`입니다.  
  
 자세한 내용은 설명서를 참조 합니다 <xref:System.String> 클래스입니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 문자열 소개](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
