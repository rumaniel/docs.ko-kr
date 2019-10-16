---
title: 명령을 사용하여 데이터 수정
ms.date: 03/30/2017
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.openlocfilehash: 34c73549f18cd4bebb8caf842b252828b7f0a185
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780566"
---
# <a name="using-commands-to-modify-data"></a>명령을 사용하여 데이터 수정
.NET Framework 데이터 공급자를 사용하여 저장 프로시저나 CREATE TABLE 및 ALTER COLUMN과 같은 데이터 정의 언어 문을 실행하여 데이터베이스 또는 카탈로그의 스키마를 조작할 수 있습니다. 이러한 명령은 행을 쿼리로 반환 하지 않으므로 **Command** 개체는이를 처리 하는 **ExecuteNonQuery** 을 제공 합니다.  
  
 **ExecuteNonQuery** 를 사용 하 여 스키마를 수정 하는 것 외에도이 메서드를 사용 하 여 데이터를 수정 하지만 행을 반환 하지 않는 SQL 문 (예: 삽입, 업데이트 및 삭제)을 처리할 수 있습니다.  
  
 **ExecuteNonQuery** 메서드는 행을 반환 하지 않지만 **Command** 개체의 **parameters** 컬렉션을 통해 입력 및 출력 매개 변수와 반환 값을 전달 하 고 반환할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 원본에서 데이터 업데이트](updating-data-in-a-data-source.md)  
 데이터베이스의 데이터를 수정하는 명령 또는 저장 프로시저를 실행하는 방법을 설명합니다.  
  
 [카탈로그 작업 수행](performing-catalog-operations.md)  
 데이터베이스 스키마를 수정하는 명령을 실행하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [명령 및 매개 변수](commands-and-parameters.md)
- [ADO.NET 개요](ado-net-overview.md)
