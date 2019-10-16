---
title: Structure 문 (Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Structure
- Structure
helpviewer_keywords:
- user-defined types [Visual Basic], Structure statement
- compound data types [Visual Basic]
- Structure keyword [Visual Basic]
- Structure statement [Visual Basic]
- UDT (user-defined types)
- types [Visual Basic], user-defined
ms.assetid: 9bd1deea-2a89-4cdc-812c-6dcbb947c391
ms.openlocfilehash: c6871a9bae84d0eff79876d7d9668ec5e91d3ebc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615093"
---
# <a name="structure-statement"></a>Structure 문
구조의 이름을 선언 하 고 변수, 속성, 이벤트 및 구조를 구성 하는 프로시저의 정의 소개 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Partial ] _  
Structure name [ ( Of typelist ) ]  
    [ Implements interfacenames ]  
    [ datamemberdeclarations ]  
    [ methodmemberdeclarations ]  
End Structure  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`attributelist`|선택 사항입니다. 참조 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)합니다.|  
|`accessmodifier`|선택 사항입니다. 다음 중 하나일 수 있습니다.<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [보호](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [개인](../../../visual-basic/language-reference/modifiers/private.md)<br />- [Protected Friend](../../language-reference/modifiers/protected-friend.md)<br/>- [Private Protected](../../language-reference/modifiers/private-protected.md) <br /><br /> [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.|  
|`Shadows`|선택 사항입니다. 참조 [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)합니다.|  
|`Partial`|선택 사항입니다. 구조체의 부분 정의 나타냅니다. 참조 [부분](../../../visual-basic/language-reference/modifiers/partial.md)합니다.|  
|`name`|필수 요소. 이 구조체의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.|  
|`Of`|선택 사항입니다. 제네릭 구조체 임을 지정 합니다.|  
|`typelist`|사용 하는 경우 필요 합니다 [의](../../../visual-basic/language-reference/statements/of-clause.md) 키워드입니다. 이 구조에 대 한 형식 매개 변수의 목록입니다. 참조 [유형 목록](../../../visual-basic/language-reference/statements/type-list.md)합니다.|  
|`Implements`|선택 사항입니다. 이 구조는 하나 이상의 인터페이스 멤버를 구현 함을 나타냅니다. 참조 [문을 구현](../../../visual-basic/language-reference/statements/implements-statement.md)합니다.|  
|`interfacenames`|사용 하는 경우 필요 합니다 `Implements` 문입니다. 이 구조를 구현 하는 인터페이스의 이름입니다.|  
|`datamemberdeclarations`|필수 요소. 0 개 이상의 `Const`, `Dim`를 `Enum`, 또는 `Event` 선언 문을 *데이터 멤버* 구조입니다.|  
|`methodmemberdeclarations`|선택 사항입니다. 0 개 이상의 선언 `Function`, `Operator`, `Property`, 또는 `Sub` 역할을 하는 프로시저 *메서드 멤버* 구조입니다.|  
|`End Structure`|필수 요소. 종료는 `Structure` 정의 합니다.|  
  
## <a name="remarks"></a>설명  
 `Structure` 문은 사용자 지정할 수 있는 복합 값 형식을 정의 합니다. A *구조* 사용자 정의 형식의 (UDT) 이전 버전의 Visual Basic을 일반화 합니다. 자세한 내용은 [구조](../../../visual-basic/programming-guide/language-features/data-types/structures.md)합니다.  
  
 구조 여러 클래스와 동일한 기능을 지원합니다. 예를 들어 구조 속성 및 절차를 가질 수, 인터페이스를 구현 및 생성자 매개 변수가 있는 수 있습니다. 그러나, 상속, 선언 및 사용과 같은 영역에서 구조체와 클래스 간의 중요 한 차이점이 있습니다. 또한 클래스는 참조 형식 및 구조체가 값 형식입니다. 자세한 내용은 [구조체와 클래스](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)합니다.  
  
 사용할 수 있습니다 `Structure` 네임 스페이스 또는 모듈 수준 에서만. 즉, 합니다 *선언 컨텍스트* 구조를 소스 파일, 네임 스페이스, 클래스, 구조체, 모듈 또는 인터페이스 여야 하 고 프로시저 또는 블록일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 구조체는 기본적으로 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 액세스 합니다. 액세스 한정자를 사용 하 여 해당 액세스 수준을 조정할 수 있습니다. 자세한 내용은 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.  
  
## <a name="rules"></a>규칙  
  
- **중첩 합니다.** 내에서 다른 한 구조를 정의할 수 있습니다. 외부 구조체 라고 합니다 *구조가 포함*, 내부 구조 라고를 *구조에 중첩 된*합니다. 그러나 중첩 된 구조체의 멤버를 포함 하는 구조체를 통해 액세스할 수 없습니다. 대신, 중첩 된 구조를 데이터 형식의 변수로 선언 해야 합니다.  
  
- **멤버 선언입니다.** 구조체의 모든 멤버를 선언 해야 합니다. 구조 멤버 수 없습니다. [보호 됨](../../../visual-basic/language-reference/modifiers/protected.md) 또는 `Protected Friend` 구조체를 상속할 수 아무 작업도 수행 합니다. 그러나 구조 자체 수 `Protected` 또는 `Protected Friend`합니다.  
  
     구조체에는 0개 이상의 비공유 변수 또는 비공유, 비사용자 정의 이벤트를 선언할 수 있습니다. 그 중 일부는 공유 되지 않는 경우에 상수, 속성 및 프로시저 수는 없습니다.  
  
- **초기화 합니다.** 선언의 일부로 구조체의 공유 되지 않는 데이터 멤버의 값을 초기화할 수 없습니다. 구조에 있는 매개 변수가 있는 생성자를 사용 하 여 이러한 데이터 멤버를 초기화 또는 구조체의 인스턴스를 만든 후 멤버에 값을 할당 해야 합니다.  
  
- **상속.** 구조체 이외의 다른 모든 형식에서 상속할 수 없습니다. <xref:System.ValueType>에서 모든 구조체는 상속 합니다. 특히 한 구조에서 다른 상속할 수 없습니다.  
  
     사용할 수 없습니다는 [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md) 지정 하는 데도 구조 정의 <xref:System.ValueType>합니다.  
  
- **구현입니다.** 구조를 사용 하는 경우는 [Implements 문](../../../visual-basic/language-reference/statements/implements-statement.md)에서 지정 하는 모든 인터페이스에 의해 정의 된 모든 멤버를 구현 해야 `interfacenames`합니다.  
  
- **기본 속성입니다.** 구조체에서는 하나 이상의 속성으로 지정할 수 해당 *속성의 기본값*를 사용 하 여 합니다 [기본](../../../visual-basic/language-reference/modifiers/default.md) 한정자입니다. 자세한 내용은 [기본](../../../visual-basic/language-reference/modifiers/default.md)입니다.  
  
## <a name="behavior"></a>동작  
  
- **액세스 수준입니다.** 구조체에 자체 액세스 수준이 있는 각 멤버를 선언할 수 있습니다. 기본적으로 모든 구조체 멤버 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스 합니다. 구조체 자체를 좀 더 제한 된 액세스 수준에 있는 경우이 자동으로 액세스를 제한 해당 멤버 액세스 한정자를 사용 하 여 해당 액세스 수준을 조정 하는 경우에 참고 합니다.  
  
- **범위입니다.** 구조체는 해당 포함 된 네임 스페이스, 클래스, 구조체 또는 모듈 전체 범위에 있습니다.  
  
     모든 구조 멤버의 범위는 전체 구조입니다.  
  
- **수명입니다.** 구조체는 자체 없습니다 수명을. 대신, 해당 구조체의 각 인스턴스 독립적인 수명이 다른 모든 인스턴스.  
  
     인스턴스 수명에서 만들어질 때 시작 되는 [New 연산자](../../../visual-basic/language-reference/operators/new-operator.md) 절. 포함 된 변수의 수명 종료 될 때 종료 됩니다.  
  
     구조체 인스턴스의 수명을 확장할 수 없습니다. 정적 구조 기능에 대 한 근사값을 모듈에 의해 제공 됩니다. 자세한 내용은 [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)합니다.  
  
     구조체 멤버에는 선언 방법 및 위치에 따라 유효 기간이 있습니다. 자세한 내용은 "수명"를 참조 하세요 [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)합니다.  
  
- **정규화 합니다.** 코드 구조 외부 멤버의 이름을 해당 구조체의 이름으로 한 정해야 합니다.  
  
     중첩된 구조체 내부에서 코드를 프로그래밍 요소에 정규화 되지 않은 참조를 만드는 경우 Visual Basic 검색 요소에 대해 먼저 포함 하 여 구조를 다음에서 중첩 된 구조의 등 포함 하는 가장 바깥쪽 요소를 합니다. 자세한 내용은 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)을 참조하세요.  
  
- **메모리 사용량** 모든 복합 데이터 형식에서와 마찬가지로 해당 멤버의 일반 저장소 할당량을 함께 추가 하 여 구조체의 총 메모리 소비량을 안전 하 게 계산할 수 없습니다. 또한 가정할 수 없습니다는 메모리에서 저장소의 순서가 사용자의 선언 순서와 동일 합니다. 구조체의 저장소 레이아웃을 제어 해야 하는 경우 적용할 수 있습니다 합니다 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 `Structure` 문입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Structure` 을 직원에 대 한 관련된 데이터 집합을 정의 합니다. 사용법을 보여줍니다 `Public`, `Friend`, 및 `Private` 데이터 항목의 민감도 맞게 멤버입니다. 또한 프로시저, 속성 및 이벤트 멤버를 보여 줍니다.  
  
 [!code-vb[VbVbalrStatements#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#57)]  
  
## <a name="see-also"></a>참고자료

- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)
- [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)
- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)
- [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md)
- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)
- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)
- [구조체와 클래스](../../../visual-basic/programming-guide/language-features/data-types/structures-and-classes.md)
