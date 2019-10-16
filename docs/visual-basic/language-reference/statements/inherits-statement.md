---
title: Inherits 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Inherits
- Inherits
helpviewer_keywords:
- Inherits statement [Visual Basic]
- Inherits statement [Visual Basic], syntax
ms.assetid: 9e6fe042-9af3-4341-8093-fc3537770cf2
ms.openlocfilehash: c39272d53fea136c83a5a09444b65a594fe3b7a7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625519"
---
# <a name="inherits-statement"></a>Inherits Statement
현재 클래스 또는 인터페이스가 다른 클래스나 인터페이스 집합에서 특성, 변수, 속성, 프로시저 및 이벤트를 상속 하도록 하면 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
Inherits basetypenames  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`basetypenames`|필수 요소. 이 클래스가 파생 되는 클래스의 이름입니다.<br /><br /> 또는<br /><br /> 이 인터페이스 파생 되는 인터페이스의 이름입니다. 여러 이름을 구분 하려면 쉼표를 사용 합니다.|  
  
## <a name="remarks"></a>설명  
 를 사용 하는 경우는 `Inherits` 문은 클래스 또는 인터페이스 정의에서 공백 및 주석이 아닌 첫 번째 줄을 이어야 합니다. 다음에 나와야 합니다 `Class` 또는 `Interface` 문입니다.  
  
 사용할 수 있습니다 `Inherits` 클래스 또는 인터페이스에만 합니다. 즉, 원본 파일, 네임 스페이스, 구조체, 모듈, 프로시저 또는 블록 상속에 대 한 선언 컨텍스트 수 없습니다.  
  
## <a name="rules"></a>규칙  
  
- **클래스를 상속 합니다.** 클래스를 사용 하는 경우는 `Inherits` 문을 하나의 기본 클래스만 지정할 수 있습니다.  
  
     클래스는 그 안에 중첩 된 클래스에서 상속할 수 없습니다.  
  
- **인터페이스 상속 합니다.** 인터페이스를 사용 하는 경우는 `Inherits` 문에서 하나 이상의 기본 인터페이스를 지정할 수 있습니다. 동일한 이름 가진 멤버를 정의 하는 경우에 두 개의 인터페이스에서 상속할 수 있습니다. 이렇게 하면 구현 코드를 구현 하는 멤버를 지정 하려면 이름 한정을 사용 해야 합니다.  
  
     인터페이스는 더 제한적인 액세스 수준 가진 다른 인터페이스에서 상속할 수 없습니다. 예를 들어, 한 `Public` 인터페이스에서 상속할 수 없습니다는 `Friend` 인터페이스입니다.  
  
     인터페이스 내에 중첩 된 인터페이스에서 상속할 수 없습니다.  
  
 .NET Framework의 클래스 상속의 예로 <xref:System.ArgumentException> 클래스에서 상속 하는 <xref:System.SystemException> 클래스입니다. 이를 제공 <xref:System.ArgumentException> 미리 정의 된 속성과 시스템 예외와 같은 필요한 절차는 <xref:System.Exception.Message%2A> 속성 및 <xref:System.Exception.ToString%2A> 메서드.  
  
 .NET Framework의 상속은 인터페이스의 예로 <xref:System.Collections.ICollection> 인터페이스에서 상속 하는 <xref:System.Collections.IEnumerable> 인터페이스입니다. 이 인해 <xref:System.Collections.ICollection> 컬렉션을 이동 하는 데 필요한 열거자의 정의 상속 하도록 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 합니다 `Inherits` 라는 클래스를 표시 하는 문을 `thisClass` 라는 기본 클래스의 모든 멤버를 상속할 수 `anotherClass`입니다.  
  
 [!code-vb[VbVbalrStatements#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#37)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 여러 인터페이스의 상속을 보여 줍니다.  
  
 [!code-vb[VbVbalrStatements#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#38)]  
  
 라는 인터페이스 `thisInterface` 이제에서 모든 정의 포함 합니다 <xref:System.IComparable>를 <xref:System.IDisposable>, 및 <xref:System.IFormattable> 상속된 된 멤버 각각에 대 한 제공 두 개체의 형식 고유의 비교를 해제 하는 인터페이스에 할당 된 리소스 개체의 값을 표현 하 고는 `String`합니다. 구현 하는 클래스 `thisInterface` 모든 기본 인터페이스의 모든 멤버를 구현 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)
- [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)
- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
