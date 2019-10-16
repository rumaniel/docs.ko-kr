---
title: 지연 된 실행과 지연 계산은 linq to XML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 31998eed-b95e-47fb-a865-9de1f337d1fb
ms.openlocfilehash: a8d3bec16fa8ca7f5c587a9fdbb6caac53b74efe
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64641996"
---
# <a name="deferred-execution-and-lazy-evaluation-in-linq-to-xml-visual-basic"></a>지연 된 실행과 지연 계산은 linq to XML (Visual Basic)
쿼리 및 축 연산은 흔히 지연된 실행을 사용하도록 구현됩니다. 이 항목에서는 지연된 실행의 요구 사항 및 장점과 몇 가지 구현 고려 사항에 대해 설명합니다.  
  
## <a name="deferred-execution"></a>지연된 실행  
 지연된 실행은 *실현된* 값이 실제로 필요할 때까지 식의 계산이 지연되는 것을 의미합니다. 지연된 실행은 특히 일련의 연결된 쿼리나 조작이 포함된 프로그램에서 큰 데이터 컬렉션을 조작해야 하는 경우 성능을 크게 높일 수 있습니다. 최상의 경우에는 지연된 실행을 통해 소스 컬렉션을 한 번만 반복할 수 있습니다.  
  
 LINQ 기술은 <xref:System.Linq?displayProperty=nameWithType>와 같은 다양한 LINQ 네임스페이스의 확장 메서드와 핵심 <xref:System.Xml.Linq.Extensions?displayProperty=nameWithType> 클래스의 멤버에서 지연된 실행을 광범위하게 사용합니다.  
  
## <a name="eager-vs-lazy-evaluation"></a>즉시 계산과 지연 계산 비교  
 지연된 실행을 구현하는 메서드를 작성하는 경우 지연 계산이나 즉시 계산 중에서 메서드 구현에 사용할 방법을 결정해야 합니다.  
  
- *지연 계산(lazy evaluation)* 에서는 소스 컬렉션의 단일 요소가 반복기를 호출할 때마다 처리됩니다. 이것이 반복기가 구현되는 일반적인 방법입니다.  
  
- *즉시 계산(eager evaluation)* 에서는 반복기를 처음 호출할 때 전체 컬렉션이 처리됩니다. 소스 컬렉션의 임시 복사본도 필요할 수 있습니다. 예를 들어, <xref:System.Linq.Enumerable.OrderBy%2A> 메서드는 첫 번째 요소를 반환하기 전에 전체 컬렉션을 정렬해야 합니다.  
  
 지연 계산은 컬렉션의 계산 전반에 오버헤드 처리를 균일하게 분산시키고 임시 데이터를 최소한으로 사용하기 때문에 대개 성능이 더 좋습니다. 물론 중간 결과를 구체화해야만 하는 연산도 있습니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서의 다음 항목에서는 지연된 실행을 보여 줍니다.  
  
- [지연된 실행 예제 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-example.md)  
  
## <a name="see-also"></a>참고자료

- [자습서: 지연 된 실행 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/tutorial-deferred-execution.md)
- [개념과 용어 (함수 변환) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/concepts-and-terminology-functional-transformation.md)
- [집계 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)
