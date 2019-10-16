---
title: 재귀 프로시저(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, procedures
- procedures [Visual Basic], that call themselves
- procedures [Visual Basic], recursive
- procedures [Visual Basic], calling
- recursive procedures
- functions [Visual Basic], calling recursively
- recursion
ms.assetid: ba1d3962-b4c3-48d3-875e-96fdb4198327
ms.openlocfilehash: b08a06a07f134b7c95251848862d39339e59fe61
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274350"
---
# <a name="recursive-procedures-visual-basic"></a>재귀 프로시저(Visual Basic)

*재귀* 프로시저는 자신을 호출 하는 프로시저입니다. 일반적으로 Visual Basic 코드를 작성 하는 가장 효과적인 방법은 아닙니다.  
  
 다음 절차에서는 재귀를 사용 하 여 원래 인수의 계승을 계산 합니다.  
  
 [!code-vb[VbVbcnProcedures#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#51)]  
  
## <a name="considerations-with-recursive-procedures"></a>재귀 프로시저에 대 한 고려 사항

 **제한 조건**. 재귀를 종료할 수 있는 조건을 하나 이상 테스트 하는 재귀 프로시저를 디자인 해야 하며, 적절 한 수의 재귀 호출 내에서 이러한 조건이 충족 되지 않는 경우도 처리 해야 합니다. 실패 없이 충족 될 수 있는 조건이 하나 이상 없으면 프로시저에서 무한 루프에서 실행 될 위험이 높습니다.

 **메모리 사용량**. 응용 프로그램에는 지역 변수에 대해 제한 된 공간이 있습니다. 프로시저는 자신을 호출할 때마다 해당 지역 변수의 추가 복사본에 대해 더 많은 공간을 사용 합니다. 이 프로세스가 무기한 지속 되 면 결국 <xref:System.StackOverflowException> 오류가 발생 합니다.

 **효율성**- 루프를 거의 항상 재귀로 대체할 수 있습니다. 루프는 인수를 전달 하 고, 추가 저장소를 초기화 하 고, 값을 반환 하는 오버 헤드를 갖지 않습니다. 재귀 호출 없이 성능이 훨씬 더 좋을 수 있습니다.

 **상호 재귀**. 두 프로시저가 서로를 호출 하는 경우 성능이 저하 되거나 무한 루프가 발생할 수 있습니다. 이러한 디자인은 단일 재귀 프로시저와 동일한 문제를 표시 하지만 검색 하 고 디버깅 하기 어려울 수 있습니다.

 **괄호를 사용 하 여를 호출**합니다. `Function` 프로시저 자체를 재귀적으로 호출 하는 경우에는 인수 목록이 없는 경우에도 프로시저 이름 뒤에 괄호를 사용 해야 합니다. 그렇지 않으면 함수 이름은 함수의 반환 값을 나타내는 것으로 간주 됩니다.

 **테스트**. 재귀 프로시저를 작성 하는 경우이를 신중 하 게 테스트 하 여 항상 제한 조건을 충족 하는지 확인 해야 합니다. 또한 재귀 호출이 너무 많기 때문에 메모리가 부족 하지 않은지 확인 해야 합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.StackOverflowException>
- [절차](index.md)
- [Sub 프로시저](sub-procedures.md)
- [Function 프로시저](function-procedures.md)
- [속성 프로시저](property-procedures.md)
- [연산자 프로시저](operator-procedures.md)
- [프로시저 매개 변수 및 인수](procedure-parameters-and-arguments.md)
- [프로시저 오버로딩](procedure-overloading.md)
- [프로시저 문제 해결](troubleshooting-procedures.md)
- [루프 구조](../control-flow/loop-structures.md)
