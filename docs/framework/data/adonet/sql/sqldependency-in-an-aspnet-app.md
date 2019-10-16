---
title: ASP.NET 응용 프로그램에서 SqlDependency
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.openlocfilehash: f3e28adc2cf7c24cee9ee344eb78404f01b79793
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780723"
---
# <a name="sqldependency-in-an-aspnet-application"></a>ASP.NET 응용 프로그램에서 SqlDependency
이 단원의 예제에서는 ASP.NET <xref:System.Data.SqlClient.SqlDependency> 개체를 활용하여 <xref:System.Web.Caching.SqlCacheDependency>를 간접적으로 사용하는 방법을 보여 줍니다. <xref:System.Web.Caching.SqlCacheDependency> 개체에서는 <xref:System.Data.SqlClient.SqlDependency>를 사용하여 알림을 수신하고 캐시를 올바르게 업데이트합니다.  
  
> [!NOTE]
> 이 샘플 코드에서는 [쿼리 알림을 사용 하도록 설정](enabling-query-notifications.md)하는 스크립트를 실행 하 여 쿼리 알림을 사용 하도록 설정 했다고 가정 합니다.  
  
## <a name="about-the-sample-application"></a>샘플 응용 프로그램 정보  
 샘플 응용 프로그램은 단일 ASP.NET 웹 페이지를 사용 하 여 **AdventureWorks** SQL Server 데이터베이스의 제품 정보를 <xref:System.Web.UI.WebControls.GridView> 컨트롤에 표시 합니다. 페이지가 로드되면 코드에서 <xref:System.Web.UI.WebControls.Label> 컨트롤에 현재 시간을 씁니다. 그런 다음 <xref:System.Web.Caching.SqlCacheDependency> 개체를 정의하고 최대 3분 동안 캐시 데이터를 저장하도록 <xref:System.Web.Caching.Cache> 개체의 속성을 설정합니다. 그런 다음 코드에서는 데이터베이스에 연결하여 데이터를 검색합니다. 페이지가 로드되고 응용 프로그램이 실행되면 ASP.NET이 캐시에서 데이터를 검색합니다. 여기서 페이지의 시간이 변경되지 않는지를 보고 확인할 수 있습니다. 모니터링되는 데이터가 변경되면 ASP.NET은 캐시를 무효화한 다음 `GridView` 컨트롤을 새 데이터로 다시 채우고 `Label` 컨트롤에 표시된 시간을 업데이트합니다.  
  
## <a name="creating-the-sample-application"></a>샘플 응용 프로그램 만들기  
 샘플 응용 프로그램을 만들고 실행하려면 다음 단계를 따르세요.  
  
1. 새 ASP.NET 웹 사이트를 만듭니다.  
  
2. <xref:System.Web.UI.WebControls.Label> 및 <xref:System.Web.UI.WebControls.GridView> 컨트롤을 Default.aspx 페이지에 추가합니다.  
  
3. 페이지의 클래스 모듈을 열고 다음 지시문을 추가합니다.  
  
    ```vb  
    Option Strict On  
    Option Explicit On  
  
    Imports System.Data.SqlClient  
    ```  
  
    ```csharp  
    using System.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. 페이지의 `Page_Load` 이벤트에 다음 코드를 추가합니다.  
  
     [!code-csharp[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#1)]
     [!code-vb[DataWorks SqlDependency.AspNet#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#1)]  
  
5. `GetConnectionString` 및 `GetSQL`의 두 가지 도우미 메서드를 추가합니다. 정의된 연결 문자열은 통합 보안을 사용합니다. 사용 중인 계정에 필요한 데이터베이스 권한이 있는지, 그리고 **AdventureWorks**샘플 데이터베이스에 알림이 설정 되어 있는지 확인 해야 합니다.
  
     [!code-csharp[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/CS/Default.aspx.cs#2)]
     [!code-vb[DataWorks SqlDependency.AspNet#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlDependency.AspNet/VB/Default.aspx.vb#2)]  
  
### <a name="testing-the-application"></a>애플리케이션 테스트  
 응용 프로그램에서는 Web Form에 표시된 데이터를 캐시하고 활동이 없으면 3분마다 새로 고칩니다. 데이터베이스가 변경되면 즉시 캐시를 새로 고칩니다. Visual Studio에서 응용 프로그램을 실행합니다. 그러면 페이지가 브라우저로 로드됩니다. 표시된 캐시 새로 고침 시간은 캐시가 마지막으로 새로 고쳐진 시간을 나타냅니다. 3분을 기다렸다 페이지를 다시 고쳐서 포스트백 이벤트가 발생하도록 합니다. 페이지에 표시된 시간이 변경됩니다. 3분이 지나기 전에 페이지를 새로 고치면 페이지에 표시된 시간이 동일하게 유지됩니다.  
  
 이제 Transact-SQL UPDATE 명령을 사용하여 데이터베이스의 데이터를 업데이트하고 페이지를 새로 고칩니다. 이제 표시된 시간을 보면 캐시가 데이터베이스의 새 데이터로 새로 고쳐졌음을 알 수 있습니다. 캐시가 업데이트되었지만 포스트백 이벤트가 발생할 때까지는 페이지에 표시된 시간이 변경되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server에서 쿼리 알림](query-notifications-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
