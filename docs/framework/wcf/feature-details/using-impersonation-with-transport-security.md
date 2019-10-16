---
title: 전송 보안을 통해 가장 사용
ms.date: 03/30/2017
ms.assetid: 426df8cb-6337-4262-b2c0-b96c2edf21a9
ms.openlocfilehash: f392dbe5806532eba181adef4ba3c8bebce9eddd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64637450"
---
# <a name="using-impersonation-with-transport-security"></a>전송 보안을 통해 가장 사용
*가장* 은 클라이언트의 id를 사용 하는 서버 응용 프로그램의 기능입니다. 리소스에 대한 액세스 확인 시 일반적으로 서비스는 가장을 사용합니다. 서버 애플리케이션은 서비스 계정을 사용하여 실행하지만 서버가 클라이언트 연결을 수락할 경우, 클라이언트의 자격 증명을 사용하여 액세스 검사를 수행하도록 클라이언트를 가장합니다. 전송 보안은 자격 증명을 전달하고 이러한 자격 증명을 사용하여 통신에 보안을 설정하기 위한 메커니즘입니다. 이 항목에서는 가장 기능을 사용 하 여 Windows Communication Foundation (WCF)에서 전송 보안을 사용 하 여 설명 합니다. 메시지 보안을 사용 하는 가장에 대 한 자세한 내용은 참조 하세요. [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)합니다.  
  
## <a name="five-impersonation-levels"></a>5개의 가장 수준  
 전송 보안은 다음 표에 설명된 대로 5개의 가장 수준을 사용합니다.  
  
|가장 수준|설명|  
|-------------------------|-----------------|  
|없음|서버 애플리케이션에서 클라이언트 가장을 시도하지 않습니다.|  
|Anonymous|서버 애플리케이션에서 클라이언트의 자격 증명에 대한 액세스 검사를 수행할 수 있지만 클라이언트 ID에 대한 정보는 수신하지 않습니다. 이 가장 수준은 명명된 파이프와 같이 시스템 상의 통신을 위해서만 사용됩니다. 원격 연결을 통해 `Anonymous`를 사용하는 경우 가장 수준이 Identify로 승격됩니다.|  
|Identify|서버 애플리케이션이 클라이언트의 ID를 알고 있으며 클라이언트 자격 증명에 대한 액세스 확인을 수행할 수 있지만, 클라이언트를 가장할 수는 없습니다. 확인 토큰 공급자가 다른 가장 수준을 제공 하지 않을 경우 WCF의 SSPI 자격 증명으로 사용 되는 기본 가장 수준입니다.|  
|Impersonate|서버 애플리케이션은 액세스 검사를 수행하는 것 이외에 클라이언트로 가장하여 서버 시스템의 리소스에 액세스할 수 있습니다. 서버 애플리케이션은 가장된 토큰에 네트워크 자격 증명이 없기 때문에 클라이언트의 ID를 사용하여 원격 시스템의 리소스에 액세스할 수 없습니다.|  
|대리자|`Impersonate`와 동일한 기능을 제공하는 것 이외에 Delegate 가장 수준을 사용하면, 서버 애플리케이션이 클라이언트의 ID를 사용하여 원격 시스템의 리소스에 액세스할 수 있으며 ID를 다른 애플리케이션에 전달할 수 있습니다.<br /><br /> **중요 한** 서버 도메인 계정이 표시 되어야 합니다 이러한 추가 기능을 사용 하는 도메인 컨트롤러에서 위임을 위해 신뢰할 수 있는 합니다. 이 가장 수준은 중요한 것으로 표시된 클라이언트 도메인 계정에서 사용할 수 없습니다.|  
  
 전송 보안을 사용 하 여 가장 일반적으로 사용 되는 수준은 `Identify` 고 `Impersonate`입니다. `None` 및 `Anonymous` 수준은 일반적인 용도로는 사용하지 않는 것이 좋으며 여러 전송에서는 인증에 이러한 수준을 사용하는 것을 지원하지 않습니다. `Delegate` 수준은 주의하여 사용해야 하는 강력한 기능입니다. 신뢰할 수 있는 서버 애플리케이션에만 자격 증명을 위임할 수 있는 권한을 제공해야 합니다.  
  
 `Impersonate` 또는 `Delegate` 수준에서 가장을 사용하려면 서버 애플리케이션에 `SeImpersonatePrivilege` 권한이 있어야 합니다. 애플리케이션이 Administrators 그룹의 계정 또는 Service SID(네트워크 서비스, 로컬 서비스 또는 로컬 시스템)의 계정에서 실행되는 경우 기본적으로 이 권한을 가집니다. 가장 기능을 사용하는 데 클라이언트 및 서버에 대한 상호 인증이 필요하지 않습니다. NTLM과 같이 가장을 지원하는 일부 인증 스키마는 상호 인증에 사용할 수 없습니다.  
  
## <a name="transport-specific-issues-with-impersonation"></a>가장을 사용하는 전송 관련 문제  
 WCF 전송을 선택을 가장에 대 한 가능한 선택 항목을 영향을 줍니다. 이 섹션에서는 표준 HTTP에 영향을 주는 문제에 설명 하 고 명명 된 파이프 전송 wcf에서입니다. 사용자 지정 전송에는 가장 지원과 관련하여 제한이 있습니다.  
  
### <a name="named-pipe-transport"></a>명명된 파이프 전송  
 명명된 파이프 전송에서는 다음 항목이 사용됩니다.  
  
- 명명된 파이프 전송은 로컬 시스템에서만 사용됩니다. WCF의 명명 된 파이프 전송은 시스템 간 연결을 명시적으로 허용 하지 않습니다.  
  
- 명명된 파이프는 `Impersonate` 또는 `Delegate` 가장 수준으로 사용할 수 없습니다. 명명된 파이프는 이러한 가장 수준에서 컴퓨터 보장을 적용할 수 없습니다.  
  
 명명 된 파이프에 대 한 자세한 내용은 참조 하세요. [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)합니다.  
  
### <a name="http-transport"></a>HTTP 전송  
 HTTP 전송을 사용 하는 바인딩 (<xref:System.ServiceModel.WSHttpBinding> 하 고 <xref:System.ServiceModel.BasicHttpBinding>)에 설명 된 대로 여러 인증 체계를 지 원하는 [Understanding HTTP Authentication](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)합니다. 지원되는 가장 수준은 인증 스키마에 따라 다릅니다. HTTP 파이프 전송에서는 다음 항목이 사용됩니다.  
  
- `Anonymous` 인증 스키마는 가장을 무시합니다.  
  
- 합니다 `Basic` 인증 스키마만 지원 합니다 `Delegate` 수준입니다. 모든 하위 가장 수준이 업그레이드됩니다.  
  
- `Digest` 인증 스키마는 `Impersonate` 및 `Delegate` 수준만 지원합니다.  
  
- 직접 선택하거나 협상을 통해 선택할 수 있는 `NTLM` 인증 스키마는 로컬 시스템에서 `Delegate` 수준만 지원합니다.  
  
- 스키마를 통해서만 선택할 수 있는 Kerberos 인증 체계는 지원되는 가장 수준으로만 사용할 수 있습니다.  
  
 HTTP 전송에 대 한 자세한 내용은 참조 하세요. [전송 선택](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [위임 및 가장](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
- [권한 부여](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)
- [방법: 서비스에서 클라이언트 가장](../../../../docs/framework/wcf/how-to-impersonate-a-client-on-a-service.md)
- [HTTP 인증 이해](../../../../docs/framework/wcf/feature-details/understanding-http-authentication.md)
