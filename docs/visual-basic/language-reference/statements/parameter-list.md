---
title: 매개 변수 목록(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- parameters [Visual Basic], Visual Basic
- parameters [Visual Basic], lists
- parameter lists [Visual Basic]
- Visual Basic code, parameter lists
- arguments [Visual Basic], Visual Basic
- procedures [Visual Basic], parameter lists
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
ms.openlocfilehash: e58d80896d11b4154c7197d4cdaf73a536fdd5e7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64583558"
---
# <a name="parameter-list-visual-basic"></a>매개 변수 목록(Visual Basic)
프로시저를 호출할 때에 필요한 매개 변수를 지정 합니다. 여러 매개 변수는 쉼표로 구분 됩니다. 다음은 하나의 매개 변수에 대 한 구문입니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## <a name="parts"></a>요소  
 `attributelist`  
 선택 사항입니다. 이 매개 변수에 적용 되는 특성 목록입니다. 묶어야 합니다 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md) 꺾쇠 괄호에서 ("`<`"및"`>`").  
  
 `Optional`  
 선택 사항입니다. 프로시저를 호출할 때이 매개 변수가 필요한 아님을 지정 합니다.  
  
 `ByVal`  
 선택 사항입니다. 프로시저를 대체 하거나 호출 코드의 해당 인수를 기본 변수 요소를 재할당할 수 없습니다는 지정 합니다.  
  
 `ByRef`  
 선택 사항입니다. 프로시저 요소를 수정할 수 기본 변수는 호출 코드에서 호출 코드 자체를 동일한 방식으로 지정 합니다.  
  
 `ParamArray`  
 선택 사항입니다. 매개 변수 목록의 마지막 매개 변수는 선택적 요소를 지정 된 데이터 형식의 배열을 지정 합니다. 그러면 호출 코드를 프로시저에 임의 개수의 인수를 전달 합니다.  
  
 `parametername`  
 필수 요소. 매개 변수를 나타내는 지역 변수의 이름입니다.  
  
 `parametertype`  
 필요한 경우 `Option Strict` 는 `On`합니다. 매개 변수를 나타내는 지역 변수 데이터 형식입니다.  
  
 `defaultvalue`  
 에 필요한 `Optional` 매개 변수입니다. 매개 변수의 데이터 형식으로 계산 되는 모든 상수 또는 상수 식입니다. 형식이 `Object`, 또는 기본 값의 수만 지정 클래스, 인터페이스, 배열 또는 구조를 `Nothing`입니다.  
  
## <a name="remarks"></a>설명  
 매개 변수는 괄호로 묶어 이며 쉼표로 구분 합니다. 데이터 형식과 매개 변수를 선언할 수 있습니다. 지정 하지 않는 경우 `parametertype`, 기본값은 `Object`합니다.  
  
 호출 코드에서 프로시저를 호출 하면 전달 하는 *인수* 각 필수 매개 변수를 합니다. 자세한 내용은 [매개 변수 간의 차이점 및 인수](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md)합니다.  
  
 호출 코드에서 각 매개 변수에 전달 인수가 호출 코드의 내부 요소에 대 한 포인터입니다. 이 요소가 있으면 *비가변* (상수, 리터럴, 열거형 또는 식)를 변경 하는 코드에 대 한 불가능 합니다. 경우는 *변수* 요소 (선언 된 변수, 필드, 속성, 배열 요소 또는 구조 요소)를 호출 하는 코드에서 변경할 수 있습니다. 자세한 내용은 [수정할 간의 차이점 및 수정할 수 없는 인수](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md)합니다.  
  
 Variable 요소에 전달 되는 경우 `ByRef`, 프로시저도 변경할 수 있습니다. 자세한 내용은 [차이점 간의 값과 By Reference 인수를 전달](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)합니다.  
  
## <a name="rules"></a>규칙  
  
- **괄호입니다.** 매개 변수 목록을 지정 하는 경우 괄호로 묶습니다 해야 있습니다. 매개 변수가 없는 경우 빈 목록을 묶는 괄호를 여전히 사용할 수 있습니다. 이 요소는 프로시저 임을 명확히 설명 하 여 코드의 가독성을 개선 합니다.  
  
- **선택적 매개 변수입니다.** 사용 하는 경우는 `Optional` 매개 변수 한정자를 모든 후속 매개 변수 목록의 선택적 및를 사용 하 여 선언할 수는 `Optional` 한정자입니다.  
  
     모든 선택적 매개 변수 선언을 제공 해야 합니다는 `defaultvalue` 절.  
  
     자세한 내용은 [선택적 매개 변수](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)합니다.  
  
- **매개 변수 배열입니다.** 지정 해야 합니다 `ByVal` 에 대 한는 `ParamArray` 매개 변수입니다.  
  
     둘 다 사용할 수 없습니다 `Optional` 고 `ParamArray` 동일한 매개 변수 목록입니다.  
  
     자세한 내용은 [매개 변수 배열](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)합니다.  
  
- **전달 메커니즘입니다.** 모든 인수에 대 한 기본 메커니즘은 `ByVal`, 프로시저를 의미 하는 내부 변수 요소를 변경할 수 없습니다. 그러나 요소 참조 형식이 면 프로시저를 수정할 수 내용이 나 기본 개체의 멤버는 대체 없거나 개체 자체를 다시 할당 하는 경우에.  
  
- **매개 변수 이름입니다.** 매개 변수의 데이터 형식 배열인 경우에 따라 `parametername` 괄호 바로 뒤에 있습니다. 매개 변수 이름에 대 한 자세한 내용은 참조 하세요. [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제와 `Function` 두 매개 변수를 정의 하는 프로시저입니다.  
  
 [!code-vb[VbVbalrStatements#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [특성 개요](../../../visual-basic/programming-guide/concepts/attributes/index.md)
- [방법: 코드에서 문 분리 및 결합](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
