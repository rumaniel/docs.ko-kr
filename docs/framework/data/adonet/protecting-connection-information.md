---
title: 연결 정보 보호
ms.date: 03/30/2017
ms.assetid: 1471f580-bcd4-4046-bdaf-d2541ecda2f4
ms.openlocfilehash: 37aab00a967b9912ba01cc3f27f68f8a3e85fdb2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783062"
---
# <a name="protecting-connection-information"></a>연결 정보 보호
애플리케이션 보안의 가장 중요한 목표 중 하나는 데이터 소스에 대한 액세스를 보호하는 것입니다. 연결 문자열을 안전하게 보호하지 않으면 이로 인해 보안상 취약한 부분이 생길 수 있습니다. 연결 정보를 일반 텍스트로 저장하거나 메모리에 유지하면 전체 시스템을 손상시킬 위험이 있습니다. 소스 코드에 포함 된 연결 문자열은 [ildasm.exe (IL 디스어셈블러)](../../tools/ildasm-exe-il-disassembler.md) 를 사용 하 여 읽어서 컴파일된 어셈블리에서 MSIL (Microsoft 중간 언어)을 볼 수 있습니다.  
  
 연결 문자열과 관련된 보안 취약성은 사용된 인증 유형, 연결 문자열을 메모리와 디스크에 유지하는 방법 및 런타임에 연결 문자열을 구성하는 기술에 따라 발생됩니다.  
  
## <a name="use-windows-authentication"></a>Windows 인증 사용  
 데이터 소스에 대한 액세스를 제한하려면 사용자 ID, 암호, 데이터 소스 이름과 같은 연결 정보의 보안을 유지해야 합니다. 사용자 정보를 노출 하지 않으려면 가능 하면 Windows 인증 ( *통합 보안*이 라고도 함)을 사용 하는 것이 좋습니다. Windows 인증은 `Integrated Security` 또는 `Trusted_Connection` 키워드를 사용하여 문자열에 지정되므로 사용자 ID와 암호를 사용할 필요가 없습니다. Windows 인증을 사용하면 사용자는 Windows에서 인증되고 서버 및 데이터베이스 리소스에 대한 액세스는 Windows 사용자 및 그룹에 부여하는 권한에 따라 결정됩니다.  
  
 Windows 인증을 사용할 수 없는 상황에서는 사용자 자격 증명이 연결 문자열에 노출되므로 각별히 유의해야 합니다. ASP.NET 애플리케이션에서 Windows 계정을 고정 ID로 구성하여 데이터베이스 및 기타 네트워크 리소스에 연결하는 데 사용할 수 있습니다. **Web.config 파일의** identity 요소에서 가장을 사용 하도록 설정 하 고 사용자 이름과 암호를 지정 합니다.  
  
```xml  
<identity impersonate="true"   
        userName="MyDomain\UserAccount"   
        password="*****" />  
```  
  
 고정 ID 계정은 데이터베이스에서 필수 권한만 부여된 권한이 낮은 계정이어야 합니다. 또한 사용자 이름과 암호가 일반 텍스트로 노출되지 않도록 구성 파일을 암호화해야 합니다.  
  
## <a name="do-not-use-universal-data-link-udl-files"></a>UDL(유니버설 데이터 링크) 파일 사용 안 함  
 UDL(유니버설 데이터 링크) 파일에 <xref:System.Data.OleDb.OleDbConnection>에 대한 연결 문자열을 저장하지 마세요. UDL은 일반 텍스트로 저장되므로 암호화될 수 없습니다. UDL 파일은 애플리케이션에 대한 외부 파일 기반 리소스이므로 .NET Framework를 사용하여 파일을 보호하거나 암호화할 수 없습니다.  
  
## <a name="avoid-injection-attacks-with-connection-string-builders"></a>연결 문자열 작성기를 통해 삽입 공격 방지  
 연결 문자열 삽입 공격은 사용자 입력에 대해 동적 문자열 연결을 사용하여 연결 문자열을 작성할 때 발생할 수 있습니다. 사용자 입력의 유효성이 확인되지 않고 악의적인 텍스트 또는 문자를 막을 수 없는 경우 공격자가 서버에서 중요한 데이터 또는 기타 리소스에 액세스할 가능성이 있습니다. 이 문제를 해결하기 위해 ADO.NET 2.0에서는 새 연결 문자열 작성기 클래스를 도입하여 연결 문자열 구문의 유효성을 확인하고 추가 매개 변수가 사용되지 않았는지 확인합니다. 자세한 내용은 [연결 문자열 작성기](connection-string-builders.md)를 참조하세요.  
  
## <a name="use-persist-security-infofalse"></a>Persist Security Info=False 사용  
 `Persist Security Info`의 기본값은 false입니다. 모든 연결 문자열에서 이 기본값을 사용하는 것이 좋습니다. `Persist Security Info`를 `true` 또는 `yes`로 설정하면 연결이 열린 다음 연결에서 사용자 ID 및 암호와 같은 보안 관련 정보를 얻을 수 있습니다. `Persist Security Info`를 `false` 또는 `no`로 설정하면 연결을 열기 위해 보안 정보를 사용한 다음 삭제하므로 신뢰할 수 없는 소스는 보안 관련 정보에 액세스할 수 없습니다.  
  
## <a name="encrypt-configuration-files"></a>구성 파일 암호화  
 연결 문자열을 구성 파일에 저장할 수도 있으며 그러면 연결 문자열을 애플리케이션 코드에 포함할 필요가 없습니다. 구성 파일은 .NET Framework에 공통 요소 집합이 정의된 표준 XML 파일입니다. 구성 파일의 연결 문자열은 일반적으로 Windows 응용 프로그램에 대 한 **app.config** 의  **\<connectionStrings >** 요소 또는 ASP.NET 응용 **프로그램의 web.config 파일 내** 에 저장 됩니다. 구성 파일에서 연결 문자열을 저장, 검색 및 암호화 하는 기본적인 방법에 대 한 자세한 내용은 [연결 문자열 및 구성 파일](connection-strings-and-configuration-files.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](securing-ado-net-applications.md)
- [보호 된 구성을 사용 하 여 구성 정보 암호화](https://docs.microsoft.com/previous-versions/aspnet/53tyfkaw(v=vs.100))
- [.NET의 보안](../../../standard/security/index.md)
- [ADO.NET 개요](ado-net-overview.md)
