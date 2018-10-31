---
title: '방법: Visual Basic에서 문자열을 문자 배열로 변환'
ms.date: 07/20/2015
helpviewer_keywords:
- character arrays [Visual Basic], converting strings
- arrays [Visual Basic], converting strings to
- examples [Visual Basic], string conversion
- strings [Visual Basic], converting to arrays
- string conversion [Visual Basic], arrays
ms.assetid: 1b54b686-ab29-413b-adce-6bd5422376eb
ms.openlocfilehash: cc12b70cddcb93a72b4421a8ddd93542ef84f55b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50202764"
---
# <a name="how-to-convert-a-string-to-an-array-of-characters-in-visual-basic"></a>방법: Visual Basic에서 문자열을 문자 배열로 변환
경우에 따라 문자열을 구문 분석 하는 경우 처럼 문자열 내에서 해당 문자의 위치 및 문자열의 문자에 대 한 데이터가 있어야 유용 합니다. 문자열을 호출 하 여 문자열에서 문자의 배열을 가져올 수는 방법을 보여 주는이 예제 <xref:System.String.ToCharArray%2A> 메서드.  
  
## <a name="example"></a>예제  
 이 예제에서는 문자열을 분할 하는 방법에 설명를 `Char` 배열 및 문자열을 분할 하는 방법을 `String` 해당 유니코드 텍스트 문자의 배열입니다. 이러한 차이 대 한 이유는 두 개 이상의 유니코드 텍스트 문자를 구성할 수 있습니다 `Char` 문자 (서로게이트 쌍 등을 결합 문자 시퀀스). 자세한 내용은 <xref:System.Globalization.TextElementEnumerator> 하 고 [유니코드 표준](https://www.unicode.org/standard/standard.html)합니다.  
  
 [!code-vb[VbVbalrStrings#75](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_1.vb)]  
  
## <a name="example"></a>예제  
 유니코드 텍스트 문자를 문자열로 분할할 하기가 더 어렵습니다이 하지만 문자열의 시각적 표현에 대 한 정보가 필요한 경우에 필요 합니다. 이 예제에서는 <xref:System.Globalization.StringInfo.SubstringByTextElements%2A> 메서드 문자열을 구성 하는 유니코드 텍스트 문자에 대 한 정보입니다.  
  
 [!code-vb[VbVbalrStrings#76](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_2.vb)]  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.String.Chars%2A>  
 <xref:System.Globalization.StringInfo?displayProperty=nameWithType>  
 [방법: 문자열 안의 문자에 액세스](../../../../visual-basic/programming-guide/language-features/strings/how-to-access-characters-in-strings.md)  
 [Visual Basic에서 문자열 및 기타 데이터 형식 사이에 변환](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)  
 [문자열](../../../../visual-basic/programming-guide/language-features/strings/index.md)
