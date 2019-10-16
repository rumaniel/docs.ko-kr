---
title: SQL Server 이진 및 큰 값 데이터
ms.date: 03/30/2017
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.openlocfilehash: 4d941ad6b7865112b45fd8c20ad89e9236e17b9d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791678"
---
# <a name="sql-server-binary-and-large-value-data"></a>SQL Server 이진 및 큰 값 데이터
SQL Server에서는 `max`, `varchar` 및 `nvarchar` 데이터 형식의 스토리지 용량을 확장하는 `varbinary` 지정자를 지원합니다. `varchar(max)`, `nvarchar(max)`및를 `varbinary(max)` 통칭 하 여 *대량 값 데이터 형식*이라고 합니다. 큰 값 데이터 형식을 사용하면 데이터를 최대 2^31-1바이트까지 저장할 수 있습니다.  
  
 SQL Server 2008에서는 데이터 형식은 아니고 열에 정의할 수 있는 특성인 FILESTREAM 특성을 지원합니다. 이 특성을 사용하면 큰 값 데이터를 데이터베이스가 아니라 파일 시스템에 저장할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ADO.NET에서 큰 값(최대값) 데이터 수정](modifying-large-value-max-data.md)  
 큰 값 데이터 형식을 사용하는 방법을 설명합니다.  
  
 [FILESTREAM 데이터](filestream-data.md)  
 FILESTREAM 특성을 사용하여 SQL Server 2008에 저장된 큰 값 데이터로 작업하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 데이터 형식 및 ADO.NET](sql-server-data-types.md)
- [ADO.NET에서 SQL Server 데이터 작업](sql-server-data-operations.md)
- [ADO.NET에서 데이터 검색 및 수정](../retrieving-and-modifying-data.md)
- [ADO.NET 개요](../ado-net-overview.md)
