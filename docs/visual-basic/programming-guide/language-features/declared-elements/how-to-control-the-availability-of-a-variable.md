---
title: '방법: 변수 (Visual Basic)의 사용 가능성 제어'
ms.date: 07/20/2015
helpviewer_keywords:
- access levels, declared elements
- Private keyword [Visual Basic], accessing variables
- access levels, variables
- Public keyword [Visual Basic], accessing variables
- Friend keyword [Visual Basic], accessing variables
- variables [Visual Basic], access level
- declared elements [Visual Basic], access level
- Protected keyword [Visual Basic], accessing variables
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
ms.openlocfilehash: 419f3eed30a5d4b35bcb9dde5242b9092ee9cb79
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64610496"
---
# <a name="how-to-control-the-availability-of-a-variable-visual-basic"></a>방법: 변수 (Visual Basic)의 사용 가능성 제어
지정 하 여 변수의 사용 가능성 제어 해당 *액세스 수준*합니다. 액세스 수준 변수에 쓰거나 읽을 수 있는 코드를 결정 합니다.  
  
- *멤버 변수* (다른 프로시저 외부 모듈 수준에서 정의 됨) 기본적으로 공용 액세스를 확인 하는 코드에 액세스할 수 있습니다. 액세스 한정자를 지정 하 여이 변경할 수 있습니다.  
  
- *지역 변수* (프로시저 내에서 정의 됨)가 프로시저 내의 코드만 액세스할 수 있지만 공용 액세스를 명목상 있어야 합니다. 지역 변수에서의 액세스 수준을 변경할 수 없지만 포함 하는 프로시저의 액세스 수준을 변경할 수 있습니다.  
  
 자세한 내용은 [액세스 수준을 Visual Basic의](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.  
  
## <a name="private-and-public-access"></a>개인 및 공용 액세스  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-module-class-or-structure"></a>변수를 해당 모듈, 클래스 또는 구조체 내 에서만 액세스할 수 있도록 하려면  
  
1. 위치는 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md) 모듈, 클래스 또는 구조체 내 서 다른 프로시저 외부 변수에 대 한 합니다.  
  
2. 포함 된 [개인](../../../../visual-basic/language-reference/modifiers/private.md) 키워드를 `Dim` 문.  
  
     읽거나 아닌 하지만 모듈, 클래스 또는 구조체 내에서 변수를 쓸 수 밖에 있습니다.  
  
#### <a name="to-make-a-variable-accessible-from-any-code-that-can-see-it"></a>변수를 볼 수 있는 모든 코드에서 액세스할 수 있도록 하려면  
  
1. 멤버 변수를 배치 합니다 `Dim` 모듈, 클래스 또는 구조체 내 서 다른 프로시저 외부 변수에 대 한 문을 합니다.  
  
2. 포함 된 [공용](../../../../visual-basic/language-reference/modifiers/public.md) 키워드를 `Dim` 문.  
  
     읽기 또는 어셈블리를 사용 하 여 상호 운용 하는 코드에서 변수를 작성할 수 있습니다.  
  
 또는  
  
1. 지역 변수를 배치 합니다 `Dim` 문을 프로시저 내에서 변수에 대 한 합니다.  
  
2. 포함 되지 않습니다 합니다 `Public` 키워드는 `Dim` 문입니다.  
  
     읽기 또는 프로시저 내에서 아무 곳 이나 있지만 아닌에서 변수를 쓸 수 밖에 있습니다.  
  
## <a name="protected-and-friend-access"></a>보호 및 Friend 액세스  
 액세스 수준 또는 해당 어셈블리의 클래스와 모든 파생된 클래스에 변수를 제한할 수 있습니다. 또한 동일한 어셈블리의 다른 위치 또는 파생된 클래스에서 코드에서 액세스를 허용 하는 이러한 제한의 합집합을 지정할 수 있습니다. 결합 하 여이 공용 구조체를 지정 합니다 `Protected` 및 `Friend` 동일한 선언에서 키워드입니다.  
  
#### <a name="to-make-a-variable-accessible-only-from-within-its-class-and-any-derived-classes"></a>변수를 해당 클래스와 모든 파생된 클래스 내 에서만 액세스할 수 있도록 하려면  
  
1. 위치는 `Dim` 클래스 내부 이지만 다른 프로시저 외부 변수에 대 한 문입니다.  
  
2. 포함 된 [보호 된](../../../../visual-basic/language-reference/modifiers/protected.md) 키워드를 `Dim` 문.  
  
     읽거나,에서 파생 된 클래스 내에서 뿐만 아니라 해당 클래스에서 변수를 쓸 수 파생 체인의 모든 클래스 외부입니다.  
  
#### <a name="to-make-a-variable-accessible-only-from-within-the-same-assembly"></a>변수를 동일한 어셈블리 내 에서만 액세스할 수 있도록 하려면  
  
1. 위치는 `Dim` 모듈, 클래스 또는 구조체 내 서 다른 프로시저 외부 변수에 대 한 문입니다.  
  
2. 포함 된 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 키워드를 `Dim` 문.  
  
     읽거나 아닌 하지만 동일한 어셈블리의 코드 뿐만 아니라 모듈, 클래스 또는 구조체 내에서 변수를 쓸 수 어셈블리 외부에 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 하 여 변수의 선언을 `Public`, `Protected`를 `Friend`, `Protected Friend`, 및 `Private` 액세스 수준을 합니다. 경우는 `Dim` 문에 대 한 액세스 수준을 지정, 포함할 필요가 없습니다를 `Dim` 키워드입니다.  
  
```  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 더 제한적인 변수를 액세스 수준에 악성 코드가 부적절 하 게 가능성이 줄어듭니다 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 액세스 수준](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)
- [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)
- [공용](../../../../visual-basic/language-reference/modifiers/public.md)
- [보호됨](../../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)
- [전용](../../../../visual-basic/language-reference/modifiers/private.md)
