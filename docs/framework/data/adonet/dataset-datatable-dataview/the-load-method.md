---
title: 로드 메서드
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
ms.openlocfilehash: da0695aff9447355b1fc44a033c1b4a1cc224435
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785876"
---
# <a name="the-load-method"></a>로드 메서드
<xref:System.Data.DataTable.Load%2A> 메서드를 사용하여 데이터 소스의 행과 함께 <xref:System.Data.DataTable>을 로드할 수 있습니다. 가장 간단한 형식으로 **DataReader**인 단일 매개 변수를 허용 하는 오버 로드 된 메서드입니다. 이 폼에서는 행이 있는 **DataTable** 을 로드 하기만 하면 됩니다. 필요에 따라 **LoadOption** 매개 변수를 지정 하 여 **DataTable**에 데이터를 추가 하는 방법을 제어할 수 있습니다.  
  
 **LoadOption** 매개 변수는 데이터 원본에서 들어오는 데이터를 테이블에 이미 있는 데이터와 결합 하는 방법을 설명 하기 때문에 **DataTable** 에 이미 데이터 행이 포함 되어 있는 경우에 특히 유용 합니다. 예를 들어 **PreserveCurrentValues** (기본값)는 **DataTable**에 행이 **추가** 된 것으로 표시 된 경우 **원래** 값 또는 각 열이 데이터 소스에서 일치 하는 행의 내용으로 설정 되도록 지정 합니다. **현재** 값에는 행이 추가 될 때 할당 된 값이 유지 되 고 행의 **RowState** 가 **변경**된 것으로 설정 됩니다.  
  
 다음 표에서는 <xref:System.Data.LoadOption> 열거형 값에 대해 간략하게 설명합니다.  
  
|LoadOption 값|Description|  
|----------------------|-----------------|  
|**OverwriteRow**|들어오는 행에 이미 **DataTable**에 있는 행과 같은 **PrimaryKey** 값이 있는 경우 각 열의 **원래** 값과 **현재** 값은 들어오는 행의 값으로 바뀌고 **RowState** 속성은로 설정 됩니다. **변경 되지 않았습니다**.<br /><br /> **DataTable** 에 없는 데이터 원본의 행은 **RowState** 값이 **변경 되지**않은 상태로 추가 됩니다.<br /><br /> 이 옵션을 적용 하면 데이터 원본의 내용과 일치 하도록 **DataTable** 의 내용이 새로 고쳐집니다.|  
|**PreserveCurrentValues (기본값)**|들어오는 행에 이미 **DataTable**에 있는 행과 같은 **PrimaryKey** 값이 있으면 **원래** 값은 들어오는 행의 내용으로 설정 되 고 **현재** 값은 변경 되지 않습니다.<br /><br /> **RowState** 를 **추가** 하거나 **수정**하는 경우 **수정**됨으로 설정 됩니다.<br /><br /> **RowState** **삭제**된 경우 **삭제**된 상태로 유지 됩니다.<br /><br /> **DataTable** 에 없는 데이터 소스의 행이 추가 되 고 **RowState** 이 변경 되지 않은 **상태로**설정 됩니다.|  
|**UpdateCurrentValues**|들어오는 행에 이미 **DataTable**에 있는 행과 같은 **PrimaryKey** 값이 있는 경우 **현재** 값이 **원래** 값으로 복사 되 고 **현재** 값이 들어오는 행의 콘텐츠로 설정 됩니다.<br /><br /> **DataTable** 의 **RowState** 이 **추가**된 경우 **RowState** 는 **추가**된 상태로 유지 됩니다. **Modified** 또는 **Deleted**로 표시 된 행의 경우에는 **RowState** 가 **수정**됩니다.<br /><br /> **DataTable** 에 없는 데이터 소스의 행이 추가 되 고 **RowState** 이 **추가**로 설정 됩니다.|  
  
 다음 예제에서는 **Load** 메서드를 사용 하 여 **Northwind** 데이터베이스에 있는 직원의 생일 목록을 표시 합니다.  
  
```vb  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.   
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## <a name="see-also"></a>참고자료

- [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)
- [ADO.NET 개요](../ado-net-overview.md)
