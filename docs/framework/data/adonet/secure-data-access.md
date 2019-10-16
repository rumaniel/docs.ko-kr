---
title: 보안 데이터 액세스
ms.date: 03/30/2017
ms.assetid: 473ebd69-21a3-4627-b95e-4e04d035c56f
ms.openlocfilehash: 122bdaf8467994f8f56ce3f6c92457be6b8b3155
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782767"
---
# <a name="secure-data-access"></a>보안 데이터 액세스
보안 ADO.NET 코드를 쓰려면 내부 데이터 저장소 또는 데이터베이스에서 사용할 수 있는 보안 메커니즘을 알아야 합니다. 또한, 애플리케이션에 포함된 다른 기능이나 구성 요소의 보안 문제도 고려해야 합니다.  
  
## <a name="authentication-authorization-and-permissions"></a>인증, 권한 부여 및 사용 권한  
 Microsoft SQL Server에 연결하는 경우에는 Windows 인증, 즉 소위 말하는 통합 보안을 사용할 수 있습니다. 이 경우 사용자 ID와 암호가 전달되는 것이 아니라 현재 활성 Windows 사용자의 ID가 사용됩니다. Windows 인증은 사용자 자격 증명이 연결 문자열에 노출되지 않기 때문에 적극 권장되는 방식입니다. Windows 인증을 사용하여 SQL Server에 연결할 수 없는 경우에는 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>를 사용하여 런타임에 연결 문자열을 만드는 방법을 고려해 보세요.  
  
 인증에 사용되는 자격 증명은 애플리케이션의 종류에 따라 다르게 처리해야 합니다. 예를 들어, Windows Forms 애플리케이션에서는 인증 정보를 입력하라는 메시지가 표시되거나 사용자의 Windows 자격 증명이 사용될 수 있습니다. 그러나 웹 애플리케이션의 경우 주로 사용자 입력을 통해서가 아닌 애플리케이션에서 제공하는 자격 증명을 사용하여 데이터에 액세스합니다.  
  
 인증된 후 사용자가 수행할 수 있는 작업의 범위는 각자에게 부여된 권한에 따라 다릅니다. 항상 최소 권한의 원칙에 따라 꼭 필요한 권한만 부여해야 합니다.  
  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[연결 정보 보호](protecting-connection-information.md)|보호되는 구성을 사용하여 연결 문자열을 암호화하는 것과 같이 연결 정보를 보호하는 기술과 최상의 보안 방법에 대해 설명합니다.|  
|[데이터 액세스 전략에 대 한 권장 사항](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))|데이터 액세스 및 데이터베이스 작업 수행에 대한 권장 방법을 제공합니다.|  
|[연결 문자열 작성기](connection-string-builders.md)|런타임에 사용자 입력을 기반으로 연결 문자열을 만드는 방법에 대해 설명합니다.|  
|[SQL Server 보안 개요](./sql/overview-of-sql-server-security.md)|SQL Server 보안 아키텍처에 대해 설명합니다.|  
  
## <a name="parameterized-commands-and-sql-injection"></a>매개 변수화된 명령 및 SQL 삽입  
 매개 변수화된 명령을 사용하면 공격자가 SQL 문에 명령을 삽입하여 서버의 보안을 손상시키는 SQL 삽입 공격을 막을 수 있습니다. 매개 변수화된 명령에서는 외부 소스에서 가져온 값이 Transact-SQL 문의 일부가 아닌 값으로만 전달되도록 하여 SQL 삽입 공격으로부터 보호합니다. 따라서 값에 삽입된 Transact-SQL 명령이 데이터 소스에서 실행되지 않으며 매개 변수 값으로만 평가됩니다. 매개 변수화된 명령은 이러한 보안상의 장점뿐만 아니라 Transact-SQL 문과 함께 전달되거나 저장 프로시저에 전달되는 값을 구성할 수 있는 편리한 방법을 제공합니다.  
  
 매개 변수화된 명령 사용에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|설명|  
|--------------|-----------------|  
|[DataAdapter 매개 변수](dataadapter-parameters.md)|`DataAdapter`와 함께 매개 변수를 사용하는 방법에 대해 설명합니다.|  
|[저장 프로시저로 데이터 수정](modifying-data-with-stored-procedures.md)|매개 변수를 지정하고 반환 값을 가져오는 방법에 대해 설명합니다.|  
|[SQL Server에서 저장 프로시저를 사용하여 권한 관리](./sql/managing-permissions-with-stored-procedures-in-sql-server.md)|SQL Server 저장 프로시저를 사용하여 데이터 액세스를 캡슐화하는 방법에 대해 설명합니다.|  
  
## <a name="script-exploits"></a>스크립트 악용  
 스크립트 악용은 웹 페이지에 삽입된 악의적 문자를 사용하는 또 다른 형태의 삽입 공격입니다. 브라우저에서는 삽입된 문자의 유효성을 검사하지 않고 문자를 페이지의 일부로 처리합니다.  
  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[스크립트 악용 개요](https://docs.microsoft.com/previous-versions/aspnet/w1sw53ds(v=vs.100))|스크립팅 및 SQL 문 악용으로부터 보호하는 방법에 대해 설명합니다.|  
  
## <a name="probing-attacks"></a>검색 공격  
 공격자는 흔히 예외에서 얻은 서버, 데이터베이스, 테이블 이름 등의 정보를 사용하여 시스템에 대한 공격을 준비합니다. 예외에는 애플리케이션이나 데이터 소스에 대한 특정 정보가 포함될 수 있으므로 클라이언트에 꼭 필요한 정보만 노출함으로써 애플리케이션 및 데이터 소스를 보다 안전하게 보호할 수 있습니다.  
  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[예외 처리 기본 사항](../../../standard/exceptions/exception-handling-fundamentals.md)|try/catch/finally 구조적 예외 처리의 기본 형태에 대해 설명합니다.|  
|[예외에 대한 모범 사례](../../../standard/exceptions/best-practices-for-exceptions.md)|최상의 예외 처리 방법에 대해 설명합니다.|  
  
## <a name="protecting-microsoft-access-and-excel-data-sources"></a>Microsoft Access 및 Excel 데이터 소스 보호  
 보안 요구 사항이 최소 수준이거나 없는 경우 Microsoft Access와 Microsoft Excel을 ADO.NET 애플리케이션의 데이터 스토리지로 사용할 수 있습니다. 두 프로그램의 보안 기능으로 어느 정도의 저지 효과는 볼 수 있지만 무분별한 사용자의 악의적인 장난을 막는 것 이상의 효과는 기대할 수 없습니다. Access 및 Excel의 실제 데이터 파일은 파일 시스템에 존재하며 모든 사용자가 액세스할 수 있습니다. 따라서 파일을 복사하거나 변경하기가 쉬워 도난이나 데이터 손실을 야기하는 공격에 취약합니다. 강력한 보안이 필요한 경우에는 파일 시스템에서 실제 데이터 파일을 읽을 수 없는 SQL Server나 다른 서버 기반 데이터베이스를 사용해야 합니다.  
  
 Access 및 Excel 데이터 보호에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|설명|  
|--------------|-----------------|  
|[보안 고려 사항 및 액세스 2007에 대 한 지침](https://go.microsoft.com/fwlink/?LinkId=98354)|파일 암호화, 암호 관리, 새로운 ACCDB 및 ACCDE 형식으로 데이터베이스 변환, 기타 보안 옵션 사용 등 Access 2007의 보안 기술에 대해 설명합니다.|  
|[액세스 보안에서 작업 그룹 정보 파일의 역할 이해](https://support.microsoft.com/kb/305542)|Access 2003 보안에서 작업 그룹 정보 파일의 역할 및 관계에 대해 설명합니다.|  
|[Microsoft Access 버전 2.0 ~ 2000의 Microsoft Access Security에 대 한 질문과 대답](https://go.microsoft.com/fwlink/?LinkId=47698)|Microsoft Access Security FAQ의 다운로드 버전입니다.|  
## <a name="enterprise-services"></a>엔터프라이즈 서비스  
 COM+에는 Windows NT 계정 및 프로세스/스레드 가장을 사용하는 고유의 보안 모델이 포함되어 있습니다. <xref:System.EnterpriseServices> 네임스페이스에서는 <xref:System.EnterpriseServices.ServicedComponent> 클래스를 통해 .NET 애플리케이션에서 관리 코드를 COM+ 보안 서비스와 통합할 수 있도록 하는 래퍼를 제공합니다.  
  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[역할 기반 보안](https://docs.microsoft.com/previous-versions/dotnet/netframework-1.1/s6y8k15h(v=vs.71))|COM+ 보안 서비스를 사용하여 관리 코드를 통합하는 방법에 대해 설명합니다.|  
  
## <a name="interoperating-with-unmanaged-code"></a>비관리 코드와의 상호 운용  
 .NET Framework는 비관리 코드와의 상호 작용을 위해 COM 구성 요소, COM+ 서비스, 외부 형식 라이브러리, 다양한 운영 체제 서비스 등을 제공합니다. 비관리 코드를 사용하려면 관리 코드에 대한 보안 경계 외부로 나가야 합니다. 코드와 코드를 호출하는 다른 코드 모두에 비관리 코드 권한(<xref:System.Security.Permissions.SecurityPermission> 플래그가 지정된 <xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode>)이 있어야 합니다. 비관리 코드로 인해 애플리케이션에 의도하지 않았던 보안상 취약한 부분이 생길 수 있습니다. 따라서 꼭 필요한 경우가 아니면 비관리 코드와의 상호 운용 작업은 피하는 것이 좋습니다.  
  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[비관리 코드와의 상호 운용](../../interop/index.md)|COM 구성 요소를 .NET Framework에 노출하는 방법과 .NET Framework 구성 요소를 COM에 노출하는 방법에 대해 설명하는 항목을 제공합니다.|
|[고급 COM 상호 운용성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))|주 interop 어셈블리, 스레딩 및 사용자 지정 마샬링 등에 대해 설명하는 고급 항목을 제공합니다.|

## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](securing-ado-net-applications.md)
- [SQL Server 보안](./sql/sql-server-security.md)
- [데이터 액세스 전략에 대 한 권장 사항](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/8fxztkff(v=vs.90))
- [연결 정보 보호](protecting-connection-information.md)
- [연결 문자열 작성기](connection-string-builders.md)
- [ADO.NET 개요](ado-net-overview.md)
