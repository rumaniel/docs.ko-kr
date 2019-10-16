---
title: "'<typename>' 형식은 'System.Collections.Generic.IEnumerable(Of T)'의 여러 인스턴스를 구현하므로 이 형식의 'For Each'가 모호합니다."
ms.date: 07/20/2015
f1_keywords:
- vbc32096
- bc32096
helpviewer_keywords:
- BC32096
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
ms.openlocfilehash: bdfb6e9b1332db1f049bb2575e97215026efe0dd
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591762"
---
# <a name="for-each-on-type-typename-is-ambiguous-because-the-type-implements-multiple-instantiations-of-systemcollectionsgenericienumerableof-t"></a>'For Each' 형식에 '\<typename >' 형식을 'System.Collections.Generic.IEnumerable (Of T)'의 여러 인스턴스화를 구현 하기 때문에 모호
A `For Each` 둘 이상 있는 반복기 변수를 지정 하는 문을 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드.  
  
 반복기 변수를 구현 하는 형식 이어야 합니다는 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 또는 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 인터페이스 중 하나에 `Collections` .NET Framework의 네임 스페이스입니다. 둘 이상의 생성 된 제네릭 인터페이스를 각 생성에 대 한 다양 한 형식 인수를 사용 하 여 구현 하는 클래스에 대 한 것 같습니다. 이 작업을 수행 하는 클래스에서 반복기 변수를 사용 하는 경우 해당 변수가 둘 이상의 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드. 이러한 경우 Visual Basic 호출할 메서드를 선택할 수 없습니다.  
  
 **오류 ID:** BC32096  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 사용 하 여 [DirectCast 연산자](../../../visual-basic/language-reference/operators/directcast-operator.md) 또는 [TryCast 연산자](../../../visual-basic/language-reference/operators/trycast-operator.md) 정의 하는 인터페이스를 반복기 변수 형식으로 캐스팅할는 <xref:System.Collections.IEnumerable.GetEnumerator%2A> 메서드를 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- [For Each...Next 문](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [인터페이스](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
