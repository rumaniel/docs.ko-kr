---
title: 샘플 데이터베이스 다운로드(LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: eb42a7af-d410-4b7f-b4a8-13c72ce6fd09
ms.openlocfilehash: c67ee699cf594f476a728c7345b47b0c32dea7ff
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795171"
---
# <a name="downloading-sample-databases-linq-to-dataset"></a>샘플 데이터베이스 다운로드(LINQ to DataSet)
LINQ to DataSet 설명서의 샘플과 연습에서는 AdventureWorks 예제 데이터베이스를 사용 합니다. 이 제품은 Microsoft 다운로드 사이트에서 무료로 다운로드할 수 있습니다. LINQ to DataSet 설명서의 샘플과 연습에서는 SQL Server를 데이터 저장소로 사용 합니다. SQL Server 대신 무료로 사용할 수 있는 SQL Server Express Edition을 데이터 저장소로 사용할 수도 있습니다.  
  
## <a name="downloading-and-installing-the-adventureworks-database"></a>AdventureWorks 데이터베이스 다운로드 및 설치  
  
#### <a name="to-download-and-install-the-adventureworks-sample-database-for-sql-server"></a>SQL Server용 AdventureWorks 샘플 데이터베이스를 다운로드하고 설치하려면  
  
1. Internet Explorer를 엽니다.  
  
2. [SQL Server 2005 샘플 및 예제 데이터베이스](https://go.microsoft.com/fwlink/?linkid=31046) 웹 사이트로 이동 합니다.  
  
3. 지침에 따라 프로세서 유형에 해당하는 AdventureWorks 샘플 데이터베이스(예: AdventureWorksDB.msi)를 다운로드하고 .MSI 파일을 로컬 컴퓨터에 저장합니다.  
  
4. 다운로드한 파일이나 SQL Server 설치 프로그램을 실행하는 동안 이전 버전의 AdventureWorks가 설치되어 있으면 AdventureWorks.msi를 실행하기 전에 이전 버전을 제거해야 합니다.  
  
#### <a name="to-remove-a-previous-download-of-an-adventureworks-sample-database"></a>AdventureWorks 샘플 데이터베이스의 이전 다운로드를 제거하려면  
  
1. AdventureWorks 또는 AdventureWorksDW 데이터베이스를 삭제합니다.  
  
2. **프로그램 추가/제거**에서 **adventureworksdb.msi** 또는 **Adventureworksbi.msi** 를 선택 하 고 **제거**를 클릭 합니다.  
  
#### <a name="to-remove-an-adventureworks-sample-database-previously-installed-using-setup"></a>설치 프로그램을 사용하여 이전에 설치된 AdventureWorks 샘플 데이터베이스를 제거하려면  
  
1. AdventureWorks 또는 AdventureWorksDW 데이터베이스를 삭제합니다.  
  
2. **프로그램 추가/제거**에서 **Microsoft SQL Server 2005** 을 선택 하 고 **변경**을 클릭 합니다.  
  
3. **구성 요소 선택**에서 **워크스테이션 구성 요소** 를 선택 하 고 **다음**을 클릭 합니다.  
  
4. **SQL Server 설치 마법사 시작**에서 **다음**을 클릭 합니다.  
  
5. **시스템 구성 검사**에서 **다음**을 클릭 합니다.  
  
6. **인스턴스 변경 또는 제거**에서 **설치 된 구성 요소 변경**을 클릭 합니다.  
  
7. **기능 선택**에서 **설명서, 샘플 및 예제 데이터베이스** 노드를 확장 합니다.  
  
8. **샘플 코드 및 응용 프로그램을**선택 합니다. **예제 데이터베이스**를 확장 하 고 제거할 예제 데이터베이스를 선택한 다음, **전체 기능을 사용할 수 없음**을 선택 합니다. **다음**을 클릭합니다.  
  
9. **설치** 를 클릭 하 고 설치 마법사를 완료 합니다.  
  
#### <a name="to-attach-the-adventureworks-sample-database-files-to-an-instance-of-sql-server"></a>AdventureWorks 샘플 데이터베이스 파일을 SQL Server 인스턴스에 연결하려면  
  
1. File sample database installer 파일을 다운로드 한 후 **adventureworksdb.msi** 파일 (또는 다운로드 한 파일)을 두 번 클릭 하 여 데이터베이스를 설치 합니다. 기본적으로 데이터베이스는 c:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data에 설치됩니다.  
  
2. 다음 스크립트 SQLCMD 또는 SQL Server Management Studio를 실행하여 AdventureWorks 데이터베이스 파일을 SQL Server 인스턴스에 연결합니다.  
  
    ```sql
    exec sp_attach_db @dbname=N'AdventureWorks', @filename1=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_Data.mdf', @filename2=N'C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data\AdventureWorks_log.ldf'  
    ```  
  
     이러한 파일을 다른 드라이브나 디렉터리에 설치한 경우에는 `sp_attach_db` 저장 프로시저를 실행하기 전에 경로를 올바르게 수정해야 합니다.  
  
## <a name="downloading-sql-server-express-edition"></a>SQL Server Express Edition 다운로드  
 LINQ to DataSet 섹션의 샘플과 연습에서는 데이터 저장소로 SQL Server 2005를 사용 하지만 대신 SQL Server Express 버전을 사용 하도록 수정할 수 있습니다. SQL Server Express Edition은 무료로 제공되며 애플리케이션과 함께 재배포할 수 있습니다. Visual Studio를 사용 하는 경우 SQL Server Express Edition은 Pro 이상 버전에 포함 되어 있습니다.  
  
#### <a name="to-download-and-install-sql-server-express-edition"></a>SQL Server Express Edition을 다운로드하여 설치하려면  
  
1. Internet Explorer를 시작합니다.  
  
2. [Microsoft SQL Server 2005 Express Edition](https://go.microsoft.com/fwlink/?LinkID=31070) 다운로드 페이지로 이동 합니다.  
  
3. 웹 사이트의 설치 지침을 따릅니다.  
  
## <a name="see-also"></a>참고자료

- [시작](getting-started-linq-to-dataset.md)
