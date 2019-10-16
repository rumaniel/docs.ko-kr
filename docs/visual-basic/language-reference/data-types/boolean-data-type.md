---
title: Boolean 데이터 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.FALSE
- vb.TRUE
- vb.Boolean
helpviewer_keywords:
- Boolean data type
- Boolean values [Visual Basic], False keyword
- False keyword [Visual Basic]
- True keyword [Visual Basic]
- Boolean values [Visual Basic], True keyword
ms.assetid: 4858e630-4813-4216-a55e-f4d0feb884e4
ms.openlocfilehash: b1e4add39cee6c733a6f4b95aa1668975f2f2d6d
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268258"
---
# <a name="boolean-data-type-visual-basic"></a>Boolean 데이터 형식(Visual Basic)
만 될 수 있는 값을 포함 `True` 또는 `False`합니다. 키워드 `True` 하 고 `False` 의 두 가지 상태에 해당 `Boolean` 변수입니다.  
  
## <a name="remarks"></a>설명  
 사용 합니다 [Boolean 데이터 형식 (Visual Basic)](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 예/아니요 또는 켜기/끄기 true/false와 같은 두 가지 상태 값을 포함 합니다.  
  
 `Boolean` 의 기본값은 `False`입니다.  
  
 `Boolean` 값은 숫자로 저장 되지 및 저장 된 값은 숫자에 해당 되지 않아야 합니다. 에 해당 하는 숫자 값을 사용 하는 코드를 작성 하지 말아야 `True` 고 `False`입니다. 사용을 제한 해야 가능 하면 `Boolean` 변수는 설계 하는 논리 값입니다.  
  
## <a name="type-conversions"></a>형식 변환  
 Visual Basic 숫자 데이터 형식 값을 변환 하는 경우 `Boolean`를 0 됩니다 `False` 고 다른 모든 값은 `True`합니다. Visual Basic로 변환 하는 경우 `Boolean` 값을 숫자 형식으로 `False` 는 0이 되 고 `True` 는-1입니다.  
  
 간에 변환할 경우 `Boolean` 값 및 숫자 데이터 형식의 경우 염두에.NET Framework 변환 메서드 항상 Visual Basic 변환 키워드와 동일한 결과 생성 하 고 있지 않습니다. 이전 버전과 호환 되는 동작을 유지 하는 Visual Basic 변환 때문입니다. 자세한 내용은 "부울 형식에 변환에 숫자 형식을 정확 하 게"의 참조 [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)합니다.  
  
## <a name="programming-tips"></a>프로그래밍 팁  
  
- **음수를 사용할 수 있습니다.** `Boolean` 숫자 형식이 아닌 및 음수 값을 나타낼 수 없습니다. 사용 하지 않아야 어떤 경우 든 `Boolean` 숫자 값을 포함 하도록 합니다.  
  
- **형식 문자입니다.** `Boolean` 에 리터럴 형식 문자 또는 식별자 형식 문자가 없습니다.  
  
- **Framework 형식입니다.** .NET Framework에서 해당하는 형식은 <xref:System.Boolean?displayProperty=nameWithType> 구조체입니다.  
  
## <a name="example"></a>예제  
 다음 예에서 `runningVB` 는 `Boolean` 간단한 예/아니요 설정을 저장 하는 변수입니다.  
  
```vb  
Dim runningVB As Boolean  
' Check to see if program is running on Visual Basic engine.  
If scriptEngine = "VB" Then  
    runningVB = True  
End If  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Boolean?displayProperty=nameWithType>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [CType 함수](../../../visual-basic/language-reference/functions/ctype-function.md)
