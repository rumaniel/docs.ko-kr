---
title: Entity FrameworkTypes용 SqlClient
ms.date: 03/30/2017
ms.assetid: f2a95ead-c845-4e97-9fb3-04b444f7ed81
ms.openlocfilehash: af3a4eea08dd3f4e1a134fcb66d92bc4a3b077c7
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248376"
---
# <a name="sqlclient-for-entity-frameworktypes"></a>Entity FrameworkTypes용 SqlClient
.NET Framework Data Provider for SQL Server(SqlClient) 공급자 매니페스트 파일에는 공급자 기본 형식의 목록, 각 형식의 패싯, 개념적 모델과 스토리지 모델 기본 형식 간의 매핑, 개념적 모델과 스토리지 모델 기본 형식 간의 승격과 변환 규칙이 포함되어 있습니다.  
  
 다음 표에서는 SQL Server 2008, SQL Server 2005 및 SQL Server 2000 데이터베이스의 형식과 이러한 형식을 개념적 모델 형식에 매핑하는 방법에 대해 설명 합니다. 이후 버전의 SQL Server에서 도입된 몇 가지 새로운 형식은 이전 버전의 SQL Server에서는 지원되지 않습니다. 해당 형식은 다음 표에 나와 있습니다.  
  
|공급자 형식<br /><br /> name|공급자 형식<br /><br /> 특성|`EDMSimpleType`<br /><br /> name|패싯|  
|----------------------------|----------------------------------|------------------------------|------------|  
|`bit`|n/a|`Edm.Boolean`|n/a|  
|`tinyint`|n/a|`Edm.Byte`|n/a|  
|`smallint`|n/a|`Edm.Int16`|n/a|  
|`int`|n/a|`Edm.Int32`|n/a|  
|`bigint`|n/a|`Edm.Int64`|n/a|  
|`float`|n/a|`Edm.Double`|n/a|  
|`real`|n/a|`Edm.Double`|n/a|  
|`decimal`|n/a|`Edm.Decimal`|소수<br /><br /> 최대 1<br /><br /> 최대화 38<br /><br /> 기본 18<br /><br /> 상시 거짓<br /><br /> 배율을<br /><br /> 최대 0<br /><br /> 최대화 38<br /><br /> 기본 0<br /><br /> 상시 거짓|  
|`numeric`|n/a|`Edm.Decimal`|소수<br /><br /> 최대 1<br /><br /> 최대화 38<br /><br /> 기본 18<br /><br /> 상시 거짓<br /><br /> 배율을<br /><br /> 최대 0<br /><br /> 최대화 38<br /><br /> 기본 0<br /><br /> 상시 거짓|  
|`smallmoney`|n/a|`Edm.Decimal`|소수<br /><br /> 기본 10<br /><br /> 상시 True<br /><br /> 배율을<br /><br /> 기본 4<br /><br /> 상시 True|  
|`money`|n/a|`Edm.Decimal`|소수<br /><br /> 기본 19<br /><br /> 상시 True<br /><br /> 배율을<br /><br /> 기본 4<br /><br /> 상시 True|  
|`binary`|n/a|`Edm.Binary`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 8000<br /><br /> 기본 8000<br /><br /> 상시 거짓<br /><br /> FixedLength:<br /><br /> 기본 True<br /><br /> 상시 True|  
|`varbinary`|n/a|`Edm.Binary`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 8000<br /><br /> 기본 8000<br /><br /> 상시 거짓<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`varbinary(max)`<br /><br /> 참고: 이 형식은 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.Binary`|MaxLength:<br /><br /> 기본 214748364780<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`image`|n/a|`Edm.Binary`|MaxLength:<br /><br /> 기본 2147483647<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`timestamp`|n/a|`Edm.Binary`|MaxLength:<br /><br /> 기본 8<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 True<br /><br /> 상시 True|  
|`rowversion`|n/a|`Edm.Binary`|MaxLength:<br /><br /> 기본 8<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 True<br /><br /> 상시 True|  
|`smalldatetime`|n/a|`Edm.DateTime`|소수<br /><br /> 기본 0<br /><br /> 상시 True|  
|`datetime`|n/a|`Edm.DateTime`|소수<br /><br /> 기본 3<br /><br /> 상시 True|  
|`date`<br /><br /> 참고: 이 형식은 SQL Server 2005 및 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.DateTime`|소수<br /><br /> 기본 0<br /><br /> 상시 거짓|  
|`time`<br /><br /> 참고: 이 형식은 SQL Server 2005 및 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.Time`|소수<br /><br /> 기본 7<br /><br /> 상시 거짓|  
|`datetime2`<br /><br /> 참고: 이 형식은 SQL Server 2005 및 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.DateTime`|소수<br /><br /> 기본 7<br /><br /> 상시 거짓|  
|`datetimeoffset`<br /><br /> 참고: 이 형식은 SQL Server 2005 및 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.DateTimeOffset`|소수<br /><br /> 기본 7<br /><br /> 상시 거짓|  
|`nvarchar`<br /><br /> 참고: 이 형식은 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.String`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 4000<br /><br /> 기본 4000<br /><br /> 상시 거짓<br /><br /> 유니코드:<br /><br /> 기본 True<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`varchar`<br /><br /> 참고: 이 형식은 SQL Server 2000에서 지원 되지 않습니다.|n/a|`Edm.String`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 8000<br /><br /> 기본 8000<br /><br /> 상시 거짓<br /><br /> 유니코드:<br /><br /> 기본 거짓<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`char`|n/a|`Edm.String`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 8000<br /><br /> 기본 8000<br /><br /> 상시 거짓<br /><br /> 유니코드:<br /><br /> 기본 거짓<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 True<br /><br /> 상시 True|  
|`nchar`|n/a|`Edm.String`|MaxLength:<br /><br /> 최대 1<br /><br /> 최대화 4000<br /><br /> 기본 4000<br /><br /> 상시 거짓<br /><br /> 유니코드:<br /><br /> 기본 True<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 True<br /><br /> 상시 True|  
|`varchar`(`max`)|n/a|`Edm.String`|MaxLength:<br /><br /> 기본 2147483647<br /><br /> 상시 True<br /><br /> 유니코드:<br /><br /> 기본 거짓<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`nvarchar`(`max`)|n/a|`Edm.String`|MaxLength:<br /><br /> 기본 1073741823<br /><br /> 상시 True<br /><br /> 유니코드:<br /><br /> 기본 True<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`ntext`|같음 비교 가능: 거짓<br /><br /> 순서 비교 가능: 거짓|`Edm.String`|MaxLength:<br /><br /> 기본 1073741823<br /><br /> 상시 True<br /><br /> 유니코드:<br /><br /> 기본 거짓<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`text`|같음 비교 가능: 거짓<br /><br /> 순서 비교 가능: 거짓|`Edm.String`|MaxLength:<br /><br /> 기본 2147483647<br /><br /> 상시 True<br /><br /> 유니코드:<br /><br /> 기본 거짓<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
|`Unique`<br /><br /> `identifier`|같음 비교 가능: True<br /><br /> 순서 비교 가능: True|`Edm.Guid`|n/a|  
|`xml`|같음 비교 가능: 거짓<br /><br /> 순서 비교 가능: 거짓|`Edm.String`|MaxLength:<br /><br /> 기본 1073741823<br /><br /> 상시 True<br /><br /> 유니코드:<br /><br /> 기본 True<br /><br /> 상시 True<br /><br /> FixedLength:<br /><br /> 기본 거짓<br /><br /> 상시 True|  
  
## <a name="see-also"></a>참고자료

- [CSDL, SSDL 및 MSL 사양](./language-reference/csdl-ssdl-and-msl-specifications.md)
