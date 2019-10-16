---
title: 원격 쿼리 실행과 로컬 실행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ee50e943-9349-4c84-ab1c-c35d3ada1a9c
ms.openlocfilehash: a21d5bbffdb1a78d3062929a1ca384a750af59a7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781162"
---
# <a name="remote-vs-local-execution"></a>원격 및 로컬 실행
쿼리를 원격으로 실행할지(즉, 데이터베이스 엔진이 데이터베이스에 대해 쿼리 실행) 아니면 로컬로 실행할지(즉, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]이 로컬 캐시에 대해 쿼리 실행) 결정할 수 있습니다.  
  
## <a name="remote-execution"></a>원격 실행  
 다음 쿼리를 고려해 보세요.  
  
 [!code-csharp[DLinqQueryConcepts#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#7)]
 [!code-vb[DLinqQueryConcepts#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#7)]  
  
 데이터베이스에 수천 개의 주문 행이 있는 경우 작은 하위 집합을 처리하기 위해 이러한 행을 모두 검색하고 싶지 않을 것입니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 <xref:System.Data.Linq.EntitySet%601> 클래스는 <xref:System.Linq.IQueryable> 인터페이스를 구현합니다. 이 방법을 사용하면 이러한 쿼리를 원격으로 실행할 수 있습니다. 이 기술의 두 가지 주요 이점은 다음과 같습니다.  
  
- 불필요한 데이터가 검색되지 않습니다.  
  
- 데이터베이스 엔진이 실행하는 쿼리는 일반적으로 데이터베이스 인덱스로 인해 더 효율적입니다.  
  
## <a name="local-execution"></a>로컬 실행  
 다른 상황에서는 관련 엔터티의 전체 집합을 로컬 캐시에 포함하려고 할 수 있습니다. 이를 위해 <xref:System.Data.Linq.EntitySet%601>은 <xref:System.Data.Linq.EntitySet%601.Load%2A>의 모든 멤버를 명시적으로 로드하기 위한 <xref:System.Data.Linq.EntitySet%601> 메서드를 제공합니다.  
  
 <xref:System.Data.Linq.EntitySet%601>이 이미 로드된 경우 후속 쿼리는 로컬로 실행됩니다. 이 방법은 다음과 같은 두 가지 이점이 있습니다.  
  
- 전체 집합을 로컬로 사용하거나 여러 번 사용해야 할 경우 원격 쿼리 및 연관된 대기 시간을 방지할 수 있습니다.  
  
- 엔터티를 완전한 엔터티로 serialize할 수 있습니다.  
  
 다음 코드 조각에서는 로컬 실행을 수행하는 방법을 보여 줍니다.  
  
 [!code-csharp[DLinqQueryConcepts#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#8)]
 [!code-vb[DLinqQueryConcepts#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#8)]  
  
## <a name="comparison"></a>비교  
 이러한 두 기능은 대규모 컬렉션을 위한 원격 실행과 소규모 컬렉션 또는 완전한 컬렉션이 필요한 상황을 위한 로컬 실행이라는 옵션이 결합된 강력한 기능을 제공합니다. <xref:System.Linq.IQueryable>을 통해 원격 실행을 구현하고 메모리 내 <xref:System.Collections.Generic.IEnumerable%601> 컬렉션에 대해 로컬 실행을 구현합니다. 로컬 실행을 강제로 적용 하려면 (즉 <xref:System.Collections.Generic.IEnumerable%601>,) [제네릭 IEnumerable로 형식 변환](convert-a-type-to-a-generic-ienumerable.md)을 참조 하세요.  
  
### <a name="queries-against-unordered-sets"></a>정렬되지 않은 집합에 대한 쿼리  
 을 구현 <xref:System.Collections.Generic.List%601> 하는 로컬 컬렉션과 관계형 데이터베이스의 순서가 지정 되지 않은 *집합* 에 대해 실행 되는 원격 쿼리를 제공 하는 컬렉션 간의 중요 한 차이점을 확인 합니다. 인덱스 값을 사용하는 메서드와 같은 <xref:System.Collections.Generic.List%601> 메서드에는 목록 의미 체계가 필요한데 이는 일반적으로 정렬되지 않은 집합에 대한 원격 쿼리를 통해 얻을 수 없습니다. 이와 같은 이유 때문에 이러한 메서드는 로컬 실행을 허용하기 위해 <xref:System.Data.Linq.EntitySet%601>을 암시적으로 로드합니다.  
  
## <a name="see-also"></a>참고자료

- [쿼리 개념](query-concepts.md)
