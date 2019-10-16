---
title: '방법: 데이터베이스 관계 매핑'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 538def39-8399-46fb-b02d-60ede4e050af
ms.openlocfilehash: b6b1eba063c9ec72ae14c12028dd0950b2ad95f5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793529"
---
# <a name="how-to-map-database-relationships"></a>방법: 데이터베이스 관계 매핑
항상 동일하게 유지되는 모든 데이터 관계를 엔터티 클래스에서 속성 참조로 인코딩할 수 있습니다. 예를 들어 Northwind 샘플 데이터베이스에서는 일반적으로 고객이 주문을 하기 때문에 고객과 고객 주문 간의 관계가 항상 모델에 존재합니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 이러한 관계를 나타내는 데 도움이 되도록 <xref:System.Data.Linq.Mapping.AssociationAttribute> 특성을 정의합니다. 이 특성은 데이터베이스에서의 외래 키 관계가 무엇인지 나타내기 위해 <xref:System.Data.Linq.EntitySet%601> 및 <xref:System.Data.Linq.EntityRef%601> 형식과 함께 사용됩니다. 자세한 내용은 [특성 기반 매핑의](attribute-based-mapping.md)Association 특성 섹션을 참조 하세요.  
  
> [!NOTE]
> AssociationAttribute 및 ColumnAttribute Storage 속성 값은 대/소문자를 구분합니다. 예를 들어 AssociationAttribute.Storage 속성의 특성에 사용하는 값은 코드의 다른 곳에서 사용하는 해당 속성 이름과 대/소문자가 동일해야 합니다. 이 일반적으로 대/소문자 구분, Visual Basic을 포함 하지 않는 이더라도 모든.NET 프로그래밍 언어에 적용 됩니다. Storage 속성에 대한 자세한 내용은 <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>를 참조하세요.  
  
 이 항목의 뒷부분에 나오는 예제처럼 대부분의 관계는 일대다입니다. 다음과 같이 일대일 및 다대다 관계를 나타낼 수도 있습니다.  
  
- 일대일: 양쪽에를 포함 <xref:System.Data.Linq.EntitySet%601> 하 여 이러한 종류의 관계를 나타냅니다.  
  
     예 `Customer` - 를들어`Customer` , 고객의 보안 코드를 테이블에서 찾을 수 없으며 권한 있는 사용자만 액세스할 수 있도록 만든 관계가있습니다.`SecurityCode`  
  
- 다 대 다: 다 대 다 관계에서 링크 테이블의 기본 키 ( *접합* 테이블)는 다른 두 테이블의 복합 외래 키로 구성 되는 경우가 많습니다.  
  
     예를 들어 링크 테이블 `Employee` - `Project` 을사용`EmployeeProject`하 여 형성 된 다 대 다 관계를 생각해 보겠습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 `Employee`, `Project` 및 `EmployeeProject`라는 세 개의 클래스를 사용하여 이러한 관계를 모델링해야 합니다. 이 경우 `Employee` 및 `Project` 간의 관계를 변경하려면 기본 키 `EmployeeProject`의 업데이트가 필요한 것처럼 보일 수 있습니다. 그러나 이 상황을 모델링하는 최선의 방법은 기존 `EmployeeProject`를 삭제하고 새 `EmployeeProject`를 만드는 것입니다.  
  
    > [!NOTE]
    > 관계형 데이터베이스에서 관계는 일반적으로 다른 테이블의 기본 키를 참조하는 외래 키 값으로 모델링됩니다. 두 테이블 간에 이동 하려면 관계형 *조인* 작업을 사용 하 여 두 테이블을 명시적으로 연결 합니다.  
    >   
    >  반면의 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]개체는 *점* 표기법을 사용 하 여 탐색 하는 참조의 컬렉션 또는 속성 참조를 사용 하 여 서로를 참조 합니다.  
  
## <a name="example"></a>예제  
 다음 일대다 예제에서 `Customer` 클래스는 고객과 고객의 주문 사이의 관계를 선언하는 속성을 가집니다.  `Orders` 속성은 <xref:System.Data.Linq.EntitySet%601> 형식입니다. 이 형식은 이 관계가 일대다(한 명의 고객과 여러 개의 주문)라는 것을 나타냅니다. <xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A> 속성은 이 속성과 비교할 관련 클래스의 속성 이름을 지정함으로써 이 연결이 이루어지는 방법을 설명하는 데 사용됩니다. 이 예 `CustomerID` 에서는 데이터베이스 *조인이* 해당 열 값을 비교 하는 것 처럼 속성을 비교 합니다.  
  
> [!NOTE]
> Visual Studio를 사용 하는 경우 개체 관계형 디자이너를 사용 하 여 클래스 간의 연결을 만들 수 있습니다.  
  
 [!code-csharp[DlinqCustomize#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#3)]
 [!code-vb[DlinqCustomize#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#3)]  
  
## <a name="example"></a>예제  
 또한 이 상황을 반대로 적용할 수도 있습니다. `Customer` 클래스를 사용하여 고객과 주문 간의 연결을 설명하는 대신에 `Order` 클래스를 사용할 수 있습니다. 다음 코드 예제와 같이 `Order` 클래스는 <xref:System.Data.Linq.EntityRef%601> 형식을 사용하여 고객에 대한 관계를 설명합니다.  
  
> [!NOTE]
> 클래스 <xref:System.Data.Linq.EntityRef%601> 는 *지연 된 로드*를 지원 합니다. 자세한 내용은 [지연 된 로드 및 즉시 로드](deferred-versus-immediate-loading.md)를 *참조 하세요* .  
  
 [!code-csharp[DLinqCustomize#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#5)]
 [!code-vb[DLinqCustomize#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>참고자료

- [방법: 코드 편집기를 사용 하 여 엔터티 클래스 사용자 지정](how-to-customize-entity-classes-by-using-the-code-editor.md)
- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
