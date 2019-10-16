---
title: ADO.NET 코드 샘플에 대 한 샘플 SQL Server 데이터베이스 가져오기
description: ADO.NET 설명서의 코드 샘플에 사용 된 샘플 SQL Server 데이터베이스와 SQL Server 및 관리 도구를 다운로드 합니다.
ms.date: 01/11/2019
ms.assetid: ef9d69a1-9461-43fe-94bb-7c836754bcb5
ms.openlocfilehash: 60566041ff4f99e96c9aee052dbcc17b5e5da9e5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794035"
---
# <a name="get-the-sample-databases-for-adonet-code-samples"></a>ADO.NET 코드 샘플에 대 한 샘플 데이터베이스 가져오기

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 설명서의 여러 예제 및 연습에서는 예제 SQL Server 데이터베이스 및 SQL Server Express를 사용 합니다. 이러한 제품은 Microsoft에서 무료로 다운로드할 수 있습니다.

## <a name="get-the-northwind-sample-database-for-sql-server"></a>SQL Server에 대 한 Northwind 샘플 데이터베이스 가져오기

다음 GitHub 리포지토리에서 `instnwnd.sql` 스크립트를 다운로드 하 여 SQL Server에 대 한 Northwind 샘플 데이터베이스를 만들고 로드 합니다.

[Microsoft SQL Server에 대 한 Northwind 및 pubs 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)

Northwind 데이터베이스를 사용 하려면 먼저 다운로드 한 `instnwnd.sql` 스크립트 파일을 실행 하 여 [SQL Server Management Studio](#get_ssms) 또는 유사한 도구를 사용 하 여 SQL Server 인스턴스에 데이터베이스를 다시 만들어야 합니다. 리포지토리의 추가 정보 파일에 있는 지침을 따르세요.

> [!TIP]
> Microsoft Access 용 Northwind 데이터베이스를 찾고 있는 경우 [Microsoft access 용 northwind 샘플 데이터베이스 설치](#northwind_access)를 참조 하세요.

## <a name="northwind_access"></a>Microsoft Access 용 Northwind 샘플 데이터베이스 가져오기

Microsoft Access 용 Northwind 샘플 데이터베이스는 Microsoft 다운로드 센터에서 사용할 수 없습니다. 액세스 내에서 직접 Northwind를 설치 하려면 다음 작업을 수행 합니다.

1. 액세스를 엽니다.

1. **온라인 템플릿 검색** 상자에 **Northwind** 를 입력 한 다음 **enter 키**를 선택 합니다.

1. 결과 화면에서 **Northwind**를 선택 합니다. Northwind 데이터베이스에 대 한 설명이 포함 된 새 창이 열립니다.

1. 새 창의 **파일 이름** 텍스트 상자에 Northwind 데이터베이스의 복사본에 대 한 파일 이름을 제공 합니다.

1. **만들기**를 선택합니다. Access는 Northwind 데이터베이스를 다운로드 하 고 파일을 준비 합니다.

1. 이 프로세스가 완료 되 면 시작 화면이 포함 된 데이터베이스가 열립니다.

## <a name="get-the-adventureworks-sample-database-for-sql-server"></a>SQL Server에 대 한 AdventureWorks 예제 데이터베이스 가져오기

다음 GitHub 리포지토리에서 SQL Server 용 AdventureWorks 샘플 데이터베이스를 다운로드 합니다.

[AdventureWorks 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)

데이터베이스 백업 파일 (\*.bak) 중 하나를 다운로드 한 후 SQL Server Management Studio (SSMS)를 사용 하 여 SQL Server 인스턴스에 백업을 복원 합니다. [Get SQL Server Management Studio](#get_ssms)를 참조 하세요.

## <a name="get_ssms"></a>SQL Server Management Studio 가져오기
다운로드 한 데이터베이스를 보거나 수정 하려는 경우 SSMS (SQL Server Management Studio)를 사용할 수 있습니다. 다음 페이지에서 SSMS를 다운로드 합니다.

[SSMS(SQL Server Management Studio) 다운로드](/sql/ssms/download-sql-server-management-studio-ssms) 

Visual Studio IDE (통합 개발 환경)에서 데이터베이스를 보고 관리할 수도 있습니다. [Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)에서 **SQL Server 개체 탐색기**의 데이터베이스에 연결 하거나 **서버 탐색기**데이터베이스에 대 한 데이터 연결을 만듭니다. **보기** 메뉴에서 다음 탐색기 창을 엽니다.

## <a name="get_sql"></a>SQL Server Express 가져오기

SQL Server Express는 응용 프로그램을 사용 하 여 재배포할 수 있는 SQL Server의 초급 수준의 무료로 제공 되는 버전입니다. 다음 페이지에서 SQL Server Express를 다운로드 합니다.
  
[SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)

[Visual studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)를 사용 하는 경우 SQL Server Express LocalDB는 visual studio의 무료 Community edition 뿐만 아니라 Professional 이상 버전에 포함 되어 있습니다.  

## <a name="see-also"></a>참고자료

- [시작](getting-started.md)
