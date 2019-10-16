---
title: '개체 이니셜라이저: 명명 된 형식과 익명 형식 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.ObjectInitializer
helpviewer_keywords:
- object initializers [Visual Basic]
- anonymous types [Visual Basic], object initializers
- initializing properties [Visual Basic]
- initializers [Visual Basic]
- named types [Visual Basic]
ms.assetid: e2df3807-a70f-49dd-ac94-f1e07f472b1b
ms.openlocfilehash: e1f461cc98fb104f78a6c83a207cff7f4eda9227
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046458"
---
# <a name="object-initializers-named-and-anonymous-types-visual-basic"></a>개체 이니셜라이저: 명명 된 형식과 익명 형식 (Visual Basic)
개체 이니셜라이저를 사용 하면 단일 식을 사용 하 여 복합 개체에 대 한 속성을 지정할 수 있습니다. 명명 된 형식과 익명 형식의 인스턴스를 만드는 데 사용할 수 있습니다.  
  
## <a name="declarations"></a>선언  
 명명 된 형식과 익명 형식의 인스턴스 선언은 거의 동일 하 게 보일 수 있지만 그 영향은 동일 하지 않습니다. 각 범주에는 자체의 기능 및 제한 사항이 있습니다. 다음 예제에서는 개체 이니셜라이저 목록을 사용 하 여 명명 된 클래스 `Customer`의 인스턴스를 선언 하 고 초기화 하는 편리한 방법을 보여 줍니다. 클래스의 이름은 키워드 `New`뒤에 지정 됩니다.  
  
 [!code-vb[VbVbalrObjectInit#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#1)]  
  
 익명 형식에 사용할 수 있는 이름이 없습니다. 따라서 익명 형식의 인스턴스화에는 클래스 이름을 포함할 수 없습니다.  
  
 [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
 두 선언의 요구 사항과 결과가 동일 하지 않습니다. 의 `namedCust`경우 `Name` 속성이 `Customer` 있는 클래스는 이미 존재 해야 하며 선언은 해당 클래스의 인스턴스를 만듭니다. 의 `anonymousCust`경우 컴파일러는 하나의 속성, 라는 `Name`문자열이 있는 새 클래스를 정의 하 고 해당 클래스의 새 인스턴스를 만듭니다.  
  
## <a name="named-types"></a>명명 된 형식  
 개체 이니셜라이저는 형식의 생성자를 호출 하는 간단한 방법을 제공 하 고 단일 문에서 일부 또는 모든 속성의 값을 설정 합니다. 컴파일러가 인수를 제공 하지 않는 경우 매개 변수가 없는 생성자 또는 하나 이상의 인수가 전송 될 경우 매개 변수가 있는 생성자를 호출 하 여 문에 대 한 적절 한 생성자를 호출 합니다. 그런 다음 지정 된 속성은 이니셜라이저 목록에 표시 되는 순서 대로 초기화 됩니다.  
  
 이니셜라이저 목록의 각 초기화는 클래스의 멤버에 초기 값을 할당 하는 것으로 구성 됩니다. 멤버의 이름과 데이터 형식은 클래스를 정의할 때 결정 됩니다. 다음 예제에서 클래스는 `Customer` 있어야 하며,에는 문자열 값을 사용할 수 있는 및 `City` 라는 `Name` 멤버가 있어야 합니다.  
  
 [!code-vb[VbVbalrObjectInit#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#3)]  
  
 또는 다음 코드를 사용 하 여 동일한 결과를 얻을 수 있습니다.  
  
 [!code-vb[VbVbalrObjectInit#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#4)]  
  
 이러한 각 선언에는 매개 변수가 없는 생성자를 사용 `Customer` 하 여 개체를 만든 다음를 `With` 사용 하 여 `Name` 및 `City` 속성의 초기 값을 지정 하는 다음 예제와 동일 합니다. 선언문.  
  
 [!code-vb[VbVbalrObjectInit#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#5)]  
  
 예를 `Customer` 들어 클래스에에 대 한 `Name`값을 보낼 수 있는 매개 변수가 있는 생성자가 포함 된 경우 다음과 같은 방법으로 개체를 `Customer` 선언 하 고 초기화할 수도 있습니다.  
  
 [!code-vb[VbVbalrObjectInit#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#6)]  
  
 다음 코드에 나와 있는 것 처럼 모든 속성을 초기화할 필요는 없습니다.  
  
 [!code-vb[VbVbalrObjectInit#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#7)]  
  
 그러나 초기화 목록은 비워 둘 수 없습니다. 초기화 되지 않은 속성은 해당 기본값을 유지 합니다.  
  
### <a name="type-inference-with-named-types"></a>명명 된 형식을 사용 하는 형식 유추  
 개체 이니셜라이저 및 로컬 형식 유추를 결합 하 `cust1` 여의 선언에 대 한 코드를 줄일 수 있습니다. 이렇게 하면 변수 선언에서 `As` 절을 생략할 수 있습니다. 변수의 데이터 형식은 할당에 의해 생성 된 개체의 형식에서 유추 됩니다. 다음 예제에서의 `cust6` `Customer`형식은입니다.  
  
 [!code-vb[VbVbalrObjectInit#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#8)]  
  
### <a name="remarks-about-named-types"></a>명명 된 형식에 대 한 설명  
  
- 개체 이니셜라이저 목록에서 클래스 멤버를 두 번 이상 초기화할 수 없습니다. 선언 `cust7` 으로 인해 오류가 발생 합니다.  
  
     [!code-vb[VbVbalrObjectInit#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#9)]  
  
- 멤버를 사용 하 여 자체 또는 다른 필드를 초기화할 수 있습니다. 에 대 한 다음 선언과 같이 멤버가 초기화 되기 전에 액세스 되는 경우에 `cust8`는 기본값이 사용 됩니다. 개체 이니셜라이저를 사용 하는 선언이 처리 되는 경우 가장 먼저 적절 한 생성자가 호출 됩니다. 그런 다음 이니셜라이저 목록의 개별 필드가 초기화 됩니다. 다음 예에서는에 대 한 기본값 `Name` 가에 `cust8`할당 되 고 초기화 된 값이에 `cust9`할당 됩니다.  
  
     [!code-vb[VbVbalrObjectInit#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#10)]  
  
     `cust3` 다음 예제에서는 및 `cust4` 의 매개 변수가 있는 생성자를 사용 하 여 `cust10` 및 `cust11`를 선언 하 고 초기화 합니다.  
  
     [!code-vb[VbVbalrObjectInit#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#11)]  
  
- 개체 이니셜라이저는 중첩 될 수 있습니다. 다음 예제 `AddressClass` 에서은 `Address` `Customer` `AddressClass`및 `State`라는두 개의 속성이 있는 클래스 이며 클래스에는의 인스턴스인 속성이 있습니다. `City`  
  
     [!code-vb[VbVbalrObjectInit#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#12)]  
  
- 초기화 목록은 비워 둘 수 없습니다.  
  
- 초기화 되는 인스턴스는 Object 형식일 수 없습니다.  
  
- 초기화 되는 클래스 멤버는 공유 멤버, 읽기 전용 멤버, 상수 또는 메서드 호출 일 수 없습니다.  
  
- 초기화 되는 클래스 멤버는 인덱싱하거나 정규화 할 수 없습니다. 다음 예제에서는 컴파일러 오류를 발생 시킵니다.  
  
     `'' Not valid.`  
  
     `' Dim c1 = New Customer With {.OrderNumbers(0) = 148662}`  
  
     `' Dim c2 = New Customer with {.Address.City = "Springfield"}`  
  
## <a name="anonymous-types"></a>익명 형식  
 무명 형식은 개체 이니셜라이저를 사용 하 여 명시적으로 정의 하지 않고 이름을 지정 하는 새 형식의 인스턴스를 만듭니다. 대신, 컴파일러는 개체 이니셜라이저 목록에서 지정 하는 속성에 따라 형식을 생성 합니다. 형식의 이름을 지정 하지 않았기 때문에 *익명 형식*이라고 합니다. 예를 들어 다음 선언을의 `cust6`이전 선언과 비교 합니다.  
  
 [!code-vb[VbVbalrObjectInit#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#13)]  
  
 구문적으로 데이터 형식 `New` 에 대해 이름이 지정 되지 않는다는 점만 다릅니다. 그러나 수행 되는 작업은 매우 다릅니다. 컴파일러는 및 `Name` `City`라는 두 개의 속성을 포함 하는 새 익명 형식을 정의 하 고 지정 된 값을 사용 하 여 인스턴스를 만듭니다. 형식 유추는 예제에서 및 `Name` `City` 의 형식을 문자열로 지정 합니다.  
  
> [!CAUTION]
> 익명 형식의 이름은 컴파일러에 의해 생성 되며 컴파일 간에 달라질 수 있습니다. 코드에서 익명 형식의 이름을 사용 하거나 사용 하지 않아야 합니다.  
  
 형식의 이름을 사용할 수 없으므로 `As` 절을 사용 하 여를 선언할 `cust13`수 없습니다. 해당 형식을 유추 해야 합니다. 런타임에 바인딩을 사용 하지 않으면 로컬 변수에 익명 형식의 사용이 제한 됩니다.  
  
 익명 형식은 쿼리에 대 한 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 중요 한 지원을 제공 합니다. 쿼리에서 익명 형식을 사용 하는 방법에 대 한 자세한 내용은 [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) 및 [LINQ 소개 Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)를 참조 하세요.  
  
### <a name="remarks-about-anonymous-types"></a>익명 형식에 대 한 설명  
  
- 일반적으로 익명 형식 선언에 있는 모든 또는 대부분의 속성은 키 속성이 됩니다 .이 속성은 속성 이름 앞에 키워드 `Key` 를 입력 하 여 표시 됩니다.  
  
     [!code-vb[VbVbalrObjectInit#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#14)]  
  
     키 속성에 대 한 자세한 내용은 [키](../../../../visual-basic/language-reference/modifiers/key.md)를 참조 하세요.  
  
- 명명 된 형식과 마찬가지로 익명 형식 정의의 이니셜라이저 목록은 적어도 하나 이상의 속성을 선언 해야 합니다.  
  
     [!code-vb[VbVbalrObjectInit#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#2)]  
  
- 무명 형식의 인스턴스를 선언 하면 컴파일러는 일치 하는 익명 형식 정의를 생성 합니다. 속성의 이름과 데이터 형식은 인스턴스 선언에서 가져오며 컴파일러에 의해 정의에 포함 됩니다. 명명 된 형식과 같이 속성의 이름을 지정 하지 않고 미리 정의 합니다. 해당 형식이 유추 됩니다. `As` 절을 사용 하 여 속성의 데이터 형식을 지정할 수는 없습니다.  
  
- 익명 형식은 여러 가지 다른 방법으로 해당 속성의 이름과 값을 설정할 수도 있습니다. 예를 들어, 무명 형식 속성은 변수의 이름과 값 또는 다른 개체의 속성 이름 및 값을 모두 사용할 수 있습니다.  
  
     [!code-vb[VbVbalrObjectInit#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrObjectInit/VB/Class1.vb#15)]  
  
     익명 형식에서 속성을 [정의 하는 옵션에 대 한 자세한 내용은 방법: 익명 형식 선언](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)에서 속성 이름 및 형식을 유추 합니다.  
  
## <a name="see-also"></a>참고자료

- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [방법: 익명 형식 선언에서 속성 이름 및 형식 유추](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [키](../../../../visual-basic/language-reference/modifiers/key.md)
- [방법: 개체 이니셜라이저를 사용 하 여 개체 선언](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
