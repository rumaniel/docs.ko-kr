---
title: '방법: 보안 컨텍스트 검사'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ServiceSecurityContext class
- WCF, security
- Claimset class
ms.assetid: 389b5a57-4175-4bc0-ada0-fc750d51149f
ms.openlocfilehash: e67ac9c452337b6f490d99ea4430ec2a02b952a1
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625799"
---
# <a name="how-to-examine-the-security-context"></a>방법: 보안 컨텍스트 검사
Windows Communication Foundation (WCF) 서비스를 프로그래밍 하는 경우 서비스 보안 컨텍스트를 사용 하면 클라이언트 자격 증명 및 서비스를 사용 하 여 인증 하는 데 사용 되는 클레임에 대 한 세부 정보를 확인할 수 있습니다. <xref:System.ServiceModel.ServiceSecurityContext> 클래스의 속성을 사용하여 이를 수행할 수 있습니다.  
  
 예를 들어 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> 또는 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 속성을 사용하여 현재 클라이언트의 ID를 검색할 수 있습니다. 클라이언트가 익명인지 여부를 확인하기 위해 <xref:System.ServiceModel.ServiceSecurityContext.IsAnonymous%2A> 속성을 사용합니다.  
  
 또한 <xref:System.ServiceModel.ServiceSecurityContext.AuthorizationContext%2A> 속성에서 클레임 컬렉션을 반복하여 클라이언트 대신 수행된 클레임을 확인할 수 있습니다.  
  
### <a name="to-get-the-current-security-context"></a>현재 보안 컨텍스트를 가져오려면  
  
- 정적 <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> 속성에 액세스하여 현재 보안 컨텍스트를 가져옵니다. 참조에서 현재 컨텍스트의 모든 속성을 검사합니다.  
  
### <a name="to-determine-the-identity-of-the-caller"></a>호출자의 ID를 확인하려면  
  
1. <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> 및 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 속성의 값을 인쇄합니다.  
  
### <a name="to-parse-the-claims-of-a-caller"></a>호출자의 클레임을 구문 분석하려면  
  
1. 현재 <xref:System.IdentityModel.Policy.AuthorizationContext> 클래스를 반환합니다. <xref:System.ServiceModel.ServiceSecurityContext.Current%2A> 속성을 사용하여 현재 서비스 보안 컨텍스트를 반환한 다음 `AuthorizationContext` 속성을 사용하여 <xref:System.ServiceModel.ServiceSecurityContext.AuthorizationContext%2A>를 반환합니다.  
  
2. <xref:System.IdentityModel.Claims.ClaimSet> 클래스의 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> 속성에서 반환된 <xref:System.IdentityModel.Policy.AuthorizationContext> 개체의 컬렉션을 구문 분석합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 현재 보안 컨텍스트의 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 및 <xref:System.ServiceModel.ServiceSecurityContext.PrimaryIdentity%2A> 속성에 대한 값, <xref:System.IdentityModel.Claims.Claim.ClaimType%2A> 속성, 클레임의 리소스 값 및 현재 보안 컨텍스트의 모든 클레임에 대한 <xref:System.IdentityModel.Claims.Claim.Right%2A> 속성을 인쇄합니다.  
  
 [!code-csharp[c_PrincipalPermissionAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#4)]
 [!code-vb[c_PrincipalPermissionAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#4)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드는 다음 네임스페이스를 사용합니다.  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.IdentityModel.Policy>  
  
- <xref:System.IdentityModel.Claims>  
  
## <a name="see-also"></a>참고자료

- [서비스에 보안 설정](../../../docs/framework/wcf/securing-services.md)
- [서비스 ID 및 인증](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)
