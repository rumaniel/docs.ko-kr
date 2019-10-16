---
title: LocalDB에 대한 SqlClient 지원
ms.date: 03/30/2017
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.openlocfilehash: d02524cd5901adeca7bc36d6fd13c7abdc46c69b
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894407"
---
# <a name="sqlclient-support-for-localdb"></a>LocalDB에 대한 SqlClient 지원
SQL Server 코드 이름 Denali 부터는 LocalDB 라고 하는 경량 버전의 SQL Server를 사용할 수 있습니다. 이 항목에서는 LocalDB 데이터베이스에 연결하는 방법을 설명합니다.  
  
## <a name="remarks"></a>설명  
 Localdb 설치 및 localdb 인스턴스 구성 방법을 비롯 한 LocalDB에 대 한 자세한 내용은 SQL Server 온라인 설명서를 참조 하세요.  
  
 LocalDB로 할 수 있는 작업:  
  
- sqllocaldb.exe 또는 app.config 파일로 LocalDB 인스턴스를 만들고 시작합니다.  
  
- sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정합니다. 예를 들어, `sqlcmd -S (localdb)\myinst`을 입력합니다.  
  
- `AttachDBFilename` 연결 문자열 키워드를 사용하여 데이터베이스를 LocalDB 인스턴스에 추가합니다. `AttachDBFilename`을 사용할 때 `Database` 연결 문자열 키워드에 데이터베이스 이름을 지정하지 않은 응용 프로그램을 닫으면 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.  
  
- 연결 문자열에서 LocalDB 인스턴스를 지정합니다. 예를 들어 인스턴스 이름이 `myInstance`이면 연결 문자열에는 다음이 포함됩니다.  
  
    `server=(localdb)\\myInstance`  
  
 `User Instance=True` 는 LocalDB 데이터베이스에 연결할 때는 사용할 수 없습니다.  
  
 [Microsoft SQL Server 2012 기능 팩](https://www.microsoft.com/download/en/details.aspx?id=29065)에서 LocalDB를 다운로드할 수 있습니다. Sc.exe를 사용 하 여 LocalDB 인스턴스의 데이터를 수정 하는 경우 SQL Server 2012의 sqlcmd가 필요 합니다 .이는 SQL Server 2012 기능 팩 에서도 가져올 수 있습니다.  
  
## <a name="programmatically-create-a-named-instance"></a>프로그래밍 방식으로 명명된 인스턴스 만들기  
 애플리케이션에서는 명명된 인스턴스를 만들고 다음과 같이 데이터베이스를 지정할 수 있습니다.  
  
- 예를 들어 다음과 같이 app.config 파일에 만들 LocalDB 인스턴스를 지정합니다.  인스턴스의 버전 번호는 LocalDB 설치의 버전 번호와 동일해야 합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- `server` 연결 문자열 키워드를 사용하여 인스턴스의 이름을 지정합니다.  `server` 연결 문자열 키워드에 지정된 인스턴스 이름은 app.config 파일에 지정된 이름과 일치해야 합니다.  
  
- `AttachDBFilename` 연결 문자열 키워드를 사용하여 .MDF 파일을 지정합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 기능 및 ADO.NET](sql-server-features-and-adonet.md)
- [ADO.NET 개요](../ado-net-overview.md)
