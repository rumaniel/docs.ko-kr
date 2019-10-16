---
title: '방법: 선언 및 Visual Basic의 기본 속성을 호출'
ms.date: 07/20/2015
helpviewer_keywords:
- defaults [Visual Basic], properties
- properties [Visual Basic], default
- procedures [Visual Basic], defining
- default properties [Visual Basic], in Visual Basic
- Visual Basic code, procedures
- Visual Basic code, properties
- default properties
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
ms.openlocfilehash: 9ca9a0ccdac3ac13429928233a0c09d58427ce74
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61665769"
---
# <a name="how-to-declare-and-call-a-default-property-in-visual-basic"></a>방법: 선언 및 Visual Basic의 기본 속성을 호출
A *속성의 기본값을* 지정 하지 않고 코드에 액세스할 수 있는 클래스 또는 구조체 속성입니다. 코드 이름은 호출 하는 경우 클래스 또는 구조 및 제외 속성을 하 고 컨텍스트 속성에 대 한 액세스 허용, Visual Basic 있을 경우 해당 클래스 또는 구조체의 기본 속성에 대 한 액세스를 확인 합니다.  
  
 클래스 또는 구조체만 가질 수 있습니다 기본 속성입니다. 그러나 기본 속성을 오버 로드할 수 있으며 둘 이상의 버전이 있을 수 있습니다.  
  
 자세한 내용은 [기본](../../../../visual-basic/language-reference/modifiers/default.md)입니다.  
  
### <a name="to-declare-a-default-property"></a>기본 속성을 선언 하려면  
  
1. 일반적인 방법으로 속성을 선언 합니다. 지정 하지 않으면 합니다 `Shared` 또는 `Private` 키워드입니다.  
  
2. 포함 된 `Default` 속성 선언에서 키워드입니다.  
  
3. 속성에 대 한 하나 이상의 매개 변수를 지정 합니다. 하나 이상의 인수를 사용 하지 않는 기본 속성을 정의할 수 없습니다.  
  
     [!code-vb[VbVbcnProcedures#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#17)]  
  
### <a name="to-call-a-default-property"></a>기본 속성을 호출 하려면  
  
1. 포함 하는 클래스 또는 구조체 형식의 변수를 선언 합니다.  
  
     [!code-vb[VbVbcnProcedures#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#16)]  
  
2. 일반적으로 포함 하는 속성 이름 식에 변수 이름만을 사용 합니다.  
  
     [!code-vb[VbVbcnProcedures#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#21)]  
  
3. 인수 목록의 괄호를 사용 하 여 변수 이름을 뒤에 있습니다. 기본 속성을 하나 이상의 인수를 수행 해야 합니다.  
  
     [!code-vb[VbVbcnProcedures#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#20)]  
  
4. 기본 속성 값을 검색할 식 또는 등호 다음에 인수 목록을 사용 하 여 변수 이름으로 사용 (`=`) 대입문에 로그인 합니다.  
  
     [!code-vb[VbVbcnProcedures#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#15)]  
  
5. 기본 속성 값을 설정 하려면 대입문의 왼쪽에는 인수 목록을 사용 하 여 변수 이름을 사용 합니다.  
  
     [!code-vb[VbVbcnProcedures#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#14)]  
  
6. 다른 속성에 액세스 하는 것 처럼에 항상 기본 속성 이름은 변수 이름과 함께 지정할 수 있습니다.  
  
     [!code-vb[VbVbcnProcedures#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#19)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 클래스의 기본 속성을 선언합니다.  
  
 [!code-vb[VbVbcnProcedures#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#12)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 기본 속성을 호출 하는 방법을 보여 줍니다 `myProperty` 클래스에 `class1`입니다. 값을 저장 하는 세 가지 대입문 `myProperty`, 및 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> 호출 값을 읽습니다.  
  
 [!code-vb[VbVbcnProcedures#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#13)]  
  
 기본 속성의 가장 일반적인 용도 <xref:Microsoft.VisualBasic.Collection.Item%2A> 다양 한 컬렉션 클래스의 속성입니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 기본 속성 소스 코드의 문자를 약간 저하 될 수 있습니다 하지만 코드를 더 읽기 어렵다고 만들 수 있습니다. 클래스 또는 구조체 이름으로 참조 하는 경우 호출 코드에서 클래스 또는 구조체에 익숙하지 않은 경우 수 없습니다 특정 클래스 또는 구조체 자체를 기본 속성을 참조 하는 액세스 하는 여부. 이 경우 미묘한 런타임 논리 오류나 컴파일러 오류가 발생할 수 있습니다.  
  
 항상 사용 하 여 기본 속성 오류 가능성을 다소 줄일 수 있습니다 합니다 [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md) 컴파일러 형식 검사를 설정 하려면 `On`합니다.  
  
 사용 하 여 미리 정의 된 클래스 또는 구조체 코드에서 결정 해야 기본 속성이 있는지 여부와 하려는 경우 해당 이름 이란 합니다.  
  
 이러한 단점 때문에 기본 속성을 정의 하지 않는 고려해 야 합니다. 코드의 가독성을 높이기 위해 항상 모든 속성에 명시적으로 참조할 수도도 기본 속성 해야 있습니다.  
  
## <a name="see-also"></a>참고자료

- [속성 프로시저](./property-procedures.md)
- [프로시저 매개 변수 및 인수](./procedure-parameters-and-arguments.md)
- [Property 문](../../../../visual-basic/language-reference/statements/property-statement.md)
- [기본](../../../../visual-basic/language-reference/modifiers/default.md)
- [Visual Basic에서 속성과 변수의 차이점](./differences-between-properties-and-variables.md)
- [방법: 속성 만들기](./how-to-create-a-property.md)
- [방법: 액세스 수준이 혼합된 된 속성 선언](./how-to-declare-a-property-with-mixed-access-levels.md)
- [방법: 속성 프로시저 호출](./how-to-call-a-property-procedure.md)
- [방법: 속성 값 입력](./how-to-put-a-value-in-a-property.md)
- [방법: 속성에서 값 가져오기](./how-to-get-a-value-from-a-property.md)
