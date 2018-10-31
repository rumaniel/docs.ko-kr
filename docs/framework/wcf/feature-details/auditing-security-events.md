---
title: 보안 이벤트 감사
ms.date: 03/30/2017
helpviewer_keywords:
- auditing security events [WCF]
ms.assetid: 5633f61c-a3c9-40dd-8070-1c373b66a716
ms.openlocfilehash: 70bd756c9de2cf6ffb43479b0b28a6d51340f905
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198084"
---
# <a name="auditing-security-events"></a>보안 이벤트 감사
Windows Communication Foundation (WCF)를 사용 하 여 만든 응용 프로그램 감사 기능을 사용 하 여 보안 이벤트 (성공, 실패 또는 둘 다)를 기록할 수 있습니다. 이벤트는 Windows의 시스템 이벤트 로그에 기록되며 이벤트 뷰어를 사용하여 검사할 수 있습니다.  
  
 관리자는 감사를 사용하여 이미 발생했거나 진행 중인 공격을 검색할 수 있습니다. 또한 감사는 개발자가 보안 관련 문제를 디버깅하는 데 도움이 됩니다. 예를 들어, 정책 검사 또는 권한 부여 구성 오류로 인해 실수로 권한 있는 사용자의 액세스가 거부될 경우 개발자는 이벤트 로그를 검사하여 오류의 원인을 신속하게 찾아서 격리시킬 수 있습니다.  
  
 WCF 보안에 대 한 자세한 내용은 참조 하세요. [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)합니다. WCF 프로그래밍에 대 한 자세한 내용은 참조 하세요. [기본 WCF 프로그래밍](../../../../docs/framework/wcf/basic-wcf-programming.md)합니다.  
  
## <a name="audit-level-and-behavior"></a>감사 수준 및 동작  
 보안 감사에는 다음과 같은 두 가지 수준이 있습니다.  
  
-   서비스 인증 수준 - 호출자에게 권한이 부여됩니다.  
  
-   메시지 수준에는 WCF 메시지의 유효성을 검사 하 고 호출자를 인증 합니다.  
  
 감사 성공 또는 실패 이라고 수준 모두를 확인할 수 있습니다 합니다 *감사 동작*합니다.  
  
## <a name="audit-log-location"></a>감사 로그 위치  
 감사 수준과 동작을 결정한 후 사용자 또는 관리자가 감사 로그의 위치를 지정할 수 있습니다. 기본값, 응용 프로그램, 보안의 세 가지 옵션 중에서 선택할 수 있습니다. 기본값을 지정한 경우 실제 로그는 사용 중인 시스템과 시스템에서 보안 로그 기록을 지원하는지 여부에 따라 달라집니다. 자세한 내용은이 항목의 뒷부분에 나오는 "운영 체제" 단원을 참조 하세요.  
  
 보안 로그에 기록하려면 `SeAuditPrivilege`가 필요합니다. 기본적으로 로컬 시스템 및 네트워크 서비스 계정에만 이 권한이 있습니다. 보안 로그 기능 `read` 및 `delete`를 관리하려면 `SeSecurityPrivilege`가 필요합니다. 기본적으로 관리자만 이 권한을 가집니다.  
  
 반대로, 인증된 사용자는 응용 프로그램 로그를 읽고 쓸 수 있습니다. [!INCLUDE[wxp](../../../../includes/wxp-md.md)]는 기본적으로 감사 이벤트를 응용 프로그램 로그에 씁니다. 이 로그는 모든 인증된 사용자에게 표시되는 개인 정보를 포함할 수도 있습니다.  
  
## <a name="suppressing-audit-failures"></a>감사 실패 억제  
 또한 감사 중에 감사 실패를 억제할지 여부를 지정하는 옵션이 있습니다. 기본적으로 감사 실패는 응용 프로그램에 영향을 주지 않습니다. 그러나 필요한 경우 이 옵션을 `false`로 설정할 수 있습니다. 그러면 예외가 throw됩니다.  
  
## <a name="programming-auditing"></a>감사 프로그래밍  
 프로그래밍 방식이나 구성을 통해 감사 동작을 지정할 수 있습니다.  
  
### <a name="auditing-classes"></a>감사 클래스  
 다음 표에서는 감사 동작을 프로그래밍하는 데 사용되는 클래스와 속성에 대해 설명합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>|감사 옵션을 서비스 동작으로 설정할 수 있습니다.|  
|<xref:System.ServiceModel.AuditLogLocation>|기록할 로그를 지정하는 열거형입니다. 가능한 값은 기본값, 응용 프로그램 및 보안입니다. 기본값을 선택하면 운영 체제에서 실제 로그 위치를 결정합니다. 이 항목의 뒷부분에 나오는 "응용 프로그램 또는 보안 이벤트 로그 선택" 단원을 참조하십시오.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A>|메시지 수준에서 감사할 메시지 인증 이벤트의 유형을 지정합니다. `None`, `Failure`, `Success` 및 `SuccessOrFailure` 중에서 선택할 수 있습니다.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A>|서비스 수준에서 감사할 서비스 인증 이벤트의 유형을 지정합니다. `None`, `Failure`, `Success` 및 `SuccessOrFailure` 중에서 선택할 수 있습니다.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A>|감사가 실패할 경우 클라이언트 요청 처리 방식을 지정합니다. 예를 들어, 서비스에서 보안 로그에 기록하려고 시도하지만 `SeAuditPrivilege`가 없는 경우 기본값 `true`를 지정했다면 실패가 무시되고 클라이언트 요청이 정상적으로 처리됩니다.|  
  
 감사 이벤트를 기록 하는 응용 프로그램 설정의 예제를 참조 하세요 [방법: 보안 이벤트 감사](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)합니다.  
  
### <a name="configuration"></a>구성  
 구성 추가 하 여 감사 동작을 지정 하려면 사용할 수도 있습니다는 [ \<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) 아래를 [ \<동작 >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)합니다. 아래에 요소를 추가 해야 합니다는 [ \<동작 >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 다음 코드와 같이 합니다.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <behavior>  
        <!— auditLogLocation="Application" or "Security" -—>  
        <serviceSecurityAudit  
                  auditLogLocation="Application"  
                  suppressAuditFailure="true"  
                  serviceAuthorizationAuditLevel="Failure"  
                  messageAuthenticationAuditLevel="SuccessOrFailure" />   
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 감사가 설정되어 있지만 `auditLogLocation`이 지정되어 있지 않으면 보안 로그 기록을 지원하는 플랫폼의 기본 로그 이름은 "Security" 로그이고, 그렇지 않으면 "Application" 로그입니다. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 및 [!INCLUDE[wv](../../../../includes/wv-md.md)] 운영 체제만 보안 로그에 쓰기를 지원합니다. 자세한 내용은이 항목의 뒷부분에 나오는 "운영 체제" 단원을 참조 하세요.  
  
## <a name="security-considerations"></a>보안 고려 사항  
 악의적인 사용자가 감사가 설정된 사실을 알고 있다면 잘못된 메시지를 보내 감사 항목을 기록할 수 있습니다. 이런 식으로 감사 로그가 채워지면 감사 시스템이 실패합니다. 이 문제를 완화하려면 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> 속성을 `true`로 설정하고 이벤트 뷰어의 속성을 사용하여 감사 동작을 제어합니다. 보기 및 이벤트 로그에서 Windows XP에서 이벤트 뷰어를 사용 하 여 관리에 대 한 자세한 내용은 Microsoft 지원 문서를 참조 [Windows XP의 이벤트 뷰어에 이벤트 로그 보기 및 관리 하는 방법을](https://go.microsoft.com/fwlink/?LinkId=89150)합니다.  
  
 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 응용 프로그램 로그에 기록되는 감사 이벤트는 모든 인증된 사용자가 볼 수 있습니다.  
  
## <a name="choosing-between-application-and-security-event-logs"></a>응용 프로그램 및 보안 이벤트 로그 선택  
 다음 표에서는 응용 프로그램 이벤트 로그에 기록할지 보안 이벤트 로그에 기록할지 여부를 선택하는 데 도움이 되는 정보를 제공합니다.  
  
#### <a name="operating-system"></a>운영 체제  
  
|시스템|응용 프로그램 로그|보안 로그|  
|------------|---------------------|------------------|  
|[!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] 이상|지원함|지원 안 함|  
|[!INCLUDE[ws2003sp1](../../../../includes/ws2003sp1-md.md)] 및 [!INCLUDE[wv](../../../../includes/wv-md.md)]|지원함|스레드 컨텍스트에 `SeAuditPrivilege`가 있어야 합니다.|  
  
#### <a name="other-factors"></a>기타 요소  
 다음 표에서는 운영 체제 이외에 로깅 사용을 제어하는 기타 설정에 대해 설명합니다.  
  
|요소|응용 프로그램 로그|보안 로그|  
|------------|---------------------|------------------|  
|정책 관리 감사|해당 사항 없음.|구성과 함께 보안 로그는 LSA(로컬 보안 기관) 정책에 의해서도 제어됩니다. "개체 액세스 감사" 범주 또한 사용하도록 설정해야 합니다.|  
|기본 사용자 경험|모든 인증된 사용자는 응용 프로그램 로그에 기록할 수 있으므로 응용 프로그램 프로세스를 위한 추가 권한 단계가 필요하지 않습니다.|응용 프로그램 프로세스(컨텍스트)에 `SeAuditPrivilege`가 있어야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>  
 <xref:System.ServiceModel.AuditLogLocation>  
 [보안 개요](../../../../docs/framework/wcf/feature-details/security-overview.md)  
 [기본 WCF 프로그래밍](../../../../docs/framework/wcf/basic-wcf-programming.md)  
 [방법: 보안 이벤트 감사](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)  
 [\<serviceSecurityAudit >](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md)  
 [\<동작 >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)  
 [Windows Server appfabric 보안 모델](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
