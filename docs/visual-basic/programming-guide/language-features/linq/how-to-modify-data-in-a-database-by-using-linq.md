---
title: '방법: LINQ (Visual Basic)를 사용 하 여 데이터베이스의 데이터를 수정 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- inserting rows [LINQ to SQL]
- deleting rows [LINQ to SQL]
- updating rows [LINQ to SQL]
- inserting data [Visual Basic]
- deleting data
- data [Visual Basic], updating
- updating data [LINQ]
- queries [LINQ in Visual Basic], data changes in database
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: cf52635f-0c1b-46c3-aff1-bdf181cf19b1
ms.openlocfilehash: 8770a8761af4b55394d9280b21d2a6a5b71b6ed5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61594220"
---
# <a name="how-to-modify-data-in-a-database-by-using-linq-visual-basic"></a>방법: LINQ (Visual Basic)를 사용 하 여 데이터베이스의 데이터를 수정 합니다.
언어 통합 쿼리 (LINQ) 쿼리를 통해 쉽게 데이터베이스 정보에 액세스 하 고 데이터베이스에서 값을 수정 합니다.  
  
 다음 예제에서는 SQL Server 데이터베이스에서 검색 하는 새 응용 프로그램을 만드는 방법 및 업데이트 정보를 보여줍니다.  
  
 이 항목의 예제는 Northwind 샘플 데이터베이스를 사용합니다. 개발 컴퓨터에이 데이터베이스가 없는 경우에 Microsoft 다운로드 센터에서 다운로드할 수 있습니다. 자세한 내용은 [샘플 데이터베이스 다운로드](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)합니다.  
  
### <a name="to-create-a-connection-to-a-database"></a>데이터베이스에 대 한 연결을 만들려면  
  
1. Visual Studio에서 엽니다 **서버 탐색기**/**데이터베이스 탐색기** 를 클릭 하 여 합니다 **보기** 메뉴를 선택한 후 **서버탐색기** / **탐색기 데이터베이스**합니다.  
  
2. 마우스 오른쪽 단추로 클릭 **데이터 연결** 에 **서버 탐색기**/**데이터베이스 탐색기**를 클릭 하 고 **연결 추가**합니다.  
  
3. Northwind 샘플 데이터베이스에 올바른 연결을 지정 합니다.  
  
### <a name="to-add-a-project-with-a-linq-to-sql-file"></a>SQL 파일에는 LINQ 사용 하 여 프로젝트를 추가 하려면  
  
1. Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. Visual basic **Windows Forms 응용 프로그램** 프로젝트 유형으로 합니다.  
  
2. **프로젝트** 메뉴에서 **새 항목 추가**를 클릭합니다. 선택 된 **LINQ to SQL 클래스** 항목 템플릿.  
  
3. 파일 이름을 `northwind.dbml`로 지정합니다. **추가**를 클릭합니다. 개체 관계형 디자이너 (O/R 디자이너)으로 열릴는 `northwind.dbml` 파일입니다.  
  
### <a name="to-add-tables-to-query-and-modify-to-the-designer"></a>쿼리 디자이너를 수정 하는 테이블을 추가 하려면  
  
1. **서버 탐색기**/**데이터베이스 탐색기**, Northwind 데이터베이스에 연결을 확장 합니다. **테이블** 폴더를 확장합니다.  
  
     O/R 디자이너를 닫은 경우 두 번 클릭 하 여 다시 열면를 `northwind.dbml` 파일 앞에 추가 합니다.  
  
2. Customers 테이블을 클릭 하 고 디자이너의 왼쪽된 창에 놓습니다.  
  
     디자이너는 프로젝트에 대 한 새 Customer 개체를 만듭니다.  
  
3. 변경 내용을 저장 하 고 디자이너를 닫습니다.  
  
4. 프로젝트를 저장합니다.  
  
### <a name="to-add-code-to-modify-the-database-and-display-the-results"></a>데이터베이스를 수정 하 고 결과 표시 하는 코드를 추가 하려면  
  
1. **도구 상자**를 끌어를 <xref:System.Windows.Forms.DataGridView> Form1 프로젝트에 대 한 기본 Windows Form 컨트롤입니다.  
  
2. O/R 디자이너에 테이블을 추가한 경우 디자이너 추가 <xref:System.Data.Linq.DataContext> 프로젝트에는 개체입니다. 이 개체는 Customers 테이블에 액세스 하는 데 사용할 수 있는 코드를 포함 합니다. 또한 테이블에 대 한 고객 컬렉션과 로컬 고객 개체를 정의 하는 코드를 포함 합니다. <xref:System.Data.Linq.DataContext> .dbml 파일의 이름에 따라 프로젝트에 대해 개체입니다. 이 프로젝트에는 <xref:System.Data.Linq.DataContext> 개체의 이름은 `northwindDataContext`합니다.  
  
     인스턴스를 만들 수는 <xref:System.Data.Linq.DataContext> 개체를 코드와 쿼리가 및 O/R 디자이너에서 지정 하는 고객 컬렉션을 수정 합니다. 호출 하 여 제출 하기 전에 고객에 게 컬렉션에 수행한 변경 내용을 데이터베이스에 반영 되지 않습니다 합니다 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 메서드는 <xref:System.Data.Linq.DataContext> 개체입니다.  
  
     Windows 폼 Form1 코드를 추가 하려면 두 번 클릭 합니다 <xref:System.Windows.Forms.Form.Load> 이벤트를 쿼리 하는 Customers 테이블의 속성으로 노출 됩니다 프로그램 <xref:System.Data.Linq.DataContext>합니다. 다음 코드를 추가합니다.  
  
    ```vb  
    Private db As northwindDataContext  
  
    Private Sub Form1_Load(ByVal sender As System.Object,   
                           ByVal e As System.EventArgs  
                          ) Handles MyBase.Load  
      db = New northwindDataContext()  
  
      RefreshData()  
    End Sub  
  
    Private Sub RefreshData()  
      Dim customers = From cust In db.Customers   
                      Where cust.City(0) = "W"   
                      Select cust  
  
      DataGridView1.DataSource = customers  
    End Sub  
    ```  
  
3. **도구 상자**, 세 개의 끌어 <xref:System.Windows.Forms.Button> 폼에 컨트롤입니다. 첫 번째 선택 `Button` 제어 합니다. 에 **속성** 창에서 `Name` 의 `Button` 컨트롤을 `AddButton` 및 `Text` 에 `Add`입니다. 두 번째 단추를 선택 하 고 설정 합니다 `Name` 속성을 `UpdateButton` 하며 `Text` 속성을 `Update`입니다. 세 번째 단추를 선택 하 고 설정 합니다 `Name` 속성을 `DeleteButton` 하며 `Text` 속성을 `Delete`입니다.  
  
4. 두 번 클릭 합니다 **추가** 코드를 추가 하는 단추는 `Click` 이벤트입니다. 다음 코드를 추가합니다.  
  
    ```vb  
    Private Sub AddButton_Click(ByVal sender As System.Object,   
                                ByVal e As System.EventArgs  
                               ) Handles AddButton.Click  
      Dim cust As New Customer With {   
        .City = "Wellington",   
        .CompanyName = "Blue Yonder Airlines",   
        .ContactName = "Jill Frank",   
        .Country = "New Zealand",   
        .CustomerID = "JILLF"}  
  
      db.Customers.InsertOnSubmit(cust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
5. 두 번 클릭 합니다 **업데이트** 코드를 추가 하는 단추 해당 `Click` 이벤트입니다. 다음 코드를 추가합니다.  
  
    ```vb  
    Private Sub UpdateButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles UpdateButton.Click  
      Dim updateCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      updateCust.ContactName = "Jill Shrader"
      updateCust.Country = "Wales"
      updateCust.CompanyName = "Red Yonder Airlines"
      updateCust.City = "Cardiff"
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
6. 두 번 클릭 합니다 **삭제할** 코드를 추가 하는 단추 해당 `Click` 이벤트입니다. 다음 코드를 추가합니다.  
  
    ```vb  
    Private Sub DeleteButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles DeleteButton.Click  
      Dim deleteCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      db.Customers.DeleteOnSubmit(deleteCust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
7. F5 키를 눌러 프로젝트를 실행합니다. 클릭 **추가** 새 레코드를 추가 합니다. 클릭 **업데이트** 새 레코드를 수정 합니다. 클릭 **삭제** 새 레코드를 삭제 합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext 메서드(O/R 디자이너)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [방법: 저장 프로시저를 할당하여 업데이트, 삽입 및 삭제 수행(O/R 디자이너)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
