---
title: 단일 클래스 쿼리(LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0b74bcf8-3f87-449f-bff7-6bcb0d69d212
ms.openlocfilehash: 8807125bd61c71217ca96f3b5a38148ed100073b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794367"
---
# <a name="single-table-queries-linq-to-dataset"></a>단일 클래스 쿼리(LINQ to DataSet)
[!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 쿼리를 구현 하는 데이터 소스에서 작동 합니다 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스 또는 <xref:System.Linq.IQueryable%601> 인터페이스입니다. <xref:System.Data.DataTable> 클래스에는 두 인터페이스가 구현되어 있지 않으므로 <xref:System.Data.DataTableExtensions.AsEnumerable%2A> 쿼리의 <xref:System.Data.DataTable> 절에서 `From`을 소스로 사용하려면 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 메서드를 호출해야 합니다.  
  
 다음 예제에서는 SalesOrderHeader 테이블에서 모든 온라인 주문을 가져와서 주문 ID, 주문 날짜 및 주문 번호를 콘솔에 출력합니다.  
  
 [!code-csharp[DP LINQ to DataSet Examples#Where1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#where1)]  
 [!code-vb[DP LINQ to DataSet Examples#Where1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#where1)] 
  
 지역 변수 쿼리는 표준 쿼리 연산자에서 하나 이상의 쿼리 연산자를 적용 하 여 하나 이상의 정보 소스에 대해 작동 하는 쿼리 식으로 초기화 됩니다 .이 경우에는 <xref:System.Data.DataSet>LINQtoDataSet의경우클래스. 이전 예제의 쿼리 식에서는 두 개의 표준 쿼리 연산자인 `Where`와 `Select`를 사용합니다.  
  
 `Where` 절에서는 조건을 기준으로 시퀀스를 필터링하며, 이 경우에는 `OnlineOrderFlag`가 `true`로 설정됩니다. `Select` 연산자는 연산자로 전달된 인수를 캡처하는 열거 가능한 개체를 할당하고 반환합니다. 위 예제에서는 세 개의 `SalesOrderID`, `OrderDate` 및 `SalesOrderNumber` 속성을 가진 익명 형식이 만들어집니다. 이러한 세 속성의 값은 `SalesOrderID` 테이블에 있는 `OrderDate`, `SalesOrderNumber` 및 `SalesOrderHeader` 열의 값으로 설정됩니다.  
  
 그런 다음 `foreach` 루프에서는 `Select`에서 반환된 열거 가능한 개체를 열거하고 쿼리 결과를 생성합니다. 쿼리는 <xref:System.Linq.Enumerable>을 구현하는 <xref:System.Collections.Generic.IEnumerable%601> 형식이므로 `foreach` 루프를 사용하는 동안 쿼리 변수가 반복될 때까지 쿼리에 대한 계산이 지연됩니다. 쿼리 계산이 지연되면 여러 차례 계산할 수 있으면서 계산할 때마다 다른 결과가 나올 수 있는 값으로 쿼리를 유지할 수 있습니다.  
  
 <xref:System.Data.DataRowExtensions.Field%2A> 메서드는 <xref:System.Data.DataRow>의 열 값에 대한 액세스를 제공하며 이전 예제에서 나오지 않은 <xref:System.Data.DataRowExtensions.SetField%2A>는 <xref:System.Data.DataRow>의 열 값을 설정합니다. <xref:System.Data.DataRowExtensions.Field%2A> 메서드와 <xref:System.Data.DataRowExtensions.SetField%2A> 메서드에서는 nullable 형식이 처리되므로 명시적으로 null 값을 검사하지 않아도 됩니다. 또한 두 메서드 모두 제네릭 메서드이므로 반환 형식을 캐스팅하지 않아도 됩니다. <xref:System.Data.DataRow>의 기존 열 접근자(예: `o["OrderDate"]`)를 사용할 수도 있지만 그렇게 하려면 반환 개체를 적절한 형식으로 캐스팅해야 합니다.  열이 nullable인 경우에는 <xref:System.Data.DataRow.IsNull%2A> 메서드를 사용하여 값이 null인지 확인해야 합니다. 자세한 내용은 [제네릭 Field 및 SetField 메서드](generic-field-and-setfield-methods-linq-to-dataset.md)합니다.  
  
 `T` 메서드 및 <xref:System.Data.DataRowExtensions.Field%2A> 메서드의 제네릭 매개 변수 <xref:System.Data.DataRowExtensions.SetField%2A>에 지정된 데이터 형식은 내부 값의 형식과 일치해야 하며, 그렇지 않으면 <xref:System.InvalidCastException>이 throw됩니다. 지정된 열 이름도 <xref:System.Data.DataSet>의 열 이름과 일치해야 하며, 그렇지 않으면 <xref:System.ArgumentException>이 throw됩니다. 두 경우 모두 쿼리가 실행되는 런타임에 데이터 열거형에서 예외가 throw됩니다.  
  
## <a name="see-also"></a>참고자료

- [크로스 테이블 쿼리](cross-table-queries-linq-to-dataset.md)
- [형식화된 데이터 집합 쿼리](querying-typed-datasets.md)
- [제네릭 Field 및 SetField 메서드](generic-field-and-setfield-methods-linq-to-dataset.md)
