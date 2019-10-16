---
title: N 계층 애플리케이션에서 데이터 검색 및 CUD 작업(LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c3133d53-83ed-4a4d-af8b-82edcf3831db
ms.openlocfilehash: 706dbda98d0e1674b76ebc6a25c7a34746720ea2
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247359"
---
# <a name="data-retrieval-and-cud-operations-in-n-tier-applications-linq-to-sql"></a>N 계층 애플리케이션에서 데이터 검색 및 CUD 작업(LINQ to SQL)
Customers 또는 Orders와 같은 엔터티 개체를 네트워크상의 클라이언트로 serialize하면 해당 엔터티가 원래 데이터 컨텍스트에서 분리됩니다. 데이터 컨텍스트에서는 분리된 엔터티 개체에 대해서는 변경 내용이나 다른 개체와의 관계를 더 이상 추적하지 않습니다. 이러한 특징은 클라이언트에서 데이터를 읽기만 하는 경우에는 문제가 되지 않습니다. 또한 클라이언트가 데이터베이스에 새 행을 추가할 수 있게 하는 것도 비교적 간단합니다. 그러나 애플리케이션에서 클라이언트가 데이터를 업데이트하거나 삭제해야 하는 경우에는 <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>를 호출하기 전에 새 데이터 컨텍스트에 엔터티를 연결해야 합니다. 또한 원래 값을 기준으로 낙관적 동시성 검사를 사용하는 경우에는 어떤 방법으로든 데이터베이스에 원래 엔터티와 수정된 엔터티를 모두 제공해야 합니다. `Attach` 메서드는 분리된 엔터티를 새 데이터 컨텍스트에 연결하기 위해 제공됩니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 엔터티 대신 프록시 개체를 serialize하는 경우에도 데이터베이스에 데이터를 전송하려면 DAL(데이터 액세스 계층)에서 엔터티를 만들어 새 <xref:System.Data.Linq.DataContext?displayProperty=nameWithType>에 연결해야 합니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 엔터티가 serialize되는 방법은 고려하지 않습니다. 개체 관계형 디자이너 및 SQLMetal 도구를 사용 하 여 WCF (Windows Communication Foundation) [를 사용 하 여 serialize 할 수 있는 클래스를 생성 하는 방법에 대 한 자세한 내용은 방법: 엔터티를 Serialize](how-to-make-entities-serializable.md)가능 하 게 만듭니다.  
  
> [!NOTE]
> `Attach` 메서드는 새 엔터티 또는 deserialize된 엔터티에 대해서만 호출해야 합니다. 엔터티는 serialization을 통해서만 원래 데이터 컨텍스트로부터 분리될 수 있습니다. 이전 데이터 컨텍스트에서 지연 로더가 있는 분리되지 않은 엔터티를 새 데이터 컨텍스트에 연결하려고 하면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 예외를 throw합니다. 서로 다른 두 데이터 컨텍스트의 지연 로더가 있는 엔터티에 대해 삽입, 업데이트 및 삭제 작업을 수행하면 예기치 않은 결과가 발생할 수 있습니다. 지연 된 로더는 지연 된 로더에 대 한 자세한 내용은 [지연 된 로드 및 즉시 로드](deferred-versus-immediate-loading.md)를 참조 하세요.  
  
## <a name="retrieving-data"></a>데이터 검색  
  
### <a name="client-method-call"></a>클라이언트 메서드 호출  
 다음 예제에서는 Windows Forms 클라이언트에서 DAL에 대해 호출하는 샘플 메서드를 보여 줍니다. 이 예제에서 DAL은 Windows 서비스 라이브러리로 구현됩니다.  
  
```vb  
Private Function GetProdsByCat_Click(ByVal sender As Object, ByVal e _  
    As EventArgs)  
  
    ' Create the WCF client proxy.  
    Dim proxy As New NorthwindServiceReference.Service1Client  
  
    ' Call the method on the service.  
    Dim products As NorthwindServiceReference.Product() = _  
        proxy.GetProductsByCategory(1)  
  
    ' If the database uses original values for concurrency checks,  
    ' the client needs to store them and pass them back to the  
    ' middle tier along with the new values when updating data.  
  
    For Each v As NorthwindClient1.NorthwindServiceReference.Product _  
        In products  
        ' Persist to a List(Of Product) declared at class scope.  
        ' Additional change-tracking logic is the responsibility  
        ' of the presentation tier and/or middle tier.  
        originalProducts.Add(v)  
    Next  
  
    ' (Not shown) Bind the products list to a control  
    ' and/or perform whatever processing is necessary.  
End Function  
```  
  
```csharp  
private void GetProdsByCat_Click(object sender, EventArgs e)  
{  
    // Create the WCF client proxy.  
    NorthwindServiceReference.Service1Client proxy =   
    new NorthwindClient.NorthwindServiceReference.Service1Client();  
  
    // Call the method on the service.  
    NorthwindServiceReference.Product[] products =   
    proxy.GetProductsByCategory(1);  
  
    // If the database uses original values for concurrency checks,   
    // the client needs to store them and pass them back to the   
    // middle tier along with the new values when updating data.  
    foreach (var v in products)  
    {  
        // Persist to a list<Product> declared at class scope.  
        // Additional change-tracking logic is the responsibility  
        // of the presentation tier and/or middle tier.  
        originalProducts.Add(v);  
    }  
  
    // (Not shown) Bind the products list to a control  
    // and/or perform whatever processing is necessary.  
    }  
```  
  
### <a name="middle-tier-implementation"></a>중간 계층 구현  
 다음 예제에서는 중간 계층에서 구현하는 인터페이스 메서드를 보여 줍니다. 다음 두 가지 주요 사항을 고려하세요.  
  
- <xref:System.Data.Linq.DataContext>는 메서드 범위에서 선언됩니다.  
  
- 메서드는 실제 결과의 <xref:System.Collections.IEnumerable> 컬렉션을 반환합니다. serializer는 쿼리를 실행하여 클라이언트/프레젠테이션 계층에 결과를 다시 보냅니다. 중간 계층에서 쿼리 결과에 로컬로 액세스하려면 쿼리 변수에 대해 `ToList` 또는 `ToArray`를 호출하여 메서드를 강제로 실행한 후 해당 목록 또는 배열을 `IEnumerable`로 반환할 수 있습니다.  
  
```vb  
Public Function GetProductsByCategory(ByVal categoryID As Integer) _  
    As IEnumerable(Of Product)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    Dim productQuery = _  
    From prod In db.Products _  
    Where prod.CategoryID = categoryID _  
    Select prod  
  
    Return productQuery.AsEnumerable()  
  
End Function  
```  
  
```csharp  
public IEnumerable<Product> GetProductsByCategory(int categoryID)  
{  
    NorthwindClasses1DataContext db =   
    new NorthwindClasses1DataContext(connectionString);  
  
    IEnumerable<Product> productQuery =  
    from prod in db.Products  
    where prod.CategoryID == categoryID  
    select prod;  
  
    return productQuery.AsEnumerable();   
}  
```  
  
 데이터 컨텍스트 인스턴스는 하나의 "작업 단위" 동안 유지되어야 합니다. 느슨하게 결합된 환경의 경우 작업 단위는 `SubmitChanges`에 대한 호출 하나가 포함된 낙관적 트랜잭션과 같이 일반적으로 크기가 작습니다. 이 때문에 데이터 컨텍스트는 메서드 범위에서 만들어지고 삭제됩니다. 작업 단위에 비즈니스 규칙 논리에 대한 호출이 포함된 경우에는 해당 작업 전체 동안 `DataContext` 인스턴스를 유지할 수 있습니다. 어떤 경우든 `DataContext` 인스턴스는 임의 개수의 트랜잭션에서 장기간 유지할 수 없습니다.  
  
 이 메서드는 Product 개체를 반환하고, 각 Product에 연결된 Order_Detail 개체의 컬렉션은 반환하지 않습니다. <xref:System.Data.Linq.DataLoadOptions> 개체를 사용하면 이 기본 동작을 변경할 수 있습니다. 자세한 내용은 [방법: 검색](how-to-control-how-much-related-data-is-retrieved.md)되는 관련 데이터의 양을 제어 합니다.  
  
## <a name="inserting-data"></a>데이터 삽입  
 새 개체를 삽입할 경우 프레젠테이션 계층에서는 중간 계층 인터페이스에서 관련 메서드를 호출하여 삽입할 새 개체를 전달합니다. 경우에 따라서는 클라이언트가 일부 값만 전달하고 중간 계층에서 개체를 직접 만들도록 하는 것이 더 효율적일 수 있습니다.  
  
### <a name="middle-tier-implementation"></a>중간 계층 구현  
 <xref:System.Data.Linq.DataContext>가 호출되면 중간 계층에서는 새 <xref:System.Data.Linq.DataContext>를 만들고 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> 메서드를 사용하여 개체를 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>에 연결한 후 개체를 삽입합니다. 예외, 콜백 및 오류 조건은 다른 모든 웹 서비스 시나리오에서와 동일한 방법으로 처리할 수 있습니다.  
  
```vb  
' No call to Attach is necessary for inserts.  
Public Sub InsertOrder(ByVal o As Order)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    db.Orders.InsertOnSubmit(o)  
  
    ' Exception handling not shown.  
    db.SubmitChanges()  
  
End Sub  
```  
  
```csharp  
// No call to Attach is necessary for inserts.  
    public void InsertOrder(Order o)  
    {  
        NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
        db.Orders.InsertOnSubmit(o);  
  
        // Exception handling not shown.  
        db.SubmitChanges();  
    }  
```  
  
## <a name="deleting-data"></a>데이터 삭제  
 데이터베이스에서 기존 개체를 삭제할 경우 프레젠테이션 계층에서는 중간 계층 인터페이스에서 관련 메서드를 호출하고, 삭제할 개체의 원래 값이 포함된 복사본을 전달합니다.  
  
 삭제 작업에는 낙관적 동시성 검사가 사용되기 때문에 삭제할 개체를 새 데이터 컨텍스트에 먼저 연결해야 합니다. 이 예제에서는 `Boolean` 매개 변수를 `false`로 설정하여 개체에 타임스탬프(RowVersion)가 없음을 나타냅니다. 그러나 데이터베이스 테이블에서 각 레코드에 대해 타임스탬프를 생성하는 경우 클라이언트측에서는 동시성 검사가 훨씬 간단해집니다. 즉, 원래 개체 또는 수정된 개체 중 하나를 전달하고 `Boolean` 매개 변수를 `true`로 설정하기만 하면 됩니다. 그러나 어떤 경우든 중간 계층에서는 일반적으로 <xref:System.Data.Linq.ChangeConflictException>을 catch해야 합니다. 낙관적 동시성 충돌 [을 처리 하는 방법에 대 한 자세한 내용은 낙관적 동시성: 개요](optimistic-concurrency-overview.md).  
  
 연결된 테이블에 외래 키 제약 조건이 있는 엔터티를 삭제할 경우에는 해당 <xref:System.Data.Linq.EntitySet%601> 컬렉션에 있는 모든 개체를 먼저 삭제해야 합니다.  
  
```vb  
' Attach is necessary for deletes.  
Public Sub DeleteOrder(ByVal order As Order)  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
  
    db.Orders.Attach(order, False)  
    ' This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order)  
  
    Try  
        ' ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict)  
  
    Catch ex As ChangeConflictException  
        ' Get conflict information, and take actions  
        ' that are appropriate for your application.  
        ' See MSDN Article "How to: Manage Change  
        ' Conflicts (LINQ to SQL).  
  
    End Try  
End Sub  
```  
  
```csharp  
// Attach is necessary for deletes.  
public void DeleteOrder(Order order)  
{  
    NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
  
    db.Orders.Attach(order, false);  
    // This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order);  
    try  
    {  
        // ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict);  
    }  
    catch (ChangeConflictException e)  
    {  
       // Get conflict information, and take actions  
       // that are appropriate for your application.  
       // See MSDN Article How to: Manage Change Conflicts (LINQ to SQL).  
    }  
}  
```  
  
## <a name="updating-data"></a>데이터 업데이트  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 낙관적 동시성이 사용되는 다음과 같은 시나리오에서 업데이트를 지원합니다.  
  
- 타임스탬프 또는 RowVersion 번호를 기반으로 하는 낙관적 동시성  
  
- 엔터티 속성 하위 집합의 원래 값을 기반으로 하는 낙관적 동시성  
  
- 원래 엔터티와 수정된 엔터티 모두를 기반으로 하는 낙관적 동시성  
  
 Customer 및 Customer와 연결된 Order 개체의 컬렉션과 같이 엔터티와 해당 관계에 대해 업데이트나 삭제 작업을 수행할 수도 있습니다. 클라이언트에서 엔터티 개체의 그래프와 해당 자식(`EntitySet`) 컬렉션을 수정할 경우 낙관적 동시성 검사에 원래 값이 필요하면 클라이언트에서는 각 엔터티와 <xref:System.Data.Linq.EntitySet%601> 개체의 원래 값을 제공해야 합니다. 클라이언트에서 한 번의 메서드 호출로 관련된 업데이트, 삭제 및 삽입을 수행하려면 각 엔터티에 대해 수행할 작업 유형을 메서드 안에 지정할 수 있어야 합니다. 그런 다음 <xref:System.Data.Linq.ITable.Attach%2A>를 호출하기 전에 중간 계층에서 적절한 <xref:System.Data.Linq.ITable.InsertOnSubmit%2A> 메서드를 호출한 후 각 엔터티에 대해 <xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A>, <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> 또는 `Attach`(삽입의 경우 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 필요하지 않음)을 호출해야 합니다. 업데이트를 시도하기 전에 원래 값을 가져오기 위한 방법으로 데이터베이스에서 데이터를 검색하지 마세요.  
  
 낙관적 동시성 [에 대 한 자세한 내용은 낙관적 동시성: 개요](optimistic-concurrency-overview.md). 낙관적 동시성 변경 충돌을 [해결 하는 방법에 대 한 자세한 내용은 방법: 변경 충돌](how-to-manage-change-conflicts.md)을 관리 합니다.  
  
 다음 예제에서는 각 시나리오를 보여 줍니다.  
  
### <a name="optimistic-concurrency-with-timestamps"></a>타임스탬프를 사용하는 낙관적 동시성  
  
```vb  
' Assume that "customer" has been sent by client.  
' Attach with "true" to say this is a modified entity  
' and it can be checked for optimistic concurrency  
' because it has a column that is marked with the  
' "RowVersion" attribute.  
  
db.Customers.Attach(customer, True)  
  
Try  
    ' Optional: Specify a ConflictMode value  
    ' in call to SubmitChanges.  
    db.SubmitChanges()  
Catch ex As ChangeConflictException  
    ' Handle conflict based on options provided.  
    ' See MSDN article "How to: Manage Change  
    ' Conflicts (LINQ to SQL)".  
End Try  
```  
  
```csharp  
// Assume that "customer" has been sent by client.  
// Attach with "true" to say this is a modified entity  
// and it can be checked for optimistic concurrency because  
//  it has a column that is marked with "RowVersion" attribute  
db.Customers.Attach(customer, true)  
try  
{  
    // Optional: Specify a ConflictMode value  
    // in call to SubmitChanges.  
    db.SubmitChanges();  
}  
catch(ChangeConflictException e)  
{  
    // Handle conflict based on options provided  
    // See MSDN article How to: Manage Change Conflicts (LINQ to SQL).  
}  
```  
  
### <a name="with-subset-of-original-values"></a>원래 값의 하위 집합을 사용하는 낙관적 동시성  
 이 경우 클라이언트는 serialize된 개체 전체 및 수정될 값을 반환합니다.  
  
```vb  
Public Sub UpdateProductInventory(ByVal p As Product, ByVal _  
    unitsInStock As Short?, ByVal unitsOnOrder As Short?)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        ' p is the original unmodified product  
        ' that was obtained from the database.  
        ' The client kept a copy and returns it now.  
        db.Products.Attach(p, False)  
  
        ' Now that the original values are in the data context,  
        ' apply the changes.  
        p.UnitsInStock = unitsInStock  
        p.UnitsOnOrder = unitsOnOrder  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle conflict based on options provided.  
            ' See MSDN article "How to: Manage Change Conflicts  
            ' (LINQ to SQL)".  
        End Try  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInventory(Product p, short? unitsInStock, short? unitsOnOrder)  
{  
    using (NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString))  
    {  
        // p is the original unmodified product  
        // that was obtained from the database.  
        // The client kept a copy and returns it now.  
        db.Products.Attach(p, false);  
  
        // Now that the original values are in the data context, apply the changes.  
        p.UnitsInStock = unitsInStock;  
        p.UnitsOnOrder = unitsOnOrder;  
        try  
        {  
             // Optional: Specify a ConflictMode value  
             // in call to SubmitChanges.  
             db.SubmitChanges();  
        }  
        catch (ChangeConflictException e)  
        {  
            // Handle conflict based on provided options.  
            // See MSDN article How to: Manage Change Conflicts  
            // (LINQ to SQL).  
        }  
    }  
}  
```  
  
### <a name="with-complete-entities"></a>전체 엔터티를 사용하는 낙관적 동시성  
  
```vb  
Public Sub UpdateProductInfo(ByVal newProd As Product, ByVal _  
    originalProd As Product)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        db.Products.Attach(newProd, originalProd)  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle potential change conflicgt in whatever way  
            ' is appropriate for your application.  
            ' For more information, see the MSDN article  
            ' "How to: Manage Change Conflicts (LINQ to  
            ' SQL)".  
        End Try  
  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInfo(Product newProd, Product originalProd)  
{  
     using (NorthwindClasses1DataContext db = new  
        NorthwindClasses1DataContext(connectionString))  
     {  
         db.Products.Attach(newProd, originalProd);  
         try  
         {  
               // Optional: Specify a ConflictMode value  
               // in call to SubmitChanges.  
               db.SubmitChanges();  
         }  
        catch (ChangeConflictException e)  
        {  
            // Handle potential change conflict in whatever way  
            // is appropriate for your application.  
            // For more information, see the MSDN article  
            // How to: Manage Change Conflicts (LINQ to SQL)/  
        }   
    }  
}  
```  
  
 컬렉션을 업데이트하려면 <xref:System.Data.Linq.ITable.AttachAll%2A> 대신 `Attach`을 호출합니다.  
  
### <a name="expected-entity-members"></a>필요한 엔터티 멤버  
 앞에서 설명한 것처럼 `Attach` 메서드를 호출하기 전에 엔터티 개체의 일부 멤버만 설정해야 합니다. 설정해야 하는 엔터티 멤버는 다음과 같은 조건을 충족해야 합니다.  
  
- 엔터티 ID의 일부여야 합니다.  
  
- 수정될 멤버여야 합니다.  
  
- 타임스탬프이거나 <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> 특성이 `Never` 이외의 값으로 설정되어 있어야 합니다.  
  
 테이블에 낙관적 동시성 검사를 위한 타임스탬프 또는 버전 번호가 사용되는 경우 <xref:System.Data.Linq.ITable.Attach%2A>를 호출하기 전에 이러한 멤버를 설정해야 합니다. 해당 Column 특성에 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> 속성이 true로 설정된 멤버는 낙관적 동시성 검사에 사용됩니다. 데이터베이스에 있는 버전 번호 또는 타임스탬프 값이 동일해야 요청된 업데이트가 제출됩니다.  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>가 `Never`로 설정되지 않은 멤버도 낙관적 동시성 검사에 사용됩니다. 다른 값이 지정되지 않은 경우 기본값은 `Always`입니다.  
  
 이러한 필수 멤버가 하나라도 없으면 <xref:System.Data.Linq.ChangeConflictException>를 호출했을 때 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>("행이 없거나 변경되었습니다.")이 throw됩니다.  
  
### <a name="state"></a>State  
 엔터티 개체를 <xref:System.Data.Linq.DataContext> 인스턴스에 연결하면 개체가 `PossiblyModified` 상태가 됩니다. 다음과 같은 세 가지 방법을 사용하여 연결된 개체를 강제로 `Modified` 상태로 만들 수 있습니다.  
  
1. 개체를 수정되지 않은 상태로 연결한 다음 필드를 직접 수정합니다.  
  
2. 개체의 현재 인스턴스와 원래 인스턴스를 사용하는 <xref:System.Data.Linq.Table%601.Attach%2A> 오버로드와 연결합니다. 이렇게 하면 이전 값과 새 값이 변경 추적기에 제공되므로 변경된 필드를 자동으로 인식할 수 있습니다.  
  
3. true로 설정된 두 번째 부울 매개 변수를 사용하는 <xref:System.Data.Linq.Table%601.Attach%2A> 오버로드와 연결합니다. 이렇게 하면 원래 값을 제공하지 않고도 수정된 개체를 변경 추적기에서 인식할 수 있습니다. 이 방법을 사용하려면 개체에 버전/타임스탬프 필드가 있어야 합니다.  
  
 자세한 내용은 [개체 상태 및 변경 내용 추적](object-states-and-change-tracking.md)을 참조 하세요.  
  
 연결하려는 개체와 ID가 동일한 엔터티 개체가 ID 캐시에 이미 있으면 <xref:System.Data.Linq.DuplicateKeyException>이 throw됩니다.  
  
 개체의 `IEnumerable` 집합과 연결하면 기존 키가 있을 경우 <xref:System.Data.Linq.DuplicateKeyException>이 throw되고 나머지 개체는 연결되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL을 사용한 N 계층 및 원격 응용 프로그램](n-tier-and-remote-applications-with-linq-to-sql.md)
- [배경 정보](background-information.md)
