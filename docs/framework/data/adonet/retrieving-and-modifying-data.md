---
title: ADO.NET에서 데이터 검색 및 수정
ms.date: 03/30/2017
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.openlocfilehash: 78012a6a5ecdfac0e4cd7c4939ae3ab0036ab716
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782855"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>ADO.NET에서 데이터 검색 및 수정
데이터베이스 애플리케이션의 기본 기능은 데이터 소스에 연결하여 포함된 데이터를 검색하는 것입니다. ADO.NET의 .NET Framework 데이터 공급자는 응용 프로그램과 데이터 원본 간의 브리지 역할을 하므로 **DataReader** 나 **DataAdapter**를 사용 하 여 데이터를 검색 하는 것 뿐만 아니라 명령을 실행할 수 있습니다. 모든 데이터베이스 애플리케이션의 한 가지 핵심 기능은 데이터베이스에 저장된 데이터를 업데이트하는 것입니다. ADO.NET에서는 데이터를 업데이트 하는 경우 **DataAdapter** 와 <xref:System.Data.DataSet>및 **명령** 개체를 사용 하며 트랜잭션 사용도 포함 될 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 소스에 연결](connecting-to-a-data-source.md)  
 데이터 소스에 대한 연결을 설정하고 연결 이벤트로 작업하는 방법을 설명합니다.  
  
 [연결 문자열](connection-strings.md)  
 연결 문자열 키워드, 보안 정보와 이에 대한 저장 및 검색을 비롯하여 다양한 연결 문자열 사용 방법을 설명하는 항목을 제공합니다.  
  
 [연결 풀링](connection-pooling.md)  
 .NET Framework 데이터 공급자의 연결 풀링에 대해 설명합니다.  
  
 [명령 및 매개 변수](commands-and-parameters.md)  
 명령 및 명령 작성기를 만드는 방법, 매개 변수를 구성하는 방법 및 명령을 실행하여 데이터를 검색하고 수정하는 방법에 대한 항목을 제공합니다.  
  
 [DataAdapter 및 DataReader](dataadapters-and-datareaders.md)  
 DataReaders, DataAdapters, 매개 변수, DataAdapter 이벤트 처리 및 배치 작업 수행 방법을 설명하는 항목을 제공합니다.  
  
 [트랜잭션 및 동시성](transactions-and-concurrency.md)  
 로컬 트랜잭션, 분산 트랜잭션 및 낙관적 동시성 관련 작업의 수행 방법을 설명하는 항목을 제공합니다.  
  
 [ID 또는 일련 번호 값 검색](retrieving-identity-or-autonumber-values.md)  
 SQL Server 테이블의 **id** 열 이나 Microsoft Access 테이블의 **Autonumber** 필드에 대해 생성 된 값을 테이블에 삽입 된 행의 열에 매핑하는 예를 제공 합니다. `DataTable`에서의 ID 값 병합에 대해 설명합니다.  
  
 [이진 데이터 검색](retrieving-binary-data.md)  
 를 사용 하 여 `CommandBehavior`이진 데이터 또는 대량 데이터 구조를 검색 하는 방법을 설명 합니다.`SequentialAccess` 의 기본 동작을 수정 `DataReader`합니다.  
  
 [저장 프로시저로 데이터 수정](modifying-data-with-stored-procedures.md)  
 저장 프로시저 입력 매개 변수와 출력 매개 변수를 사용하여 데이터베이스에 행을 삽입하여 새 ID 값을 반환하는 방법을 설명합니다.  
  
 [데이터베이스 스키마 정보 검색](retrieving-database-schema-information.md)  
 데이터 소스에서 사용 가능한 데이터베이스나 카탈로그, 데이터베이스의 테이블 및 뷰를 비롯하여 테이블에 대한 제약 조건 및 기타 스키마 정보를 가져오는 방법을 설명합니다.  
  
 [DbProviderFactory](dbproviderfactories.md)  
 공급자 팩터리 모델에 대해 설명하고 `System.Data.Common` 네임스페이스의 기본 클래스를 사용하는 방법을 보여 줍니다.  
  
 [ADO.NET의 데이터 추적](data-tracing.md)  
 ADO.NET에서 기본 제공 데이터 추적 기능을 제공하는 방법을 설명합니다.  
  
 [성능 카운터](performance-counters.md)  
 `SqlClient` 및 `OracleClient`에서 사용할 수 있는 성능 카운터에 대해 설명합니다.  
  
 [비동기 프로그래밍](asynchronous-programming.md)  
 비동기 프로그래밍에 대 한 ADO.NET 지원에 대해 설명 합니다.  
  
 [SqlClient 스트리밍 지원](sqlclient-streaming-support.md)  
 데이터를 메모리에 완전히 로드 하지 않고도 SQL Server에서 데이터를 스트리밍하는 응용 프로그램을 작성 하는 방법에 대해 설명 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 형식 매핑](data-type-mappings-in-ado-net.md)
- [DataSet, DataTable 및 DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET 응용 프로그램 보안](securing-ado-net-applications.md)
- [SQL Server 및 ADO.NET](./sql/index.md)
- [ADO.NET 개요](ado-net-overview.md)
