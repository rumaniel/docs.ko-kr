---
title: 컨텍스트 연결
ms.date: 03/30/2017
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.openlocfilehash: 26578d0c6a5e4553e57673561f94090b9a1fd1a5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791503"
---
# <a name="the-context-connection"></a>컨텍스트 연결
내부 데이터 액세스 문제는 매우 일반적인 시나리오입니다. 즉, CLR(공용 언어 런타임) 저장 프로시저나 함수가 실행 중인 서버와 동일한 서버에 액세스하려는 상황을 말합니다. 한 가지 옵션은 <xref:System.Data.SqlClient.SqlConnection>을 사용하여 연결을 만들고 로컬 서버를 가리키는 연결 문자열을 지정한 다음 연결을 여는 것입니다. 이를 수행하려면 로그인에 사용할 자격 증명을 지정해야 합니다. 이 경우 연결이 저장 프로시저나 함수가 아닌 다른 데이터베이스 세션에서 이루어지거나, `SET` 옵션이 서로 다르거나, 연결이 개별 트랜잭션에서 이루어지거나, 임시 테이블에 나타나지 않는 등의 상황이 발생합니다. 관리되는 저장 프로시저나 함수 코드가 SQL Server 프로세스에서 실행되면 해당 서버에 연결된 누군가가 SQL 문을 실행하여 이를 호출했기 때문입니다. 대개는 저장 프로시저나 함수가 해당 연결의 컨텍스트에서 해당 트랜잭션, `SET` 옵션 등과 함께 실행되기를 원할 것입니다. 이를 컨텍스트 연결이라고 합니다.  
  
 컨텍스트 연결을 사용하면 Transact-SQL 문을 처음 코드를 호출한 곳과 동일한 컨텍스트에서 실행할 수 있습니다. 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
1. [컨텍스트 연결](https://go.microsoft.com/fwlink/?LinkId=115395)  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
