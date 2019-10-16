---
title: 주요 보안 개념
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- unauthorized access
- permissions [.NET Framework]
- security [.NET Framework], about security
ms.assetid: 3cfced4f-ea02-4e66-ae98-d69286363e98
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fe4c2e1775313039e8612ae7efbd3d22af710bab
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917253"
---
# <a name="key-security-concepts"></a>주요 보안 개념
Microsoft .NET Framework는 모바일 코드에 대한 보안 문제를 해결하고 사용자에게 수행할 수 있는 권한이 있는 작업을 구성 요소가 확인할 수 있게 해주는 지원을 제공하기 위해 역할 기반 보안을 제공합니다.  
  
## <a name="type-safety-and-security"></a>형식 안전성 및 보안  
 형식 안전 코드는 액세스 권한이 부여된 메모리 위치에만 액세스합니다. 이 토론에서 형식 안전성은 특히 메모리 형식 안전성을 가리키며 보다 광범위한 의미의 형식 안전성과 혼동해서는 안 됩니다. 예를 들어 형식 안전 코드는 다른 개체의 전용 필드에서 값을 읽을 수 없습니다. 잘 정의된 허용되는 방식으로만 형식에 액세스합니다.  
  
 JIT(Just-In-Time) 컴파일 중에 선택적 검증 프로세스는 네이티브 기계어 코드로 JIT 컴파일될 메서드의 메타데이터 및 MSIL(Microsoft Intermediate Language)을 검사하여 형식이 안전한지 확인합니다. 코드에 검증을 건너뛸 수 있는 권한이 있으면 이 프로세스를 건너뜁니다. 검증에 대한 자세한 내용은 [관리되는 실행 프로세스](../../../docs/standard/managed-execution-process.md)를 참조하세요.  
  
 형식 안전성 검증은 관리 코드를 실행하기 위한 필수 사항이 아니지만 형식 안전성은 어셈블리 격리 및 보안 적용에서 중요한 역할을 합니다. 코드 형식이 안전한 경우 공용 언어 런타임에서 어셈블리를 서로 완전히 격리할 수 있습니다. 이 격리는 어셈블리가 서로 부정적인 영향을 줄 수 없도록 하며 애플리케이션 안정성을 향상시킵니다. 형식이 안전한 구성 요소는 서로 다른 수준에서 신뢰된 경우에도 동일한 프로세스에서 안전하게 실행할 수 있습니다. 코드 형식이 안전하지 않은 경우 원치 않는 부작용이 발생할 수 있습니다. 예를 들면, 관리 코드가 네이티브(비관리) 코드로 호출되어 부정적인 작업을 수행하는 것을 런타임에서 방지할 수 없습니다. 코드 형식이 안전하면 런타임의 보안 적용 메커니즘에서 권한이 없을 경우 네이티브 코드에 액세스하지 않도록 합니다. 형식이 안전하지 않은 모든 코드를 실행하려면 전달된 열거형 멤버 <xref:System.Security.Permissions.SecurityPermissionAttribute.SkipVerification%2A>과 함께 <xref:System.Security.Permissions.SecurityPermission>이 부여되어야 합니다.  
  
 자세한 내용은 [코드 액세스 보안 기본 사항](../../../docs/framework/misc/code-access-security-basics.md)을 참조하세요.  
  
## <a name="principal"></a>보안 주체  
 보안 주체는 사용자의 ID 및 역할을 나타내고 사용자 대신 역할을 수행합니다. .NET Framework의 역할 기반 보안은 다음 세 종류의 보안 주체를 지원합니다.  
  
- 일반 보안 주체는 Windows 사용자 및 역할과 독립적으로  존재하는 사용자와 역할을 나타냅니다.  
  
- Windows 보안 주체는 Windows 사용자와 해당 역할(또는 해당 Windows 그룹)을 나타냅니다. Windows 보안 주체는 다른 사용자를 가장할 수 있습니다. 이는 해당 사용자에게 속하는 ID를 제공하는 동안 보안 주체가 사용자 대신 리소스에 액세스할 수 있음을 의미합니다.  
  
- 해당 특정 애플리케이션에 필요한 방식으로 애플리케이션에서 사용자 지정 보안 주체를 정의할 수 있습니다. 보안 주체의 ID 및 역할의 기본 개념을 확장할 수 있습니다.  
  
 자세한 내용은 [Principal 개체 및 Identity 개체](../../../docs/standard/security/principal-and-identity-objects.md)를 참조하세요.  
  
## <a name="authentication"></a>인증  
 인증은 사용자 자격 증명을 검사하고 일부 권한에 대해 해당 자격 증명의 유효성을 검사하여 보안 주체의 ID를 찾고 확인하는 프로세스입니다. 인증 중에 얻은 정보를 코드에서 직접 사용할 수 있습니다. .NET Framework 역할 기반 보안을 사용하여 현재 사용자를 인증하고 해당 보안 주체가 코드에 액세스할 수 있도록 할지 여부를 결정할 수도 있습니다. 특정 역할에 대해 보안 주체를 인증하는 방법의 예는 <xref:System.Security.Principal.WindowsPrincipal.IsInRole%2A?displayProperty=nameWithType> 메서드 오버로드를 참조하세요. 예를 들어 <xref:System.Security.Principal.WindowsPrincipal.IsInRole%28System.String%29?displayProperty=nameWithType> 오버로드를 사용하여 현재 사용자가 Administrators 그룹의 멤버인지 확인할 수 있습니다.  
  
 현재 다양한 인증 메커니즘이 사용되며, 대부분 .NET Framework 역할 기반 보안과 함께 사용할 수 있습니다. 가장 일반적으로 사용되는 메커니즘 중 일부는 기본, 다이제스트, Passport, 운영 체제(예: NTLM 또는 Kerberos) 또는 애플리케이션 정의 메커니즘입니다.  
  
### <a name="example"></a>예제  
 다음 예제에서는 활성 보안 주체가 관리자여야 합니다. `name` 매개 변수는 `null`이므로 관리자인 모든 사용자가 요구를 전달할 수 있습니다.  
  
> [!NOTE]
> Windows Vista에서는 UAC(사용자 계정 컨트롤)가 사용자 권한을 결정합니다. 기본 제공 Administrators 그룹의 멤버인 경우 두 개의 런타임 액세스 토큰(표준 사용자 액세스 토큰 및 관리자 액세스 토큰)이 할당됩니다. 기본적으로 표준 사용자 역할이 지정됩니다. 관리자 권한이 필요한 코드를 실행하려면 먼저 표준 사용자에서 관리자로 권한을 높여야 합니다. 애플리케이션 아이콘을 마우스 오른쪽 단추로 클릭하고 관리자로 실행하도록 지정하여 애플리케이션을 시작하면 이 작업을 수행할 수 있습니다.  
  
 [!code-cpp[Classic PrincipalPermission Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CPP/source.cpp#1)]
 [!code-csharp[Classic PrincipalPermission Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/CS/source.cs#1)]
 [!code-vb[Classic PrincipalPermission Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_Classic/classic PrincipalPermission Example/VB/source.vb#1)]  
  
 다음 예제에서는 보안 주체 및 보안 주체가 사용할 수 있는 역할의 ID를 확인하는 방법을 보여 줍니다. 이 예제의 애플리케이션은 현재 사용자가 애플리케이션을 사용하도록 허용하는 역할에 있는지 확인하기 위한 것일 수 있습니다.  
  
 [!code-cpp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CPP/source.cpp#1)]
 [!code-csharp[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/CS/source.cs#1)]
 [!code-vb[System.Security.Principal.WindowsBuiltInRole Example#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Security.Principal.WindowsBuiltInRole Example/VB/source.vb#1)]  
  
## <a name="authorization"></a>권한 부여  
 권한 부여는 보안 주체가 요청된 작업을 수행할 수 있는지 여부를 확인하는 프로세스입니다. 권한 부여는 인증 후 발생하며 보안 주체의 ID 및 역할에 대한 정보를 사용하여 보안 주체가 액세스할 수 있는 리소스를 확인합니다. .NET Framework 역할 기반 보안을 사용하여 권한 부여를 구현할 수 있습니다.
