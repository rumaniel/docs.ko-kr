---
title: 코드 액세스 보안
ms.date: 03/30/2017
helpviewer_keywords:
- named permission sets, code access security
- call stacks
- malicious code
- stack walk
- security [.NET Framework], code access security
- permissions [.NET Framework], code access security
- trusted code
- mobile code security
- unmanaged code, code access security
- granting permissions, code access security
- user authentication, code access security
- code access security
ms.assetid: 859af632-c80d-4736-8d6f-1e01b09ce127
author: mairaw
ms.author: mairaw
ms.openlocfilehash: bdb4e84170d4d3b95b8b51f12e0787937aaaf961
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205652"
---
# <a name="code-access-security"></a>코드 액세스 보안
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 복잡하게 연결된 오늘날의 컴퓨터 시스템은 다양한 알 수 없는 소스에서 시작되는 코드에 자주 노출됩니다. 코드를 전자 메일에 첨부 하거나, 문서에 포함 하거나, 인터넷을 통해 다운로드할 수 있습니다. 많은 컴퓨터 사용자는 데이터를 손상하거나 제거하여 시간과 비용 손실을 초래할 수 있는 악성 모바일 코드(바이러스와 웜 포함)의 효과를 직접 체험했습니다.  
  
 가장 일반적인 보안 메커니즘은 로그온 자격 증명(일반적으로 암호)에 따라 사용자에게 권한을 부여하고 사용자가 액세스할 수 있는 리소스(대개 디렉터리 및 파일)를 제한합니다. 그러나 이 접근 방식은 여러 가지 문제를 해결하지 못합니다. 사용자는 많은 소스에서 코드를 가져오며, 이 중의 일부는 신뢰할 수 없습니다. 코드에 버그 또는 취약성이 포함될 수 있으며, 이로 인해 코드가 악성 코드에 의해 악용될 수 있습니다. 코드에서 사용자가 예상하지 못한 작업을 수행하는 경우가 있습니다. 결과적으로 신중하고 신뢰할 수 있는 사용자가 악의적이거나 오류가 많은 소프트웨어를 실행할 경우 컴퓨터 시스템이 손상되고 개인 데이터가 유출될 수 있습니다. 대부분의 운영 체제 보안 메커니즘에서는 웹 페이지의 스크립트를 제외하고 코드를 실행하려면 코드의 모든 부분을 완전히 신뢰할 수 있어야 합니다. 따라서 시스템 간에 트러스트 관계가 없는 경우에도 한 컴퓨터 시스템에서 시작된 코드가 다른 시스템에서 보호된 상태로 실행될 수 있도록 허용하는 널리 적용 가능한 보안 메커니즘이 여전히 필요합니다.  
  
 .NET Framework에서는 악성 모바일 코드로부터 컴퓨터 시스템을 보호하고, 알 수 없는 출처의 코드가 보호된 상태로 실행될 수 있도록 하고, 신뢰할 수 있는 코드가 의도적으로 또는 실수로 보안을 손상시키지 않도록 방지하는 코드 액세스 보안이라는 보안 메커니즘을 제공합니다. 코드 액세스 보안을 통해 코드 발생 위치 및 코드 ID의 다른 측면에 따라 다양한 수준으로 코드를 신뢰할 수 있습니다. 또한 코드 액세스 보안은 코드에 다양한 신뢰 수준을 적용하여 실행되려면 완전히 신뢰할 수 있어야 하는 코드의 양을 최소화합니다. 코드 액세스 보안을 사용하면 코드가 악의적이거나 오류가 많은 코드에서 악용될 가능성을 줄일 수 있습니다. 코드에서 수행할 수 있도록 허용해야 하는 작업 집합을 지정할 수 있으므로 책임을 줄일 수 있습니다. 코드 액세스 보안은 코드에서 보안 취약성으로 인해 발생할 수 있는 손상을 최소화하는 데 도움이 될 수도 있습니다.  
  
> [!NOTE]
> .NET Framework 4에서 코드 액세스 보안에 대 한 주요 변경 내용이 적용 되었습니다. 가장 주목할 만한 변경은 [보안 투명성](security-transparent-code.md)이지만 코드 액세스 보안에 영향을 주는 다른 중요 한 변경 내용도 있습니다. 이러한 변경 내용에 대 한 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조 하세요.  
  
 코드 액세스 보안은 주로 라이브러리 코드와 부분적으로 신뢰할 수 있는 애플리케이션에 영향을 줍니다. 라이브러리 개발자는 부분적으로 신뢰할 수 있는 애플리케이션의 무단 액세스로부터 코드를 보호해야 합니다. 부분적으로 신뢰할 수 있는 애플리케이션은 인터넷과 같은 외부 소스에서 로드된 애플리케이션입니다. 데스크톱이나 로컬 인트라넷에 설치된 애플리케이션은 완전 신뢰로 실행됩니다. 완전 신뢰 응용 프로그램은 완전히 신뢰할 수 있으므로 [보안 투명](security-transparent-code.md)으로 표시 되지 않는 한 코드 액세스 보안의 영향을 받지 않습니다. 완전 신뢰 애플리케이션에 대한 유일한 제한 사항은 <xref:System.Security.SecurityTransparentAttribute> 특성으로 표시된 애플리케이션이 <xref:System.Security.SecurityCriticalAttribute> 특성으로 표시된 코드를 호출할 수 없다는 것입니다. 코드 액세스 보안을 적용할 수 있도록 부분적으로 신뢰할 수 있는 애플리케이션은 샌드박스(예: Internet Explorer)에서 실행되어야 합니다. 인터넷에서 응용 프로그램을 다운로드 하 여 데스크톱에서 실행 하려고 하면 다음과 같은 메시지가 표시 됩니다 <xref:System.NotSupportedException> . "이전 버전의 .NET Framework에서 어셈블리를 샌드 박싱 한 네트워크 위치에서 어셈블리를 로드 하려고 했습니다. .NET Framework의 이 릴리스는 기본적으로 CAS 정책을 사용하도록 설정하지 않으므로 이러한 로드는 위험할 수 있습니다." 응용 프로그램을 신뢰할 수 있는 경우 [ \<loadFromRemoteSources > 요소](../configure-apps/file-schema/runtime/loadfromremotesources-element.md)를 사용 하 여 완전 신뢰로 실행 되도록 설정할 수 있습니다. 샌드박스에서 응용 프로그램을 실행 [하는 방법에 대 한 자세한 내용은 방법: 샌드박스에서 부분적으로 신뢰할 수 있는 코드 실행](how-to-run-partially-trusted-code-in-a-sandbox.md)의 설명대로 신뢰할 수 없는 코드에 별도의 폴더를 사용합니다.  
  
 코드에서 단일 코드 액세스 보안 호출을 수행하지 않는 경우에도 공용 언어 런타임을 대상으로 하는 모든 관리 코드가 코드 액세스 보안의 혜택을 받습니다. 자세한 내용은 [코드 액세스 보안 기본 사항](code-access-security-basics.md)을 참조하세요.  
  
<a name="key_functions"></a>   
## <a name="key-functions-of-code-access-security"></a>코드 액세스 보안의 주요 기능  
 코드 액세스 보안은 보호된 리소스와 작업에 대한 코드의 액세스를 제한하는 데 도움이 됩니다. .NET Framework에서 코드 액세스 보안은 다음 기능을 수행합니다.  
  
- 다양한 시스템 리소스에 액세스하는 데 필요한 권한을 나타내는 권한 및 권한 집합을 정의합니다.  
  
- 코드에서 해당 코드의 호출자가 특정 권한을 갖도록 요구할 수 있도록 합니다.  
  
- 코드의 호출자가 디지털 서명을 갖도록 해당 코드가 요구하여 특정 조직이나 사이트의 호출자만이 보호된 코드를 호출할 수 있도록 합니다.  
  
- 호출 스택에 있는 모든 호출자에게 부여된 권한과 해당 호출자가 가져야 하는 권한을 비교하여 런타임에 코드를 제한합니다.  
  
<a name="walking_the_call_stack"></a>   
## <a name="walking-the-call-stack"></a>호출 스택 워크  
 리소스에 액세스하거나 작업을 수행할 수 있는 권한이 코드에 있는지 확인하기 위해서 런타임 보안 시스템은 호출 스택 워크를 수행하여 각 호출자에게 부여된 권한과 요청된 권한을 비교합니다. 호출 스택의 호출자에게 요청된 권한이 없는 경우 보안 예외가 발생하고 액세스가 거부됩니다. 스택 워크는 신뢰 수준이 낮은 코드가 신뢰 수준이 높은 코드를 호출하고 해당 코드를 통해 권한 없는 작업을 수행하는 유인 공격을 방지하기 위한 것입니다. 런타임에 모든 호출자의 권한을 요구할 경우 성능에 영향을 주지만 신뢰 수준이 낮은 코드에 의한 유인 공격으로부터 코드를 보호하는 데 필요합니다. 성능을 최적화하기 위해 코드에서 수행하는 스택 워크 수를 줄일 수 있지만 이 경우 보안 약점이 노출되지 않는지 항상 확인해야 합니다.  
  
 다음 그림에서는 Assembly A4의 메서드가 해당 호출자에게 P 권한이 있도록 요구할 때 발생하는 스택 워크를 보여 줍니다.  
  
 ![코드 액세스 보안](media/slide-10a.gif "slide_10a")  
보안 스택 워크  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[코드 액세스 보안 기본 사항](code-access-security-basics.md)|코드 액세스 보안 및 가장 일반적인 용도를 설명합니다.|  
|[보안 투명 코드, 수준 2](security-transparent-code-level-2.md)|.NET Framework 4의 보안 투명성 모델에 대해 설명 합니다.|  
|[부분적으로 신뢰할 수 있는 코드에서 라이브러리 사용](using-libraries-from-partially-trusted-code.md)|비관리 코드에 라이브러리를 사용할 수 있도록 하는 방법 및 비관리 코드에서 라이브러리를 사용하는 방법을 설명합니다.|  
|[주요 보안 개념](../../standard/security/key-security-concepts.md)|.NET Framework 보안 시스템에서 사용되는 주요 용어와 개념을 개략적으로 설명합니다.|  
|[역할 기반 보안](../../standard/security/role-based-security.md)|역할 기반 보안을 통합하는 방법을 설명합니다.|  
|[Cryptographic Services](../../standard/security/cryptographic-services.md)|애플리케이션에 암호화를 통합하는 방법을 설명합니다.|
