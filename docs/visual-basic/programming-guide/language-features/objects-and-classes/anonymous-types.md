---
title: 익명 형식(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.AnonymousType
helpviewer_keywords:
- anonymous types [Visual Basic], about anonymous types
- anonymous types [Visual Basic]
- types [Visual Basic], anonymous
ms.assetid: 7b87532c-4b3e-4398-8503-6ea9d67574a4
ms.openlocfilehash: 2d134b8c8ef202a91b35ad8645bf63622b5e8030
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040837"
---
# <a name="anonymous-types-visual-basic"></a>익명 형식(Visual Basic)
Visual Basic는 데이터 형식에 대 한 클래스 정의를 작성 하지 않고 개체를 만들 수 있도록 하는 익명 형식을 지원 합니다. 대신 컴파일러가 클래스를 생성합니다. 클래스에는 사용할 수 있는 이름이 없고에서 <xref:System.Object>직접 상속 되며 개체를 선언할 때 지정 하는 속성이 포함 됩니다. 데이터 형식의 이름을 지정 하지 않았기 때문에 *익명 형식*이라고 합니다.  
  
 다음 예제에서는 변수 `product` 를 선언 하 고, `Name` 및 `Price`라는 두 개의 속성이 있는 무명 형식의 인스턴스로 만듭니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#1)]  
  
 쿼리 *식은* 익명 형식을 사용 하 여 쿼리에 의해 선택 된 데이터 열을 결합 합니다. 특정 쿼리에서 선택할 수 있는 열을 예측할 수 없으므로 결과 유형을 미리 정의할 수 없습니다. 익명 형식을 사용 하면 임의 개수의 열을 순서 대로 선택 하는 쿼리를 작성할 수 있습니다. 컴파일러는 지정 된 속성 및 지정 된 순서와 일치 하는 데이터 형식을 만듭니다.  
  
 다음 예제 `products` 에서는 각각 여러 속성을 포함 하는 제품 개체의 목록입니다. 변수 `namePriceQuery` 는 실행 시 `Name` 및 `Price`라는 두 개의 속성이 있는 익명 형식의 인스턴스 컬렉션을 반환 하는 쿼리 정의를 포함 합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#2)]  
  
 변수 `nameQuantityQuery` 는 실행 시 `Name` 및 `OnHand`라는 두 개의 속성이 있는 익명 형식의 인스턴스 컬렉션을 반환 하는 쿼리 정의를 포함 합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#3)]  
  
 익명 형식에 대해 컴파일러에서 생성 하는 코드에 대 한 자세한 내용은 [익명 형식 정의](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)를 참조 하세요.  
  
> [!CAUTION]
> 익명 형식의 이름은 컴파일러에서 생성 되며 컴파일 간에 달라질 수 있습니다. 프로젝트를 다시 컴파일할 때 이름이 변경 될 수 있기 때문에 코드에서를 사용 하거나 익명 형식의 이름을 사용 하면 안 됩니다.  
  
## <a name="declaring-an-anonymous-type"></a>무명 형식 선언  
 무명 형식의 인스턴스 선언에서는 이니셜라이저 목록을 사용 하 여 형식의 속성을 지정 합니다. 무명 형식을 선언 하는 경우에는 속성을 지정할 수 있으며, 메서드 또는 이벤트와 같은 다른 클래스 요소는 지정할 수 없습니다. 다음 예제 `product1` 에서는 `Name` 와 `Price`라는 두 개의 속성이 있는 무명 형식의 인스턴스입니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#4)]  
  
 속성을 키 속성으로 지정 하는 경우이 속성을 사용 하 여 두 익명 형식 인스턴스가 같은지 비교할 수 있습니다. 그러나 키 속성의 값은 변경할 수 없습니다. 자세한 내용은이 항목의 뒷부분에 나오는 키 속성 섹션을 참조 하세요.  
  
 무명 형식의 인스턴스를 선언 하는 것은 개체 이니셜라이저를 사용 하 여 명명 된 형식의 인스턴스를 선언 하는 것과 같습니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#5)]  
  
 익명 형식 속성 [을 지정 하는 다른 방법에 대 한 자세한 내용은 방법: 익명 형식 선언](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)에서 속성 이름 및 형식을 유추 합니다.  
  
## <a name="key-properties"></a>키 속성  
 키 속성은 다음과 같은 몇 가지 기본적인 방법으로 키가 아닌 속성과 다릅니다.  
  
- 두 인스턴스가 같은지 여부를 확인 하기 위해 키 속성의 값만 비교 됩니다.  
  
- 키 속성의 값은 읽기 전용 이며 변경할 수 없습니다.  
  
- 익명 형식에 대 한 컴파일러 생성 해시 코드 알고리즘에는 키 속성 값만 포함 됩니다.  
  
### <a name="equality"></a>같음  
 익명 형식의 인스턴스는 동일한 익명 형식의 인스턴스인 경우에만 동일할 수 있습니다. 컴파일러는 다음 조건을 충족 하는 경우 두 인스턴스를 동일한 형식의 인스턴스로 처리 합니다.  
  
- 이러한 어셈블리는 동일한 어셈블리에 선언 됩니다.  
  
- 해당 속성의 이름은 동일 하 고 유추 된 형식이 같으며 동일한 순서로 선언 됩니다. 이름 비교는 대/소문자를 구분 하지 않습니다.  
  
- 각각의 동일한 속성이 키 속성으로 표시 됩니다.  
  
- 각 선언에서 하나 이상의 속성이 키 속성입니다.  
  
 키 속성이 없는 무명 형식의 인스턴스는 자체와 동일 합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#6)]  
  
 동일한 익명 형식의 두 인스턴스는 해당 키 속성의 값이 동일한 경우에 동일 합니다. 다음 예에서는 같음을 테스트 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#7)]  
  
### <a name="read-only-values"></a>읽기 전용 값  
 키 속성의 값은 변경할 수 없습니다. 예 `prod8` 를 들어 앞의 예제에서 `Name` `Price` `read-only`및필드는 이지만 변경할 수있습니다.`OnHand`  
  
 [!code-vb[VbVbalrAnonymousTypes#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#8)]  
  
## <a name="anonymous-types-from-query-expressions"></a>쿼리 식의 익명 형식  
 쿼리 식에는 항상 익명 형식을 만들 필요가 없습니다. 가능 하면 기존 형식을 사용 하 여 열 데이터를 저장 합니다. 이는 쿼리가 데이터 원본에서 전체 레코드를 반환 하거나 각 레코드의 필드를 하나만 반환 하는 경우에 발생 합니다. 다음 코드 예제 `customers` 에서는 `Customer` 클래스의 개체 컬렉션입니다. 클래스에는 많은 속성이 있으며 쿼리 결과에서 순서에 관계 없이 하나 이상의 속성을 포함할 수 있습니다. 처음 두 예제에서는 쿼리가 명명 된 형식의 요소를 선택 하기 때문에 익명 형식이 필요 하지 않습니다.  
  
- `custs1`가 문자열 이기 때문 `cust.Name` 에 문자열의 컬렉션을 포함 합니다.  
  
     [!code-vb[VbVbalrAnonymousTypes#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#30)]  
  
- `custs2`의 `Customer` `Customer` 각 요소가 개체이 고 전체 요소가 쿼리에서 선택 되기 때문에 개체의 컬렉션을 포함 합니다. `customers`  
  
     [!code-vb[VbVbalrAnonymousTypes#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#31)]  
  
 그러나 적절 한 명명 된 형식은 항상 사용할 수 있는 것은 아닙니다. 한 가지 목적으로 고객 이름 및 주소를 선택 하 고, 다른 사용자에 대 한 고객 ID 번호 및 위치를 선택 하 고, 세 번째에 대 한 고객 이름, 주소 및 주문 기록을 선택할 수 있습니다. 익명 형식을 사용 하면 결과를 저장 하기 위해 새 명명 된 형식을 먼저 선언 하지 않고 임의의 순서로 속성 조합을 선택할 수 있습니다. 대신 컴파일러는 각 속성 컴파일에 대해 무명 형식을 만듭니다. 다음 쿼리는의 `Customer` `customers`각 개체에서 고객의 이름과 ID 숫자만 선택 합니다. 따라서 컴파일러는 이러한 두 속성만 포함 하는 무명 형식을 만듭니다.  
  
 [!code-vb[VbVbalrAnonymousTYpes#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#32)]  
  
 무명 형식의 속성 이름과 데이터 형식은 모두, `Select` `cust.Name` 및 `cust.ID`에 대 한 인수에서 가져옵니다. 쿼리에서 만든 무명 형식의 속성은 항상 키 속성입니다. 다음 `custs3` `Name` `ID`루프에서를 실행 하는 경우 결과는 두 개의 키 속성인 및가 있는 익명 형식의 인스턴스 컬렉션입니다. `For Each`  
  
 [!code-vb[VbVbalrAnonymousTypes#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class2.vb#33)]  
  
 로 `custs3` 표현 되는 컬렉션의 요소는 강력한 형식이 며 IntelliSense를 사용 하 여 사용 가능한 속성을 탐색 하 고 해당 형식을 확인할 수 있습니다.  
  
 자세한 내용은 [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)를 참조 하세요.  
  
## <a name="deciding-whether-to-use-anonymous-types"></a>익명 형식 사용 여부 결정  
 개체를 익명 클래스의 인스턴스로 만들기 전에이 옵션을 선택 하는 것이 가장 좋습니다. 예를 들어 관련 데이터를 포함 하는 임시 개체를 만들려는 경우 전체 클래스에 포함 될 수 있는 다른 필드와 메서드가 필요 하지 않은 경우 무명 형식은 좋은 솔루션입니다. 또한 각 선언에 대해 다른 속성을 선택 하려는 경우 나 속성의 순서를 변경 하려는 경우에는 익명 형식도 편리 합니다. 그러나 프로젝트에 같은 속성을 가진 개체가 여러 개 포함 되어 있는 경우에는 클래스 생성자를 사용 하 여 명명 된 형식을 사용 하 여 보다 쉽게 선언할 수 있습니다. 예를 들어 적절 한 생성자를 사용 하는 경우 익명 형식의 여러 인스턴스를 선언 `Product` 하는 것 보다 클래스의 여러 인스턴스를 선언 하는 것이 더 쉽습니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#9)]  
  
 명명 된 형식의 또 다른 장점은 컴파일러에서 실수로 잘못 된 형식의 속성 이름을 catch 할 수 있다는 것입니다. 앞의 예제 `firstProd2` `secondProd2`에서, 및 `thirdProd2` 는 동일한 익명 형식의 인스턴스인 것입니다. 그러나 다음 방법 중 하나를 실수로 선언 `thirdProd2` 하는 경우 해당 형식은 및 `secondProd2`의 `firstProd2` 형식과 다를 수 있습니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrAnonymousTypes/VB/Class1.vb#10)]  
  
 무엇 보다도, 명명 된 형식의 인스턴스에 적용 되지 않는 익명 형식의 사용에 대 한 제한 사항이 있습니다. `firstProd2`, `secondProd2` 및`thirdProd2` 는 동일한 익명 형식의 인스턴스입니다. 그러나 공유 익명 형식의 이름은 사용할 수 없으며 코드에서 형식 이름이 필요한 위치에 나타날 수 없습니다. 예를 들어, 무명 형식은 메서드 시그니처를 정의 하는 데 사용 하거나 다른 변수나 필드를 선언 하거나 모든 형식 선언에 사용할 수 없습니다. 따라서 메서드 간에 정보를 공유 해야 하는 경우에는 익명 형식이 적절 하지 않습니다.  
  
## <a name="an-anonymous-type-definition"></a>익명 형식 정의  
 익명 형식의 인스턴스 선언에 대 한 응답으로 컴파일러는 지정 된 속성을 포함 하는 새 클래스 정의를 만듭니다.  
  
 익명 형식에 키 속성이 하나 이상 포함 <xref:System.Object>되어 있으면 정의는 <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>및 <xref:System.Object.ToString%2A>에서 상속 된 세 개의 멤버를 재정의 합니다. 같음을 테스트 하 고 해시 코드 값을 결정 하기 위해 생성 된 코드는 키 속성만 고려 합니다. 익명 형식에 키 속성이 없으면만 <xref:System.Object.ToString%2A> 재정의 됩니다. 익명 형식의 명시적으로 명명 된 속성은 이러한 생성 된 메서드와 충돌할 수 없습니다. 즉,, 또는 `.Equals` `.ToString` 를 사용 `.GetHashCode`하 여 속성의 이름을 지정할 수 없습니다.  
  
 하나 이상의 키 속성이 있는 무명 형식 정의는 <xref:System.IEquatable%601?displayProperty=nameWithType> 인터페이스를 구현 하기도 합니다. 여기서 `T` 은 익명 형식의 형식입니다.  
  
 컴파일러에서 생성 되는 코드 및 재정의 된 메서드의 기능에 대 한 자세한 내용은 [익명 형식 정의](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [방법: 익명 형식 선언에서 속성 이름 및 형식 유추](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [익명 형식 정의](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)
- [키](../../../../visual-basic/language-reference/modifiers/key.md)
