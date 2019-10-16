---
title: Operator 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.operator
helpviewer_keywords:
- operators [Visual Basic]
- procedures [Visual Basic], operator
- Narrowing keyword [Visual Basic], conversion operators
- Visual Basic code, operators
- Widening keyword [Visual Basic], conversion operators
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- overloaded operators [Visual Basic]
- operator overloading
- operator procedures
- Operator statement [Visual Basic]
- CType function [Visual Basic], Operator statement
ms.assetid: b12ec4af-1ad7-4a17-865b-c5ee96320ae5
ms.openlocfilehash: 4162f7cb5d8b89a1e5e8e7db429cf4e8dd9b700a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64583585"
---
# <a name="operator-statement"></a>Operator Statement
연산자 기호, 피연산자 및 클래스 또는 구조체에서 연산자 프로시저를 정의 하는 코드를 선언 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
[ <attrlist> ] Public [ Overloads ] Shared [ Shadows ] [ Widening | Narrowing ]   
Operator operatorsymbol ( operand1 [, operand2 ]) [ As [ <attrlist> ] type ]  
    [ statements ]  
    [ statements ]  
    Return returnvalue  
    [ statements ]  
End Operator  
```  
  
## <a name="parts"></a>요소  
 `attrlist`  
 선택 사항입니다. 참조 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)합니다.  
  
 `Public`  
 필수 요소. 이 연산자 프로시저가 있음을 나타냅니다 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스 합니다.  
  
 `Overloads`  
 선택 사항입니다. 참조 [오버 로드](../../../visual-basic/language-reference/modifiers/overloads.md)합니다.  
  
 `Shared`  
 필수 요소. 이 연산자 프로시저 임을 나타냅니다는 [공유](../../../visual-basic/language-reference/modifiers/shared.md) 프로시저입니다.  
  
 `Shadows`  
 선택 사항입니다. 참조 [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)합니다.  
  
 `Widening`  
 지정 하지 않으면 변환 연산자에 필요한 `Narrowing`합니다. 이 연산자 프로시저 정의 함을 나타냅니다는 [Widening](../../../visual-basic/language-reference/modifiers/widening.md) 변환 합니다. 이 도움말 페이지에 "확대 변환과 축소 변환"을 참조 하세요.  
  
 `Narrowing`  
 지정 하지 않으면 변환 연산자에 필요한 `Widening`합니다. 이 연산자 프로시저 정의 함을 나타냅니다는 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md) 변환 합니다. 이 도움말 페이지에 "확대 변환과 축소 변환"을 참조 하세요.  
  
 `operatorsymbol`  
 필수 요소. 기호 또는이 연산자 프로시저 정의 하는 연산자의 식별자입니다.  
  
 `operand1`  
 필수 요소. 이름과 (변환 연산자를 포함 하 여) 단항 연산자의 단일 피연산자는 이항 연산자의 왼쪽된 피연산자의 형식입니다.  
  
 `operand2`  
 이항 연산자에 필요합니다. 이름과 이항 연산자의 오른쪽 피연산자의 형식입니다.  
  
 `operand1` 및 `operand2` 는 다음과 같은 구문 및 부분:  
  
 `[ ByVal ] operandname [ As operandtype ]`  
  
|파트|설명|  
|----------|-----------------|  
|`ByVal`|선택 사항 이지만 전달 메커니즘 이어야 합니다 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md)합니다.|  
|`operandname`|필수 요소. 이 피연산자를 나타내는 변수의 이름입니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.|  
|`operandtype`|선택적 경우가 아니면 `Option Strict` 는 `On`합니다. 이 피연산자의 데이터 형식입니다.|  
  
 `type`  
 선택적 경우가 아니면 `Option Strict` 는 `On`합니다. 연산자 프로시저 값의 데이터 형식을 반환합니다.  
  
 `statements`  
 선택 사항입니다. 블록에서 연산자 프로시저를 실행 하는 문입니다.  
  
 `returnvalue`  
 필수 요소. 연산자 프로시저가 호출 코드에 반환 하는 값입니다.  
  
 `End` `Operator`  
 필수 요소. 이 연산자 프로시저의 정의 종료합니다.  
  
## <a name="remarks"></a>설명  
 사용할 수 있습니다 `Operator` 클래스 또는 구조체에만 합니다. 즉, 합니다 *선언 컨텍스트* 연산자는 소스 파일, 네임 스페이스, 모듈, 인터페이스, 프로시저 또는 블록 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.  
  
 모든 연산자는 반드시 `Public Shared`입니다. 지정할 수 없습니다 `ByRef`, `Optional`, 또는 `ParamArray` 두 피연산자에 대 한 합니다.  
  
 반환 값을 저장 하는 연산자 기호 또는 식별자를 사용할 수 없습니다. 사용 해야는 `Return` 문 및 해당 값을 지정 해야 합니다. 임의 개수의 `Return` 문을 프로시저에서 아무 곳 이나 나타날 수 있습니다.  
  
 연산자 정의 하는 이러한 방식으로 라고 *연산자 오버 로드*사용 여부는 `Overloads` 키워드입니다. 다음 표에는 정의할 수 있는 연산자가 나와 있습니다.  
  
|형식|연산자|  
|----------|---------------|  
|단항|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|  
|이항|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|  
|변환(단항)|`CType`|  
  
 `=` 이진 목록의 연산자는 비교 연산자, 대입 연산자가 없습니다.  
  
 정의 하는 경우 `CType`를 지정 해야 `Widening` 또는 `Narrowing`합니다.  
  
## <a name="matched-pairs"></a>일치 하는 쌍  
 일치 하는 쌍으로 특정 연산자를 정의 해야 합니다. 이러한 쌍의 두 연산자를 정의 하는 경우 다른도 정의 해야 합니다. 일치 하는 쌍 다음과 같습니다.  
  
- `=` 및 `<>`  
  
- `>` 및 `<`  
  
- `>=` 및 `<=`  
  
- `IsTrue` 및 `IsFalse`  
  
## <a name="data-type-restrictions"></a>데이터 형식 제한 사항  
 정의한 모든 연산자는 클래스 또는 구조체 정의를 포함 해야 합니다. 이 클래스 또는 구조체의 다음 데이터 형식으로 표시 되어야 함을 의미 합니다.  
  
- 단항 연산자의 피연산자입니다.  
  
- 하나 이상의 이항 연산자의 피연산자입니다.  
  
- 피연산자 또는 변환 연산자의 반환 형식입니다.  
  
 특정 연산자에는 제한 사항 다음과 같이 입력 하는 추가 데이터:  
  
- 정의 하는 경우는 `IsTrue` 하 고 `IsFalse` 연산자를 모두 반환 해야 합니다 `Boolean` 형식.  
  
- 정의 하는 경우는 `<<` 및 `>>` 연산자는 둘 다 지정 해야 합니다 `Integer` 에 대 한 입력을 `operandtype` 의 `operand2`합니다.  
  
 두 피연산자의 형식에 해당 하는 반환 형식이 없습니다. 예를 들어, 비교 연산자와 같은 `=` 또는 `<>` 반환할 수 있습니다 `Boolean` 도 아닌 경우 `Boolean`합니다.  
  
## <a name="logical-and-bitwise-operators"></a>논리 및 비트 연산자  
 합니다 `And`, `Or`를 `Not`, 및 `Xor` 연산자 Visual Basic의 논리 또는 비트 작업을 수행할 수 있습니다. 그러나 클래스 또는 구조체에서 이러한 연산자 중 하나를 정의 하는 경우 해당 연산을 정의할 수 있습니다.  
  
 정의할 수 없습니다는 `AndAlso` 연산자를 사용 하 여 직접는 `Operator` 문입니다. 사용할 수 있습니다 `AndAlso` 다음 조건을 충족 하는 경우:  
  
- 정의한 `And` 에 대 한 사용 하려는 같은 피연산자 유형에 따라 `AndAlso`합니다.  
  
- 정의 `And` 클래스 또는 구조체를 정의한 것과 동일한 형식을 반환 합니다.  
  
- 정의한 합니다 `IsFalse` 연산자를 정의한 클래스 또는 구조체에서 `And`합니다.  
  
 마찬가지로, 사용할 수 있습니다 `OrElse` 정의 하는 경우 `Or` 동일한 피연산자에서 클래스 또는 구조체의 반환 형식을 사용 하 여 정의한 `IsTrue` 클래스 또는 구조입니다.  
  
## <a name="widening-and-narrowing-conversions"></a>Widening and Narrowing Conversions  
 A *확대 변환은* 런타임 시 항상 성공 하는 동안를 *축소 변환* 런타임에 실패할 수 있습니다. 자세한 내용은 [Widening and Narrowing Conversions](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)을 참조하세요.  
  
 변환 프로시저를 선언 하는 경우 `Widening`, 프로시저 코드가 발생 한 모든 오류를 생성 하지 해야 합니다. 이것은 다음을 의미합니다.  
  
- 형식의 올바른 값을 반환 항상 해야 `type`합니다.  
  
- 모든 예외 및 다른 오류 조건을 처리 해야 합니다.  
  
- 호출 하는 프로시저의 모든 오류 반환을 처리 해야 합니다.  
  
 되도록 선언 해야 변환 프로시저 성공 하지 않을 수 있는 가능성이 없거나는 처리 되지 않은 예외가 발생할 수 있습니다, `Narrowing`합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 합니다 `Operator` 연산자 프로시저를 포함 하는 구조체의 윤곽선을 정의 하는 문을 합니다 `And`, `Or`, `IsFalse`, 및 `IsTrue` 연산자. `And` 및 `Or` 형식의 두 개의 피연산자 `abc` 반환 형식 및 `abc`합니다. `IsFalse` 및 `IsTrue` 형식의 단일 피연산자를 각각 사용 `abc` 돌아와 `Boolean`합니다. 이러한 정의 사용 하도록 호출 코드를 사용 하면 `And`, `AndAlso`를 `Or`, 및 `OrElse` 형식의 피연산자를 사용 하 여 `abc`입니다.  
  
 [!code-vb[VbVbalrStatements#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#44)]  
  
## <a name="see-also"></a>참고자료

- [IsFalse 연산자](../../../visual-basic/language-reference/operators/isfalse-operator.md)
- [IsTrue 연산자](../../../visual-basic/language-reference/operators/istrue-operator.md)
- [확장](../../../visual-basic/language-reference/modifiers/widening.md)
- [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)
- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [연산자 프로시저](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)
- [방법: 연산자 정의](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [방법: 변환 연산자를 정의 합니다.](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [방법: 연산자 프로시저 호출](../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)
- [방법: 연산자를 정의 하는 클래스를 사용 합니다.](../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)
