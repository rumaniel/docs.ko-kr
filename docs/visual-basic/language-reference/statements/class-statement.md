---
title: Class 문(Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Class
helpviewer_keywords:
- class modules
- Class statement [Visual Basic]
- classes [Visual Basic], fields
- fields [Visual Basic], of classes
- class types [Visual Basic], class statements
- classes [Visual Basic], creating
- classes [Visual Basic], data members
- data members [Visual Basic], of classes
ms.assetid: f2664f38-eb5a-4d4b-a374-1d041521fb6c
ms.openlocfilehash: 2e4514686afcbbe0e9ff0b3326c1be212db4f9f8
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005158"
---
# <a name="class-statement-visual-basic"></a>Class 문(Visual Basic)
클래스의 이름을 선언 하 고 클래스에서 구성 하는 변수, 속성, 이벤트 및 프로시저의 정의를 소개 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ MustInherit | NotInheritable ] [ Partial ] _  
Class name [ ( Of typelist ) ]  
    [ Inherits classname ]  
    [ Implements interfacenames ]  
    [ statements ]  
End Class  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`attributelist`|(선택 사항) [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)을 참조 하십시오.|  
|`accessmodifier`|(선택 사항) 다음 중 하나일 수 있습니다.<br /><br /> -   [공용](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [보호](../../../visual-basic/language-reference/modifiers/protected.md) 됨<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [개인](../../../visual-basic/language-reference/modifiers/private.md)<br />-   으로[보호 된 Friend](../../language-reference/modifiers/protected-friend.md)<br />- [개인 보호](../../language-reference/modifiers/private-protected.md) 됨<br/><br/> [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.|  
|`Shadows`|(선택 사항) [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)를 참조 하세요.|  
|`MustInherit`|(선택 사항) [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)을 참조 하십시오.|  
|`NotInheritable`|(선택 사항) [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)를 참조 하세요.|  
|`Partial`|(선택 사항) 클래스의 부분 정의를 나타냅니다. [부분](../../../visual-basic/language-reference/modifiers/partial.md)을 참조 하세요.|  
|`name`|필수. 이 클래스의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.|  
|`Of`|(선택 사항) 제네릭 클래스 임을 지정 합니다.|  
|`typelist`|[Of](../../../visual-basic/language-reference/statements/of-clause.md) 키워드를 사용 하는 경우 필수 사항입니다. 이 클래스에 대 한 형식 매개 변수 목록입니다. [형식 목록](../../../visual-basic/language-reference/statements/type-list.md)을 참조 하십시오.|  
|`Inherits`|(선택 사항) 이 클래스가 다른 클래스의 멤버를 상속 함을 나타냅니다. [Inherits 문](../../../visual-basic/language-reference/statements/inherits-statement.md)을 참조 하세요.|  
|`classname`|@No__t-0 문을 사용 하는 경우 필요 합니다. 이 클래스가 파생 되는 클래스의 이름입니다.|  
|`Implements`|(선택 사항) 이 클래스가 하나 이상의 인터페이스의 멤버를 구현 함을 나타냅니다. [Implements 문](../../../visual-basic/language-reference/statements/implements-statement.md)을 참조 하세요.|  
|`interfacenames`|@No__t-0 문을 사용 하는 경우 필요 합니다. 이 클래스가 구현 하는 인터페이스의 이름입니다.|  
|`statements`|(선택 사항) 이 클래스의 멤버를 정의 하는 문입니다.|  
|`End Class`|필수. @No__t-0 정의를 종료 합니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 문은 새 데이터 형식을 정의 합니다. *클래스* 는 OOP (개체 지향 프로그래밍)의 기본 빌딩 블록입니다. 자세한 내용은 [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)를 참조 하세요.  
  
 @No__t-0은 네임 스페이스 또는 모듈 수준 에서만 사용할 수 있습니다. 즉, 클래스의 *선언 컨텍스트* 는 소스 파일, 네임 스페이스, 클래스, 구조체, 모듈 또는 인터페이스 여야 하며 프로시저 또는 블록일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 클래스의 각 인스턴스에는 다른 모든 인스턴스와 독립적인 수명이 있습니다. 이 수명은 [새 Operator](../../../visual-basic/language-reference/operators/new-operator.md) 절 또는 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>과 같은 함수에 의해 생성 될 때 시작 됩니다. 인스턴스를 가리키는 모든 변수가 [Nothing](../../../visual-basic/language-reference/nothing.md) 또는 다른 클래스의 인스턴스로 설정 된 경우 종료 됩니다.  
  
 클래스의 기본값은 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 액세스입니다. 액세스 한정자를 사용 하 여 액세스 수준을 조정할 수 있습니다. 자세한 내용은 [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
## <a name="rules"></a>규칙  
  
- **중첩할.** 다른 클래스 내에서 클래스 하나를 정의할 수 있습니다. 외부 클래스를 *포함 하는 클래스*라고 하 고 내부 클래스를 *중첩 클래스*라고 합니다.  
  
- **상속.** 클래스가 [Inherits 문을](../../../visual-basic/language-reference/statements/inherits-statement.md)사용 하는 경우 기본 클래스 또는 인터페이스를 하나만 지정할 수 있습니다. 클래스는 둘 이상의 요소에서 상속할 수 없습니다.  
  
     클래스는 더 제한적인 액세스 수준을 가진 다른 클래스에서 상속할 수 없습니다. 예를 들어 `Public` 클래스는 `Friend` 클래스에서 상속할 수 없습니다.  
  
     클래스는 그 안에 중첩 된 클래스에서 상속할 수 없습니다.  
  
- **구현이.** 클래스에서 [Implements 문을](../../../visual-basic/language-reference/statements/implements-statement.md)사용 하는 경우 `interfacenames`에서 지정 하는 모든 인터페이스에서 정의 된 모든 멤버를 구현 해야 합니다. 이에 대 한 예외는 기본 클래스 멤버의 재구현입니다. 자세한 내용은 [Implements](../../../visual-basic/language-reference/statements/implements-clause.md)의 "재구현"를 참조 하십시오.  
  
- **기본 속성입니다.** 클래스는 최대 하나의 속성을 *기본 속성*으로 지정할 수 있습니다. 자세한 내용은 [기본값](../../../visual-basic/language-reference/modifiers/default.md)을 참조 하세요.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 클래스 내에서 각 멤버를 고유한 액세스 수준으로 선언할 수 있습니다. 클래스 멤버는 기본적으로 [Private](../../../visual-basic/language-reference/modifiers/private.md) access로 사용 되는 변수 및 상수를 제외 하 고 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스를 사용 합니다. 클래스의 멤버 중 하나 보다 제한 된 액세스 권한이 있는 경우 클래스 액세스 수준이 우선적으로 적용 됩니다.  
  
- **범위.** 클래스는 포함 하는 네임 스페이스, 클래스, 구조체 또는 모듈 전체에 걸쳐 있습니다.  
  
     모든 클래스 멤버의 범위는 전체 클래스입니다.  
  
     **수명.** Visual Basic는 정적 클래스를 지원 하지 않습니다. 정적 클래스와 동일한 기능을 모듈에서 제공 합니다. 자세한 내용은 [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)을 참조 하세요.  
  
     클래스 멤버의 수명은 선언 된 방법과 위치에 따라 달라 집니다. 자세한 내용은 [Visual Basic 수명](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)을 참조 하세요.  
  
- **조인의.** 클래스 외부의 코드는 해당 클래스의 이름을 사용 하 여 멤버의 이름을 정규화 해야 합니다.  
  
     중첩 된 클래스 내의 코드가 프로그래밍 요소에 대 한 정규화 되지 않은 참조를 만드는 경우, Visual Basic는 중첩 된 클래스에서 먼저 요소를 검색 한 다음 해당 요소를 포함 하는 클래스에서 가장 바깥쪽 포함 요소로 검색 합니다.  
  
## <a name="classes-and-modules"></a>클래스 및 모듈  
 이러한 요소에는 여러 가지 유사점이 있지만 몇 가지 중요 한 차이점도 있습니다.  
  
- **기술.** 이전 버전의 Visual Basic에서는 *클래스 모듈* (cls 파일)과 *표준 모듈* (bas 파일)의 두 가지 모듈 형식을 인식 합니다. 현재 버전은 이러한 *클래스* 및 *모듈*을 각각 호출 합니다.  
  
- **공유 멤버.** 클래스의 멤버가 공유 또는 인스턴스 멤버 인지 여부를 제어할 수 있습니다.  
  
- **개체 방향입니다.** 클래스는 개체 지향적 이지만 모듈은 그렇지 않습니다. 클래스의 인스턴스를 하나 이상 만들 수 있습니다. 자세한 내용은 [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Class` 문을 사용 하 여 클래스와 여러 멤버를 정의 합니다.  
  
 [!code-vb[VbVbalrStatements#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#62)]  
  
## <a name="see-also"></a>참조

- [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [구조체와 클래스](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [ 개체 수명: 개체를 만들고 제거 하는 방법 @ no__t-0
- [Generic Types in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [방법: 제네릭 클래스 사용](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
