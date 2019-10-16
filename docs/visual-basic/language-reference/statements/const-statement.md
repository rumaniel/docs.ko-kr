---
title: Const 문(Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Const
helpviewer_keywords:
- Const statement [Visual Basic]
ms.assetid: 495b318d-b7c5-4198-94f8-0790a541b07a
ms.openlocfilehash: 522ac71767707ae90a3f1d11d45ef8b29471ae6c
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005114"
---
# <a name="const-statement-visual-basic"></a>Const 문(Visual Basic)
하나 이상의 상수를 선언 하 고 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
[ <attributelist> ] [ accessmodifier ] [ Shadows ]   
Const constantlist  
```  
  
## <a name="parts"></a>요소  
 `attributelist`  
 (선택 사항) 이 문에 선언 된 모든 상수에 적용 되는 특성의 목록입니다. 꺾쇠 괄호 ("`<`" 및 "`>`")의 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md) 을 참조 하십시오.  
  
 `accessmodifier`  
 (선택 사항) 이러한 상수에 액세스할 수 있는 코드를 지정 하려면이 옵션을 사용 합니다. [Public](../../../visual-basic/language-reference/modifiers/public.md), [protected](../../../visual-basic/language-reference/modifiers/protected.md), [Friend](../../../visual-basic/language-reference/modifiers/friend.md), [protected friend](../modifiers/protected-friend.md), [private](../../../visual-basic/language-reference/modifiers/private.md)또는 [private Protected](../../language-reference/modifiers/private-protected.md)일 수 있습니다.
  
 `Shadows`  
 (선택 사항) 기본 클래스에서 프로그래밍 요소를 다시 선언 하 고 숨기는 데 사용 합니다. [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)를 참조 하세요.  
  
 `constantlist`  
 필수. 이 문에서 선언 되는 상수 목록입니다.  
  
 `constant` `[ ,` `constant` `... ]`  
  
 각 `constant`에는 다음과 같은 구문과 요소가 있습니다.  
  
 `constantname` `[ As` `datatype` `] =` `initializer`  
  
|부분|설명|  
|----------|-----------------|  
|`constantname`|필수. 상수의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.|  
|`datatype`|필요한 경우 `Option Strict` 는 `On`합니다. 상수의 데이터 형식입니다.|  
|`initializer`|필수. 컴파일 시간에 평가 되 고 상수에 할당 되는 식입니다.|  
  
## <a name="remarks"></a>설명  
 응용 프로그램에서 변경 되지 않는 값이 있는 경우 명명 된 상수를 정의 하 고 리터럴 값 대신 사용할 수 있습니다. 이름은 값 보다 쉽게 기억할 수 있습니다. 상수를 한 번만 정의 하 고 코드의 여러 위치에서 사용할 수 있습니다. 이후 버전에서 값을 다시 정의 해야 하는 경우 `Const` 문은 변경 해야 합니다.  
  
 @No__t-0은 모듈 또는 프로시저 수준 에서만 사용할 수 있습니다. 즉, 변수에 대 한 *선언 컨텍스트* 는 클래스, 구조체, 모듈, 프로시저 또는 블록 이어야 하며 소스 파일, 네임 스페이스 또는 인터페이스 일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 지역 상수 (프로시저 내)는 기본적으로 공용 액세스로 설정 되며 액세스 한정자를 사용할 수 없습니다. 클래스 및 모듈 멤버 상수 (프로시저 외부)는 기본적으로 private access로, 구조체 멤버 상수는 기본적으로 공용 액세스로 사용 됩니다. 액세스 한정자를 사용 하 여 액세스 수준을 조정할 수 있습니다.  
  
## <a name="rules"></a>규칙  
  
- **선언 컨텍스트입니다.** 프로시저 외부에서 모듈 수준에 선언 된 상수는 *멤버 상수*입니다. 선언 하는 클래스, 구조체 또는 모듈의 멤버입니다.  
  
     프로시저 수준에서 선언 된 상수는 *지역 상수*입니다. 선언 하는 프로시저 또는 블록에 대해 로컬입니다.  
  
- **특성.** 로컬 상수가 아닌 멤버 상수에만 특성을 적용할 수 있습니다. 특성은 어셈블리의 메타 데이터에 정보를 제공 하며,이는 로컬 상수와 같은 임시 저장소에는 의미가 없습니다.  
  
- **수정자.** 기본적으로 모든 상수는 `Shared`, `Static` 및 `ReadOnly`입니다. 상수를 선언 하는 경우 이러한 키워드를 사용할 수 없습니다.  
  
     프로시저 수준에서 `Shadows` 또는 액세스 한정자를 사용 하 여 지역 상수를 선언할 수 없습니다.  
  
- **여러 상수.** 동일한 선언문에서 여러 상수를 선언 하 여 각 상수에 대해 `constantname` 부분을 지정할 수 있습니다. 여러 상수를 쉼표로 구분 합니다.  
  
## <a name="data-type-rules"></a>데이터 형식 규칙  
  
- **데이터 형식.** @No__t-0 문은 변수의 데이터 형식을 선언할 수 있습니다. 모든 데이터 형식 또는 열거형의 이름을 지정할 수 있습니다.  
  
- **기본 형식입니다.** @No__t-0을 지정 하지 않으면 상수는 `initializer`의 데이터 형식을 사용 합니다. @No__t-0과 `initializer`을 모두 지정 하는 경우에는 `initializer`의 데이터 형식을 `datatype`으로 변환할 수 있어야 합니다. @No__t-0 또는 `initializer`이 모두 없는 경우에는 데이터 형식이 기본적으로 `Object`가 됩니다.  
  
- **서로 다른 형식.** 선언 하는 각 변수에 대해 별도의 `As` 절을 사용 하 여 상수에 대해 서로 다른 데이터 형식을 지정할 수 있습니다. 그러나 일반적인 `As` 절을 사용 하 여 여러 개의 상수를 동일한 형식으로 선언할 수 없습니다.  
  
- **초기.** @No__t-0에서 모든 상수의 값을 초기화 해야 합니다. @No__t-0을 사용 하 여 상수에 할당할 식을 제공 합니다. 식에는 리터럴, 이미 정의 된 다른 상수 및 이미 정의 된 열거형 멤버가 모두 조합 될 수 있습니다. 산술 연산자와 논리 연산자를 사용 하 여 이러한 요소를 결합할 수 있습니다.  
  
     @No__t-0에서 변수 또는 함수를 사용할 수 없습니다. 그러나 `CByte` 및 `CShort`과 같은 변환 키워드를 사용할 수 있습니다. 상수 `String` 또는 `Char` 인수를 사용 하 여 호출 하는 경우 컴파일 시간에 계산할 수 있으므로 `AscW`을 사용할 수도 있습니다.  
  
## <a name="behavior"></a>동작  
  
- **범위.** 로컬 상수는 해당 프로시저 또는 블록 내 에서만 액세스할 수 있습니다. 멤버 상수는 클래스, 구조체 또는 모듈 내의 어디에서 나 액세스할 수 있습니다.  
  
- **조인의.** 클래스, 구조체 또는 모듈 외부의 코드는 해당 클래스, 구조체 또는 모듈의 이름으로 멤버 상수의 이름을 한 정해야 합니다. 프로시저 또는 블록 외부의 코드는 해당 프로시저나 블록 내의 지역 상수를 참조할 수 없습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Const` 문을 사용 하 여 리터럴 값 대신 사용할 상수를 선언 합니다.  
  
 [!code-vb[VbVbalrStatements#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#13)]  
  
## <a name="example"></a>예제  
 데이터 형식이 `Object` 인 상수를 정의 하는 경우 Visual Basic 컴파일러는 `Object` 대신 `initializer`의 형식을 제공 합니다. 다음 예제에서 상수 `naturalLogBase`은 런타임 형식이 `Decimal`입니다.  
  
 [!code-vb[VbVbalrStatements#87](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#87)]  
  
 이전 예제에서는 `CStr`를 사용 하 여 <xref:System.Type>을 `String`로 변환할 수 없기 때문에 [GetType 연산자](../../../visual-basic/language-reference/operators/gettype-operator.md)에서 반환 하는 @no__t 1 개체에 <xref:System.Type.ToString%2A> 메서드를 사용 합니다.  
  
## <a name="see-also"></a>참조

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- [Enum 문](../../../visual-basic/language-reference/statements/enum-statement.md)
- [#Const 지시문](../../../visual-basic/language-reference/directives/const-directive.md)
- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [ReDim 문](../../../visual-basic/language-reference/statements/redim-statement.md)
- [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [상수 및 열거형](../../../visual-basic/programming-guide/language-features/constants-enums/index.md)
- [상수 및 열거형](../../../visual-basic/language-reference/constants-and-enumerations.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
