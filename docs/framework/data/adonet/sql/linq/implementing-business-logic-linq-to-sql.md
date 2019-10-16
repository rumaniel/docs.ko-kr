---
title: 비즈니스 논리 구현(LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c4577590-7b12-42e1-84a6-95aa2562727e
ms.openlocfilehash: 5261aab1ef6641651f856b8ebb024f64ad32ee59
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781433"
---
# <a name="implementing-business-logic-linq-to-sql"></a>비즈니스 논리 구현(LINQ to SQL)
이 항목에서 "비즈니스 논리"는 데이터베이스에서 데이터를 삽입, 업데이트 또는 삭제하기 전에 데이터에 적용하는 모든 사용자 지정 규칙 또는 유효성 검사 테스트를 의미합니다. 비즈니스 논리를 "비즈니스 규칙" 또는 "도메인 논리"라고도 합니다. N 계층 애플리케이션의 경우 비즈니스 논리는 일반적으로 프레젠테이션 계층이나 데이터 액세스 계층과 독립적으로 수정될 수 있도록 논리 계층으로 디자인됩니다. 비즈니스 논리는 데이터베이스 데이터의 업데이트, 삽입 또는 삭제 전과 후에 데이터 액세스 계층에서 호출될 수 있습니다.  
  
 비즈니스 논리는 필드의 형식이 테이블 열의 형식과 호환되는지 확인하는 스키마 유효성 검사처럼 간단한 논리부터 훨씬 더 복잡한 방식으로 상호 작용하는 개체의 집합으로 구성된 논리까지 매우 다양합니다. 규칙은 데이터베이스에 저장 프로시저로 구현되거나 메모리 내 개체로 구현될 수 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하면 비즈니스 논리가 어떻게 구현되었는지에 관계없이 부분 클래스와 부분 메서드(Partial Method)를 사용하여 비즈니스 논리와 데이터 액세스 코드를 분리할 수 있습니다.  
  
## <a name="how-linq-to-sql-invokes-your-business-logic"></a>LINQ to SQL로 비즈니스 논리를 호출하는 방법  
 디자인 타임에 수동으로 또는 개체 관계형 디자이너 또는 SQLMetal을 사용 하 여 엔터티 클래스를 생성 하는 경우 partial 클래스로 정의 됩니다. 즉, 별도의 코드 파일에서 사용자 지정 비즈니스 논리가 포함된 엔터티 클래스의 다른 부분을 사용자가 정의할 수 있습니다. 컴파일할 때 이 두 부분은 하나의 클래스로 병합됩니다. 그러나 개체 관계형 디자이너 또는 SQLMetal을 사용 하 여 엔터티 클래스를 다시 생성 해야 하는 경우에는이 작업을 수행할 수 있습니다. 그러면 클래스의 일부가 수정 되지 않습니다.  
  
 엔터티와 <xref:System.Data.Linq.DataContext>를 정의하는 부분 클래스에는 부분 메서드가 포함됩니다. 부분 메서드는 엔터티 또는 엔터티 속성을 업데이트, 삽입 또는 삭제하기 전과 후에 비즈니스 논리를 적용하는 데 사용할 수 있는 확장성 지점입니다. 부분 메서드는 컴파일 시간 이벤트 정도로 생각할 수 있습니다. 코드 생성기에서는 메서드 시그니처를 정의하고 `DataContext` 생성자인 get/set 속성 접근자에서 메서드를 호출하며 경우에 따라 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 호출되면 메서드를 내부적으로 호출합니다. 그러나 특정 부분 메서드를 구현하지 않으면 컴파일할 때 관련된 모든 참조 및 정의가 제거됩니다.  
  
 별도의 코드 파일에 작성하는 구현 정의에는 필요한 모든 사용자 지정 논리를 수행할 수 있습니다. 부분 클래스 자체를 도메인 계층으로 사용하거나 부분 메서드의 구현 정의에서 별도의 개체로 호출할 수 있습니다. 어느 방법을 사용하든 비즈니스 논리는 데이터 액세스 코드 및 프레젠테이션 계층 코드에서 완벽하게 분리됩니다.  
  
## <a name="a-closer-look-at-the-extensibility-points"></a>확장성 지점 자세히 보기  
 다음 예제에서는 두 개의 `DataContext` `Customers` 테이블 및 `Orders`를 포함 하는 클래스에 대 한 개체 관계형 디자이너에 의해 생성 된 코드의 일부를 보여 줍니다. 이 코드에서는 클래스의 각 테이블에 대해 Insert, Update 및 Delete 메서드를 정의합니다.  
  
```vb  
Partial Public Class Northwnd  
    Inherits System.Data.Linq.DataContext  
  
    Private Shared mappingSource As _  
        System.Data.Linq.Mapping.MappingSource = New _  
        AttributeMappingSource  
  
    #Region "Extensibility Method Definitions"  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub InsertCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub UpdateCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub DeleteCustomer(instance As Customer)  
    End Sub  
    Partial Private Sub InsertOrder(instance As [Order])  
    End Sub  
    Partial Private Sub UpdateOrder(instance As [Order])  
    End Sub  
    Partial Private Sub DeleteOrder(instance As [Order])  
    End Sub  
    #End Region  
```  
  
```csharp  
public partial class MyNorthWindDataContext : System.Data.Linq.DataContext  
    {  
        private static System.Data.Linq.Mapping.MappingSource mappingSource = new AttributeMappingSource();  
  
        #region Extensibility Method Definitions  
        partial void OnCreated();  
        partial void InsertCustomer(Customer instance);  
        partial void UpdateCustomer(Customer instance);  
        partial void DeleteCustomer(Customer instance);  
        partial void InsertOrder(Order instance);  
        partial void UpdateOrder(Order instance);  
        partial void DeleteOrder(Order instance);  
        #endregion  
```  
  
 부분 클래스에 Insert, Update 및 Delete 메서드를 구현할 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 런타임에서는 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 호출되면 기본 메서드 대신 사용자가 구현한 메서드를 호출합니다. 이렇게 하면 만들기, 읽기, 업데이트 및 삭제 작업의 기본 동작을 재정의할 수 있습니다. 자세한 내용은 [연습: 엔터티 클래스](/visualstudio/data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes)의 삽입, 업데이트 및 삭제 동작을 사용자 지정 합니다.  
  
 `OnCreated` 메서드는 클래스 생성자에서 호출됩니다.  
  
```vb  
Public Sub New(ByVal connection As String)  
    MyBase.New(connection, mappingSource)  
    OnCreated()  
End Sub  
```  
  
```csharp  
public MyNorthWindDataContext(string connection) :  
            base(connection, mappingSource)  
        {  
            OnCreated();  
        }  
```  
  
 엔터티 클래스에는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]가 호출되면 엔터티가 생성되고 로드되고 유효성이 검사될 때 `SubmitChanges` 런타임에서 호출하는 세 개의 메서드가 있습니다. 또한 엔터티 클래스에는 각 속성에 대해 두 개의 부분 메서드, 즉 속성을 설정하기 전에 호출되는 부분 메서드와 속성을 설정한 후에 호출되는 부분 메서드가 있습니다. 다음 코드 예제에서는 `Customer` 클래스에 대해 생성되는 몇 가지 메서드를 보여 줍니다.  
  
```vb  
#Region "Extensibility Method Definitions"  
    Partial Private Sub OnLoaded()  
    End Sub  
    Partial Private Sub OnValidate(action As _  
        System.Data.Linq.ChangeAction)  
    End Sub  
    Partial Private Sub OnCreated()  
    End Sub  
    Partial Private Sub OnCustomerIDChanging(value As String)  
    End Sub  
    Partial Private Sub OnCustomerIDChanged()  
    End Sub  
    Partial Private Sub OnCompanyNameChanging(value As String)  
    End Sub  
    Partial Private Sub OnCompanyNameChanged()  
    End Sub  
' ...Additional Changing/Changed methods for each property.  
```  
  
```csharp  
#region Extensibility Method Definitions  
    partial void OnLoaded();  
    partial void OnValidate();  
    partial void OnCreated();  
    partial void OnCustomerIDChanging(string value);  
    partial void OnCustomerIDChanged();  
    partial void OnCompanyNameChanging(string value);  
    partial void OnCompanyNameChanged();  
// ...additional Changing/Changed methods for each property  
```  
  
 `CustomerID` 속성에 대한 다음 예제에서 볼 수 있는 것처럼 이러한 메서드는 set 속성 접근자에서 호출됩니다.  
  
```vb  
Public Property CustomerID() As String  
    Set  
        If (String.Equals(Me._CustomerID, value) = False) Then  
            Me.OnCustomerIDChanging(value)  
            Me.SendPropertyChanging()  
            Me._CustomerID = value  
            Me.SendPropertyChanged("CustomerID")  
            Me.OnCustomerIDChanged()  
        End If  
    End Set  
End Property  
```  
  
```csharp  
public string CustomerID  
{  
    set  
    {  
        if ((this._CustomerID != value))  
        {  
            this.OnCustomerIDChanging(value);  
            this.SendPropertyChanging();  
            this._CustomerID = value;  
            this.SendPropertyChanged("CustomerID");  
            this.OnCustomerIDChanged();  
        }  
     }  
}  
```  
  
 사용자가 작성하는 클래스 부분에 메서드의 구현 정의를 작성할 수 있습니다. Visual Studio에서를 입력 `partial` 하면 클래스의 다른 부분에 있는 메서드 정의에 대 한 IntelliSense가 표시 됩니다.  
  
```vb  
Partial Public Class Customer  
    Private Sub OnCustomerIDChanging(value As String)  
        ' Perform custom validation logic here.  
    End Sub  
End Class  
```  
  
```csharp  
partial class Customer   
    {  
        partial void OnCustomerIDChanging(string value)  
        {  
            //Perform custom validation logic here.  
        }  
    }  
```  
  
 부분 메서드를 사용하여 애플리케이션에 비즈니스 논리를 추가하는 방법에 대한 자세한 내용을 보려면 다음 항목을 참조하세요.  
  
 [방법: 엔터티 클래스에 유효성 검사 추가](/visualstudio/data-tools/how-to-add-validation-to-entity-classes)  
  
 [연습: 엔터티 클래스의 삽입, 업데이트 및 삭제 동작 사용자 지정](/visualstudio/data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes)  
  
 [연습: 엔터티 클래스에 유효성 검사 추가](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/bb629301(v=vs.120))  
  
## <a name="see-also"></a>참고자료

- [Partial 클래스 및 메서드](../../../../../csharp/programming-guide/classes-and-structs/partial-classes-and-methods.md)
- [부분 메서드](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)
- [LINQ to SQL Tools in Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)(Visual Studio의 LINQ to SQL 도구)
- [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
