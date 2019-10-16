---
title: Implements 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Implements
- Implements
helpviewer_keywords:
- Implements statement [Visual Basic], syntax
- Implements statement [Visual Basic]
- interface implementation [Visual Basic], Implements statement
ms.assetid: 1fafb83f-f55a-4215-8ea9-681e8622613d
ms.openlocfilehash: 1f0c6b052ead303e0b43465dac2067422abc4ef8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61637741"
---
# <a name="implements-statement"></a>Implements 문
인터페이스 또는 클래스에서 구현 해야 하는 인터페이스 멤버의 경우 또는 나타나는 구조 정의 하나 이상 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Implements interfacename [, ...]  
-or-  
Implements interfacename.interfacemember [, ...]  
```  
  
## <a name="parts"></a>요소  
 `interfacename`  
 필수 요소. 해당 속성, 프로시저 및 이벤트 클래스 또는 구조체에서 해당 멤버에 의해 구현 되어야 하는 인터페이스입니다.  
  
 `interfacemember`  
 필수 요소. 구현 되는 인터페이스의 멤버입니다.  
  
## <a name="remarks"></a>설명  
 인터페이스는 컬렉션의 프로토타입 멤버 (속성, 프로시저 및 이벤트)를 나타내는 인터페이스를 캡슐화 합니다. 인터페이스 멤버;에 대 한 선언에만 포함 클래스와 구조체는 이러한 멤버를 구현합니다. 자세한 내용은 [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)를 참조하세요.  
  
 합니다 `Implements` 문 바로 뒤에 나와야 합니다 `Class` 또는 `Structure` 문.  
  
 인터페이스를 구현 하는 경우 인터페이스에서 선언 된 모든 멤버를 구현 해야 합니다. 모든 멤버를 생략 하면 구문 오류가 있는 것으로 간주 됩니다. 개별 멤버를 구현 하려면 지정 합니다 [구현](../../../visual-basic/language-reference/statements/implements-clause.md) 키워드 (분리 되는 `Implements` 문) 클래스 또는 구조체에서 멤버를 선언 하는 경우. 자세한 내용은 [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)를 참조하세요.  
  
 클래스를 사용할 수 있습니다 [개인](../../../visual-basic/language-reference/modifiers/private.md) 속성 프로시저 하며 이러한 멤버의 구현을 인터페이스의 형식으로 선언 된 변수를 구현 하는 클래스의 인스턴스로 캐스팅 액세스할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 하는 방법의 `Implements` 인터페이스의 멤버를 구현 하는 문입니다. 라는 인터페이스가 정의 `ICustomerInfo` 이벤트, 속성 및 프로시저를 사용 하 여 합니다. 클래스 `customerInfo` 인터페이스에 정의 된 모든 멤버를 구현 합니다.  
  
 [!code-vb[VbVbalrStatements#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#33)]  
  
 클래스 `customerInfo` 사용 하는 `Implements` 클래스의 모든 멤버를 구현 함을 나타내기 위해 별도 소스 코드 줄에서 문은 `ICustomerInfo` 인터페이스입니다. 각 멤버는 클래스에서 사용 하 여는 `Implements` 키워드는 인터페이스 멤버를 구현 함을 나타내려면 멤버 선언의 일부로 합니다.  
  
## <a name="example"></a>예제  
 다음 두 절차 앞의 예제에서 구현 된 인터페이스를 사용 하는 방법을 보여 줍니다. 구현을 테스트 하려면 다음이 절차 호출 프로젝트에 추가 된 `testImplements` 프로시저입니다.  
  
 [!code-vb[VbVbalrStatements#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#34)]  
  
## <a name="see-also"></a>참고자료

- [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
