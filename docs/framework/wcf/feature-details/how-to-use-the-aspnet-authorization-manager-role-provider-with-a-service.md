---
title: '방법: 서비스에서 ASP.NET 권한 부여 관리자 역할 공급자 사용'
ms.date: 03/30/2017
ms.assetid: f21deb81-91ef-49ef-94d6-494785143271
ms.openlocfilehash: 778af929b4cfc96ce0683d304be5f8fb87a0e47b
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65880194"
---
# <a name="how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service"></a>방법: 서비스에서 ASP.NET 권한 부여 관리자 역할 공급자 사용
ASP.NET 웹 서비스를 호스트 하는 경우에 서비스에 권한 부여를 제공 하는 응용 프로그램에 권한 부여 관리자를 통합할 수 있습니다. 애플리케이션 개발자는 권한 부여 관리자를 사용하여 개별 작업을 정의할 수 있습니다. 개별 작업은 그룹으로 분류되어 작업을 형성할 수 있습니다. 관리자는 역할에 특정 작업 또는 개별 작업을 수행할 권한을 부여할 수 있습니다. 권한 부여 관리자는 역할, 작업 및 사용자를 관리할 수 있도록 MMC(Microsoft Management Console) 스냅인과 같은 관리 도구를 제공합니다. 관리자는 XML 파일, Active Directory 또는 ADAM(Active Directory Application Mode) 저장소에서 권한 부여 관리자 정책 저장소를 구성합니다.  
  
 권한 부여 관리자는 웹 서비스를 호스팅하는 ASP.NET 응용 프로그램에 대 한 권한 부여 관리자 ASP.NET 역할 공급자를 구성 하 여 응용 프로그램에 통합 됩니다. 다른 ASP.NET 역할 공급자와 같은 권한 부여 관리자 ASP.NET 역할 공급자 사용 하 여 구성 되는 <`providers`> 요소입니다.  
  
 다음 코드 예제는 권한 부여 관리자를 애플리케이션에 통합하는 웹 서비스에 대한 구성 파일의 일부입니다.  
  
```xml  
<system.web>  
    <roleManager enabled="true" defaultProvider="AzManRoleProvider">  
      <providers>  
        <add name="AzManRoleProvider"  
             type="System.Web.Security.AuthorizationStoreRoleProvider, System.Web, Version=2.0.0.0, Culture=neutral, publicKeyToken=b03f5f7f11d50a3a"  
             connectionStringName="AzManPolicyStoreConnectionString"   
             applicationName="SecureService"/>  
      </providers>  
    </roleManager>  
</system.web>  
```  
  
 WCF 응용 프로그램을 사용 하 여 ASP.NET 역할 공급자를 통합 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: ASP.NET 역할 공급자를 사용 하 여 서비스를 사용 하 여](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)입니다. ASP.NET을 사용 하 여 권한 부여 관리자를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: Use Authorization Manager (AzMan) with ASP.NET 2.0](https://go.microsoft.com/fwlink/?LinkId=71303)합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 서비스에서 ASP.NET 역할 공급자 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
