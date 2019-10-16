---
title: ServiceAuthorizationBehavior
ms.date: 03/30/2017
ms.assetid: 77dad8e8-fea4-4d1c-b366-2f01a2a87f78
ms.openlocfilehash: 51555e3357b8c33a53261c4894d97798b0a05656
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61957057"
---
# <a name="serviceauthorizationbehavior"></a>ServiceAuthorizationBehavior
ServiceAuthorizationBehavior  
  
## <a name="syntax"></a>구문  
  
```csharp
class ServiceAuthorizationBehavior : Behavior  
{  
  boolean ImpersonateCallerForAllOperations;  
  string PrincipalPermissionMode;  
  string RoleProvider;  
  string ServiceAuthorizationManager;  
};  
```  
  
## <a name="methods"></a>메서드  
 ServiceAuthorizationBehavior 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 ServiceAuthorizationBehavior 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="impersonatecallerforalloperations"></a>ImpersonateCallerForAllOperations  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 들어오는 메시지가 제공하는 자격 증명을 사용하여 서비스가 가장을 시도하는지 여부를 제어하는 값입니다.  
  
### <a name="principalpermissionmode"></a>PrincipalPermissionMode  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 서버에서 작업을 수행할 때 사용되는 주체입니다.  
  
### <a name="roleprovider"></a>RoleProvider  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 ASP.NET 역할 공급자의 이름입니다.  
  
### <a name="serviceauthorizationmanager"></a>ServiceAuthorizationManager  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 사용자 지정 인증에 사용되는 권한 부여 관리자입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>
