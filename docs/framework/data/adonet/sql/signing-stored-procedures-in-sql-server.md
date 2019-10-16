---
title: SQL Server에서 저장 프로시저에 서명
ms.date: 01/05/2018
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
ms.openlocfilehash: 8dc62527be7273d3ce3222d4d261b81bc40b1e19
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791805"
---
# <a name="signing-stored-procedures-in-sql-server"></a>SQL Server에서 저장 프로시저에 서명

디지털 설명은 서명자의 프라이빗 키로 암호화된 데이터 다이제스트입니다. 프라이빗 키를 사용하면 디지털 서명이 소유자별로 고유하게 유지됩니다. 저장 프로시저, 함수 (인라인 테이블 반환 함수 제외), 트리거 및 어셈블리에 서명할 수 있습니다.

인증서나 비대칭 키를 사용하여 저장 프로시저에 서명할 수 있습니다. 이 기능은 권한을 소유권 체인을 통해 상속할 수 없거나 동적 SQL과 같이 소유권 체인이 끊어진 시나리오를 위해 디자인되었습니다. 그런 다음 인증서에 매핑된 사용자를 만들어 저장 프로시저에서 액세스 해야 하는 개체에 대 한 인증서 사용자 권한을 부여할 수 있습니다.

동일한 인증서에 매핑된 로그인을 만든 다음이 로그인에 필요한 서버 수준 사용 권한을 부여 하거나 하나 이상의 고정 서버 역할에 로그인을 추가할 수도 있습니다. 이는 더 높은 수준의 권한이 필요한 `TRUSTWORTHY` 시나리오에 대 한 데이터베이스 설정을 사용 하지 않도록 하기 위한 것입니다.

저장 프로시저를 실행 하면 SQL Server는 인증서 사용자 및/또는 로그인의 사용 권한을 호출자의 권한과 결합 합니다. `EXECUTE AS` 절과 달리 프로시저의 실행 컨텍스트는 변경 되지 않습니다. 로그인과 사용자 이름을 반환하는 기본 제공 함수는 인증서 사용자 이름이 아니라 호출자의 이름을 반환합니다.

## <a name="creating-certificates"></a>인증서 만들기

인증서 나 비대칭 키를 사용 하 여 저장 프로시저에 서명 하는 경우 실행 사용자와 함께 저장 프로시저 코드의 암호화 된 해시로 구성 된 데이터 다이제스트가 개인 키를 사용 하 여 만들어집니다. 런타임에 데이터 다이제스트는 공개 키로 암호 해독되어 저장 프로시저의 해시 값과 비교됩니다. Execute as user를 변경 하면 디지털 서명이 더 이상 일치 하지 않도록 해시 값이 무효화 됩니다. 저장 프로시저를 수정 하면 서명이 완전히 삭제 되므로 개인 키에 대 한 액세스 권한이 없는 사용자가 저장 프로시저 코드를 변경할 수 없습니다. 두 경우 모두 코드 또는 실행 사용자를 변경할 때마다 프로시저에 다시 서명 해야 합니다.

모듈에 서명 하는 데는 다음과 같은 두 가지 필수 단계가 있습니다.

1. Transact-SQL `CREATE CERTIFICATE [certificateName]` 문을 사용하여 인증서를 만듭니다. 이 문에는 시작 및 종료 날짜와 암호를 설정하기 위한 몇 가지 옵션이 있습니다. 기본 만료 날짜는 1 년입니다.

1. Transact-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` 문을 사용하여 프로시저에 인증서로 서명합니다.

모듈이 서명 되 면 인증서와 연결 되어야 하는 추가 권한을 보유 하기 위해 하나 이상의 보안 주체를 만들어야 합니다.

모듈에 추가 데이터베이스 수준 사용 권한이 필요한 경우:

1. Transact-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]` 문을 사용하여 해당 인증서와 연결된 데이터베이스 사용자를 만듭니다. 이 사용자는 데이터베이스에만 존재 하며 동일한 인증서에서 로그인을 만들지 않은 경우 로그인과 연결 되지 않습니다.

1. 필요한 데이터베이스 수준 사용 권한을 인증서 사용자에 게 부여 합니다.

모듈에 추가 서버 수준 사용 권한이 필요한 경우:

1. 인증서를 `master` 데이터베이스에 복사 합니다.

1. Transact-sql `CREATE LOGIN [userName] FROM CERTIFICATE [certificateName]` 문을 사용 하 여 해당 인증서와 연결 된 로그인을 만듭니다.

1. 인증서 로그인에 필요한 서버 수준 사용 권한을 부여 합니다.

> [!NOTE]
> 인증서는 DENY 문을 사용하여 호출된 권한을 가진 사용자에게 권한을 부여할 수 없습니다. DENY는 항상 GRANT보다 높은 우선 순위를 갖기 때문에 호출자가 인증서 사용자에게 부여된 권한을 상속 받지 않도록 방지합니다.

## <a name="external-resources"></a>외부 리소스

자세한 내용은 다음 리소스를 참조하세요.

|리소스|설명|
|--------------|-----------------|
|[모듈 로그인](https://go.microsoft.com/fwlink/?LinkId=98590) SQL Server 온라인 설명서|모듈 서명을 설명하고 샘플 시나리오 및 관련 Transact-SQL 항목 링크를 제공합니다.|
|SQL Server 온라인 설명서에서 [인증서를 사용 하 여 저장 프로시저 서명](/sql/relational-databases/tutorial-signing-stored-procedures-with-a-certificate)|인증서로 저장 프로시저에 서명하는 방법에 대한 자습서를 제공합니다.|

## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 저장 프로시저를 사용하여 권한 관리](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server에서 동적 보안 SQL 작성](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)
- [저장 프로시저로 데이터 수정](../modifying-data-with-stored-procedures.md)
- [ADO.NET 개요](../ado-net-overview.md)
