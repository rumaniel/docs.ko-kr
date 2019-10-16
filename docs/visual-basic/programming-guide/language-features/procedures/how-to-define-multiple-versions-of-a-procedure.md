---
title: '방법: 여러 버전의 프로시저 (Visual Basic)를 정의 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
- procedure overloading [Visual Basic], multiple versions
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
ms.openlocfilehash: fc7a8e18394b904f0c22a80f71dee091d4f786ab
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61863833"
---
# <a name="how-to-define-multiple-versions-of-a-procedure-visual-basic"></a>방법: 여러 버전의 프로시저 (Visual Basic)를 정의 합니다.
여러 버전의 프로시저를 정의할 수 있습니다 *오버 로드* 이름은 같지만 다른 매개 변수 목록을 사용 하 여 각 버전에 대 한 것입니다. 오버 로드의 용도 이름으로 구분할 필요 없이 프로시저의 밀접 한 관련이 있는 여러 버전을 정의 하는 것입니다.  
  
 자세한 내용은 [Procedure Overloading](./procedure-overloading.md)을 참조하세요.  
  
### <a name="to-define-multiple-versions-of-a-procedure"></a>여러 버전의 프로시저를 정의 하려면  
  
1. 작성 한 `Sub` 또는 `Function` 정의 하려면 프로시저의 각 버전에 대 한 선언문입니다. 모든 선언에서 이름이 프로시저를 사용 합니다.  
  
2. 앞에 야 합니다 `Sub` 또는 `Function` 사용 하 여 각 선언에서 키워드를 [오버 로드](../../../../visual-basic/language-reference/modifiers/overloads.md) 키워드입니다. 선택적으로 생략할 수 `Overloads` 선언 중 하나에 포함 하는 경우를 제외한 선언에 포함 해야 모든 선언에 있습니다.  
  
3. 각 선언문 다음 프로시저는 특별 한 경우 호출 코드에서 해당 버전의 매개 변수 목록과 일치 하는 인수를 제공 하는 위치를 처리 하는 코드를 작성 합니다. 필요가 없습니다 테스트 하는 매개 변수에 대 한 호출 코드에 제공 합니다. Visual Basic에서는 프로시저의 일치 하는 버전 제어를 전달합니다.  
  
4. 사용 하 여 프로시저의 각 버전을 종료 합니다 `End Sub` 또는 `End Function` 문으로 적절 하 게 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 정의 `Sub` 고객의 잔액에 대 한 트랜잭션을 게시 하는 절차입니다. 사용 된 `Overloads` 이름과 다른 고객 계정 번호를 허용 하는 프로시저의 두 버전을 정의 하는 키워드입니다.  
  
 [!code-vb[VbVbcnProcedures#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#72)]  
  
 호출 코드로 고객 id를 가져올 수는 `String` 또는 `Integer`, 다음 두 경우 모두 동일한 호출 문을 사용 하 여 합니다.  
  
 이러한 버전을 호출 하는 방법에 대 한 정보에 대 한 합니다 `post` 프로시저 참조 [방법: 오버 로드 된 프로시저 호출](./how-to-call-an-overloaded-procedure.md)합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 각 오버 로드 된 버전의 프로시저 이름이 같지만 서로 다른 매개 변수 목록이 있는지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [프로시저 문제 해결](./troubleshooting-procedures.md)
- [방법: 선택적 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [방법: 무한 개수의 매개 변수를 사용 하는 프로시저 오버 로드](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [프로시저를 오버로드할 때 고려해야 할 사항](./considerations-in-overloading-procedures.md)
- [오버로드 확인](./overload-resolution.md)
