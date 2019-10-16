---
title: '방법: 개체 이니셜라이저 (Visual Basic)를 사용 하 여 개체 선언'
ms.date: 07/20/2015
helpviewer_keywords:
- declaring objects using object initializer
- object initializers [Visual Basic]
- initializers [Visual Basic]
- Video How tos, Visual Basic
ms.assetid: 0f53a553-efd6-466d-80bf-6b679e5cd174
ms.openlocfilehash: 850e20fe8b5b6bfd392c80c87950a81a1a8a5c24
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755205"
---
# <a name="how-to-declare-an-object-by-using-an-object-initializer-visual-basic"></a>방법: 개체 이니셜라이저 (Visual Basic)를 사용 하 여 개체 선언
개체 이니셜라이저를 사용 하 여 선언 하 고 단일 문으로 클래스의 인스턴스를 인스턴스화할 수 있습니다. 또한 매개 변수화 된 생성자를 호출 하지 않고 동시에, 하나 이상의 멤버 인스턴스를 초기화할 수 있습니다.  
  
 개체 이니셜라이저를 사용 하 여 명명 된 형식의 인스턴스를 만들 때 클래스에 대 한 매개 변수가 없는 생성자 라고 지정한 순서에 지정 된 멤버의 초기화가 수행 합니다.  
  
 다음 절차에는 인스턴스를 만드는 방법을 보여 줍니다는 `Student` 세 가지 방법으로 클래스입니다. 클래스 이름, 성 및 특히 클래스 year 속성에 있습니다. 새 인스턴스를 만들고 각 세 가지 선언 `Student`, 속성을 사용 하 여 `First` "Michael," 속성을로 `Last` "Tucker"로 설정 하 고 다른 모든 멤버를 기본값으로 설정 합니다. 프로시저의 각 선언 하면 개체 이니셜라이저를 사용 하지 않는 다음 예제와 같습니다.  
  
 [!code-vb[VbVbalrObjectInit#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#20)]  
  
 구현은 합니다 `Student` 클래스를 참조 하십시오 [방법: 항목 목록을 만드는](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)합니다. 클래스를 설정 하는 목록을 만듭니다. 해당 항목에서 코드를 복사할 수 있습니다 `Student` 개체를 사용 하 여 작동 합니다.  
  
### <a name="to-create-an-object-of-a-named-class-by-using-an-object-initializer"></a>개체 이니셜라이저를 사용 하 여 명명된 된 클래스의 개체를 만들려면  
  
1. 생성자를 사용 하는 계획 된 것 처럼 선언을 시작 합니다.  
  
     `Dim student1 As New Student`  
  
2. 키워드를 입력 `With`초기화 목록을 중괄호로 옵니다.  
  
     `Dim student1 As New Student With { <initialization list> }`  
  
3. 초기화 목록에서 초기화 하 고 초기 값을 할당 하려는 각 속성을 포함 합니다. 속성의 이름은 마침표 앞에 있습니다.  
  
     [!code-vb[VbVbalrObjectInit#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#21)]  
  
     클래스의 하나 이상의 멤버를 초기화할 수 있습니다.  
  
4. 또는 클래스의 새 인스턴스를 선언 하 고에 값을 할당할 수 있습니다. 인스턴스를 먼저 선언 `Student`:  
  
     `Dim student2 As Student`  
  
5. 인스턴스 만들기를 시작 `Student` 일반적인 방법입니다.  
  
     `Dim student2 As Student = New Student`  
  
6. 형식 `With` 및 다음 개체 이니셜라이저를 하나 이상의 멤버의 새 인스턴스를 초기화 합니다.  
  
     [!code-vb[VbVbalrObjectInit#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#22)]  
  
7. 생략 하 여 이전 단계에서 정의 단순화할 수 `As Student`입니다. 이 작업을 수행 하는 경우 컴파일러는 결정 `student3` 의 인스턴스가 `Student` 지역 형식 유추를 사용 하 여 합니다.  
  
     [!code-vb[VbVbalrObjectInit#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class2.vb#23)]  
  
     자세한 내용은 [로컬 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [방법: 항목 목록 만들기](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)
- [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
