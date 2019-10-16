---
title: WIF를 사용하여 클레임 기반 권한 부여
ms.date: 03/30/2017
ms.assetid: e24000a3-8fd8-4c0e-bdf0-39882cc0f6d8
author: BrucePerlerMS
ms.openlocfilehash: ebf4c28bd2a46c21535b596af22d1fa420d20e71
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045499"
---
# <a name="claims-based-authorization-using-wif"></a>WIF를 사용하여 클레임 기반 권한 부여
신뢰 당사자 응용 프로그램에서 권한 부여에 따라 인증된 ID가 액세스할 수 있도록 허용되는 리소스 및 이러한 리소스에서 수행할 수 있도록 허용되는 작업이 결정됩니다. 권한 부여가 부적절하거나 취약한 상태인 경우 정보가 노출되거나 데이터가 변조될 수 있습니다. 이 항목에서는 ACS(Windows Azure Access Control Service)와 같은 STS(보안 토큰 서비스) 및 WIF(Windows Identity Foundation)를 사용하여 클레임 인식 ASP.NET 웹 응용 프로그램과 서비스에 대한 권한 부여를 구현하기 위해 사용할 수 있는 방법에 대해 간략하게 설명합니다.  
  
## <a name="overview"></a>개요  
 .NET Framework는 첫 번째 버전부터 권한 부여를 구현하는 유연한 메커니즘을 제공해 왔습니다. 이 메커니즘은 **IPrincipal** 및 **IIdentity**와 같은 두 가지 간단한 인터페이스를 기반으로 합니다. **IIdentity**의 구체적인 구현은 인증된 사용자를 나타냅니다. 예를 들어 **WindowsIdentity** 구현은 Active Directory에 의해 인증된 사용자를 나타내고, **GenericIdentity**는 사용자 지정 인증 프로세스를 통해 ID가 확인된 사용자를 나타냅니다. **IPrincipal**의 구체적인 구현은 역할 저장소에 따라 역할을 사용하여 권한을 확인하는 데 유용합니다. 예를 들어 **WindowsPrincipal**은 Active Directory 그룹의 멤버에 대한 **WindowsIdentity**를 확인합니다. **IPrincipal** 인터페이스에서 **IsInRole** 메서드를 호출하면 이러한 확인이 수행됩니다. 역할을 기반으로 액세스 권한을 확인하는 것을 RBAC(역할 기반 Access Control)라고 합니다. 자세한 내용은 [역할 기반 액세스 제어](claims-based-authorization-using-wif.md#BKMK_1)를 참조하세요.  클레임을 사용하여 친숙한 역할 기반 권한 부여 메커니즘을 지원하기 위해 역할에 대한 정보를 전달할 수 있습니다.  
  
 또한 클레임을 사용하여 역할보다 훨씬 복잡한 권한 부여 결정을 수행할 수도 있습니다. 클레임은 연령, 우편 번호, 신발 크기 등 사용자에 대한 거의 모든 정보를 기반으로 할 수 있습니다. 임의의 클레임을 기반으로 하는 액세스 제어 메커니즘을 클레임 기반 권한 부여라고 합니다. 자세한 내용은 [클레임 기반 권한 부여](claims-based-authorization-using-wif.md#BKMK_2)를 참조하세요.  
  
<a name="BKMK_1"></a>   
## <a name="role-based-access-control"></a>역할 기반 Access Control  
 RBAC는 사용자 역할에 따라 응용 프로그램에서 사용자 권한을 관리하고 적용하는 권한 부여 방법입니다. 사용자에게 작업을 수행하는 데 필요한 역할이 있는 경우 액세스 권한이 부여되고, 그렇지 않으면 액세스가 거부됩니다.  
  
### <a name="iprincipalisinrole-method"></a>IPrincipal.IsInRole 메서드  
 클레임 인식 응용 프로그램에서 RBAC 방식을 구현 하려면 비 클레임 인식 응용 프로그램에서와 마찬가지로 **IPrincipal** 인터페이스에서 **IsInRole ()** 메서드를 사용 합니다. 다음과 같은 여러 가지 방법으로 **IsInRole()** 메서드를 사용할 수 있습니다.  
  
- **IPrincipal.IsInRole(“Administrator”)** 의 명시적 호출 이 방법에서는 결과가 부울입니다. 이는 조건문에서 사용되며, 코드에서 임의의 위치에 사용할 수 있습니다.  
  
- 보안 요청 **PrincipalPermission.Demand()** 사용 이 방법에서는 요청이 충족되지 않는 경우 결과가 예외입니다. 이는 예외 처리 전략에 맞아야 합니다. 부울 반환과 비교했을 때 예외가 발생하면 성능적인 측면에서 비용이 훨씬 많이 듭니다. 이는 코드에서 임의의 위치에 사용할 수 있습니다.  
  
- 선언적 특성 **[PrincipalPermission(SecurityAction.Demand, Role = “Administrator”)]** 사용 이 방법은 메서드를 데코레이팅하는 데 사용되므로 선언적이라고 합니다. 메서드 구현 내의 코드 블록에는 사용할 수 없습니다. 요청이 충족되지 않는 경우 결과가 예외입니다. 예외 처리 전략에 맞는지 확인해야 합니다.  
  
- **web.config**의 **\<authorization>** 섹션을 사용하여 URL 권한 부여 사용 이 방법은 URL 수준에서 권한 부여를 관리하는 경우 적합합니다. 이는 앞서 언급한 것 중에서 가장 정교하지 않은 수준입니다. 이 방법의 장점은 구성 파일에서 내용이 변경되므로 변경 내용을 활용하기 위해 코드를 컴파일하지 않는다는 점입니다.  
  
### <a name="expressing-roles-as-claims"></a>역할을 클레임으로 표시  
 **IsInRole()** 메서드가 호출되면 현재 사용자에게 해당 역할이 있는지 확인하는 검사가 수행됩니다. 클레임 인식 응용 프로그램에서는 역할이 토큰에서 사용할 수 있는 역할 클레임 형식으로 표시됩니다. 역할 클레임 형식은 다음 URI를 사용하여 표시됩니다.  
  
 `http://schemas.microsoft.com/ws/2008/06/identity/claims/role`
  
 여러 가지 방법으로 역할 클레임 형식을 사용하여 토큰을 보강할 수 있습니다.  
  
- **토큰 발급 중**. 사용자가 인증되면 Microsoft Azure ACS(Access Control Service)와 같은 페더레이션 공급자 또는 ID 공급자 STS에 의해 역할 클레임이 발급될 수 있습니다.  
  
- **ClaimsAuthenticationManager를 사용하여 임의의 클레임을 클레임 역할 형식으로 변형** ClaimsAuthenticationManager는 WIF의 일부로 제공되는 구성 요소입니다. 이는 토큰을 검사하고 클레임을 추가, 변경 또는 제거하여 해당 토큰을 변형하면서 응용 프로그램을 시작할 때 요청을 가로챌 수 있도록 허용합니다. ClaimsAuthenticationManager를 사용 하 여 클레임 [을 변환 하는 방법에 대 한 자세한 내용은 방법: WIF 및 ACS](https://go.microsoft.com/fwlink/?LinkID=247445)를 사용 하는 클레임 인식 ASP.NET 응용 프로그램에서 RBAC (역할 기반 Access Control)를 구현 합니다.  
  
- **samlSecurityTokenRequirement 구성 섹션을 사용하여 임의의 클레임을 역할 형식으로 매핑** - 구성만 사용하여 클레임 변형을 완료하며 코딩이 필요하지 않은 선언적 방법입니다.  
  
<a name="BKMK_2"></a>   
## <a name="claims-based-authorization"></a>클레임 기반 권한 부여  
 클레임 기반 권한 부여는 액세스를 허용하거나 거부하는 권한 부여 결정이 클레임에서 결정을 내리는 데 사용할 수 있는 데이터를 사용하는 임의의 논리를 기반으로 수행되는 방법입니다. RBAC의 경우 사용되는 유일한 클레임은 역할 형식 클레임이라는 점에 유의하십시오. 사용자가 특정 역할에 속하는지 여부를 확인하기 위해 역할 형식 클레임이 사용되었습니다. 클레임 기반 권한 부여 방법을 사용하여 권한 부여 결정을 내리는 과정을 설명하기 위해 다음 단계를 고려하십시오.  
  
1. 응용 프로그램에서 사용자가 인증을 받아야 하는 요청을 수신합니다.  
  
2. WIF가 사용자를 ID 공급자로 리디렉션하고, 인증되면 응용 프로그램 요청에 대한 클레임이 있는 사용자를 나타내는 연결된 보안 토큰과 함께 해당 요청이 생성됩니다. WIF가 이러한 클레임을 사용자를 나타내는 보안 주체와 연결합니다.  
  
3. 응용 프로그램이 의사 결정 논리 메커니즘에 클레임을 전달합니다. 이는 메모리 내 코드, 웹 서비스에 대한 호출, 데이터베이스에 대한 쿼리, 정교한 규칙 엔진 또는 ClaimsAuthorizationManager를 사용하는 방식일 수 있습니다.  
  
4. 의사 결정 메커니즘이 클레임에 따라 결과를 계산합니다.  
  
5. 결과가 true이면 액세스가 허용되고 false인 경우에는 거부됩니다. 예를 들어, 규칙은 사용자가 21세 이상이고 워싱턴 주에 거주하는 것일 수 있습니다.  
  
 <xref:System.Security.Claims.ClaimsAuthorizationManager>는 응용 프로그램에서 클레임 기반 권한 부여를 위한 의사 결정 논리를 표면화하는 데 유용합니다. ClaimsAuthorizationManager는 .NET 4.5의 일부로 제공되는 WIF 구성 요소입니다. ClaimsAuthorizationManager를 사용하면 들어오는 요청을 가로채고 들어오는 클레임에 따라 권한 부여 결정을 수행하도록 선택 항목의 논리를 구현할 수 있습니다. 이는 권한 부여 논리를 변경해야 하는 경우 중요합니다. 이러한 경우 ClaimsAuthorizationManager를 사용해도 응용 프로그램의 무결성에 영향을 미치지 않으므로, 변경으로 인해 응용 프로그램에 오류가 발생할 가능성이 줄어듭니다. ClaimsAuthorizationManager를 사용 하 여 클레임 기반 액세스 제어를 구현 하는 방법에 대 한 [자세한 내용은 방법: WIF 및 ACS](https://go.microsoft.com/fwlink/?LinkID=247446)를 사용 하 여 클레임 인식 ASP.NET 응용 프로그램에서 클레임 권한 부여를 구현 합니다.
