---
title: Delegate 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Delegate
helpviewer_keywords:
- delegate keyword [Visual Basic]
- Delegate statement [Visual Basic]
ms.assetid: f799c518-0817-40cc-ad0b-4da846fdba57
ms.openlocfilehash: 880b4cf75d518506d2bcf788ad8460274dcccefc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61638221"
---
# <a name="delegate-statement"></a>Delegate 문
대리자를 선언 하는 데 사용 합니다. 대리자는 참조 형식을 참조 하는 `Shared` 메서드 형식 또는 개체의 인스턴스 메서드. 매개 변수 및 반환 형식을 일치 하는 프로시저는이 대리자 클래스의 인스턴스를 만드는 데 사용할 수 있습니다. 다음 대리자 인스턴스를 사용 하 여 프로시저에 나중에 호출할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shadows ] Delegate [ Sub | Function ] name [( Of typeparamlist )] [([ parameterlist ])] [ As type ]  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`attrlist`|선택 사항입니다. 이 대리자에 적용 되는 특성 목록입니다. 여러 특성은 쉼표로 구분합니다. 묶어야 합니다 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md) 꺾쇠 괄호에서 ("`<`"및"`>`").|  
|`accessmodifier`|선택 사항입니다. 대리자에 액세스할 수 있는 코드를 지정 합니다. 다음 중 하나일 수 있습니다.<br /><br /> - [공용](../../../visual-basic/language-reference/modifiers/public.md)합니다. 대리자를 선언 하는 요소에 액세스할 수 있는 모든 코드 액세스할 수 있습니다.<br />-   [보호 된](../../../visual-basic/language-reference/modifiers/protected.md)합니다. 대리자의 클래스 또는 파생된 클래스 내 코드만 액세스할 수 있습니다.<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)합니다. 동일한 어셈블리 내 코드만 대리자를 액세스할 수 있습니다.<br />- [개인](../../../visual-basic/language-reference/modifiers/private.md)합니다. 대리자를 선언 하는 요소 내의 코드만 액세스할 수 있습니다.<br /><br /> - [Protected Friend](../../language-reference/modifiers/protected-friend.md) 대리자의 클래스나 파생된 클래스에서 동일한 어셈블리 내의 코드는 대리자를 액세스할 수 있습니다. <br />- [Private Protected](../../language-reference/modifiers/private-protected.md) 코드 대리자의 클래스 내에서 또는 동일한 어셈블리의 파생된 클래스에서 대리자를 액세스할 수 있습니다. |  
|`Shadows`|선택 사항입니다. 이 대리자는 동일 하 게 명명 된 프로그래밍 요소 또는 기본 클래스에서 오버 로드 된 요소 집합을 다시 선언 하 고 숨기도록를 나타냅니다. 모든 종류의 선언된 요소를 다른 종류로 섀도잉할 수 있습니다.<br /><br /> 섀도잉된 요소는 섀도잉 요소에 액세스할 수 없는 위치를 제외하고 해당 요소를 섀도잉하는 파생 클래스 내에서 사용할 수 없습니다. 예를 들어 경우는 `Private` 요소 기본 클래스 요소에 액세스할 수 있는 권한이 없는 코드를 숨기면는 `Private` 요소 대신 기본 클래스 요소에 액세스 합니다.|  
|`Sub`|선택 사항 이지만 하나 `Sub` 또는 `Function` 나타나야 합니다. 이 절차를 대리자로 선언 `Sub` 값을 반환 하지 않는 프로시저입니다.|  
|`Function`|선택 사항 이지만 하나 `Sub` 또는 `Function` 나타나야 합니다. 이 절차를 대리자로 선언 `Function` 값을 반환 하는 프로시저입니다.|  
|`name`|필수 요소. 대리자 형식의 이름 표준 변수 명명 규칙을 따릅니다.|  
|`typeparamlist`|선택 사항입니다. 이 대리자에 대 한 형식 매개 변수의 목록입니다. 여러 형식 매개 변수는 쉼표로 구분 됩니다. 필요에 따라 각 형식 매개 변수에 선언할 수 변형을 사용 하 여 `In` 고 `Out` 제네릭 한정자입니다. 묶어야 합니다 [형식 목록](../../../visual-basic/language-reference/statements/type-list.md) 괄호 안에 사용 하 여 정의 하 고는 `Of` 키워드.|  
|`parameterlist`|선택 사항입니다. 호출 될 때 프로시저에 전달 되는 매개 변수의 목록입니다. 묶어야 합니다 [매개 변수 목록](../../../visual-basic/language-reference/statements/parameter-list.md) 괄호 안에 있습니다.|  
|`type`|지정 하는 경우 필요한를 `Function` 프로시저입니다. 반환 값의 데이터 형식입니다.|  
  
## <a name="remarks"></a>설명  
 `Delegate` 문에서 대리자 클래스의 매개 변수 및 반환 형식을 정의 합니다. 매개 변수 및 반환 형식을 일치 하는 프로시저는이 대리자 클래스의 인스턴스를 만드는 데 사용할 수 있습니다. 절차 다음 나중에 호출할 수 대리자 인스턴스를 통해 대리자의 호출 하 여 `Invoke` 메서드.  
  
 프로시저 내부가 아니라 네임 스페이스, 모듈, 클래스 또는 구조 수준에서 대리자를 선언할 수 있습니다.  
  
 각 대리자 클래스는 개체 메서드의 사양이 전달되는 생성자를 정의합니다. 대리자 생성자에 대한 인수는 메서드 또는 람다 식에 대한 참조여야 합니다.  
  
 메서드에 대한 참조를 지정하려면 다음 구문을 사용합니다.  
  
 `AddressOf` [`expression`.]`methodname`  
  
 `expression`의 컴파일 타임 형식은 해당 시그니처가 대리자 클래스의 시그니처와 일치하는 지정된 이름의 메서드를 포함하는 클래스 또는 인터페이스의 이름이어야 합니다. `methodname`은 공유 메서드이거나 인스턴스 메서드일 수 있습니다. `methodname`은 클래스의 기본 메서드에 대해 대리자를 만들더라도 선택 사항이 아닙니다.  
  
 람다 식을 지정하려면 다음 구문을 사용합니다.  
  
 `Function` ([`parm` As `type`, `parm2` As `type2`, ...]) `expression`  
  
 함수의 시그니처는 대리자 형식의 시그니처와 일치해야 합니다. 람다 식에 대한 자세한 내용은 [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)을 참조하세요.  
  
 대리자에 대한 자세한 내용은 [대리자](../../../visual-basic/programming-guide/language-features/delegates/index.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Delegate` 두 숫자에서 작동 하 고 숫자로 반환에 대 한 대리자를 선언 하는 문입니다. `DelegateTest` 메서드가 형식의 대리자의 인스턴스를 사용 하 고 숫자의 쌍에서 작동 하는 데 사용 합니다.  
  
 [!code-vb[VbVbalrDelegates#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDelegates/VB/Class1.vb#14)]  
  
## <a name="see-also"></a>참고자료

- [AddressOf 연산자](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Of](../../../visual-basic/language-reference/statements/of-clause.md)
- [대리자](../../../visual-basic/programming-guide/language-features/delegates/index.md)
- [방법: 제네릭 클래스 사용](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [공 분산 및 반공 분산](../../programming-guide/concepts/covariance-contravariance/index.md)
- [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)
- [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)
