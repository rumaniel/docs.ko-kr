---
title: ServiceSecurityAuditBehavior
ms.date: 03/30/2017
ms.assetid: 2c5809e7-5364-44ce-bc71-848be4672e2a
ms.openlocfilehash: 30679e1f67c6943bf674a6bbd8bf12be090765a8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956899"
---
# <a name="servicesecurityauditbehavior"></a>ServiceSecurityAuditBehavior
ServiceSecurityAuditBehavior  
  
## <a name="syntax"></a>구문  
  
```csharp  
class ServiceSecurityAuditBehavior : Behavior  
{  
  string AuditLogLocation;  
  string MessageAuthenticationAuditLevel;  
  string ServiceAuthorizationAuditLevel;  
  boolean SuppressAuditFailure;  
};  
```  
  
## <a name="methods"></a>메서드  
 ServiceSecurityAuditBehavior 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 ServiceSecurityAuditBehavior 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="auditloglocation"></a>AuditLogLocation  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 감사 로그의 위치입니다.  
  
### <a name="messageauthenticationauditlevel"></a>MessageAuthenticationAuditLevel  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 감사 이벤트 로깅에 사용되는 메시지 인증 수준의 형식입니다.  
  
### <a name="serviceauthorizationauditlevel"></a>ServiceAuthorizationAuditLevel  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 감사 로그에 기록되는 권한 부여 이벤트의 형식입니다.  
  
### <a name="suppressauditfailure"></a>SuppressAuditFailure  
 데이터 형식: boolean  
  
 액세스 형식: 읽기 전용  
  
 감사 로그 쓰기의 실패를 표시하지 않기 위한 동작을 지정하는 부울 값입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>
