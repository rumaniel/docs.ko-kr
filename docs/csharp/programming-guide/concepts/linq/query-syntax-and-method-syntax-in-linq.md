---
title: LINQ의 쿼리 구문 및 메서드 구문(C#)
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], query syntax vs. method syntax
- queries [LINQ in C#], syntax comparisons
ms.assetid: eedd6dd9-fec2-428c-9581-5b8783810ded
ms.openlocfilehash: 8351661bdb7eaf841577eb128a8fec12efed2360
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591415"
---
# <a name="query-syntax-and-method-syntax-in-linq-c"></a>LINQ의 쿼리 구문 및 메서드 구문(C#)
[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)](Language Integrated Query) 소개 설명서에 있는 대부분의 쿼리는 LINQ 선언적 쿼리 구문을 사용하여 작성되었습니다. 그러나 쿼리 구문은 코드를 컴파일할 때 .NET CLR(공용 언어 런타임)에 대한 메서드 호출로 변환해야 합니다. 이러한 메서드 호출은 `Where`, `Select`, `GroupBy`, `Join`, `Max`, `Average` 등과 같은 표준 쿼리 연산자를 호출합니다. 사용자는 쿼리 구문 대신 메서드 구문을 사용하여 연산자를 직접 호출할 수 있습니다.  
  
 쿼리 구문과 메서드 구문은 의미상 동일하지만, 쿼리 구문이 더 간단하고 읽기 쉽다고 생각하는 사람이 많습니다. 일부 쿼리는 메서드 호출로 표현해야 합니다. 예를 들어, 지정된 조건과 일치하는 요소 수를 검색하는 쿼리를 표현하려면 메서드 호출을 사용해야 합니다. 또한 소스 시퀀스에서 최대값을 갖는 요소를 검색하는 쿼리에 대해서도 메서드 호출을 사용해야 합니다. <xref:System.Linq> 네임스페이스의 표준 쿼리 연산자에 대한 참조 문서는 일반적으로 메서드 구문을 사용합니다. 따라서 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 작성하기 시작한 경우에도 쿼리 및 쿼리 식 자체에서 메서드 구문을 사용하는 방법을 잘 알고 있으면 유용합니다.  
  
## <a name="standard-query-operator-extension-methods"></a>표준 쿼리 연산자 확장 메서드  
 다음 예제는 간단한 *쿼리 식* 및 *메서드 기반 쿼리*로서 작성된, 의미상 동등한 쿼리를 보여 줍니다.  
  
 [!code-csharp[csLINQGettingStarted#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#22)]  
  
 두 예제에서 출력은 동일합니다. 쿼리 변수의 형식이 두 양식에서 모두 동일한 것을 알 수 있습니다(<xref:System.Collections.Generic.IEnumerable%601>).  
  
 메서드 기반 쿼리를 이해할 수 있도록 더 자세히 살펴보겠습니다. 식의 오른쪽에서 `where` 절이 이제 `numbers` 개체의 인스턴스 메서드로 표현된 것을 알 수 있습니다. 이 개체를 다시 호출하면 `IEnumerable<int>` 형식을 갖게 됩니다. 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스에 대해 잘 알고 있다면 여기에 `Where` 메서드가 없다는 사실을 알 것입니다. 그러나 Visual Studio IDE에서 IntelliSense 완성 목록을 호출하면 `Where` 메서드뿐 아니라 `Select`, `SelectMany`, `Join`, `Orderby` 등의 다른 많은 메서드도 볼 수 있습니다. 이들은 모두 표준 쿼리 연산자입니다.  
  
 ![Intellisense에서 모든 표준 쿼리 연산자를 보여주는 스크린샷](./media/query-syntax-and-method-syntax-in-linq/standard-query-operators.png)  
  
 <xref:System.Collections.Generic.IEnumerable%601>이 이러한 추가 메서드를 포함하도록 다시 정의된 것처럼 보이지만 실제로는 그렇지 않습니다. 표준 쿼리 연산자는 *확장 메서드*라는 새로운 종류의 메서드로서 구현됩니다. 확장 메서드는 기존 형식을 "확장"하며, 마치 형식에 대한 인스턴스 메서드인 것처럼 호출할 수 있습니다. 표준 쿼리 연산자는 <xref:System.Collections.Generic.IEnumerable%601>을 확장하므로 `numbers.Where(...)`를 작성할 수 있습니다.  
  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]를 사용하기 시작할 때 확장 메서드에 대해 알아야 할 것은, 정확한 `using` 지시문을 사용하여 이를 애플리케이션의 범위로 가져오는 방법뿐입니다. 애플리케이션의 관점에서는 일반 인스턴스 메서드와 확장 메서드가 동일합니다.  
  
 확장 메서드에 대한 자세한 내용은 [확장 메서드](../../classes-and-structs/extension-methods.md)를 참조하세요. 표준 쿼리 연산자에 대한 자세한 내용은 [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)를 참조하세요. [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 및 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 같은 일부 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자는 <xref:System.Collections.Generic.IEnumerable%601> 이외의 다른 형식에 대해 자체 표준 쿼리 연산자 및 추가 확장 메서드를 구현합니다.  
  
## <a name="lambda-expressions"></a>람다 식  
 앞의 예제에서 조건식(`num % 2 == 0`)은 `Where` 메서드에 인라인 인수로 전달됩니다. `Where(num => num % 2 == 0).` 이 인라인 식을 람다 식이라고 합니다. 이 방법을 사용하면 무명 메서드나 제네릭 대리자 또는 식 트리로서 좀 더 복잡한 형식으로 작성해야 하는 코드를 편리하게 작성할 수 있습니다. C#에서 `=>`는 "goes to"로 읽는 람다 연산자입니다. 연산자 왼쪽의 `num`은 쿼리 식의 `num`에 해당하는 입력 변수입니다. 컴파일러는 `numbers`가 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 형식이라는 것을 알고 있으므로 `num`의 형식을 유추할 수 있습니다. 람다의 본문은 쿼리 구문의 식 또는 다른 C# 식이나 문의 식과 동일하며, 메서드 호출 및 기타 복잡한 논리를 포함할 수 있습니다. "반환 값"은 식 결과입니다.  
  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 사용을 시작하기 위해 람다를 광범위하게 사용할 필요는 없습니다. 그러나 특정 쿼리는 메서드 구문으로만 표현할 수 있으며 그중 일부는 람다 식이 필요합니다. 람다에 익숙해지면 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 도구 상자에서 람다가 강력하고 유연한 도구임을 알게 될 것입니다. 자세한 내용은 [람다 식](../../statements-expressions-operators/lambda-expressions.md)을 참조하세요.  
  
## <a name="composability-of-queries"></a>쿼리 작성 가능성  
 이전 코드 예제에서는 `Where` 호출 시 점 연산자를 사용하여 `OrderBy` 메서드를 호출합니다. `Where`가 필터링된 시퀀스를 생성하면 `Orderby`는 이를 정렬하여 해당 시퀀스에서 작동합니다. 쿼리는 `IEnumerable`을 반환하기 때문에, 사용자는 메서드 호출을 함께 연결하여 메서드 구문에서 쿼리를 작성합니다. 사용자가 쿼리 구문을 사용하여 쿼리를 작성할 때 백그라운드에서는 컴파일러가 이 작업을 수행합니다. 쿼리 변수는 쿼리 결과를 저장하지 않기 때문에 언제든지 수정할 수 있으며, 실행한 후에도 언제든지 새 쿼리의 기반으로 사용할 수 있습니다.  
