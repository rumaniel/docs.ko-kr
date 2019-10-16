---
title: 개체 ID
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c788f2f9-65cc-4455-9907-e8388a268e00
ms.openlocfilehash: 053c861bae951f044d30d048951aa072b3d85a42
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792946"
---
# <a name="object-identity"></a>개체 ID
런타임의 개체는 고유한 ID를 가집니다. 동일한 개체를 참조하는 두 개의 변수는 실제로 해당 개체의 동일한 인스턴스를 참조합니다. 따라서 하나의 변수를 통해 수행한 변경 내용을 다른 변수를 통해 즉시 볼 수 있습니다.  
  
 관계형 데이터베이스 테이블의 행에는 고유한 ID가 없습니다. 각 행에 고유한 기본 키가 있으므로 두 개 행이 동일한 키 값을 공유하지 않습니다. 그러나 데이터베이스 테이블의 콘텐츠에만 이 제한이 적용됩니다.  
  
 실제로는 애플리케이션이 데이터를 사용하는 다른 계층으로 데이터베이스의 데이터를 가져오는 경우가 가장 일반적입니다. 이는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 지원하는 모델입니다. 데이터를 데이터베이스에서 행으로 가져올 때 동일한 데이터를 나타내는 두 개의 행이 실제로 동일한 행 인스턴스에 해당하지 않습니다. 특정 고객을 두 번 쿼리할 경우 두 개의 데이터 행을 얻게 되며 각 행은 동일한 정보를 포함합니다.  
  
 개체의 경우 전혀 다른 결과가 발생합니다. <xref:System.Data.Linq.DataContext>에 동일한 정보를 반복해서 요청할 경우 실제로 동일한 개체 인스턴스가 제공될 것입니다. 개체가 애플리케이션에 대해 특별한 의미를 가지며 동일한 개체로 작동할 것으로 예상되므로 이 동작이 발생합니다. 개체를 계층 구조나 그래프로 디자인하고 동일한 항목을 여러 번 요청했으면 개체는 이와 같이 검색되고 중복된 많은 인스턴스가 제공되지 않습니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 <xref:System.Data.Linq.DataContext>는 개체 ID를 관리합니다. 데이터베이스에서 새 행을 검색할 때마다 해당 기본 키별로 ID 테이블에 행이 기록되고 새 개체가 만들어집니다. 동일한 해당 행을 검색할 때마다 원래 개체 인스턴스가 애플리케이션에 다시 전달됩니다. 이와 같은 방식으로 <xref:System.Data.Linq.DataContext>는 데이터베이스에 인식하는 ID의 개념(즉, 기본 키)을 언어에서 인식하는 ID의 개념(즉, 인스턴스)으로 변환합니다. 애플리케이션은 처음 검색된 상태로만 개체를 봅니다. 새 데이터는 다를 경우 삭제됩니다. 자세한 내용은 [Id 캐시에서 개체 검색](retrieving-objects-from-the-identity-cache.md)을 참조 하세요.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 낙관적 업데이트를 지원하기 위해 이 방법을 사용하여 로컬 개체의 무결성을 관리합니다. 개체가 처음 만들어진 후에 발생한 변경만 애플리케이션에 의해 수행된 변경이므로 애플리케이션에서 의도하는 바를 분명히 알 수 있습니다. 도중에 외부로부터 변경이 발생한 경우에는 `SubmitChanges()`가 호출될 때 해당 변경 내용이 식별됩니다.  
  
> [!NOTE]
> 쿼리에 의해 요청된 개체를 이미 검색된 개체로 쉽게 식별할 수 있는 경우 쿼리가 실행되지 않습니다. ID 테이블은 이전에 검색된 모든 개체의 캐시로 작동합니다.  
  
## <a name="examples"></a>예  
  
### <a name="object-caching-example-1"></a>개체 캐싱 예제 1  
 이 예제에서는 동일한 쿼리를 두 번 실행할 경우 항상 메모리의 동일한 개체에 대한 참조가 수신됩니다.  
  
 [!code-csharp[DLinqObjectIdentity#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#1)]
 [!code-vb[DLinqObjectIdentity#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#1)]  
  
### <a name="object-caching-example-2"></a>개체 캐싱 예제 2  
 이 예제에서는 데이터베이스에서 동일한 행을 반환하는 다른 쿼리를 실행할 경우 항상 메모리의 동일한 개체에 대한 참조가 수신됩니다.  
  
 [!code-csharp[DLinqObjectIdentity#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectIdentity/cs/Program.cs#2)]
 [!code-vb[DLinqObjectIdentity#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectIdentity/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
