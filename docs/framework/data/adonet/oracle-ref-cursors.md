---
title: Oracle REF CURSOR
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 7cd29a6a20015c7ce4475b0211cb07f7ee78b530
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794876"
---
# <a name="oracle-ref-cursors"></a>Oracle REF CURSOR
Oracle의 .NET Framework Data Provider는 Oracle **REF CURSOR** 데이터 형식을 지원 합니다. Oracle REF CURSOR를 사용하는 데이터 공급자를 사용할 경우 다음 동작을 고려해야 합니다.  
  
> [!NOTE]
> 일부 동작이 MSDAORA(Microsoft OLE DB Provider for Oracle)의 동작과 다릅니다.  
  
- 성능상의 이유로 Oracle의 Data Provider는 명시적으로 지정 하지 않는 한 MSDAORA 처럼 **REF CURSOR** 데이터 형식을 자동으로 바인딩하지 않습니다.  
  
- 데이터 공급자는 REF CURSOR 매개 변수를 지정하는 데 사용되는 {resultset} 이스케이프를 포함하여 ODBC 이스케이프 시퀀스를 지원하지 않습니다.  
  
- REF cursor를 반환 하는 저장 프로시저를 실행 <xref:System.Data.OracleClient.OracleParameterCollection> 하려면 **커서** 와 <xref:System.Data.OracleClient.OracleParameter.Direction%2A> **출력**의를 <xref:System.Data.OracleClient.OracleType> 사용 하 여에 매개 변수를 정의 해야 합니다. 데이터 공급자는 REF CURSOR를 출력 매개 변수로만 바인딩하는 것을 지원하며 REF CURSOR를 입력 매개 변수로 지원하지 않습니다.  
  
- 매개 변수 값에서 <xref:System.Data.OracleClient.OracleDataReader>를 가져오는 것은 지원되지 않습니다. 값의 형식은 명령이 실행된 후의 <xref:System.DBNull>입니다.  
  
- REF 커서 를 사용 하는 경우 (예:를 호출 <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>하는 경우)에만 CommandBehavior 열거형 값이 **CloseConnection**, 다른 모든 값은 무시 됩니다.  
  
- **OracleDataReader** 에서 참조 커서의 순서는 **OracleParameterCollection**의 매개 변수 순서에 따라 달라 집니다. <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> 속성은 무시됩니다.  
  
- PL/SQL **테이블** 데이터 형식은 지원 되지 않습니다. 그러나 REF CURSOR가 더 효율적입니다. **테이블** 데이터 형식을 사용 해야 하는 경우 MSDAORA와 함께 OLE DB .net Data Provider를 사용 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [REF CURSOR 예제](ref-cursor-examples.md)  
 REF CURSOR의 사용을 보여 주는 세 가지 예제가 들어 있습니다.  
  
 [OracleDataReader의 REF CURSOR 매개 변수](ref-cursor-parameters-in-an-oracledatareader.md)  
 REF CURSOR 매개 변수를 반환 하는 PL/SQL 저장 프로시저를 실행 하 고 값을 **OracleDataReader**로 읽는 방법을 보여 줍니다.  
  
 [OracleDataReader를 사용하여 여러 REF CURSOR에서 데이터 검색](retrieving-data-from-multiple-ref-cursors.md)  
 두 개의 REF CURSOR 매개 변수를 반환 하는 PL/SQL 저장 프로시저를 실행 하 고 **OracleDataReader**를 사용 하 여 값을 읽는 방법을 보여 줍니다.  
  
 [하나 이상의 REF CURSOR를 사용하여 데이터 세트 채우기](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 두 개의 REF CURSOR 매개 변수를 반환하는 PL/SQL 저장 프로시저를 실행하여 반환되는 행으로 <xref:System.Data.DataSet>을 채우는 방법을 보여 줍니다.  
  
## <a name="see-also"></a>참고자료

- [Oracle 및 ADO.NET](oracle-and-adonet.md)
- [ADO.NET 개요](ado-net-overview.md)
