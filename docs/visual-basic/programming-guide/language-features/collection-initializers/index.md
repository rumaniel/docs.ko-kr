---
title: 컬렉션 이니셜라이저(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.CollectionInitializer
helpviewer_keywords:
- collection initializers [Visual Basic]
ms.assetid: a9290329-77b0-4fdf-ae75-8fc17287f469
ms.openlocfilehash: 538efc11e477a4e90b7bca286da4ed56105d7ecb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906830"
---
# <a name="collection-initializers-visual-basic"></a>컬렉션 이니셜라이저(Visual Basic)

*컬렉션 이니셜라이저*는 컬렉션을 만들고 값의 초기 집합으로 채울 수 있도록 하는 약식 구문을 제공합니다. 컬렉션 이니셜라이저는 알려진 값(예: 메뉴 옵션 또는 범주 목록, 숫자 값의 초기 집합, 일 또는 월 이름과 같은 문자열의 정적 목록 또는 유효성 검사에 사용되는 상태 목록과 같은 지리적 위치)의 집합에서 컬렉션을 만드는 경우에 유용합니다.

항목 컬렉션에 대한 자세한 내용은 [컬렉션](../../../../visual-basic/programming-guide/concepts/collections.md)을 참조하세요.

`From` 키워드 뒤에 중괄호(`{}`)를 사용하여 컬렉션 이니셜라이저를 식별합니다. 이것은 [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)에서 설명된 배열 리터럴 구문과 비슷합니다. 다음 예제에서는 컬렉션 이니셜라이저를 사용하여 컬렉션을 만드는 다양한 방법을 보여 줍니다.

[!code-vb[VbVbalrCollectionInitializers#1](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#1)]

> [!NOTE]
> C#에서도 컬렉션 이니셜라이저를 제공합니다. C# 컬렉션 이니셜라이저는 Visual Basic 컬렉션 이니셜라이저와 같은 기능을 제공합니다. C# 컬렉션 이니셜라이저에 대한 자세한 내용은 [개체 및 컬렉션 이니셜라이저](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)를 참조하세요.

## <a name="syntax"></a>구문

컬렉션 이니셜라이저는 다음 코드에서처럼 `From` 키워드 뒤에서 중괄호(`{}`)로 묶인 쉼표로 구분된 값 목록으로 구성됩니다.

[!code-vb[VbVbalrCollectionInitializers#2](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#2)]

<xref:System.Collections.Generic.List%601> 또는 <xref:System.Collections.Generic.Dictionary%602>와 같은 컬렉션을 만들 경우 다음 코드와 같이 컬렉션 이니셜라이저 앞에 컬렉션 형식을 제공해야 합니다.

[!code-vb[VbVbalrCollectionInitializers#13](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#13)]

> [!NOTE]
> 같은 컬렉션 개체를 초기화하기 위해 컬렉션 이니셜라이저 및 개체 이니셜라이저를 결합할 수는 없습니다. 개체 이니셜라이저를 사용하여 컬렉션 이니셜라이저에서 개체를 초기화할 수 있습니다.

## <a name="creating-a-collection-by-using-a-collection-initializer"></a>컬렉션 이니셜라이저를 사용 하 여 컬렉션 만들기

컬렉션 이니셜라이저를 사용하여 컬렉션을 만들 경우 컬렉션 이니셜라이저로 제공되는 각 값은 컬렉션의 적절한 `Add` 메서드에 전달됩니다. 예를 들어 컬렉션 이니셜라이저를 사용하여 <xref:System.Collections.Generic.List%601>를 만들 경우 컬렉션 이니셜라이저의 각 문자열 값은 <xref:System.Collections.Generic.List%601.Add%2A> 메서드에 전달됩니다. 컬렉션 이니셜라이저를 사용하여 컬렉션을 만들려면 지정된 형식이 유효한 컬렉션 형식이어야 합니다. 유효한 컬렉션 형식의 예에는 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 구현하거나 <xref:System.Collections.CollectionBase> 클래스를 상속하는 클래스가 포함됩니다. 또한 지정된 형식은 다음 조건을 충족하는 `Add` 메서드를 노출해야 합니다.

- `Add` 메서드는 컬렉션 이니셜라이저가 호출되고 있는 범위에서 사용할 수 있어야 합니다. 컬렉션의 public이 아닌 메서드에 액세스할 수 있는 시나리오에서 컬렉션 이니셜라이저를 사용하는 경우 `Add` 메서드는 public일 필요가 없습니다.

- `Add` 메서드는 컬렉션 클래스의 인스턴스 멤버 또는 `Shared` 멤버이거나 확장 메서드여야 합니다.

- 오버로드 확인 규칙에 따라 컬렉션 이니셜라이저에서 제공되는 형식과 일치할 수 있는 `Add` 메서드가 있어야 합니다.

 예를 들어 다음 코드 예제에서는 컬렉션 이니셜라이저를 사용하여 `List(Of Customer)` 컬렉션을 만드는 방법을 보여 줍니다. 코드가 실행되면 각 `Customer` 개체가 제네릭 목록의 `Add(Customer)` 메서드에 전달됩니다.

[!code-vb[VbVbalrCollectionInitializers#9](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#9)]

다음 코드 예제에서는 컬렉션 이니셜라이저를 사용하지 않는 동일한 코드를 보여 줍니다.

[!code-vb[VbVbalrCollectionInitializers#10](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#10)]

`Customer` 개체에 대한 생성자와 일치하는 매개 변수가 있는 `Add` 메서드가 컬렉션에 포함된 경우 다음 섹션에 설명된 대로 `Add` 메서드에 대한 매개 변수 값을 컬렉션 이니셜라이저 내에 중첩할 수 있습니다. 컬렉션에 이런 `Add` 메서드가 없는 경우 확장 메서드로 만들 수 있습니다. 만드는 방법의 예는 `Add` 메서드는 컬렉션에 대 한 확장 메서드로 참조 [방법: 만들기는 확장 메서드는 컬렉션 이니셜라이저에서 사용 되는 추가](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)합니다. 컬렉션 이니셜라이저를 사용 하 여 사용할 수 있는 사용자 지정 컬렉션을 만드는 방법의 예제를 참조 하세요. [방법: 컬렉션 이니셜라이저에서 사용 되는 컬렉션을 만드는](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)합니다.

## <a name="nesting-collection-initializers"></a>컬렉션 이니셜라이저 중첩

값을 컬렉션 이니셜라이저 내에 중첩하여 만들고 있는 컬렉션에 대한 `Add` 메서드의 특정 오버로드를 식별할 수 있습니다. `Add` 메서드에 전달된 값은 배열 리터럴 또는 컬렉션 이니셜라이저에서 하는 것과 같이 쉼표로 구분하고 중괄호(`{}`)로 묶어야 합니다.

중첩된 값을 사용하여 컬렉션을 만들 경우 중첩된 값 목록의 각 요소는 요소 형식과 일치하는 `Add` 메서드에 인수로 전달됩니다. 예를 들어 다음 코드 예제에서는 키가 `Integer` 형식이고 값이 `String` 형식인 <xref:System.Collections.Generic.Dictionary%602>를 만듭니다. 각 중첩된 값 목록은 `Dictionary`에 대한 <xref:System.Collections.Generic.Dictionary%602.Add%2A> 메서드와 일치합니다.

[!code-vb[VbVbalrCollectionInitializers#5](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#5)]

이전 코드 예제는 다음 코드와 동일합니다.

[!code-vb[VbVbalrCollectionInitializers#6](../../../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCollectionInitializers/VB/Module1.vb#6)]

첫 번째 중첩 수준의 중첩된 값 목록만 컬렉션 형식에 대한 `Add` 메서드에 전송됩니다. 더 깊은 중첩 수준은 배열 리터럴로 처리되고 중첩된 값 목록이 컬렉션의 `Add` 메서드와 일치하지 않습니다.

## <a name="related-topics"></a>관련 항목

|제목|설명|
|---|---|
|[방법: 만들기는 컬렉션 이니셜라이저에서 사용 되는 확장 메서드를 추가 합니다.](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)|컬렉션 이니셜라이저의 값으로 컬렉션을 채우는 데 사용될 수 있는 `Add`라는 확장 메서드를 만드는 방법을 보여 줍니다.|
|[방법: 컬렉션 이니셜라이저에서 사용 되는 컬렉션 만들기](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)|`IEnumerable`을 구현하는 컬렉션 클래스에 `Add` 메서드를 포함하여 컬렉션 이니셜라이저를 사용할 수 있도록 설정하는 방법을 보여 줍니다.|

## <a name="see-also"></a>참고자료

- [컬렉션](../../../../visual-basic/programming-guide/concepts/collections.md)
- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md)
- [자동으로 구현된 속성](../../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)
- [방법: Visual Basic에서 배열 변수 초기화](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [방법: 항목 목록 만들기](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)
