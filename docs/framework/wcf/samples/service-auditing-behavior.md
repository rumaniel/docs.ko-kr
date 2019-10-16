---
title: Service Auditing Behavior
ms.date: 03/30/2017
ms.assetid: 59bf0cda-e496-4418-a3a1-2f0f6e85f8ce
ms.openlocfilehash: 6d5f254f4f94adfaeaf5632ddd696891af177e93
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964554"
---
# <a name="service-auditing-behavior"></a>Service Auditing Behavior
이 샘플에서는 서비스 작업 중에 서비스 이벤트 감사를 활성화하기 위해 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>를 사용하는 방법을 보여 줍니다. 이 샘플은 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)을 기반으로 합니다. 서비스와 클라이언트는 [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)를 사용 하 여 구성 되었습니다. `clientCredentialType` `Windows` [보안 > 의\<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) `mode` 특성이로 설정 되어 있고가로설정되어있습니다.`Message` 이 샘플에서 클라이언트는 콘솔 응용 프로그램(.exe)이고 서비스는 IIS(인터넷 정보 서비스)를 통해 호스트됩니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 서비스 구성 파일은 `serviceSecurityAudit` 요소를 사용하여 감사를 구성합니다.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      ...  
<!-- serviceSecurityAudit allows specification of audit location   
     and whether to audit success, failure or both. This service   
     logs success and failure of messageAuthentication   
     to the default location -->  
     <serviceSecurityAudit auditLogLocation ="Default" messageAuthenticationAuditLevel = "SuccessOrFailure" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 콘솔 창에서 Enter 키를 누릅니다.  
  
 결과 감사 로그는 이벤트 뷰어를 실행하여 볼 수 있습니다. 기본적으로 Windows XP에서는 애플리케이션 로그에서 감사 이벤트를 볼 수 있지만 Windows Server 2003 및 Windows Vista에서는 보안 로그에서 감사 이벤트를 볼 수 있습니다. Windows Server 2008 및 Windows 7에서는 애플리케이션 및 서비스 로그에서 감사 이벤트를 볼 수 있습니다. 감사 이벤트의 위치는 `auditLogLocation` 특성을 "Application" 또는 "Security"로 설정 하 여 지정할 수 있습니다. 자세한 내용은 [방법: 보안 이벤트](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)를 감사 합니다. 이벤트가 보안 로그에 기록 되는 경우 LocalSecurityPolicy > 사용 개체 액세스는 "성공" 및 "실패"에 대해 설정 해야 합니다.  
  
 이벤트 로그를 확인하면 감사 이벤트의 소스는 "ServiceModel Audit 3.0.0.0"입니다. 메시지 인증 감사 레코드의 범주는 "MessageAuthentication" 이지만 서비스 권한 부여 감사 레코드의 범주는 "ServiceAuthorization"입니다.  
  
 메시지 인증 감사 이벤트는 메시지가 훼손되었는지 여부, 메시지가 만료되었는지 여부 및 클라이언트가 서비스에서 인증될 수 있는지 여부를 포함합니다. 이 이벤트는 클라이언트의 ID와 함께 인증의 성공 여부, 메시지와 연결된 동작과 함께 메시지가 보내진 엔드포인트에 대한 정보를 제공합니다.  
  
 서비스 권한 부여 감사 이벤트는 서비스 권한 부여 관리자가 내린 권한 부여 결정을 포함합니다. 이 이벤트는 클라이언트 ID와 함께 권한 부여의 성공 여부, 메시지가 보내진 엔드포인트, 메시지와 연결된 동작, 들어오는 메시지에서 생성된 권한 부여 컨텍스트의 식별자 및 액세스 결정을 내린 권한 부여 관리자의 형식에 대한 정보를 제공합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
## <a name="see-also"></a>참고자료

- [감사](../../../../docs/framework/wcf/feature-details/auditing-security-events.md)
- [방법: 보안 이벤트 감사](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)
