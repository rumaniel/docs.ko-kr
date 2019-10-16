---
title: 개체 변수 값(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], values
- values [Visual Basic], of object variables
- data types [Visual Basic], object variable
- variables [Visual Basic], object
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
ms.openlocfilehash: 728f097b3c084e5292cb2d2bf5a0c1d20bdad922
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004589"
---
# <a name="object-variable-values-visual-basic"></a>개체 변수 값(Visual Basic)
[Object 데이터 형식의](../../../../visual-basic/language-reference/data-types/object-data-type.md) 변수는 모든 형식의 데이터를 참조할 수 있습니다. @No__t-0 변수에 저장 하는 값은 메모리의 다른 위치에 유지 되는 반면 변수 자체는 데이터에 대 한 포인터를 보유 합니다.  
  
## <a name="object-classifier-functions"></a>개체 분류자 함수  
 Visual Basic는 다음 표에 나와 있는 것 처럼 @no__t 0 변수가 참조 하는 항목에 대 한 정보를 반환 하는 함수를 제공 합니다.  
  
|기능|개체 변수가 참조 하는 경우 True를 반환 합니다.|  
|--------------|---------------------------------------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A>|단일 값이 아닌 값의 배열입니다.|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A>|날짜 [데이터 형식](../../../../visual-basic/language-reference/data-types/date-data-type.md) 값 또는 날짜 및 시간 값으로 해석 될 수 있는 문자열입니다.|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|누락 되거나 존재 하지 않는 데이터를 나타내는 <xref:System.DBNull> 형식의 개체입니다.|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A>|@No__t에서 파생 되는 예외 개체입니다.|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[Nothing](../../../../visual-basic/language-reference/nothing.md), 즉 변수에 현재 할당 된 개체가 없습니다.|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|숫자 또는 숫자로 해석할 수 있는 문자열입니다.|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A>|참조 형식 (예: 문자열, 배열, 대리자 또는 클래스 형식)|  
  
 이러한 함수를 사용 하 여 작업 또는 프로시저에 잘못 된 값을 제출 하지 않도록 방지할 수 있습니다.  
  
## <a name="typeof-operator"></a>TypeOf 연산자  
 [TypeOf 연산자](../../../../visual-basic/language-reference/operators/typeof-operator.md) 를 사용 하 여 현재 개체 변수가 특정 데이터 형식을 참조 하는지 여부를 확인할 수도 있습니다. @No__t-0 ... `Is` 식은 피연산자의 런타임 형식이에서 파생 되거나 지정 된 형식을 구현 하는 경우에 `True`로 계산 됩니다.  
  
 다음 예에서는 값과 참조 형식을 참조 하는 개체 변수에 대해 `TypeOf`을 사용 합니다.  
  
```vb  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 앞의 예제에서는 **디버그** 창에 다음 줄을 씁니다.  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 개체 변수 `num`은 `Integer` 형식의 데이터를 참조 하 고, `frm`는 <xref:System.Windows.Forms.Form> 클래스의 개체를 참조 합니다.  
  
## <a name="object-arrays"></a>개체 배열  
 @No__t-0 변수의 배열을 선언 하 고 사용할 수 있습니다. 이는 다양 한 데이터 형식 및 개체 클래스를 처리 해야 하는 경우에 유용 합니다. 배열의 모든 요소에는 동일한 선언 된 데이터 형식이 있어야 합니다. 이 데이터 형식을 `Object`으로 선언 하면 개체와 클래스 인스턴스를 배열에 있는 다른 데이터 형식과 함께 저장할 수 있습니다.  
  
## <a name="see-also"></a>참조

- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 선언](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [개체 변수 할당](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)
- [방법: 개체의 현재 인스턴스 @ no__t-0을 참조 하십시오.
- [방법: 개체 변수가 참조 하는 형식 확인 @ no__t-0
- [방법: 두 개체가 관련 되어 있는지 확인 @ no__t-0
- [방법: 두 개체가 동일한 지 여부를 확인 합니다. @ no__t-0
- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
