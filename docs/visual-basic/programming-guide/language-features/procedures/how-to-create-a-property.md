---
title: '방법: 속성 (Visual Basic) 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- Visual Basic code, properties
- properties [Visual Basic]
ms.assetid: 4d229712-6be8-4c5c-bac5-06995ce9185a
ms.openlocfilehash: 91f34de36e88724ccab21097bf54a4604f7eee37
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61665782"
---
# <a name="how-to-create-a-property-visual-basic"></a>방법: 속성 (Visual Basic) 만들기
속성 정의 간에 묶습니다를 `Property` 문 및 `End Property` 문. 이 정의 내에서 정의 `Get` 프로시저는 `Set` 프로시저 중 하나 또는 둘 다. 이러한 프로시저 내에서 모든 속성의 코드에 표시 됩니다.  
  
 합니다 `Get` 속성의 값을 검색 하는 절차 및 `Set` 프로시저는 값을 저장 합니다. 속성이 읽기/쓰기 액세스를 하려는 경우 두 프로시저를 정의 해야 합니다. 읽기 전용 속성에 대 한 정의 `Get`, 고 쓰기 전용 속성에 대 한 정의 `Set`합니다.  
  
### <a name="to-create-a-property"></a>속성을 만들려면  
  
1. 외부 속성 또는 프로시저를 사용 하 여는 [Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)고 뒤에 `End Property` 문입니다.  
  
2. 매개 변수를 사용 하는 속성, 경우에 따라는 `Property` 키워드 프로시저 이름이 매개 변수 목록 괄호를 사용 합니다.  
  
3. 괄호 다음에 `As` 절 속성의 값의 데이터 형식을 지정 합니다. 쓰기 전용 속성에도 데이터 형식을 지정 해야 합니다.  
  
4. 추가 `Get` 고 `Set` 프로시저를 적절 하 게 합니다. 다음 지침을 참조 하십시오.  
  
### <a name="to-create-a-get-procedure-that-retrieves-a-property-value"></a>속성 값을 검색 하는 Get 프로시저를 만들려면  
  
1. 간에 `Property` 및 `End Property` 문을 작성을 [Get 문을](../../../../visual-basic/language-reference/statements/get-statement.md)뒤를 `End Get` 문. 모든 매개 변수를 정의할 필요가 없습니다를 `Get` 프로시저입니다.  
  
2. 사이의 속성의 값을 검색 하는 코드 문을 배치 합니다 `Get` 및 `End Get` 문입니다. 이 코드는 다른 계산 및 생성 하 고 속성의 값을 반환 하는 것 외에도 데이터 조작에 포함할 수 있습니다.  
  
3. 사용 하 여를 `Return` 문을 호출 코드에 속성의 값을 반환 합니다.  
  
 작성 해야 합니다는 `Get` 읽기 / 쓰기 속성 및 읽기 전용 속성에 대 한 절차입니다. 정의할 수 없습니다는 `Get` 쓰기 전용 속성에 대 한 절차입니다.  
  
### <a name="to-create-a-set-procedure-that-writes-a-propertys-value"></a>속성 값을 쓰는 집합 프로시저를 만들려면  
  
1. 간에 `Property` 및 `End Property` 문을 작성을 [Set 문을](../../../../visual-basic/language-reference/statements/set-statement.md)뒤를 `End Set` 문.  
  
2. 에 `Set` 문을 따릅니다는 `Set` 매개 변수 목록 괄호로 묶어 키워드. 이 매개 변수 목록 호출 코드에서 전달 된 값에 대 한 하나 이상의 값 매개 변수를 포함 해야 합니다. 이 값 매개 변수의 기본 이름은 `Value`, 하지만 해당 하는 경우 다른 이름을 사용할 수 있습니다. Value 매개 변수 데이터 형식이 해당 속성과 같은 있어야 합니다.  
  
3. 값은 속성을 저장 하는 코드 문을 배치 합니다 `Set` 및 `End Set` 문. 이 코드는 다른 계산 및 유효성 검사 및 속성의 값을 저장 하는 것 외에도 데이터 조작에 포함할 수 있습니다.  
  
4. 호출 코드에서 제공 된 값에 적용할 값 매개 변수를 사용 합니다. 대입문에서 직접이 값을 저장 하거나 저장할 내부 값을 계산 하는 식에 사용할 수 있습니다.  
  
 작성 해야 합니다는 `Set` 쓰기 전용 속성 및 읽기 / 쓰기 속성에 대 한 절차입니다. 정의할 수 없습니다는 `Set` 읽기 전용 속성에 대 한 절차입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 두 구성 요소 이름, 첫 번째 이름과 마지막 이름으로 전체 이름을 저장 하는 읽기/쓰기 속성을 만듭니다. 호출 코드를 읽을 때 `fullName`, `Get` 프로시저는 두 구성 요소 이름을 결합을 전체 이름을 반환 합니다. 호출 코드에서 새 전체 이름으로 할당 하는 경우는 `Set` 프로시저 두 구성 요소 이름으로 중단 하려고 합니다. 공간을 찾지 못하면, 모든 첫 번째 이름으로 저장 합니다.  
  
 [!code-vb[VbVbcnProcedures#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#8)]  
  
 다음 예제에서는 속성 프로시저를 호출 하는 일반적인 `fullName`합니다. 속성 값을 설정 하는 첫 번째 호출 및 두 번째 호출에서 검색 합니다.  
  
 [!code-vb[VbVbcnProcedures#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>참고자료

- [절차](./index.md)
- [속성 프로시저](./property-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Visual Basic에서 속성과 변수의 차이점](./differences-between-properties-and-variables.md)
- [방법: 액세스 수준이 혼합된 된 속성 선언](./how-to-declare-a-property-with-mixed-access-levels.md)
- [방법: 속성 프로시저 호출](./how-to-call-a-property-procedure.md)
- [방법: 선언 및 Visual Basic의 기본 속성을 호출](./how-to-declare-and-call-a-default-property.md)
- [방법: 속성 값 입력](./how-to-put-a-value-in-a-property.md)
- [방법: 속성에서 값 가져오기](./how-to-get-a-value-from-a-property.md)
