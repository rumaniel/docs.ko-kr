---
title: '방법: 제네릭 클래스 (Visual Basic)를 사용 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- type parameters [Visual Basic], defining
- data type arguments [Visual Basic], defining
- arguments [Visual Basic], data types
- Of keyword [Visual Basic], using
- generic parameters
- data type parameters
- generics [Visual Basic], about generics
- data types [Visual Basic], as parameters
- data types [Visual Basic], as arguments
- parameters [Visual Basic], type
- types [Visual Basic], generic
- parameters [Visual Basic], generic
- generics [Visual Basic], creating generic types
- data type arguments
- parameters [Visual Basic], data type
- data type parameters [Visual Basic], defining
- type arguments [Visual Basic], defining
- arguments [Visual Basic], type
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
ms.openlocfilehash: b069d3a0249f6aff2f9f09c5a560e5708bd60aa6
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593364"
---
# <a name="how-to-use-a-generic-class-visual-basic"></a>방법: 제네릭 클래스 (Visual Basic)를 사용 합니다.
*형식 매개 변수* 를 사용하는 클래스를 *제네릭 클래스*라고 합니다. 제네릭 클래스를 사용 중인 경우 이러한 각 매개 변수에 대해 *형식 인수* 를 제공하여, 여기에서 *생성된 클래스* 를 만들 수 있습니다. 그런 다음 생성된 클래스 형식의 변수를 선언하고, 생성된 클래스의 인스턴스를 만들어 해당 변수에 할당할 수 있습니다.  
  
 클래스 이외에도 제네릭 구조체, 인터페이스, 프로시저 및 대리자도 정의할 수 있습니다.  
  
 다음 절차는.NET Framework에 정의 된 제네릭 클래스를 사용 하 고에서 인스턴스를 만듭니다.  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a>형식 매개 변수를 가져오는 클래스를 사용하려면  
  
1. 소스 파일의 시작 부분에 포함 됩니다.는 [Imports 문 (.NET Namespace 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 가져오려는 <xref:System.Collections.Generic?displayProperty=nameWithType> 네임 스페이스입니다. 이렇게 하면 <xref:System.Collections.Queue?displayProperty=nameWithType> 같은 다른 큐 클래스와 차별화하기 위해 정규화하지 않고도 <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> 클래스를 참조할 수 있습니다.  
  
2. 일반적인 방법으로 개체를 만들지만 추가 `(Of type)` 클래스 이름 바로 뒤 합니다.  
  
     다음 예에서는 동일한 클래스(<xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>)를 사용하여, 서로 다른 데이터 형식의 항목을 포함하는 두 개의 큐 개체를 만듭니다. 각 큐의 끝에 항목을 추가한 다음 각 큐의 앞부분부터 항목을 제거하고 표시합니다.  
  
     [!code-vb[VbVbalrDataTypes#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Visual Basic의 제네릭 형식](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [언어 독립성 및 언어 독립적 구성 요소](../../../../standard/language-independence-and-language-independent-components.md)
- [Of](../../../../visual-basic/language-reference/statements/of-clause.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [방법: 다른 데이터 형식에 동일한 기능을 제공할 수 있는 클래스 정의](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)
- [반복기](../../../../visual-basic/programming-guide/concepts/iterators.md)
