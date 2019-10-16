---
title: Oracle 데이터 형식 매핑
ms.date: 03/30/2017
ms.assetid: ec34ae21-bbbb-4adb-b672-83865e2a8451
ms.openlocfilehash: be478741069e9edd406d73c0b75d5960b9909896
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783429"
---
# <a name="oracle-data-type-mappings"></a>Oracle 데이터 형식 매핑
다음 표에는 Oracle 데이터 형식과 <xref:System.Data.OracleClient.OracleDataReader>에 대한 해당 데이터 형식의 매핑이 나열되어 있습니다.  
  
|Oracle 데이터 형식|OracleDataReader.GetValue에 의해 반환되는 .NET Framework 데이터 형식|OracleDataReader.GetOracleValue에 의해 반환되는 OracleClient 데이터 형식|설명|  
|----------------------|--------------------------------------------------------------------|------------------------------------------------------------------------|-------------|  
|**BFILE**|**Byte[]**|<xref:System.Data.OracleClient.OracleBFile>||  
|**BLOB**|**Byte[]**|<xref:System.Data.OracleClient.OracleLob>||  
|**CHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**CLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**DATE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**FLOAT**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|이 데이터 형식은 **숫자** 데이터 형식에 대 한 별칭이 며에서 <xref:System.Data.OracleClient.OracleDataReader> 부동 소수점 값 <xref:System.Data.OracleClient.OracleNumber> 대신 **Decimal** 을 반환 하도록 디자인 되었습니다. .NET Framework 데이터 형식을 사용하면 오버플로가 발생할 수 있습니다.|  
|**INTEGER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|이 데이터 형식은 **NUMBER (38)** 데이터 형식에 대 한 별칭이 며,는 **Decimal** 또는 <xref:System.Data.OracleClient.OracleNumber> integer 값 대신 <xref:System.Data.OracleClient.OracleDataReader> 를 반환 하도록 디자인 되었습니다. .NET Framework 데이터 형식을 사용하면 오버플로가 발생할 수 있습니다.|  
|**기간을 월로**|**Int32**|<xref:System.Data.OracleClient.OracleMonthSpan>||  
|**간격 일-초**|**TimeSpan**|<xref:System.Data.OracleClient.OracleTimeSpan>||  
|**LONG**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**긴 원시**|**Byte[]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**NCHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**NCLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**NUMBER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|.NET Framework 데이터 형식을 사용하면 오버플로가 발생할 수 있습니다.|  
|**NVARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**RAW**|**Byte[]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**REF 커서**|||Oracle **REF CURSOR** 데이터 형식은 <xref:System.Data.OracleClient.OracleDataReader> 개체에서 지원 되지 않습니다.|  
|**ROWID**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**TIMESTAMP**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**현지 표준 시간대를 사용 하는 타임 스탬프**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**표준 시간대가 있는 타임 스탬프**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**부호 없는 정수**|**숫자**|<xref:System.Data.OracleClient.OracleNumber>|이 데이터 형식은 **NUMBER (38)** 데이터 형식의 별칭이 며에서 <xref:System.Data.OracleClient.OracleDataReader> **Decimal** 또는 <xref:System.Data.OracleClient.OracleNumber> unsigned 정수 값 대신를 반환 하도록 디자인 되었습니다. .NET Framework 데이터 형식을 사용하면 오버플로가 발생할 수 있습니다.|  
|**VARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
  
 다음 표에서는 Oracle 데이터 .NET Framework 형식과이를 매개 변수로 바인딩할 때 사용할 데이터**형식 (system.string** 및 <xref:System.Data.OracleClient.OracleType>)을 보여 줍니다.  
  
|Oracle 데이터 형식|매개 변수로 바인딩하는 DbType 열거형|매개 변수로 바인딩하는 OracleType 열거형|설명|  
|----------------------|-----------------------------------------------|---------------------------------------------------|-------------|  
|**BFILE**||**BFile**|Oracle **에서는 bfile을** **bfile** 매개 변수로만 바인딩할 수 있습니다. Oracle에 대 한 .NET Data Provider **byte []** 또는 <xref:System.Data.OracleClient.OracleBinary>등의**BFILE** 이 아닌 값을 바인딩하려는 경우이를 자동으로 생성 하지 않습니다.|  
|**BLOB**||**Blob**|Oracle **에서는 blob를** **blob** 매개 변수로 바인딩할 수 있습니다. Oracle에 대 한 .NET Data Provider **byte []** 또는 <xref:System.Data.OracleClient.OracleBinary>와 같은**BLOB** 이 아닌 값을 바인딩하려는 경우이를 자동으로 생성 하지 않습니다.|  
|**CHAR**|**AnsiStringFixedLength**|**Char**||  
|**CLOB**||**Clob**|Oracle **에서는 clob을** **clob** 매개 변수로 바인딩할 수 있습니다. **System.string** 또는<xref:System.Data.OracleClient.OracleString>와 같은**CLOB** 이 아닌 값을 바인딩하려는 경우에는 Oracle 용 .net Data Provider 자동으로 생성 하지 않습니다.|  
|**DATE**|**DateTime**|**DateTime**||  
|**FLOAT**|**Single, Double, Decimal**|**Float, Double, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A>는 **system.object** 및 <xref:System.Data.OracleClient.OracleType>를 확인 합니다.|  
|**INTEGER**|**SByte, Int16, Int32, Int64, Decimal**|**SByte, Int16, Int32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A>는 **system.object** 및 <xref:System.Data.OracleClient.OracleType>를 확인 합니다.|  
|**기간을 월로**|**Int32**|**IntervalYearToMonth**|<xref:System.Data.OracleClient.OracleType>은 Oracle 9i 클라이언트 및 서버 소프트웨어를 모두 사용할 때만 사용할 수 있습니다.|  
|**간격 일-초**|**개체**|**IntervalDayToSecond**|<xref:System.Data.OracleClient.OracleType>은 Oracle 9i 클라이언트 및 서버 소프트웨어를 모두 사용할 때만 사용할 수 있습니다.|  
|**LONG**|**AnsiString**|**LongVarChar**||  
|**긴 원시**|**이진**|**LongRaw**||  
|**NCHAR**|**StringFixedLength**|**NChar**||  
|**NCLOB**||**NClob**|Oracle **에서는 nclob를** **nclob** 매개 변수로만 바인딩할 수 있습니다. Oracle의 .NET Data Provider는 **system.string** 또는 <xref:System.Data.OracleClient.OracleString>와 같은**NCLOB** 가 아닌 값을 바인딩하려는 경우 자동으로 생성 하지 않습니다.|  
|**NUMBER**|**VarNumeric**|**숫자**||  
|**NVARCHAR2**|**String**|**NVarChar**||  
|**RAW**|**이진**|**Raw**||  
|**REF 커서**||**커서**|자세한 내용은 [ORACLE REF cursor](oracle-ref-cursors.md)를 참조 하십시오.|  
|**ROWID**|**AnsiString**|**Rowid**||  
|**TIMESTAMP**|**DateTime**|**타임스탬프**|<xref:System.Data.OracleClient.OracleType>은 Oracle 9i 클라이언트 및 서버 소프트웨어를 모두 사용할 때만 사용할 수 있습니다.|  
|**현지 표준 시간대를 사용 하는 타임 스탬프**|**DateTime**|**TimestampLocal**|<xref:System.Data.OracleClient.OracleType>은 Oracle 9i 클라이언트 및 서버 소프트웨어를 모두 사용할 때만 사용할 수 있습니다.|  
|**표준 시간대가 있는 타임 스탬프**|**DateTime**|**TimestampWithTz**|<xref:System.Data.OracleClient.OracleType>은 Oracle 9i 클라이언트 및 서버 소프트웨어를 모두 사용할 때만 사용할 수 있습니다.|  
|**부호 없는 정수**|**Byte, UInt16, UInt32, UInt64, Decimal**|**Byte, UInt16, Uint32, Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A>는 **system.object** 및 <xref:System.Data.OracleClient.OracleType>를 확인 합니다.|  
|**VARCHAR2**|**AnsiString**|**VarChar**||  
  
 <xref:System.Data.OracleClient.OracleParameter> 개체의 <xref:System.Data.OracleClient.OracleParameter.Value%2A> 속성에 사용 되는 **inputoutput**, **output**및 **ReturnValue** **ParameterDirection** 값은 입력 값이 Oracle 데이터 형식이 아닌 경우에 .NET Framework 데이터 형식입니다. 예: <xref:System.Data.OracleClient.OracleString>또는). <xref:System.Data.OracleClient.OracleNumber> **REF CURSOR**, **BFILE**또는 **LOB** 데이터 형식에는 적용 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [Oracle 및 ADO.NET](oracle-and-adonet.md)
- [ADO.NET 개요](ado-net-overview.md)
