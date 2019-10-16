---
title: WCF에서 권한 부여
ms.date: 03/30/2017
helpviewer_keywords:
- authorization [WCF]
- security [WCF], authorization
ms.assetid: 8ea0b552-af65-45b0-a157-c6c111b8ce5e
ms.openlocfilehash: 8c605b310f19a05f994296d8f4268b91b408fb18
ms.sourcegitcommit: c4e9d05644c9cb89de5ce6002723de107ea2e2c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2019
ms.locfileid: "65881201"
---
# <a name="authorization-in-wcf"></a>WCF에서 권한 부여
권한 부여는 서비스나 파일과 같은 리소스에 대한 액세스 및 권한을 제어하는 프로세스입니다. 이 섹션의에서 항목에서는에 Windows Communication Foundation (WCF)에서 다양 한 방법으로 기본 작업을 수행 하는 방법을 보여 줍니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Access Control 메커니즘](../../../../docs/framework/wcf/feature-details/access-control-mechanisms.md)  
 WCF 및 제안 된 사용 권한 부여 메커니즘의 간략 한 개요를 제공합니다.  
  
 [방법: PrincipalPermissionAttribute 클래스를 사용 하 여 액세스 제한](../../../../docs/framework/wcf/how-to-restrict-access-with-the-principalpermissionattribute-class.md)  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>를 사용하여 서비스에 대한 액세스를 제한하는 프로세스를 보여 줍니다.  
  
 [방법: 서비스에서 ASP.NET 역할 공급자 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)  
 Asp.net 역할 공급자 기능을 사용할 수 있도록 서비스의 구성을 안내 합니다.  
  
 [방법: 서비스에서 ASP.NET 권한 부여 관리자 역할 공급자 사용](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service.md)  
 ASP.NET 권한 부여 관리자를 사용 하 여 웹 사이트에 대 한 권한 부여를 관리할 수 있습니다. WCF는 클라이언트의 권한 부여 ASP.NET/Authorization 관리자 조합을 활용할 마찬가지로 수 있습니다.  
  
 [ID 모델을 사용하여 클레임 및 권한 부여 관리](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)  
 클레임 기반 권한 부여에 ID 모델 인프라를 사용하는 기본적인 사용법에 대해 설명합니다 .  
  
 [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)  
 위임과 가장의 차이점을 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.ServiceModel.Description.PrincipalPermissionMode>  
  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute>  
  
## <a name="related-sections"></a>관련 단원  
 [인증](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)  
  
## <a name="see-also"></a>참고자료

- [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
