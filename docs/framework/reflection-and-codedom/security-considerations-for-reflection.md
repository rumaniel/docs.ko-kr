---
title: 리플렉션의 보안 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- permissions [.NET Framework], reflection
- MethodInfo parameters
- reflection, security
- partial trust,reflection
- nonpublic members
- reflection,partial trust
- link demands
ms.assetid: 42d9dc2a-8fcc-4ff3-b002-4ff260ef3dc5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 852490c57a2954e9d56799ef8deebbef31d5f665
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045893"
---
# <a name="security-considerations-for-reflection"></a>리플렉션의 보안 고려 사항

리플렉션은 형식 및 멤버에 대한 정보를 가져오고 멤버에 액세스하는 기능(즉, 메서드 및 생성자 호출, 속성 값 가져오기 및 설정, 이벤트 처리기 추가 및 제거 등)을 제공합니다. 리플렉션을 사용하여 형식 및 멤버에 대한 정보를 가져오는 기능은 제한되지 않습니다. 모든 코드에서 리플렉션을 사용하여 다음 작업을 수행할 수 있습니다.

- 형식 및 멤버를 열거하고 해당 메타데이터를 검사합니다.

- 어셈블리 및 모듈을 열거하고 검사합니다.

반면, 리플렉션을 사용하여 멤버에 액세스하는 경우 제한 사항이 적용됩니다. .NET Framework 4부터 신뢰할 수 있는 코드만 리플렉션을 사용하여 보안에 중요한 멤버에 액세스할 수 있습니다. 또한 신뢰할 수 있는 코드만 리플렉션을 사용하여 컴파일된 코드에서 직접 액세스할 수 없는 public이 아닌 멤버에 액세스할 수 있습니다. 마지막으로, 안전상 중요한 멤버에 액세스하기 위해 리플렉션을 사용하는 코드는 컴파일된 코드와 마찬가지로 안전상 중요한 멤버에서 요구하는 권한을 가져야 합니다.

필요한 권한이 적용되는 경우 코드에서 리플렉션을 사용하여 다음 종류의 액세스를 수행할 수 있습니다.

- 보안에 중요하지 않은 public 멤버에 액세스합니다.

- 해당 멤버가 보안에 중요하지 않은 경우 컴파일된 코드에서 액세스할 수 있는 public이 아닌 멤버에 액세스합니다. public이 아닌 이러한 멤버의 예는 다음과 같습니다.

  - 호출 코드 기본 클래스의 보호된 멤버 (리플렉션에서는 제품군 수준 액세스라고 함)

  - 호출 코드 어셈블리의 `internal` 멤버(Visual Basic에서는 `Friend` 멤버) (리플렉션에서는 어셈블리 수준 액세스라고 함)

  - 호출 코드를 포함하는 다른 클래스 인스턴스의 private 멤버

예를 들어 샌드박스 애플리케이션 도메인에서 실행되는 코드는 애플리케이션 도메인이 추가 권한을 부여하지 않는 한 이 목록에 설명된 액세스로 제한됩니다.

.NET Framework 2.0 Service Pack 1부터 일반적으로 액세스할 수 없는 멤버에 액세스하려고 하면 대상 개체 및 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>의 권한 부여 집합에 대한 요구가 생성됩니다. 완전 신뢰 수준으로 실행되는 코드(예: 명령줄에서 시작된 애플리케이션의 코드)는 항상 이러한 권한을 충족시킬 수 있습니다. 이 경우 이 문서의 뒷부분에 설명된 것처럼 보안에 중요한 멤버에 액세스할 때의 제한 사항이 적용됩니다.

필요한 경우 이 문서의 뒷부분에 있는 [일반적으로 액세스할 수 없는 멤버 액세스](#accessingNormallyInaccessible) 섹션에 설명된 대로 샌드박스 애플리케이션 도메인에서 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그로 <xref:System.Security.Permissions.ReflectionPermission>을 부여할 수 있습니다.

<a name="accessingSecurityCritical"></a>

## <a name="accessing-security-critical-members"></a>보안에 중요한 멤버 액세스

<xref:System.Security.SecurityCriticalAttribute>가 있거나, <xref:System.Security.SecurityCriticalAttribute>를 가진 형식에 속하거나, 보안에 중요한 어셈블리에 있는 경우 멤버가 보안에 중요합니다. .NET Framework 4부터 보안에 중요한 멤버에 액세스하기 위한 규칙은 다음과 같습니다.

- 코드를 완전히 신뢰할 수 있는 경우에도 투명 코드는 리플렉션을 사용하여 보안에 중요한 멤버에 액세스할 수 없습니다. <xref:System.MethodAccessException>, <xref:System.FieldAccessException> 또는 <xref:System.TypeAccessException>이 발생합니다.

- 부분 신뢰로 실행되는 코드는 투명으로 처리됩니다.

이러한 규칙은 보안에 중요한 멤버를 컴파일된 코드에서 직접 액세스하는지 또는 리플렉션을 사용하여 액세스하는지에 관계없이 동일합니다.

명령줄에서 실행 되는 애플리케이션 코드는 완전 신뢰로 실행됩니다. 투명으로 표시되지 않은 한 리플렉션을 사용하여 보안에 중요한 멤버에 액세스할 수 있습니다. 동일한 코드가 부분 신뢰(예: 샌드박스 애플리케이션 도메인에서)로 실행될 때 어셈블리의 신뢰 수준은 보안 중요 코드에 액세스할 수 있는지 여부를 결정합니다. 어셈블리에 강력한 이름이 있고 글로벌 어셈블리 캐시에 설치된 경우, 신뢰할 수 있는 어셈블리이며 보안에 중요한 멤버를 호출할 수 있습니다. 신뢰할 수 없는 경우 투명으로 표시되지 않았어도 투명하게 되며 보안에 중요한 멤버를 액세스할 수 없습니다.

.NET Framework 4의 보안 모델에 대한 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조하세요.

## <a name="reflection-and-transparency"></a>리플렉션 및 투명도

.NET Framework 4부터 공용 언어 런타임에서 어셈블리의 신뢰 수준 및 애플리케이션 도메인의 신뢰 수준을 포함하여 여러 요소의 형식 또는 멤버에 대한 투명도 수준을 결정합니다. 리플렉션은 형식의 투명도 수준을 검색할 수 있게 해주는 <xref:System.Type.IsSecurityCritical%2A>, <xref:System.Type.IsSecuritySafeCritical%2A> 및 <xref:System.Type.IsSecurityTransparent%2A> 속성을 제공합니다. 다음 표에서는 이러한 속성의 유효한 조합을 보여 줍니다.

|보안 수준|IsSecurityCritical|IsSecuritySafeCritical|IsSecurityTransparent|
|--------------------|------------------------|----------------------------|---------------------------|
|위험|`true`|`false`|`false`|
|안전에 중요|`true`|`true`|`false`|
|투명|`false`|`false`|`true`|

이러한 속성을 사용하는 것이 어셈블리 및 해당 형식의 보안 주석을 검사하고 현재 신뢰 수준을 확인한 다음 런타임 규칙을 복제하는 것보다 훨씬 더 간단합니다. 예를 들어 동일한 형식이 명령줄에서 실행되는 경우 보안에 중요하고, 샌드박스 애플리케이션 도메인에서 실행되는 경우 보안에 투명할 수 있습니다.

<xref:System.Reflection.MethodBase>, <xref:System.Reflection.FieldInfo>, <xref:System.Reflection.Emit.TypeBuilder>, <xref:System.Reflection.Emit.MethodBuilder> 및 <xref:System.Reflection.Emit.DynamicMethod> 클래스에도 비슷한 속성이 있습니다. 기타 리플렉션 및 리플렉션 내보내기 추상화의 경우 연결된 메서드에 보안 특성이 적용됩니다. 예를 들어 속성의 경우 속성 접근자에 적용됩니다.

<a name="accessingNormallyInaccessible"></a>

## <a name="accessing-members-that-are-normally-inaccessible"></a>일반적으로 액세스할 수 없는 멤버 액세스

리플렉션을 사용하여 공용 언어 런타임의 접근성 규칙에 따라 액세스할 수 없는 멤버를 호출하려면 코드에 다음 두 가지 권한 중 하나를 부여해야 합니다.

- 코드에서 public이 아닌 멤버를 호출할 수 있게 하려면 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그를 통해 코드에 <xref:System.Security.Permissions.ReflectionPermission>을 부여해야 합니다.

  > [!NOTE]
  > 기본적으로 보안 정책은 인터넷에서 시작된 코드에 대해 이 권한을 거부합니다. 인터넷에서 시작된 코드에는 이 권한을 부여하면 안 됩니다.

- 호출된 멤버를 포함하는 어셈블리의 권한 부여 집합이 호출 코드를 포함하는 어셈블리의 권한 부여 집합과 같거나 하위 집합인 경우 코드가 public이 아닌 멤버를 호출할 수 있도록 허용하려면 다음을 수행합니다. 코드는 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>에 부여되어야 합니다.

예를 들어 애플리케이션 도메인 인터넷 권한 및 <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그를 통한 <xref:System.Security.Permissions.ReflectionPermission>을 부여한 다음 두 어셈블리 A와 B를 사용하여 인터넷 애플리케이션을 실행한다고 가정합니다.

- 어셈블리 B의 권한 부여 집합은 A에 부여되지 않은 권한을 포함하지 않으므로 어셈블리 A가 리플렉션을 사용하여 어셈블리 B의 private 멤버에 액세스할 수 있습니다.

- mscorlib.dll은 완전히 신뢰할 수 있어 어셈블리 A에 부여되지 않은 권한이 있으므로 어셈블리 A가 리플렉션을 사용하여 mscorlib.dll과 같은 .NET Framework 어셈블리의 private 멤버에 액세스할 수 없습니다. 런타임에 코드 액세스 보안이 스택을 이동하는 경우 <xref:System.MemberAccessException>이 발생합니다.

## <a name="serialization"></a>Serialization

직렬화를 위해 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter%2A?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.SecurityPermission>은 접근성에 관계없이 직렬화 가능 형식의 멤버를 가져오고 설정하는 기능을 제공합니다. 이 권한을 통해 코드에서 인스턴스의 private 상태를 검색하고 변경할 수 있습니다. 적절한 권한이 부여되는 것 외에도 메타데이터에서 형식이 직렬화 가능으로 [표시](../../standard/attributes/applying-attributes.md)되어야 합니다.

## <a name="parameters-of-type-methodinfo"></a>MethodInfo 형식의 매개 변수

특히 신뢰할 수 있는 코드의 경우 <xref:System.Reflection.MethodInfo> 매개 변수를 사용하는 public 멤버를 작성하지 마세요. 이러한 멤버는 악성 코드에 더 취약할 수 있습니다. 예를 들어 <xref:System.Reflection.MethodInfo> 매개 변수를 사용하는 신뢰할 수 있는 코드의 public 멤버를 살펴보겠습니다. public 멤버가 제공된 매개 변수에 대해 <xref:System.Reflection.MethodBase.Invoke%2A> 메서드를 간접적으로 호출한다고 가정합니다. public 멤버가 필요한 권한 검사를 수행하지 않는 경우 보안 시스템에서 호출자를 신뢰할 수 있는 것으로 결정하기 때문에 <xref:System.Reflection.MethodBase.Invoke%2A> 메서드가 항상 성공합니다. 악성 코드에 메서드를 직접 호출할 수 있는 권한이 없는 경우에도 public 멤버를 호출하여 간접적으로 호출할 수 있습니다.

## <a name="version-information"></a>버전 정보

- .NET Framework 4부터 투명 코드는 리플렉션을 사용하여 보안에 중요한 멤버에 액세스할 수 없습니다.

- <xref:System.Security.Permissions.ReflectionPermissionFlag.RestrictedMemberAccess?displayProperty=nameWithType> 플래그는 .NET Framework 2.0 서비스 팩 1에 도입되었습니다. 이전 버전의 .NET Framework에서는 리플렉션을 사용하여 public이 아닌 멤버에 액세스하는 코드에 <xref:System.Security.Permissions.ReflectionPermissionFlag.MemberAccess?displayProperty=nameWithType> 플래그가 필요합니다. 부분적으로 신뢰할 수 있는 코드에는 이 권한을 부여하면 안 됩니다.

- .NET Framework 2.0부터 리플렉션을 사용하여 public이 아닌 형식과 멤버에 대한 정보를 가져오는 데 필요한 권한은 없습니다. 이전 버전에서는 <xref:System.Security.Permissions.ReflectionPermissionFlag.TypeInformation?displayProperty=nameWithType> 플래그가 있는 <xref:System.Security.Permissions.ReflectionPermission>이 필요합니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Security.Permissions.ReflectionPermissionFlag>
- <xref:System.Security.Permissions.ReflectionPermission>
- <xref:System.Security.Permissions.SecurityPermission>
- [보안 변경 내용](../security/security-changes.md)
- [코드 액세스 보안](../misc/code-access-security.md)
- [리플렉션 내보내기의 보안 문제점](security-issues-in-reflection-emit.md)
- [형식 정보 보기](viewing-type-information.md)
- [특성 적용](../../standard/attributes/applying-attributes.md)
- [사용자 지정 특성 액세스](accessing-custom-attributes.md)
