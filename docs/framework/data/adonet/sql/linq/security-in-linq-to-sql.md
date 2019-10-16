---
title: LINQ to SQL의 보안
ms.date: 03/30/2017
ms.assetid: d49787f7-414e-4c71-aa33-80a5895536b1
ms.openlocfilehash: f1ebf2f72fbfe3b27b9fbfd41f0dd65c70103620
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781190"
---
# <a name="security-in-linq-to-sql"></a>LINQ to SQL의 보안
데이터베이스에 연결할 때는 항상 보안 위험이 따릅니다. LINQ to SQL에서는 SQL Server에서 데이터를 사용하는 여러 가지 새로운 방법을 제공하지만 추가적인 보안 메커니즘은 지원하지 않습니다.  
  
## <a name="access-control-and-authentication"></a>액세스 제어 및 인증  
 LINQ to SQL에는 고유의 사용자 모델이나 인증 메커니즘이 없으므로 SQL Server 보안을 사용하여 개체 모델에 매핑되는 데이터베이스, 데이터베이스 테이블, 뷰 및 저장 프로시저에 대한 액세스를 제어해야 합니다. 또한 사용자에게 필수적인 액세스 권한만 최소한으로 부여하고 사용자 인증을 위한 강력한 암호를 설정하도록 요청하세요.  
  
## <a name="mapping-and-schema-information"></a>매핑 및 스키마 정보  
 개체 모델 또는 외부 매핑 파일의 SQL-CLR 형식 매핑 및 데이터베이스 스키마 정보를 사용하여 파일 시스템의 파일에 액세스할 수 있습니다. 개체 모델 또는 외부 매핑 파일에 액세스할 수 있는 모든 사용자가 스키마 정보를 사용할 수 있다고 가정 합니다. 스키마 정보에 대 한 광범위 한 액세스를 방지 하려면 파일 보안 메커니즘을 사용 하 여 소스 파일 및 매핑 파일을 보호 합니다.  
  
## <a name="connection-strings"></a>연결 문자열  
 가능하면 연결 문자열에 암호를 사용하지 않아야 합니다. 개체 관계형 디자이너 또는 SQLMetal 명령줄 도구를 사용하는 경우 연결 문자열은 자체적으로 보안 위험 요소일 뿐 아니라 개체 모델 또는 외부 매핑 파일에 일반 텍스트로 추가될 수도 있습니다. 따라서 파일 시스템을 통해 개체 모델 또는 외부 매핑 파일에 액세스할 수 있는 사용자는 누구든지 연결 문자열에 포함된 연결 암호를 볼 수 있습니다.  
  
 이러한 위험을 최소화 하려면 통합 보안을 사용 하 여 SQL Server와 신뢰할 수 있는 연결을 만듭니다. 이러한 접근 방식을 사용하면 연결 문자열에서 암호를 저장하지 않아도 됩니다. 자세한 내용은 [SQL Server 보안](../sql-server-security.md)을 참조 하세요.  
  
 통합 보안을 사용하지 않는 경우에는 연결 문자열에 일반 텍스트 암호를 사용해야 합니다. 연결 문자열을 보호하는 가장 좋은 방법은 다음과 같습니다. 아래 항목은 위험 수준에 따라 오름차순으로 나열되어 있습니다.  
  
- 통합 보안을 사용합니다.  
  
- 암호를 사용하여 연결 문자열을 보호하고 연결 문자열의 경유를 최소화합니다.  
  
- 연결 문자열 대신 노출 기간이 제한되는 <xref:System.Data.SqlClient.SqlConnection?displayProperty=nameWithType> 클래스를 사용합니다. <xref:System.Data.Linq.DataContext?displayProperty=nameWithType>을 사용하여 LINQ to SQL <xref:System.Data.SqlClient.SqlConnection> 클래스를 인스턴스화할 수 있습니다.  
  
- 모든 연결 문자열의 수명과 접근할 수 있는 지점을 최소화합니다.  
  
## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
- [질문과 대답](frequently-asked-questions.md)
