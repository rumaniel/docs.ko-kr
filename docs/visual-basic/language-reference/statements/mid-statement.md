---
title: Mid 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.MidB
- vb.Mid
helpviewer_keywords:
- substrings [Visual Basic], Mid statement
- strings [Visual Basic], substrings
- Mid statement [Visual Basic]
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
ms.openlocfilehash: 212ce1f06a01c39acbce43d8d069dae3526b1b4d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963546"
---
# <a name="mid-statement"></a>Mid 문
`String` 변수의 지정 된 문자 수를 다른 문자열의 문자로 바꿉니다.  
  
## <a name="syntax"></a>구문  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>요소  
 `Target`  
 필수. `String` 수정할 변수의 이름입니다.  
  
 `Start`  
 필수. `Integer` 식입니다. 텍스트 바꾸기가 시작 `Target` 되는의 문자 위치입니다. `Start`는 1부터 사용 하는 인덱스를 사용 합니다.  
  
 `Length`  
 선택 사항입니다. `Integer` 식입니다. 바꿀 문자 수입니다. 생략 하면 `String` 가 모두 사용 됩니다.  
  
 `StringExpression`  
 필수. `String`의 `Target`일부를 바꾸는 식입니다.  
  
## <a name="exceptions"></a>예외  
  
|예외 형식|조건|  
|--------------------|---------------|  
|<xref:System.ArgumentException>|`Start`< = 0 또는 `Length` < 0입니다.|  
  
## <a name="remarks"></a>설명  
 대체 되는 문자 수는 항상의 `Target`문자 수보다 작거나 같습니다.  
  
 Visual Basic에는 <xref:Microsoft.VisualBasic.Strings.Mid%2A> 함수 및 `Mid` 문입니다. 이러한 요소는 모두 문자열에서 문자의 지정된 된 수에 작동 하지만 `Mid` 해당 문자를 반환 하는 함수는 `Mid` 문은 문자를 대체 합니다. 자세한 내용은 <xref:Microsoft.VisualBasic.Strings.Mid%2A>을 참조하세요.  
  
> [!NOTE]
> 이전 버전의 Visual Basic 문은문자열이아닌바이트단위로대체합니다.`MidB` 더블 바이트 문자 집합 (DBCS) 애플리케이션의 문자열을 변환에 주로 사용 됩니다. 모든 Visual Basic 문자열은 유니코드, 및 `MidB` 는 지원 되지 않습니다.  
  
## <a name="example"></a>예제  
 이 예에서는 `Mid` 문을 사용 하 여 문자열 변수의 지정 된 문자 수를 다른 문자열의 문자로 바꿉니다.  
  
 [!code-vb[VbVbalrStrings#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#5)]  
  
## <a name="requirements"></a>요구 사항  
 **네임스페이스:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **모듈:** `Strings`  
  
 **어셈블리** Visual Basic 런타임 라이브러리(Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Strings.Mid%2A>
- [문자열](../../../visual-basic/programming-guide/language-features/strings/index.md)
- [Visual Basic의 문자열 소개](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
