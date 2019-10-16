---
title: ServiceCredentials
ms.date: 03/30/2017
ms.assetid: 9c780793-4785-46f7-add9-ac1ebeadb614
ms.openlocfilehash: d9563bd3bfe067ad83bfa03e7c6375a9db933f14
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956983"
---
# <a name="servicecredentials"></a>ServiceCredentials
ServiceCredentials  
  
## <a name="syntax"></a>구문  
  
```csharp
class ServiceCredentials : Behavior  
{  
  string ClientCertificate;  
  string IssuedTokenAuthentication;  
  string Peer;  
  string SecureConversationAuthentication;  
  string ServiceCertificate;  
  string UserNameAuthentication;  
  string WindowsAuthentication;  
};  
```  
  
## <a name="methods"></a>메서드  
 ServiceCredentials 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 ServiceCredentials 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="clientcertificate"></a>ClientCertificate  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 이 서비스에 대한 클라이언트 인증서 인증 및 구축 설정입니다.  
  
### <a name="issuedtokenauthentication"></a>IssuedTokenAuthentication  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 이 서비스에 대해 현재 발급된 토큰 인증 설정입니다.  
  
### <a name="peer"></a>Peer  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 피어 전송 엔드포인트가 사용하는 현재 자격 증명 인증 및 구축 설정입니다.  
  
### <a name="secureconversationauthentication"></a>SecureConversationAuthentication  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 현재 보안 대화 설정을 지정합니다.  
  
### <a name="servicecertificate"></a>ServiceCertificate  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 이 서비스와 연관된 인증서입니다.  
  
### <a name="usernameauthentication"></a>UserNameAuthentication  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 이 서비스에 대한 사용자 이름/암호 설정입니다.  
  
### <a name="windowsauthentication"></a>WindowsAuthentication  
 데이터 형식: string  
  
 액세스 형식: 읽기 전용  
  
 이 서비스에 대한 Windows 인증 설정입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.ServiceCredentials>
