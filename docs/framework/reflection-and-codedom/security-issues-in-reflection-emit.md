---
title: 리플렉션 내보내기의 보안 문제점
ms.date: 03/30/2017
helpviewer_keywords:
- partially trusted code
- emitting dynamic assemblies, security
- reflection emit, security
- reflection emit, partial trust scenarios
- partial trust,emitting dynamic methods
- anonymously hosted dynamic methods [.NET Framework]
- emitting dynamic assemblies,partial trust scenarios
- dynamic assemblies, security
ms.assetid: 0f8bf8fa-b993-478f-87ab-1a1a7976d298
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f2bdaef52bbc4cac0abfcbf8724f3c5c602bc8f0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045794"
---
# <a name="security-issues-in-reflection-emit"></a>리플렉션 내보내기의 보안 문제점
.NET Framework에서는 MSIL(Microsoft Intermediate Language)을 내보내는 세 가지 방법을 제공하며, 각각 고유한 보안 문제가 있습니다.  
  
- [동적 어셈블리](#Dynamic_Assemblies)  
  
- [익명으로 호스트된 동적 메서드](#Anonymously_Hosted_Dynamic_Methods)  
  
- [기존 어셈블리와 연결된 동적 메서드](#Dynamic_Methods_Associated_with_Existing_Assemblies)  
  
 동적 코드를 생성하는 방법에 관계없이 생성된 코드를 실행하려면 생성된 코드가 사용하는 형식 및 메서드에 필요한 모든 권한이 있어야 합니다.  
  
> [!NOTE]
> .NET Framework의 이후 릴리스에서는 코드에 반영하고 코드를 내보내는 데 필요한 권한이 변경되었습니다. 이 항목의 뒷부분에 있는 [버전 정보](#Version_Information)를 참조하세요.  
  
<a name="Dynamic_Assemblies"></a>   
## <a name="dynamic-assemblies"></a>동적 어셈블리  
 동적 어셈블리는 <xref:System.AppDomain.DefineDynamicAssembly%2A?displayProperty=nameWithType> 메서드의 오버로드를 사용하여 만듭니다. 이 메서드의 오버로드는 시스템 수준의 보안 정책이 제거되어 .NET Framework 4에서 대부분 사용되지 않습니다. [보안 변경 내용](../security/security-changes.md)을 참조하세요. 나머지 오버로드는 신뢰 수준에 관계없이 모든 코드에서 실행할 수 있습니다. 이러한 오버로드는 만들 때 동적 어셈블리에 적용할 특성 목록을 지정하는 오버로드와 그러지 않은 오버로드의 두 그룹으로 나뉩니다. 어셈블리를 만들 때 <xref:System.Security.SecurityRulesAttribute> 특성을 적용하여 어셈블리에 대한 투명도 모델을 지정하지 않을 경우 내보내는 어셈블리에서 투명도 모델이 상속됩니다.  
  
> [!NOTE]
> 동적 어셈블리를 만든 후에 <xref:System.Reflection.Emit.AssemblyBuilder.SetCustomAttribute%2A> 메서드를 사용하여 적용하는 특성은 어셈블리를 디스크에 저장하고 메모리에 다시 로드할 때까지 적용되지 않습니다.  
  
 동적 어셈블리의 코드는 다른 어셈블리에 표시되는 형식 및 멤버에 액세스할 수 있습니다.  
  
> [!NOTE]
> 동적 어셈블리는 동적 멤버가 public이 아닌 형식 및 멤버에 액세스할 수 있도록 허용하는 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 및 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그를 사용하지 않습니다.  
  
 임시 동적 어셈블리는 메모리에 만들어지고 디스크에 저장되지 않으므로 파일 액세스 권한이 필요하지 않습니다. 동적 어셈블리를 디스크에 저장하려면 적절한 플래그가 있는 <xref:System.Security.Permissions.FileIOPermission>이 필요합니다.  
  
### <a name="generating-dynamic-assemblies-from-partially-trusted-code"></a>부분적으로 신뢰할 수 있는 코드에서 동적 어셈블리 생성  
 인터넷 권한이 있는 어셈블리가 임시 동적 어셈블리를 생성하고 해당 코드를 실행할 수 있는 다음 조건을 고려합니다.  
  
- 동적 어셈블리가 다른 어셈블리의 public 형식 및 멤버만 사용합니다.  
  
- 이러한 형식과 멤버가 요구하는 권한이 부분적으로 신뢰할 수 있는 어셈블리의 권한 부여 집합에 포함되어 있습니다.  
  
- 어셈블리가 디스크에 저장되지 않습니다.  
  
- 디버그 기호가 생성되지 않습니다. `Internet` 및 `LocalIntranet` 권한 집합에는 필요한 권한이 포함되지 않습니다.  
  
<a name="Anonymously_Hosted_Dynamic_Methods"></a>   
## <a name="anonymously-hosted-dynamic-methods"></a>익명으로 호스트된 동적 메서드  
 익명으로 호스트된 동적 메서드는 연결된 형식이나 모듈을 지정하지 않는 두 개의 <xref:System.Reflection.Emit.DynamicMethod> 생성자인 <xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%29> 및 <xref:System.Reflection.Emit.DynamicMethod.%23ctor%28System.String%2CSystem.Type%2CSystem.Type%5B%5D%2CSystem.Boolean%29>를 사용하여 만듭니다. 이러한 생성자는 완전히 신뢰할 수 있는 시스템 제공 보안 투명 어셈블리에 동적 메서드를 배치합니다. 이 생성자를 사용하거나 동적 메서드에 대한 코드를 내보내는 데 필요한 권한은 없습니다.  
  
 대신 익명으로 호스트된 동적 메서드를 만들 때 호출 스택이 캡처됩니다. 메서드를 생성할 때 캡처된 호출 스택에 대해 보안 요구가 수행됩니다.  
  
> [!NOTE]
> 개념적으로, 메서드의 생성하는 동안 요구가 수행됩니다. 즉, 각 MSIL 명령을 내보낼 때 요구를 수행할 수 있습니다. 현재 구현에서는 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A>를 호출하지 않고 메서드가 호출된 경우 <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A?displayProperty=nameWithType> 메서드를 호출하거나 JIT(Just-In-Time) 컴파일러를 호출할 때 모든 요구가 수행됩니다.  
  
 애플리케이션 도메인에서 허용하는 경우, 익명으로 호스트되는 동적 메서드는 다음 제한 사항에 따라 JIT 가시성 검사를 건너뛸 수 있습니다. 익명으로 호스트되는 동적 메서드로 액세스되는 비공개 형식과 멤버는 내보내기 호출 스택의 해당 권한 부여 집합과 같거나 하위 집합인 어셈블리에 있어야 합니다. JIT 가시성 검사를 건너뛸 수 있는 이 제한된 기능은 애플리케이션 도메인에서 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그로 <xref:System.Security.Permissions.ReflectionPermission> 권한을 부여하는 경우에 사용할 수 있습니다.  
  
- 메서드가 public 형식 및 멤버만 사용하는 경우에는 생성 중 권한이 필요하지 않습니다.  
  
- JIT 가시성 검사를 건너뛰도록 지정하면 메서드를 생성할 때 수행되는 요구에 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission> 및 액세스되는 public이 아닌 멤버를 포함하는 어셈블리의 권한 부여 집합이 포함됩니다.  
  
 public이 아닌 멤버의 권한 부여 집합을 고려하기 때문에 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 권한이 부여된 부분적으로 신뢰할 수 있는 코드는 신뢰할 수 있는 어셈블리의 public이 아닌 멤버를 실행하여 권한을 높일 수 없습니다.  
  
 다른 내보낸 코드와 마찬가지로, 동적 메서드를 실행하려면 동적 메서드가 사용하는 메서드에서 요구하는 권한이 있어야 합니다.  
  
 익명으로 호스트된 동적 메서드를 호스트하는 시스템 어셈블리는 .NET Framework 4 이전의 .NET Framework에서 사용된 투명도 모델인 <xref:System.Security.SecurityRuleSet.Level1?displayProperty=nameWithType> 투명도 모델을 사용합니다.  
  
 자세한 내용은 <xref:System.Reflection.Emit.DynamicMethod> 클래스를 참조하세요.  
  
### <a name="generating-anonymously-hosted-dynamic-methods-from-partially-trusted-code"></a>부분적으로 신뢰할 수 있는 코드에서 익명으로 호스트된 동적 메서드 생성  
 인터넷 권한이 있는 어셈블리가 익명으로 호스트된 동적 메서드를 생성하고 실행할 수 있는 다음 조건을 고려합니다.  
  
- 동적 메서드가 public 형식 및 멤버만 사용합니다. 권한 부여 집합에 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>가 포함된 경우 권한 부여 집합이 내보내는 어셈블리의 권한 부여 집합과 같거나 하위 집합인 어셈블리의 public이 아닌 형식 및 멤버를 사용할 수 있습니다.  
  
- 동적 메서드가 사용하는 모든 형식과 멤버에 필요한 권한이 부분적으로 신뢰할 수 있는 어셈블리의 권한 부여 집합에 포함되어 있습니다.  
  
> [!NOTE]
> 동적 메서드가 디버그 기호를 지원하지 않습니다.  
  
<a name="Dynamic_Methods_Associated_with_Existing_Assemblies"></a>   
## <a name="dynamic-methods-associated-with-existing-assemblies"></a>기존 어셈블리와 연결된 동적 메서드  
 동적 메서드를 기존 어셈블리의 형식이나 모듈에 연결하려면 연결된 형식이나 모듈을 지정하는 <xref:System.Reflection.Emit.DynamicMethod> 생성자 중 하나를 사용합니다. 동적 메서드를 기존 형식이나 모듈에 연결하면 동적 메서드가 public이 아닌 형식과 멤버에 액세스할 수 있으므로 이 생성자를 호출하는 데 필요한 권한은 경우에 따라 다릅니다.  
  
- 형식과 연결된 동적 메서드는 private 멤버를 비롯한 해당 형식의 모든 멤버와 연결된 형식을 포함하는 어셈블리의 모든 내부 형식과 멤버에 액세스할 수 있습니다.  
  
- 모듈과 연결된 동적 메서드는 모듈의 모든 `internal` 형식과 멤버(Visual Basic에서는 `Friend`, 공용 언어 런타임 메타데이터에서는 `assembly`)에 액세스할 수 있습니다.  
  
 또한 JIT 컴파일러의 가시성 검사를 건너뛰는 기능을 지정하는 생성자를 사용할 수 있습니다. 이렇게 하면 동적 메서드가 액세스 수준에 관계없이 모든 어셈블리의 모든 형식과 멤버에 액세스할 수 있습니다.  
  
 생성자가 요구하는 권한은 동적 메서드에 제공할 액세스 권한에 따라 달라집니다.  
  
- 메서드가 public 형식과 멤버만 사용하고 메서드를 고유한 형식이나 모듈에 연결하는 경우에는 권한이 필요하지 않습니다.  
  
- JIT 가시성 검사를 건너뛰도록 지정하는 경우 생성자는 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>을 요구합니다.  
  
- 고유한 어셈블리의 다른 형식을 포함하여 다른 형식에 동적 메서드를 연결하는 경우 생성자는 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission> 및 <xref:System.Security.Permissions.SecurityPermissionFlag.ControlEvidence?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.SecurityPermission>을 요구합니다.  
  
- 다른 어셈블리의 형식이나 모듈에 동적 메서드를 연결하는 경우 생성자는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission> 및 다른 모듈을 포함하는 어셈블리의 권한 부여 집합을 요구합니다. 즉, 호출 스택에 대상 모듈의 권한 부여 집합에 있는 모든 권한과 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>가 포함되어야 합니다.  
  
    > [!NOTE]
    > 대상 권한 부여 집합 및 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 요구가 실패할 경우 생성자는 이전 버전과의 호환성을 위해 <xref:System.Security.Permissions.SecurityPermissionFlag.ControlEvidence?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.SecurityPermission>을 요구합니다.  
  
 이 목록의 항목은 내보내는 어셈블리의 권한 부여 집합 측면에서 설명하지만 요구는 애플리케이션 도메인 경계를 포함하여 전체 호출 스택에 대해 수행됩니다.  
  
 자세한 내용은 <xref:System.Reflection.Emit.DynamicMethod> 클래스를 참조하세요.  
  
### <a name="generating-dynamic-methods-from-partially-trusted-code"></a>부분적으로 신뢰할 수 있는 코드에서 동적 메서드 생성  
  
> [!NOTE]
> 부분적으로 신뢰할 수 있는 코드에서 동적 메서드를 생성하는 경우 [익명으로 호스트된 동적 메서드](#Anonymously_Hosted_Dynamic_Methods)를 사용하는 것이 좋습니다.  
  
 인터넷 권한이 있는 어셈블리가 동적 메서드를 생성하고 실행할 수 있는 다음 조건을 고려합니다.  
  
- 동적 메서드가 메서드를 내보내는 모듈 또는 형식과 연결되어 있거나, 해당 권한 부여 집합이 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>를 포함하며 권한 부여 집합이 내보내는 어셈블리의 권한 부여 집합과 같거나 하위 집합인 어셈블리의 모듈과 연결되어 있습니다.  
  
- 동적 메서드가 public 형식 및 멤버만 사용합니다. 해당 권한 부여 집합이 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType>를 포함하며 권한 부여 집합이 내보내는 어셈블리의 권한 부여 집합과 같거나 하위 집합인 어셈블리의 모듈과 연결된 경우 연결된 모듈에서 `internal`(Visual Basic에서는 `Friend`, 공용 언어 런타임 메타데이터에서는 `assembly`)로 표시된 형식과 멤버를 사용할 수 있습니다.  
  
- 동적 메서드가 사용하는 모든 형식과 멤버가 요구하는 권한이 부분적으로 신뢰할 수 있는 어셈블리의 권한 부여 집합에 포함되어 있습니다.  
  
- 동적 메서드가 JIT 가시성 검사를 건너뛰지 않습니다.  
  
> [!NOTE]
> 동적 메서드가 디버그 기호를 지원하지 않습니다.  
  
<a name="Version_Information"></a>   
## <a name="version-information"></a>버전 정보  
 .NET Framework 4부터 시스템 수준의 보안 정책이 제거되었으며 보안 투명도가 기본 적용 메커니즘이 되었습니다. [보안 변경 내용](../security/security-changes.md)을 참조하세요.  
  
 .NET Framework 2.0 Service Pack 1부터 동적 어셈블리와 동적 메서드를 내보낼 때 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>이 더 이상 필요하지 않습니다. 이 플래그는 .NET Framework의 모든 이전 버전에서 필요합니다.  
  
> [!NOTE]
> <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>은 기본적으로 명명된 권한 집합 `FullTrust` 및 `LocalIntranet` 에 포함되지만 `Internet` 권한 집합에는 포함되지 않습니다. 따라서 이전 버전의 .NET Framework에서는 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit>에 대해 <xref:System.Security.PermissionSet.Assert%2A>를 실행하는 경우에만 인터넷 권한으로 라이브러리를 사용할 수 있습니다. 코딩 오류가 있을 경우 보안 허점이 발생할 수 있으므로 이러한 라이브러리는 신중한 보안 검토가 필요합니다. .NET Framework 2.0 SP1에서는 코드 생성이 기본적으로 권한 있는 작업이 아니기 때문에 보안 요구를 실행하지 않고 부분 신뢰 시나리오에서 코드를 내보낼 수 있습니다. 즉, 생성된 코드에 코드를 내보내는 어셈블리보다 많은 권한이 없습니다. 따라서 코드를 내보내는 라이브러리가 보안상 투명할 수 있으며 <xref:System.Security.Permissions.ReflectionPermissionFlag.ReflectionEmit>를 어설션할 필요가 없으므로 보안 라이브러리 작성 작업이 간소화됩니다.  
  
 또한 .NET Framework 2.0 SP1에서는 부분적으로 신뢰할 수 있는 동적 메서드에서 public이 아닌 형식과 멤버에 액세스하기 위한 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그가 도입되었습니다. 이전 버전의 .NET Framework에서는 public이 아닌 형식과 멤버에 액세스하는 동적 메서드에 대해 부분적으로 신뢰할 수 있는 코드에 부여하면 안 되는 권한인 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그가 필요합니다.  
  
 끝으로, .NET Framework 2.0 SP1에서는 익명으로 호스트된 메서드가 도입되었습니다.  
  
### <a name="obtaining-information-on-types-and-members"></a>형식 및 멤버에 대한 정보 가져오기  
 .NET Framework 2.0부터 public이 아닌 형식과 멤버에 대한 정보를 가져오는 데 필요한 권한은 없습니다. 리플렉션을 사용하여 동적 메서드를 내보내는 데 필요한 정보를 가져옵니다. 예를 들어 <xref:System.Reflection.MethodInfo> 개체를 사용하여 메서드 호출을 내보냅니다. 이전 버전의 .NET Framework에서는 <xref:System.Security.Permissions.ReflectionPermissionFlag.TypeInformation?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>이 필요합니다. 자세한 내용은 [리플렉션의 보안 고려 사항](security-considerations-for-reflection.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [리플렉션의 보안 고려 사항](security-considerations-for-reflection.md)
- [동적 메서드 및 어셈블리 내보내기](emitting-dynamic-methods-and-assemblies.md)
