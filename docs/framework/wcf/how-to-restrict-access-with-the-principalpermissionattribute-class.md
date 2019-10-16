---
title: '방법: PrincipalPermissionAttribute 클래스를 사용하여 액세스 제한'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PrincipalPermissionAttribute class
- WCF, authorization
- WCF, security
ms.assetid: 5162f5c4-8781-4cc4-9425-bb7620eaeaf4
ms.openlocfilehash: 3b109e3e6817c300af1e79258d555562dcba067a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951017"
---
# <a name="how-to-restrict-access-with-the-principalpermissionattribute-class"></a>방법: PrincipalPermissionAttribute 클래스를 사용하여 액세스 제한
Windows 도메인 컴퓨터의 리소스에 대한 액세스 제어는 기본적인 보안 작업입니다. 예를 들어, 특정 사용자만 급여 정보와 같은 민감한 데이터를 볼 수 있어야 합니다. 이 항목에서는 사용자가 미리 정의된 그룹에 속하도록 요청하여 메서드에 대한 액세스를 제한하는 방법을 설명합니다. 작업 예제는 [서비스 작업에 대 한 액세스 권한 부여](../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)를 참조 하세요.  
  
 작업은 두 가지 별도의 절차로 구성됩니다. 첫 번째는 그룹을 만들어 이 그룹을 사용자로 채웁니다. 두 번째는 그룹을 지정할 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 클래스를 적용합니다.  
  
### <a name="to-create-a-windows-group"></a>Windows 그룹을 만들려면  
  
1. **컴퓨터 관리** 콘솔을 엽니다.  
  
2. 왼쪽 패널에서 **로컬 사용자 및 그룹**을 클릭 합니다.  
  
3. **그룹**을 마우스 오른쪽 단추로 클릭 하 고 **새 그룹**을 클릭 합니다.  
  
4. **그룹 이름** 상자에 새 그룹의 이름을 입력 합니다.  
  
5. **설명** 상자에 새 그룹에 대 한 설명을 입력 합니다.  
  
6. **추가** 단추를 클릭 하 여 그룹에 새 멤버를 추가 합니다.  
  
7. 사용자 자신을 그룹에 추가하고 다음 코드를 테스트하려면, 컴퓨터를 로그오프한 후 다시 로그온하여 그룹에 포함되어야 합니다.  
  
### <a name="to-demand-user-membership"></a>사용자 멤버 자격을 요구하려면  
  
1. 구현 된 서비스 계약 코드가 포함 된 WCF (Windows Communication Foundation) 코드 파일을 엽니다. 계약을 구현 하는 방법에 대 한 자세한 내용은 [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)을 참조 하세요.  
  
2. <xref:System.Security.Permissions.PrincipalPermissionAttribute> 특성을 특정 그룹에 대해 제한되어야 하는 각 메서드에 적용합니다. <xref:System.Security.Permissions.SecurityAttribute.Action%2A> 속성을 <xref:System.Security.Permissions.SecurityAction.Demand>로 설정하고 <xref:System.Security.Permissions.PrincipalPermissionAttribute.Role%2A> 속성을 그룹 이름으로 설정합니다. 예를 들어:  
  
     [!code-csharp[c_PrincipalPermissionAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#1)]
     [!code-vb[c_PrincipalPermissionAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#1)]  
  
    > [!NOTE]
    > <xref:System.Security.Permissions.PrincipalPermissionAttribute> 특성을 계약에 적용하면 <xref:System.Security.SecurityException>이 throw됩니다. 메서드 수준에서만 이 특성을 적용할 수 있습니다.  
  
## <a name="using-a-certificate-to-control-access-to-a-method"></a>인증서를 사용하여 메서드에 대한 액세스 제어  
 또한 클라이언트 자격 증명 형식이 인증서인 경우 `PrincipalPermissionAttribute` 클래스를 사용하여 메서드에 대한 액세스를 제어할 수 있습니다. 이를 수행하려면 인증서의 주체 및 지문이 있어야 합니다.  
  
 인증서의 속성 [을 검사 하려면 방법: MMC 스냅인](../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)을 사용 하 여 인증서를 봅니다. 지문 값 [을 찾으려면 방법: 인증서](../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)의 지문을 검색 합니다.  
  
#### <a name="to-control-access-using-a-certificate"></a>인증서를 사용하여 액세스를 제어하려면  
  
1. <xref:System.Security.Permissions.PrincipalPermissionAttribute> 클래스를 액세스를 제한할 메서드에 적용합니다.  
  
2. 특성의 동작을 <xref:System.Security.Permissions.SecurityAction.Demand?displayProperty=nameWithType>로 설정합니다.  
  
3. `Name` 속성을 주체 이름 및 인증서 지문으로 구성된 문자열로 설정합니다. 다음 예제와 같이 두 개의 값을 세미콜론 및 공백으로 구분합니다.  
  
     [!code-csharp[c_PrincipalPermissionAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#2)]
     [!code-vb[c_PrincipalPermissionAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#2)]  
  
4. 다음 구성 예제와 같이 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> 속성을 <xref:System.ServiceModel.Description.PrincipalPermissionMode.UseAspNetRoles>로 설정합니다.  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
      <behavior name="SvcBehavior1">  
      <serviceAuthorization principalPermissionMode="UseAspNetRoles" />  
      </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
     이 값을 `UseAspNetRoles`로 설정하면 `Name`의 `PrincipalPermissionAttribute` 속성이 문자열 비교를 수행하는 데 사용됨을 나타냅니다. 인증서가 클라이언트 자격 증명으로 사용 되는 경우 기본적으로 WCF는 인증서 일반 이름 및 지문을 세미콜론으로 연결 하 여 클라이언트의 기본 id에 대 한 고유한 값을 만듭니다. `UseAspNetRoles`를 서비스의 `PrincipalPermissionMode`로 설정한 경우 이 기본 ID 값을 `Name` 속성 값과 비교하여 사용자의 액세스 권한을 결정합니다.  
  
     또는 자체 호스팅되는 서비스를 만드는 경우 코드의 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> 속성을 다음 코드와 같이 설정합니다.  
  
     [!code-csharp[c_PrincipalPermissionAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_principalpermissionattribute/cs/source.cs#3)]
     [!code-vb[c_PrincipalPermissionAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_principalpermissionattribute/vb/source.vb#3)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Permissions.PrincipalPermissionAttribute>
- <xref:System.Security.Permissions.SecurityAction.Demand>
- <xref:System.Security.Permissions.PrincipalPermissionAttribute.Role%2A>
- [서비스 작업에 대한 액세스 승인](../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)
- [보안 개요](../../../docs/framework/wcf/feature-details/security-overview.md)
- [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)
