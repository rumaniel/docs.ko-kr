---
title: .NET Framework Data Provider for Oracle의 시스템 요구 사항
ms.date: 03/30/2017
ms.assetid: 054f76b9-1737-43f0-8160-84a00a387217
ms.openlocfilehash: 664357fb08a6100b8b69d2b4e11edc77cdb81ac7
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833646"
---
# <a name="system-requirements-for-the-net-framework-data-provider-for-oracle"></a>.NET Framework Data Provider for Oracle의 시스템 요구 사항

.NET Framework Data Provider for Oracle에는 MDAC(Microsoft Data Access Components) 버전 2.6 이상이 필요하며 MDAC 2.8 SP1을 사용하는 것이 좋습니다.  
  
 또한 Oracle 8i Release 3(8.1.7) Client 이상이 설치되어 있어야 합니다.  
  
 UTF16은 Oracle 9i에 새로 도입된 기능이므로 Oracle 9i 버전 이전의 Oracle Client 소프트웨어는 UTF16 데이터베이스에 액세스할 수 없습니다. 이 기능을 사용하려면 클라이언트 소프트웨어를 Oracle 9i 이상으로 업그레이드해야 합니다.  
  
## <a name="working-with-the-data-provider-for-oracle-and-unicode-data"></a>Data Provider for Oracle 및 유니코드 데이터 사용  
 
다음은 Oracle 및 Oracle 클라이언트 라이브러리의 .NET Framework Data Provider을 사용할 때 고려해 야 하는 유니코드 관련 문제의 목록입니다. 자세한 내용은 Oracle 설명서를 참조하세요.  
  
### <a name="setting-the-unicode-value-in-a-connection-string-attribute"></a>연결 문자열 특성에 유니코드 값 설정  

Oracle을 사용하는 경우 다음과 같은 연결 문자열 특성을 사용하여  
  
`Unicode=True`
  
UTF-16 모드에서 Oracle 클라이언트 라이브러리를 초기화할 수 있습니다. 이렇게 하면 Oracle 클라이언트 라이브러리에서 멀티바이트 문자열 대신 UCS-2와 매우 유사한 UTF-16을 받아들이게 됩니다. 따라서 Data Provider for Oracle에서 추가 변환 작업 없이도 언제든지 Oracle 코드 페이지를 사용할 수 있습니다. 이 구성은 Oracle 9i 클라이언트를 사용하여 대체 문자 집합 AL16UTF16으로 Oracle 9i 데이터베이스와 통신하는 경우에만 사용할 수 있습니다. Oracle 9i 클라이언트가 Oracle 9i 서버와 통신할 때 유니코드 **CommandText** 값을 Oracle9i 서버에서 사용 하는 적절 한 멀티 바이트 문자 집합으로 변환 하려면 추가 리소스가 필요 합니다. 하지만 연결 문자열에 `Unicode=True`를 추가하여 안전한 구성을 얻게 된다는 사실을 알면 이러한 노력을 피할 수 있습니다.  
  
### <a name="mixing-versions-of-oracle-client-and-oracle-server"></a>혼합 버전의 Oracle 클라이언트 및 Oracle 서버  

서버의 국가별 문자 집합이 AL16UTF16로 지정 된 경우 (Oracle 9i의 기본 설정) oracle 8i 클라이언트는 Oracle 9i 데이터베이스의 **NCHAR**, **NVARCHAR2**또는 **NCLOB** 데이터에 액세스할 수 없습니다. Oracle 9i까지는 UTF-16 문자 집합에 대한 지원이 도입되지 않았기 때문에 Oracle 8i 클라이언트에서는 이를 읽을 수 없습니다.  
  
### <a name="working-with-utf-8-data"></a>UTF-8 데이터 사용  

대체 문자 집합을 설정하려면 레지스트리 키 HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE\HOMEID\NLS_LANG을 UTF8로 설정합니다. 자세한 내용은 플랫폼에서 Oracle 설치 설명을 참조하세요. 기본 설정은 Oracle Client 소프트웨어를 설치하는 언어의 기본 문자 집합입니다. 언어를 연결하는 데이터베이스의 국가별 언어 문자 집합과 일치하도록 설정하지 않으면 매개 변수 및 열 바인딩 과정에 국가별 문자 집합이 아닌 기본 데이터베이스 문자 집합으로 데이터를 주고 받게 됩니다.  
  
### <a name="oraclelob-can-only-update-full-characters"></a>전체 문자만 업데이트할 수 있는 OracleLob  

유용성을 위해 개체는 <xref:System.Data.OracleClient.OracleLob> .NET Framework Stream 클래스에서 상속 하며 **readbyte** 및 **writebyte** 메서드를 제공 합니다. 또한 Oracle **LOB** 개체의 섹션에서 작동 하는 **CopyTo** 및 **Erase**같은 메서드를 구현 합니다. 이와 대조적으로 Oracle 클라이언트 소프트웨어는 문자 **LOB**(**CLOB** 및 **NCLOB**)를 사용 하는 다양 한 api를 제공 합니다. 그러나 이러한 API는 전체 문자에 대해서만 작동합니다. 이러한 차이로 인해 Oracle의 Data Provider는 바이트 단위 방식으로 UTF-16 데이터를 사용 하기 위한 **읽기** 및 **readbyte** 지원을 구현 합니다. 그러나 **OracleLob** 개체의 다른 메서드는 전체 문자 작업만 허용 합니다.  
  
## <a name="see-also"></a>참조

- [Oracle 및 ADO.NET](oracle-and-adonet.md)
- [ADO.NET 개요](ado-net-overview.md)
