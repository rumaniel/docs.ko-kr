---
title: '방법: 사용자 지정 보안 주체 ID 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- IPrincipal
- IAuthorizationPolicy
- PrincipalPermissionMode
- PrincipalPermissionAttribute
ms.assetid: c4845fca-0ed9-4adf-bbdc-10812be69b61
ms.openlocfilehash: 05a90c4020f225414b21e82684e46b3c2abda010
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797077"
---
# <a name="how-to-create-a-custom-principal-identity"></a>방법: 사용자 지정 보안 주체 ID 만들기
<xref:System.Security.Permissions.PrincipalPermissionAttribute>는 서비스 메서드에 대한 액세스를 제어하는 선언적 수단입니다. 이 특성을 사용하는 경우 <xref:System.ServiceModel.Description.PrincipalPermissionMode> 열거는 권한 부여를 검사하기 위한 모드를 지정합니다. 이 모드를 <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom>으로 설정하면 사용자가 <xref:System.Security.Principal.IPrincipal> 속성에 의해 반환된 사용자 지정 <xref:System.Threading.Thread.CurrentPrincipal%2A> 클래스를 지정할 수 있습니다. 이 항목에서는 <xref:System.ServiceModel.Description.PrincipalPermissionMode.Custom>이 사용자 지정 권한 부여 정책 및 사용자 지정 보안 주체와 함께 사용되는 시나리오를 보여 줍니다.  
  
 를 사용 하 <xref:System.Security.Permissions.PrincipalPermissionAttribute> [는 방법에 대 한 자세한 내용은 방법: PrincipalPermissionAttribute 클래스](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)를 사용 하 여 액세스를 제한 합니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[PrincipalPermissionMode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/principalpermissionmode/cs/source.cs#8)]
 [!code-vb[PrincipalPermissionMode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/principalpermissionmode/vb/source.vb#8)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 컴파일하려면 다음 네임스페이스에 대한 참조가 필요합니다.  
  
- <xref:System>  
  
- <xref:System.Collections.Generic>  
  
- <xref:System.Security.Permissions>  
  
- <xref:System.Security.Principal>  
  
- <xref:System.Threading>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Description>  
  
- <xref:System.IdentityModel.Claims>  
  
- <xref:System.IdentityModel.Policy>  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.PrincipalPermissionMode>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- [방법: 서비스에서 ASP.NET 역할 공급자 사용](../feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
- [방법: PrincipalPermissionAttribute 클래스를 사용 하 여 액세스 제한](../how-to-restrict-access-with-the-principalpermissionattribute-class.md)
