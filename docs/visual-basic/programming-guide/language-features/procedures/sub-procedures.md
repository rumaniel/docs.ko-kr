---
title: Sub 프로시저(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Sub procedures [Visual Basic], about Sub procedures
- statement blocks
- Sub procedures [Visual Basic], calling
- procedures [Visual Basic], calling
- Sub procedures [Visual Basic], syntax
- Sub procedures
- procedures [Visual Basic], Sub
- syntax [Visual Basic], Sub procedures
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
ms.openlocfilehash: b70594e002bbf08f0890586e78df901ccb26c7ce
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61791823"
---
# <a name="sub-procedures-visual-basic"></a>Sub 프로시저(Visual Basic)
A `Sub` 절차는 일련의 Visual Basic 문으로 둘러싸인 합니다 `Sub` 및 `End Sub` 문. `Sub` 프로시저는 작업을 수행한 다음 호출 코드에 제어를 반환 하지만 호출 코드에 값을 반환 하지는 않습니다.  
  
 프로시저를 호출할 때마다 해당 문이 실행 됩니다 후 첫 번째 실행 가능 문을 사용 하 여 시작 합니다 `Sub` 문과 첫 번째 끝 `End Sub`, `Exit Sub`, 또는 `Return` 문을 발견 했습니다.  
  
 정의할 수 있습니다는 `Sub` 모듈, 클래스 및 구조체에는 프로시저입니다. 기본적으로 `Public`, 즉 호출할 수 어디에서 나 모듈, 클래스 또는 구조체 정의 액세스 권한이 있는 응용 프로그램에서 합니다. 용어 *메서드*, 설명를 `Sub` 또는 `Function` 프로시저의 정의 외부에서 액세스 되는 모듈, 클래스 또는 구조체입니다. 자세한 내용은 [프로시저](./index.md)를 참조하세요.  
  
 `Sub` 프로시저 호출 코드에서 전달 되는 식, 상수, 변수 등의 인수를 사용할 수 있습니다.  
  
## <a name="declaration-syntax"></a>선언 구문  
 선언 구문이 `Sub` 절차는 다음과 같습니다.  
  
 `[` *modifiers* `] Sub`  *subname* `[(` *parameterlist* `)]`  
  
 `' Statements of the Sub procedure.`  
  
 `End Sub`  
  
 `modifiers` 액세스 수준 및 오버 로드, 재정의 공유 및 숨기기에 대 한 정보를 지정할 수 있습니다. 자세한 내용은 [Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md)합니다.  
  
## <a name="parameter-declaration"></a>매개 변수 선언  
 각 프로시저 매개 변수에 어떻게 변수를 선언 하면, 매개 변수 이름과 데이터 형식을 지정 비슷하게 선언할 수 있습니다. 전달 메커니즘을 지정할 수도 있습니다 및 선택적 매개 변수 인지 또는 매개 변수 배열입니다.  
  
 매개 변수 목록의 각 매개 변수에 대 한 구문은 다음과 같습니다.  
  
 `[Optional] [ByVal | ByRef] [ParamArray]`  *parametername*  `As`  *datatype*  
  
 매개 변수가 선택적 이면 해당 선언의 일부로 기본값도 제공 해야 합니다. 기본값을 지정 하는 구문은 아래와 같습니다.  
  
 `Optional [ByVal | ByRef]`  *parametername*  `As`  *datatype*  `=`  *defaultvalue*  
  
### <a name="parameters-as-local-variables"></a>로컬 변수로 매개 변수  
 제어 절차를 통과 하는 경우 각 매개 변수를 지역 변수로 처리 됩니다. 이 프로시저의 수명 기간 동안 동일 하 고 해당 범위는 전체 과정을 의미 합니다.  
  
## <a name="calling-syntax"></a>호출 구문  
 호출 하는 `Sub` 독립 실행형 호출 문 명시적으로 사용 하 여 프로시저입니다. 식에서 해당 이름을 사용 하 여 호출할 수 없습니다. 선택적 인수가 아닌 모든 인수에 대 한 값을 제공 해야 하 고 인수 목록을 괄호로 묶어야 합니다. 인수 없이 제공 되는 경우에 필요에 따라 괄호를 생략할 수 있습니다. 사용 된 `Call` 키워드는 선택 사항 이지만 권장 하지는 않습니다.  
  
 에 대 한 호출에 대 한 구문을 `Sub` 절차는 다음과 같습니다.  
  
 `[Call]`  *subname* `[(` *argumentlist* `)]`  
  
 호출할 수 있습니다는 `Sub` 정의 하는 클래스 외부에서 메서드. 먼저 사용 해야 합니다 `New` 클래스의 인스턴스를 만들거나 메서드를 호출 하는 키워드는 클래스의 인스턴스를 반환 합니다. 자세한 내용은 [새 운영자](../../../../visual-basic/language-reference/operators/new-operator.md)합니다. 호출 하려면 다음 구문을 사용할 수는 다음을 `Sub` 인스턴스 개체의 메서드:  
  
 *개체*. *methodname*`[(`*argumentlist*`)]`  
  
### <a name="illustration-of-declaration-and-call"></a>선언 및 호출의 그림  
 다음 `Sub` 프로시저는 응용 프로그램에서 수행 하려는 작업을 컴퓨터 사용자에 게 알려 타임 스탬프를 표시 합니다. 모든 작업의 시작 부분에이 코드를 복제 하는 대신 응용 프로그램 호출 `tellOperator` 다양 한 위치에서. 문자열을 전달 하는 각 호출의 `task` 시작 하려는 작업을 식별 하는 인수입니다.  
  
 [!code-vb[VbVbcnProcedures#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#2)]  
  
 다음 예제에서는 일반적인 호출 `tellOperator`합니다.  
  
 [!code-vb[VbVbcnProcedures#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [Function 프로시저](./function-procedures.md)
- [속성 프로시저](./property-procedures.md)
- [연산자 프로시저](./operator-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Sub 문](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [방법: 값을 반환 하지 않는 프로시저 호출](./how-to-call-a-procedure-that-does-not-return-a-value.md)
- [방법: Visual Basic의 이벤트 처리기를 호출 합니다.](./how-to-call-an-event-handler.md)
