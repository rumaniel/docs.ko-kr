---
title: SQL-CLR 형식 매핑
ms.date: 07/23/2018
ms.assetid: 4ed76327-54a7-414b-82a9-7579bfcec04b
ms.openlocfilehash: 6710c58a430c35dae41a1a381335019fd3e75192
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053036"
---
# <a name="sql-clr-type-mapping"></a>SQL-CLR 형식 매핑
LINQ to SQL에서 관계형 데이터베이스의 데이터 모델은 사용자가 선택한 프로그래밍 언어로 표현되는 개체 모델에 매핑됩니다. 애플리케이션을 실행하면 LINQ to SQL에서는 개체 모델의 통합 언어 쿼리를 SQL로 변환하여 실행을 위해 데이터베이스로 전송합니다. 데이터베이스에서 결과가 반환되면 LINQ to SQL에서는 해당 결과를 사용자의 프로그래밍 언어로 작업할 수 있는 개체로 다시 변환합니다.  
  
 개체 모델과 데이터베이스 간에 데이터를 변환 하려면 *형식 매핑을* 정의 해야 합니다. LINQ to SQL에서는 형식 매핑을 사용하여 각 CLR(공용 언어 런타임) 형식을 특정 SQL Server 형식과 연결합니다. 특성 기반 매핑을 사용하여 개체 모델 내부에 형식 매핑 및 데이터베이스 구조와 테이블 관계 같은 다른 매핑 정보를 정의할 수 있습니다. 또는 외부 매핑 파일을 사용하여 개체 모델 외부에 매핑 정보를 지정할 수도 있습니다. 자세한 내용은 [특성 기반 매핑](attribute-based-mapping.md) 및 [외부 매핑](external-mapping.md)을 참조 하세요.  
  
 이 항목에서는 다음 사항에 대해 설명합니다.  
  
- [기본 형식 매핑](#DefaultTypeMapping)  
  
- [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)  
  
- [CLR과 SQL 실행의 동작 차이점](#BehaviorDiffs)  
  
- [열거형 매핑](#EnumMapping)  
  
- [숫자 매핑](#NumericMapping)  
  
- [텍스트 및 XML 매핑](#TextMapping)  
  
- [날짜 및 시간 매핑](#DateMapping)  
  
- [이진 매핑](#BinaryMapping)  
  
- [기타 매핑](#MiscMapping)  
  
<a name="DefaultTypeMapping"></a>   
## <a name="default-type-mapping"></a>기본 형식 매핑  
 개체 모델 또는 외부 매핑 파일은 O/R 디자이너(개체 관계형 디자이너) 또는 SQLMetal 명령줄 도구를 사용하여 자동으로 만들 수 있습니다. 이러한 도구의 기본 형식 매핑은 SQL Server 데이터베이스 내의 열에 매핑될 CLR 형식을 정의합니다. 이러한 도구를 사용 하는 방법에 대 한 자세한 내용은 [개체 모델 만들기](creating-the-object-model.md)를 참조 하세요.  
  
 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 메서드를 사용하여 개체 모델 또는 외부 매핑 파일의 매핑 정보를 기초로 SQL Server 데이터베이스를 만들 수도 있습니다. <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 메서드의 기본 형식 매핑은 개체 모델의 CLR 형식에 매핑되도록 만들 SQL Server 열의 형식을 정의합니다. 자세한 내용은 [방법: 데이터베이스](how-to-dynamically-create-a-database.md)를 동적으로 만듭니다.  
  
<a name="BehaviorMatrix"></a>   
## <a name="type-mapping-run-time-behavior-matrix"></a>형식 매핑 런타임 동작 매트릭스  
 다음 다이어그램에서는 데이터를 데이터베이스에서 검색하거나 데이터베이스에 저장할 때 특정 형식 매핑에 대해 예상되는 런타임 동작을 보여 줍니다. serialization의 경우를 제외하고 LINQ to SQL에서는 이 매트릭스에 지정되어 있는 CLR 또는 SQL Server 데이터 형식 간 매핑만 지원합니다. Serialization 지원에 대 한 자세한 내용은 [이진 serialization](#BinarySerialization)을 참조 하세요.  
 
![SQL CLR 데이터 형식 매핑 테이블 SQL Server](./media/sql-clr-type-mapping.png)

> [!NOTE]
> 일부 형식 매핑의 경우 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다.  
  
### <a name="custom-type-mapping"></a>사용자 지정 형식 매핑  
 LINQ to SQL을 사용할 경우 O/R 디자이너, SQLMetal 및 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> 메서드에 사용되는 기본 형식 매핑에 제한이 없습니다. DBML 파일에 명시적으로 지정하는 방법으로 사용자 지정 형식 매핑을 만들 수 있습니다. 그런 다음 이 DBML 파일을 사용하여 개체 모델 코드 및 매핑 파일을 만들 수 있습니다. 자세한 내용은 [SQL-CLR 사용자 지정 형식 매핑](sql-clr-custom-type-mappings.md)을 참조 하세요.  
  
<a name="BehaviorDiffs"></a>   
## <a name="behavior-differences-between-clr-and-sql-execution"></a>CLR 및 SQL 실행 간의 동작 차이  
 CLR과 SQL Server는 전체 자릿수 및 실행 측면에서 차이점이 있기 때문에 어디서 계산을 수행하는지에 따라 결과나 동작이 다를 수 있습니다. LINQ to SQL 쿼리에서 계산을 수행하면 실제로 계산은 Transact-SQL로 변환된 후 SQL Server 데이터베이스에서 실행됩니다. LINQ to SQL 쿼리 외부에서 수행되는 계산은 CLR 컨텍스트 내에서 실행됩니다.  
  
 예를 들어 다음은 CLR과 SQL Server 사이의 몇 가지 동작 차이점입니다.  
  
- SQL Server에서는 일부 데이터 형식이 CLR에서 이에 해당되는 데이터 형식과 다르게 정렬됩니다. 예를 들어 SQL Server의 `UNIQUEIDENTIFIER` 데이터 형식은 CLR의 <xref:System.Guid?displayProperty=nameWithType> 데이터 형식과 다르게 정렬됩니다.  
  
- SQL Server에서는 일부 문자열의 비교 연산이 CLR과 다르게 처리됩니다. SQL Server의 경우 문자열 비교 동작은 서버의 데이터 정렬 설정에 따라 다릅니다. 자세한 내용은 Microsoft SQL Server 온라인 설명서에서 [데이터 정렬 작업](https://go.microsoft.com/fwlink/?LinkId=115330) 을 참조 하세요.  
  
- SQL Server에서는 매핑된 일부 함수에 대해 CLR과는 다른 값을 반환할 수 있습니다. 예를 들어 두 문자열이 후행 공백에서만 차이가 있는 경우 SQL Server에서는 두 문자열이 동일한 것으로 간주되는 반면 CLR에서는 두 문자열이 다른 것으로 간주되기 때문에 같음 함수가 각각 다른 값을 반환합니다.  
  
<a name="EnumMapping"></a>   
## <a name="enum-mapping"></a>Enum 매핑  
 LINQ to SQL에서는 다음과 같은 두 가지 방법으로 CLR <xref:System.Enum?displayProperty=nameWithType> 형식을 SQL Server 형식에 매핑합니다.  
  
- SQL 숫자 형식에 대한 매핑(`TINYINT`, `SMALLINT`, `INT`, `BIGINT`)  
  
     CLR <xref:System.Enum?displayProperty=nameWithType> 형식을 SQL 숫자 형식에 매핑할 경우 CLR <xref:System.Enum?displayProperty=nameWithType>의 기본 정수 값이 SQL Server 데이터베이스 열의 값에 매핑됩니다. 예를 들어 <xref:System.Enum?displayProperty=nameWithType>라는 `DaysOfWeek`에 기본 정수 값이 3인 `Tue`라는 멤버가 포함된 경우 해당 멤버는 데이터베이스 값 3에 매핑됩니다.  
  
- SQL 텍스트 형식에 대한 매핑(`CHAR`, `NCHAR`, `VARCHAR`, `NVARCHAR`)  
  
     CLR <xref:System.Enum?displayProperty=nameWithType> 형식을 SQL 텍스트 형식에 매핑할 경우 SQL 데이터베이스 값이 CLR <xref:System.Enum?displayProperty=nameWithType> 멤버의 이름에 매핑됩니다. 예를 들어 <xref:System.Enum?displayProperty=nameWithType>라는 `DaysOfWeek`에 기본 정수 값이 3인 `Tue`라는 멤버가 포함된 경우 해당 멤버는 데이터베이스 값 `Tue`에 매핑됩니다.  
  
> [!NOTE]
> SQL 텍스트 형식을 CLR <xref:System.Enum?displayProperty=nameWithType>에 매핑할 경우에는 매핑되는 SQL 열에 <xref:System.Enum> 멤버의 이름만 포함해야 합니다. 다른 값은 <xref:System.Enum>에 매핑되는 SQL 열에 사용할 수 없습니다.  
  
 O/R 디자이너 및 SQLMetal 명령줄 도구는 SQL 형식을 CLR <xref:System.Enum> 클래스에 자동으로 매핑할 수 없습니다. O/R 디자이너 및 SQLMetal에 사용하려면 DBML 파일을 사용자 지정하여 이 매핑을 명시적으로 구성해야 합니다. 사용자 지정 형식 매핑에 대 한 자세한 내용은 [SQL-CLR 사용자 지정 형식 매핑](sql-clr-custom-type-mappings.md)을 참조 하세요.  
  
 열거를 위한 SQL 열은 다른 숫자 및 텍스트 열과 형식이 동일 하기 때문에 이러한 도구는 다음 [숫자 매핑](#NumericMapping) 및 [텍스트 및 XML 매핑](#TextMapping) 섹션에 설명 된 대로 사용자의 의도를 인식 하지 못하고 기본적으로 매핑됩니다. DBML 파일을 사용 하 여 코드를 생성 하는 방법에 대 한 자세한 내용은 [LINQ to SQL에서 코드 생성](code-generation-in-linq-to-sql.md)을 참조 하세요.  
  
 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드는 CLR <xref:System.Enum?displayProperty=nameWithType> 형식에 매핑되는 숫자 형식의 SQL 열을 만듭니다.  
  
<a name="NumericMapping"></a>   
## <a name="numeric-mapping"></a>숫자 매핑  
 LINQ to SQL에서는 여러 CLR 및 SQL Server 숫자 형식을 매핑할 수 있습니다. 다음 표에는 데이터베이스를 기초로 개체 모델 또는 외부 매핑 파일을 빌드할 때 O/R 디자이너와 SQLMetal에서 선택하는 CLR 형식이 나와 있습니다.  
  
|SQL Server 형식|O/R 디자이너 및 SQLMetal에서 사용하는 기본 CLR 형식 매핑|  
|---------------------|-----------------------------------------------------------------|  
|`BIT`|<xref:System.Boolean?displayProperty=nameWithType>|  
|`TINYINT`|<xref:System.Int16?displayProperty=nameWithType>|  
|`INT`|<xref:System.Int32?displayProperty=nameWithType>|  
|`BIGINT`|<xref:System.Int64?displayProperty=nameWithType>|  
|`SMALLMONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`MONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`DECIMAL`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`NUMERIC`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`REAL/FLOAT(24)`|<xref:System.Single?displayProperty=nameWithType>|  
|`FLOAT/FLOAT(53)`|<xref:System.Double?displayProperty=nameWithType>|  
  
 다음 표에는 개체 모델 또는 외부 매핑 파일에 정의된 CLR 형식에 매핑되도록 만들 SQL 열의 형식을 정의하기 위해 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 사용하는 기본 형식 매핑이 나와 있습니다.  
  
|CLR 형식|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>에서 사용하는 기본 SQL Server 형식|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Boolean?displayProperty=nameWithType>|`BIT`|  
|<xref:System.Byte?displayProperty=nameWithType>|`TINYINT`|  
|<xref:System.Int16?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.Int32?displayProperty=nameWithType>|`INT`|  
|<xref:System.Int64?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.SByte?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.UInt16?displayProperty=nameWithType>|`INT`|  
|<xref:System.UInt32?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.UInt64?displayProperty=nameWithType>|`DECIMAL(20)`|  
|<xref:System.Decimal?displayProperty=nameWithType>|`DECIMAL(29,4)`|  
|<xref:System.Single?displayProperty=nameWithType>|`REAL`|  
|<xref:System.Double?displayProperty=nameWithType>|`FLOAT`|  
  
 이 외에도 여러 가지 숫자 매핑을 선택할 수 있지만 일부의 경우에는 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다. 자세한 내용은 [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)를 참조 하세요.  
  
### <a name="decimal-and-money-types"></a>Decimal 및 Money 형식  
 SQL Server `DECIMAL` 형식의 기본 전체 자릿수(소수점을 기준으로 왼쪽과 오른쪽에 18자리)는 이 형식과 기본적으로 쌍을 이루는 CLR <xref:System.Decimal?displayProperty=nameWithType> 형식의 전체 자릿수보다 훨씬 적습니다. 이 때문에 데이터베이스에 데이터를 저장할 때 전체 자릿수가 손실될 수 있습니다. 그러나 SQL Server의 `DECIMAL` 형식이 30자리 이상으로 구성된 경우에는 그 반대의 결과가 발생할 수 있습니다. SQL Server `DECIMAL` 형식의 전체 자릿수가 CLR <xref:System.Decimal?displayProperty=nameWithType>의 전체 자릿수보다 크게 구성된 경우 데이터베이스에서 데이터를 검색할 때 전체 자릿수가 손실될 수 있습니다.  
  
 CLR `MONEY` 형식과 기본적으로 쌍을 이루는 SQL Server `SMALLMONEY` 및 <xref:System.Decimal?displayProperty=nameWithType> 형식도 전체 자릿수가 훨씬 적기 때문에 데이터베이스에 데이터를 저장할 때 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다.  
  
<a name="TextMapping"></a>   
## <a name="text-and-xml-mapping"></a>텍스트 및 XML 매핑  
 LINQ to SQL에서는 여러 텍스트 기반 형식 및 XML 형식을 매핑할 수도 있습니다. 다음 표에는 데이터베이스를 기초로 개체 모델 또는 외부 매핑 파일을 빌드할 때 O/R 디자이너와 SQLMetal에서 선택하는 CLR 형식이 나와 있습니다.  
  
|SQL Server 형식|O/R 디자이너 및 SQLMetal에서 사용하는 기본 CLR 형식 매핑|  
|---------------------|-----------------------------------------------------------------|  
|`CHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`VARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NVARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`TEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`NTEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`XML`|<xref:System.Xml.Linq.XElement?displayProperty=nameWithType>|  
  
 다음 표에는 개체 모델 또는 외부 매핑 파일에 정의된 CLR 형식에 매핑되도록 만들 SQL 열의 형식을 정의하기 위해 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 사용하는 기본 형식 매핑이 나와 있습니다.  
  
|CLR 형식|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>에서 사용하는 기본 SQL Server 형식|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Char?displayProperty=nameWithType>|`NCHAR(1)`|  
|<xref:System.String?displayProperty=nameWithType>|`NVARCHAR(4000)`|  
|<xref:System.Char?displayProperty=nameWithType>[]|`NVARCHAR(4000)`|  
|`Parse()` 및 `ToString()`을 구현하는 사용자 지정 형식|`NVARCHAR(MAX)`|  
  
 이 외에도 여러 가지 텍스트 기반 및 XML 매핑을 선택할 수 있지만 일부의 경우에는 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다. 자세한 내용은 [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)를 참조 하세요.  
  
### <a name="xml-types"></a>XML 형식  
 SQL Server `XML` 데이터 형식은 Microsoft SQL Server 2005부터 사용할 수 있습니다. SQL Server `XML` 데이터 형식은 <xref:System.Xml.Linq.XElement>, <xref:System.Xml.Linq.XDocument> 또는 <xref:System.String>에 매핑할 수 있습니다. <xref:System.Xml.Linq.XElement>로 읽어 들일 수 없는 XML 조각이 열에 저장된 경우 런타임 오류를 방지하기 위해 해당 열을 <xref:System.String>에 매핑해야 합니다. <xref:System.String>에 매핑해야 하는 XML 조각은 다음과 같습니다.  
  
- XML 요소의 시퀀스  
  
- 특성  
  
- PI(공용 식별자)  
  
- 주석  
  
 <xref:System.Xml.Linq.XElement> [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)와 같이 및 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> <xref:System.Xml.Linq.XDocument> 를 SQL Server에 매핑할 수 있지만이 메서드에는 이러한 형식에 대 한 기본 SQL Server 형식 매핑이 없습니다.  
  
### <a name="custom-types"></a>사용자 지정 형식  
 클래스가 `Parse()` 및 `NVARCHAR``CHAR` `NCHAR` `TEXT` `VARCHAR` `XML` `NTEXT`를 구현 하는 경우 개체를 모든 SQL 텍스트 형식 (,,,,,,)에 매핑할 수 있습니다. `ToString()` 개체는 `ToString()`에서 반환하는 값을 매핑된 데이터베이스 열에 전송함으로써 데이터베이스에 저장되고, 데이터베이스에서 반환하는 문자열에 대해 `Parse()`를 호출함으로써 다시 생성됩니다.  
  
> [!NOTE]
> LINQ to SQL에서 <xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType>을 사용한 serialization은 지원되지 않습니다.  
  
<a name="DateMapping"></a>   
## <a name="date-and-time-mapping"></a>날짜 및 시간 매핑  
 LINQ to SQL을 사용하면 여러 SQL Server 날짜 및 시간 형식을 매핑할 수 있습니다. 다음 표에는 데이터베이스를 기초로 개체 모델 또는 외부 매핑 파일을 빌드할 때 O/R 디자이너와 SQLMetal에서 선택하는 CLR 형식이 나와 있습니다.  
  
|SQL Server 형식|O/R 디자이너 및 SQLMetal에서 사용하는 기본 CLR 형식 매핑|  
|---------------------|-----------------------------------------------------------------|  
|`SMALLDATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME2`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIMEOFFSET`|<xref:System.DateTimeOffset?displayProperty=nameWithType>|  
|`DATE`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`TIME`|<xref:System.TimeSpan?displayProperty=nameWithType>|  
  
 다음 표에는 개체 모델 또는 외부 매핑 파일에 정의된 CLR 형식에 매핑되도록 만들 SQL 열의 형식을 정의하기 위해 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 사용하는 기본 형식 매핑이 나와 있습니다.  
  
|CLR 형식|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>에서 사용하는 기본 SQL Server 형식|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.DateTime?displayProperty=nameWithType>|`DATETIME`|  
|<xref:System.DateTimeOffset?displayProperty=nameWithType>|`DATETIMEOFFSET`|  
|<xref:System.TimeSpan?displayProperty=nameWithType>|`TIME`|  
  
 이 외에도 여러 가지 날짜 및 시간 매핑을 선택할 수 있지만 일부의 경우에는 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다. 자세한 내용은 [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)를 참조 하세요.  
  
> [!NOTE]
> SQL Server 형식 `DATETIME2`, `DATETIMEOFFSET`, `DATE` 및 `TIME`은 Microsoft SQL Server 2008부터 사용할 수 있습니다. LINQ to SQL에서는 .NET Framework 버전 3.5 SP1부터 이러한 새로운 형식의 매핑이 지원됩니다.  
  
### <a name="systemdatetime"></a>System.Datetime  
 CLR <xref:System.DateTime?displayProperty=nameWithType> 형식의 범위 및 전체 자릿수는 `DATETIME` 메서드의 기본 형식 매핑인 SQL Server <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 형식의 범위 및 전체 자릿수보다 큽니다. `DATETIME`의 범위를 벗어나는 날짜와 관련된 예외가 발생하지 않도록 하려면 Microsoft SQL Server 2008부터 사용할 수 있는 `DATETIME2`를 사용하세요. `DATETIME2`는 CLR <xref:System.DateTime?displayProperty=nameWithType>의 범위 및 전체 자릿수와 일치할 수 있습니다.  
  
 SQL Server 날짜에는 CLR에서 지원되는 기능인 <xref:System.TimeZone> 개념이 없습니다. 원래 <xref:System.TimeZone> 정보에 관계없이 <xref:System.TimeZone> 값은 <xref:System.DateTimeKind> 변환 없이 데이터베이스에 있는 그대로 저장됩니다. <xref:System.DateTime> 값이 데이터베이스에서 검색될 경우 해당 값은 <xref:System.DateTime>가 <xref:System.DateTimeKind>로 지정되어 <xref:System.DateTimeKind.Unspecified>에 있는 그대로 로드됩니다. 지원 되 <xref:System.DateTime?displayProperty=nameWithType> 는 메서드에 대 한 자세한 내용은 [system.web 메서드](system-datetime-methods.md)를 참조 하세요.  
  
### <a name="systemtimespan"></a>System.TimeSpan  
 Microsoft SQL Server 2008 및 .NET Framework 3.5 SP1에서는 CLR <xref:System.TimeSpan?displayProperty=nameWithType> 형식을 SQL Server `TIME` 형식에 매핑할 수 있습니다. 그러나 CLR <xref:System.TimeSpan?displayProperty=nameWithType>에서 지원되는 범위와 SQL Server `TIME` 형식에서 지원되는 범위에는 상당한 차이가 있습니다. 0보다 작거나 23:59:59.9999999시간보다 큰 값을 SQL `TIME`에 매핑하면 오버플로 예외가 발생합니다. 자세한 내용은 [Timespan.zero 메서드](system-timespan-methods.md)를 참조 하세요.  
  
 Microsoft SQL Server 2000 및 SQL Server 2005에서는 데이터베이스 필드를 <xref:System.TimeSpan>에 매핑할 수 없습니다. 그러나 <xref:System.TimeSpan> 값은 <xref:System.TimeSpan> 빼기에서 반환되거나 리터럴 또는 바인딩된 변수로 식에 삽입될 수 있기 때문에 <xref:System.DateTime>에 대한 연산은 지원됩니다.  
  
<a name="BinaryMapping"></a>   
## <a name="binary-mapping"></a>이진 매핑  
 여러 SQL Server 형식을 CLR <xref:System.Data.Linq.Binary?displayProperty=nameWithType> 형식에 매핑할 수 있습니다. 다음 표에는 데이터베이스를 기초로 개체 모델 또는 외부 매핑 파일을 빌드할 때 O/R 디자이너와 SQLMetal에서 CLR <xref:System.Data.Linq.Binary?displayProperty=nameWithType> 형식을 정의하는 SQL Server 형식이 나와 있습니다.  
  
|SQL Server 형식|O/R 디자이너 및 SQLMetal에서 사용하는 기본 CLR 형식 매핑|  
|---------------------|-----------------------------------------------------------------|  
|`BINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(MAX)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(MAX)``FILESTREAM` 특성 사용|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`IMAGE`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`TIMESTAMP`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
  
 다음 표에는 개체 모델 또는 외부 매핑 파일에 정의된 CLR 형식에 매핑되도록 만들 SQL 열의 형식을 정의하기 위해 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 사용하는 기본 형식 매핑이 나와 있습니다.  
  
|CLR 형식|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>에서 사용하는 기본 SQL Server 형식|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Byte?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Runtime.Serialization.ISerializable?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
  
 이 외에도 여러 가지 이진 매핑을 선택할 수 있지만 일부의 경우에는 데이터베이스 관련 변환 과정에서 오버플로 또는 데이터 손실 예외가 발생할 수 있습니다. 자세한 내용은 [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)를 참조 하세요.  
  
### <a name="sql-server-filestream"></a>SQL Server FILESTREAM  
 `FILESTREAM` 열의 `VARBINARY(MAX)` 특성은 Microsoft SQL Server 2008부터 사용할 수 있으며 .NET Framework 버전 3.5 SP1부터 LINQ to SQL을 사용하여 매핑할 수 있습니다.  
  
 `VARBINARY(MAX)` 개체에 `FILESTREAM` 특성이 있는 <xref:System.Data.Linq.Binary> 열을 매핑할 수는 있지만 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 `FILESTREAM` 특성이 있는 열을 자동으로 생성할 수는 없습니다. 에 대 한 `FILESTREAM`자세한 내용은 Microsoft SQL Server 온라인 설명서의 [FILESTREAM 개요](https://go.microsoft.com/fwlink/?LinkId=115291) 를 참조 하세요.  
  
<a name="BinarySerialization"></a>   
### <a name="binary-serialization"></a>이진 Serialization  
 클래스에서 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하는 경우 개체를 모든 SQL 이진 필드(`BINARY`, `VARBINARY`, `IMAGE`)로 serialize할 수 있습니다. 개체는 <xref:System.Runtime.Serialization.ISerializable> 인터페이스가 구현되는 방법에 따라 serialize 및 deserialize됩니다. 자세한 내용은 [이진 Serialization](https://go.microsoft.com/fwlink/?LinkId=115581)합니다.  
  
<a name="MiscMapping"></a>   
## <a name="miscellaneous-mapping"></a>기타 매핑  
 다음 표에서는 위에서 언급하지 않은 기타 형식의 기본 형식 매핑을 보여 줍니다. 다음 표에는 데이터베이스를 기초로 개체 모델 또는 외부 매핑 파일을 빌드할 때 O/R 디자이너와 SQLMetal에서 선택하는 CLR 형식이 나와 있습니다.  
  
|SQL Server 형식|O/R 디자이너 및 SQLMetal에서 사용하는 기본 CLR 형식 매핑|  
|---------------------|-----------------------------------------------------------------|  
|`UNIQUEIDENTIFIER`|<xref:System.Guid?displayProperty=nameWithType>|  
|`SQL_VARIANT`|<xref:System.Object?displayProperty=nameWithType>|  
  
 다음 표에는 개체 모델 또는 외부 매핑 파일에 정의된 CLR 형식에 매핑되도록 만들 SQL 열의 형식을 정의하기 위해 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 메서드에서 사용하는 기본 형식 매핑이 나와 있습니다.  
  
|CLR 형식|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType>에서 사용하는 기본 SQL Server 형식|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Guid?displayProperty=nameWithType>|`UNIQUEIDENTIFIER`|  
|<xref:System.Object?displayProperty=nameWithType>|`SQL_VARIANT`|  
  
 LINQ to SQL에서는 이러한 기타 형식에 대해 여기에 나와 있는 것 이외의 형식 매핑은 지원하지 않습니다.  자세한 내용은 [형식 매핑 런타임 동작 매트릭스](#BehaviorMatrix)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [특성 기반 매핑](attribute-based-mapping.md)
- [외부 매핑](external-mapping.md)
- [데이터 형식 및 함수](data-types-and-functions.md)
- [SQL-CLR 형식 불일치](sql-clr-type-mismatches.md)
