---
title: 배열 변환(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [Visual Basic], converting type
- type conversion [Visual Basic], arrays
- conversions [Visual Basic], type
- arrays [Visual Basic], data types
- conversions [Visual Basic], data type
- object arrays [Visual Basic], converting type
- data type conversion [Visual Basic], array conversions
- conversions [Visual Basic], array types
- object arrays
ms.assetid: fceff7d2-a1b7-44c7-b9aa-8bd831d8a444
ms.openlocfilehash: f69ed6e0040f33f810d324a76859d448e9dc7632
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64601137"
---
# <a name="array-conversions-visual-basic"></a>배열 변환(Visual Basic)
다음 조건이 충족 되는 배열 형식 다른 배열 형식으로 변환할 수 있습니다.  
  
- **동일한 차수입니다.** 두 배열의 차수가 동일 해야, 즉, 동일한 차원 수 있어야 합니다. 그러나 각 차원의 길이 같이 필요가 없습니다.  
  
- **요소 데이터 형식입니다.** 두 배열 요소의 데이터 형식에는 참조 형식 이어야 합니다. 변환할 수 없습니다는 `Integer` 배열을 `Long` 배열 또는 심지어는 `Object` 하나 이상의 값 형식이 포함 되어 있으므로 배열입니다. 자세한 내용은 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)을 참조하세요.  
  
- **변환 가능성입니다.** 두 배열의 요소 형식 간에 변환, 확대 또는 축소 수 있어야 합니다. 이 요구 사항은 실패 하는 예제는 간의 변환 된 `String` 에서 파생 된 클래스의 배열 및 배열 <xref:System.Attribute?displayProperty=nameWithType>합니다. 이러한 두 형식 nothing 공통적으로 있고 어떤 종류의 변환 작업 없이 서로 간에 존재 합니다.  
  
 다른 배열 형식 변환을 확대 되었거나 해당 요소의 변환을 확대 또는 축소 하는 여부에 따라 축소 됩니다. 자세한 내용은 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)을 참조하세요.  
  
## <a name="conversion-to-an-object-array"></a>개체 배열로 변환  
 선언 하는 경우는 `Object` 초기화 하지 않고, 해당 요소 형식 배열이 `Object` 으로 초기화 되지 않은 상태로 유지 됩니다. 특정 클래스의 배열에 설정 하는 경우 해당 클래스의 형식에 적용 됩니다. 그러나 기본 형식과 여전히 `Object`, 및 관련된 클래스의 다른 배열에 이후에 설정할 수 있습니다. 모든 클래스에서 파생 되므로 `Object`, 다른 클래스에 모든 클래스에서 배열의 요소 형식을 변경할 수 있습니다.  
  
 다음 예제에서는 형식 간의 변환이 존재 `student` 하 고 `String`에서 파생 되지만 `Object`이므로 모든 할당은 유효 합니다.  
  
```  
' Assume student has already been defined as a class.  
Dim testArray() As Object  
' testArray is still an Object array at this point.  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
testArray = New student(3) {}  
' testArray is now of type student().  
testArray = names  
' testArray is now a String array.  
```  
  
### <a name="underlying-type-of-an-array"></a>기본 형식의 배열  
 특정 클래스를 사용 하 여 배열, 원래 선언 하는 경우의 기본 요소 형식은 해당 클래스를입니다. 이후에 설정 하면 다른 클래스의 배열에 두 클래스 간의 변환과 이어야 합니다.  
  
 다음 예에서 `students` 되는 `student` 배열입니다. 변환 작업 없이 사이 존재 하므로 `String` 및 `student`, 마지막 문이 실패 합니다.  
  
```  
Dim students() As student  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
students = New Student(3) {}  
' The following statement fails at compile time.  
students = names  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Visual Basic의 형식 변환](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [암시적 변환과 명시적 변환](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [문자열과 다른 형식 사이의 변환](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)
- [방법: Visual Basic에서 다른 형식으로 변환할 개체](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)
- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
