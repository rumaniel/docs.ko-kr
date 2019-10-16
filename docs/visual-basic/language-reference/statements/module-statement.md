---
title: Module 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Module
- vb.Module
helpviewer_keywords:
- modules, classes
- modules
- Module statement [Visual Basic]
- modules, declaring
- standard modules
- classes [Visual Basic], vs. modules
- declarations [Visual Basic], modules
ms.assetid: a1243afc-14a5-45df-95d5-51118aeac362
ms.openlocfilehash: 08268fd473a3a916f41f2f46090e3245acda07dd
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68513013"
---
# <a name="module-statement"></a>Module 문
모듈 이름을 선언 하 고 모듈에서 구성 하는 변수, 속성, 이벤트 및 프로시저의 정의를 소개 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb 
[ <attributelist> ] [ accessmodifier ]  Module name  
    [ statements ]  
End Module  
```  
  
## <a name="parts"></a>요소  
 `attributelist`  
 선택 사항입니다. [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)을 참조 하십시오.  
  
 `accessmodifier`  
 선택 사항입니다. 다음 중 하나일 수 있습니다.  
  
- [공개](../../../visual-basic/language-reference/modifiers/public.md)  
  
- [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
 [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.  
  
 `name`  
 필수 요소. 이 모듈의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.  
  
 `statements`  
 선택 사항입니다. 이 모듈의 변수, 속성, 이벤트, 프로시저 및 중첩 형식을 정의 하는 문입니다.  
  
 `End Module`  
 정의를 `Module` 종료 합니다.  
  
## <a name="remarks"></a>설명  
 `Module` 문은 네임 스페이스 전체에서 사용할 수 있는 참조 형식을 정의 합니다. *모듈* ( *표준 모듈이*라고도 함)은 클래스와 비슷하지만 몇 가지 중요 한 차이점이 있습니다. 모든 모듈에는 정확히 하나의 인스턴스가 있으며 변수에 만들거나 할당할 필요가 없습니다. 모듈은 상속을 지원 하거나 인터페이스를 구현 하지 않습니다. 모듈은 클래스 또는 구조체 라는 점에서 *형식이* 아닙니다. 프로그래밍 요소를 모듈의 데이터 형식으로 선언할 수 없습니다.  
  
 는 네임 스페이스 `Module` 수준 에서만 사용할 수 있습니다. 즉, 모듈의 *선언 컨텍스트* 는 소스 파일 또는 네임 스페이스 여야 하 고 클래스, 구조체, 모듈, 인터페이스, 프로시저 또는 블록일 수 없습니다. 모듈은 다른 모듈 또는 모든 형식 내에서 중첩할 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 모듈의 수명은 프로그램의 수명과 동일 합니다. 해당 멤버는 모두 `Shared`이므로 프로그램의 수명과 동일 합니다.  
  
 모듈은 기본적으로 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 액세스를 사용 합니다. 액세스 한정자를 사용 하 여 액세스 수준을 조정할 수 있습니다. 자세한 내용은 [Visual Basic의 액세스 수준](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조 하세요.  
  
 모듈의 모든 멤버는 암시적으로 `Shared`입니다.  
  
## <a name="classes-and-modules"></a>클래스 및 모듈  
 이러한 요소에는 여러 가지 유사점이 있지만 몇 가지 중요 한 차이점도 있습니다.  
  
- **기술.** 이전 버전의 Visual Basic에서는 *클래스 모듈* (cls 파일)과 *표준 모듈* (bas 파일)의 두 가지 모듈 형식을 인식 합니다. 현재 버전은 이러한 *클래스* 및 *모듈*을 각각 호출 합니다.  
  
- **공유 멤버.** 클래스의 멤버가 공유 또는 인스턴스 멤버 인지 여부를 제어할 수 있습니다.  
  
- **개체 방향입니다.** 클래스는 개체 지향적 이지만 모듈은 그렇지 않습니다. 따라서 클래스만 개체로 인스턴스화할 수 있습니다. 자세한 내용은 [개체 및 클래스](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)를 참조 하세요.  
  
## <a name="rules"></a>규칙  
  
- **수정자.** 모든 모듈 멤버는 암시적으로 [공유](../../../visual-basic/language-reference/modifiers/shared.md)됩니다. 멤버를 선언할 때 `Shared` 키워드를 사용할 수 없으며, 멤버의 공유 상태를 변경할 수 없습니다.  
  
- **상속.** 모듈은 모든 모듈이 상속 하는 이외의 <xref:System.Object>형식에서 상속할 수 없습니다. 특히 한 모듈은 다른 모듈에서 상속할 수 없습니다.  
  
     을 지정 <xref:System.Object>하는 경우에도 [Inherits 문을](../../../visual-basic/language-reference/statements/inherits-statement.md) 모듈 정의에 사용할 수 없습니다.  
  
- **기본 속성입니다.** 모듈에서 기본 속성을 정의할 수 없습니다. 자세한 내용은 [기본값](../../../visual-basic/language-reference/modifiers/default.md)을 참조 하세요.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 모듈 내에서 각 멤버를 고유한 액세스 수준으로 선언할 수 있습니다. 모듈 멤버는 기본적으로 [Private](../../../visual-basic/language-reference/modifiers/private.md) access로 기본 사용 되는 변수 및 상수를 제외 하 고 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스를 사용 합니다. 모듈의 멤버 중 하나 보다 제한 된 액세스 권한이 있으면 지정 된 모듈 액세스 수준이 우선적으로 적용 됩니다.  
  
- **범위.** 모듈은 전체 네임 스페이스 범위에 있습니다.  
  
     모든 모듈 멤버의 범위는 전체 모듈입니다. 모든 멤버가 *형식 승격*을 거칩니다. 그러면 해당 범위가 모듈이 포함 된 네임 스페이스로 승격 됩니다. 자세한 내용은 [형식 승격](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)을 참조 하세요.  
  
- **조인의.** 프로젝트에 여러 모듈을 포함할 수 있으며, 둘 이상의 모듈에서 같은 이름을 사용 하 여 멤버를 선언할 수 있습니다. 그러나 참조를 해당 모듈 외부에서 가져온 경우 적절 한 모듈 이름을 사용 하 여 이러한 멤버에 대 한 참조를 정규화 해야 합니다. 자세한 내용은 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbalrStatements#69](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#69)]  
  
## <a name="see-also"></a>참고자료

- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [Namespace 문](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [형식 승격](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)
