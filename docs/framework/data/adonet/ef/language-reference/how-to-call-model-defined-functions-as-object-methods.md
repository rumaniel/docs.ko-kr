---
title: '방법: 개체 메서드로 모델 정의 함수 호출'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33bae8a8-4ed8-4a1f-85d1-c62ff288cc61
ms.openlocfilehash: 787ead2c52f874af2ca1a02bf009da40cee875ae
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250764"
---
# <a name="how-to-call-model-defined-functions-as-object-methods"></a>방법: 개체 메서드로 모델 정의 함수 호출
이 항목에서는 모델 정의 함수를 <xref:System.Data.Objects.ObjectContext> 개체의 메서드 또는 사용자 지정 클래스의 정적 메서드로 호출하는 방법에 대해 설명합니다. *모델 정의 함수* 는 개념적 모델에 정의 된 함수입니다. 이 항목의 절차에서는 이러한 함수를 LINQ to Entities 쿼리에서 호출하는 대신 직접 호출하는 방법에 대해 설명합니다. LINQ to Entities 쿼리에서 모델 정의 함수를 [호출 하는 방법에 대 한 자세한 내용은 방법: 쿼리에서](how-to-call-model-defined-functions-in-queries.md)모델 정의 함수를 호출 합니다.  
  
 모델 정의 함수를 <xref:System.Data.Objects.ObjectContext> 메서드 또는 사용자 지정 클래스의 정적 메서드로 호출하려면 먼저 메서드를 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>가 있는 모델 정의 함수로 매핑해야 합니다. 그러나 <xref:System.Data.Objects.ObjectContext> 클래스의 메서드를 정의하는 경우에는 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 속성을 사용하여 LINQ 공급자를 노출해야 하고, 사용자 지정 클래스의 정적 메서드를 정의하는 경우에는 <xref:System.Linq.IQueryable.Provider%2A> 속성을 사용하여 LINQ 공급자를 노출해야 합니다. 자세한 내용은 다음 절차 아래에 나오는 예제를 참조하세요.  
  
 다음 절차에서는 모델 정의 함수를 <xref:System.Data.Objects.ObjectContext> 개체의 메서드 및 사용자 지정 클래스의 정적 메서드로 호출하는 방법에 대해 간단히 설명합니다. 절차 다음에 나오는 예제에서는 절차의 단계를 보다 자세히 설명합니다. 이러한 절차에서는 사용자가 개념적 모델에서 함수를 정의했다고 가정합니다. 자세한 내용은 [방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다.  
  
### <a name="to-call-a-model-defined-function-as-a-method-on-an-objectcontext-object"></a>모델 정의 함수를 ObjectContext 개체의 메서드로 호출하려면  
  
1. Entity Framework 도구에 의해 자동으로 생성된 <xref:System.Data.Objects.ObjectContext> 클래스에서 파생되는 partial 클래스를 확장하기 위해 소스 파일을 추가합니다. CLR 스텁을 별도의 소스 파일에서 정의하면 파일을 다시 생성할 때 변경 내용이 손실되지 않습니다.  
  
2. 다음 작업을 수행하는 <xref:System.Data.Objects.ObjectContext> 클래스에 CLR(공용 언어 런타임) 메서드를 추가합니다.  
  
    - 개념적 모델에 정의된 함수로 매핑합니다. 메서드를 매핑하려면 메서드에 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>를 적용해야 합니다. 특성의 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 매개 변수는 개념적 모델의 네임스페이스 이름이고, 특성의 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 매개 변수는 개념적 모델의 함수 이름입니다. LINQ에서 함수 이름을 확인할 때는 대/소문자가 구분됩니다.  
  
    - <xref:System.Linq.IQueryProvider.Execute%2A> 속성에 의해 반환된 <xref:System.Data.Objects.ObjectContext.QueryProvider%2A> 메서드의 결과를 반환합니다.  
  
3. 메서드를 <xref:System.Data.Objects.ObjectContext> 클래스 인스턴스의 멤버로 호출합니다.  
  
### <a name="to-call-a-model-defined-function-as-static-method-on-a-custom-class"></a>모델 정의 함수를 사용자 지정 클래스의 정적 메서드로 호출하려면  
  
1. 다음 작업을 수행하는 정적 메서드가 포함된 애플리케이션에 클래스를 추가합니다.  
  
    - 개념적 모델에 정의된 함수로 매핑합니다. 메서드를 매핑하려면 메서드에 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute>를 적용해야 합니다. 특성의 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.NamespaceName%2A> 매개 변수는 개념적 모델의 네임스페이스 이름이고, 특성의 <xref:System.Data.Objects.DataClasses.EdmFunctionAttribute.FunctionName%2A> 매개 변수는 개념적 모델의 함수 이름입니다.  
  
    - <xref:System.Linq.IQueryable> 인수를 받아들입니다.  
  
    - <xref:System.Linq.IQueryProvider.Execute%2A> 속성에 의해 반환된 <xref:System.Linq.IQueryable.Provider%2A> 메서드의 결과를 반환합니다.  
  
2. 메서드를 사용자 지정 클래스의 정적 메서드 멤버로 호출합니다.  
  
## <a name="example"></a>예제  
 **모델 정의 함수를 ObjectContext 개체의 메서드로 호출**  
  
 다음 예제에서는 모델 정의 함수를 <xref:System.Data.Objects.ObjectContext> 개체의 메서드로 호출하는 방법에 대해 설명합니다. 이 예에서는 [AdventureWorks Sales 모델](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)을 사용 합니다.  
  
 지정된 제품의 제품 수익을 반환하는 다음 개념적 모델 함수를 살펴보세요. (개념적 모델 [에 함수를 추가 하는 방법에 대 한 자세한 내용은 방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다.  
  
 [!code-xml[DP L2E Methods on ObjectContext#4](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#4)]  

## <a name="example"></a>예제  
 다음 코드에서는 위의 개념적 모델 함수로 매핑되는 `AdventureWorksEntities` 클래스에 메서드를 추가합니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#2)]
 [!code-vb[DP L2E Methods on ObjectContext#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#2)]  
  
## <a name="example"></a>예제  
 다음 코드에서는 위의 메서드를 호출하여 지정된 제품의 제품 수익을 표시합니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#3)]
 [!code-vb[DP L2E Methods on ObjectContext#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#3)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 컬렉션을 반환하는 모델 정의 함수를 <xref:System.Linq.IQueryable%601> 개체로 호출하는 방법에 대해 설명합니다. 제공된 제품 ID의 모든 `SalesOrderDetails`를 반환하는 다음 개념적 모델 함수를 살펴보세요.  
  
 [!code-xml[DP L2E Methods on ObjectContext#7](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#7)]  
  
## <a name="example"></a>예제  
 다음 코드에서는 위의 개념적 모델 함수로 매핑되는 `AdventureWorksEntities` 클래스에 메서드를 추가합니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#8)]
 [!code-vb[DP L2E Methods on ObjectContext#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#8)]  
  
## <a name="example"></a>예제  
 다음 코드에서는 메서드를 호출합니다. 반환된 <xref:System.Linq.IQueryable%601> 쿼리는 각 `SalesOrderDetail`의 품목 합계를 반환하도록 보다 구체화됩니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#9)]
 [!code-vb[DP L2E Methods on ObjectContext#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#9)]  
  
## <a name="example"></a>예제  
 **모델 정의 함수를 사용자 지정 클래스의 정적 메서드로 호출**  
  
 다음 예제에서는 모델 정의 함수를 사용자 지정 클래스의 정적 메서드로 호출하는 방법에 대해 설명합니다. 이 예에서는 [AdventureWorks Sales 모델](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)을 사용 합니다.  
  
> [!NOTE]
> 모델 정의 함수를 사용자 지정 클래스의 정적 메서드로 호출할 때 모델 정의 함수는 컬렉션을 받아들이고 컬렉션의 값 집계를 반환해야 합니다.  
  
 SalesOrderDetail 컬렉션의 제품 수익을 반환하는 다음 개념적 모델 함수를 살펴보세요. (개념적 모델 [에 함수를 추가 하는 방법에 대 한 자세한 내용은 방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다.  
  
 [!code-xml[DP L2E Methods on ObjectContext#1](../../../../../../samples/snippets/xml/VS_Snippets_Data/dp l2e methods on objectcontext/xml/adventureworks.edmx#1)]
  
## <a name="example"></a>예제  
 다음 코드에서는 위의 개념적 모델 함수로 매핑되는 정적 메서드가 포함된 애플리케이션에 클래스를 추가합니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#5)]
 [!code-vb[DP L2E Methods on ObjectContext#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/class1.vb#5)]  
  
## <a name="example"></a>예제  
 다음 코드에서는 위의 메서드를 호출하여 SalesOrderDetail 컬렉션의 제품 수익을 표시합니다.  
  
 [!code-csharp[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e methods on objectcontext/cs/program.cs#6)]
 [!code-vb[DP L2E Methods on ObjectContext#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e methods on objectcontext/vb/module1.vb#6)]  
  
## <a name="see-also"></a>참고자료

- [.edmx 파일 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))
- [LINQ to Entities에서 쿼리](queries-in-linq-to-entities.md)
- [LINQ to Entities 쿼리에서 함수 호출](calling-functions-in-linq-to-entities-queries.md)
