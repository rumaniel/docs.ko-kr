---
title: Principal 개체 및 Identity 개체
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- WindowsIdentity objects
- GenericIdentity objects
- GenericPrincipal objects
- identity objects, about identity objects
- security [.NET Framework], identity objects
- principal objects, about principal objects
- security [.NET Framework], principals
- WindowsPrincipal objects
ms.assetid: aa5930ad-f3d7-40aa-b6f6-c6edcd5c64f7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c5b74f2608022d48dbd7e63e4ddf6112c333e3f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018755"
---
# <a name="principal-and-identity-objects"></a>Principal 개체 및 Identity 개체
Id 또는 역할을 통해 사용자의 관리 되는 코드를 검색할 수는 <xref:System.Security.Principal.IPrincipal> 에 대 한 참조를 포함 하는 개체는 <xref:System.Security.Principal.IIdentity> 개체입니다. Identity 개체와 Principal 개체를 사용자 및 그룹 계정과 같이 익숙한 개념과 비교해 보면 쉽게 이해할 수 있습니다. 대부분의 네트워크 환경에서 사용자 계정은 사람 또는 프로그램을 나타내고, 그룹 계정은 특정 사용자 범주 및 해당 사용자들이 소유하는 권한을 나타냅니다. 마찬가지로, .NET Framework의 Identity 개체는 사용자를 나타내고, 역할은 멤버 및 보안 컨텍스트를 나타냅니다. .NET Framework에서 Principal 개체는 Identity 개체와 역할을 모두 캡슐화합니다. .NET Framework 애플리케이션에서는 보안 주체의 ID 또는 더 일반적인 경우에는 역할 멤버에 따라 보안 주체에 권한을 부여합니다.  
  
## <a name="identity-objects"></a>Identity 개체  
 Identity 개체는 확인 중인 사용자 또는 엔터티에 대한 정보를 캡슐화합니다. 가장 기본적인 수준의 Identity 개체에는 이름 및 인증 형식이 포함되어 있습니다. 이름으로는 사용자의 이름 또는 Windows 계정 이름이 사용될 수 있고, 인증 형식으로는 Kerberos V5와 같은 지원되는 로그온 프로토콜 또는 사용자 지정 값이 사용될 수 있습니다. .NET Framework에 정의 된 <xref:System.Security.Principal.GenericIdentity> 기타 특수 한 대부분의 사용자 지정 로그온 시나리오에 사용할 수 있는 개체 <xref:System.Security.Principal.WindowsIdentity> 응용 프로그램을 Windows 인증을 사용 하려는 경우 사용할 수 있는 개체입니다. 또한 사용자 지정 사용자 정보를 캡슐화하는 고유한 identity 클래스를 직접 정의할 수도 있습니다.  
  
 <xref:System.Security.Principal.IIdentity> 인터페이스 이름 및 인증 유형, 예: NTLM 또는 Kerberos V5에 액세스 하기 위한 속성을 정의 합니다. 모든 **Identity** 클래스는 **IIdentity** 인터페이스를 구현합니다. **Identity** 개체와 스레드가 현재 실행 중인 Windows NT 프로세스 토큰 사이의 관계가 반드시 필요한 것은 아닙니다. 그러나 **Identity** 개체가 **WindowsIdentity** 개체인 경우 해당 ID는 Windows NT 보안 토큰을 나타내는 것으로 간주됩니다.  
  
## <a name="principal-objects"></a>Principal 개체  
 Principal 개체는 코드가 실행되는 보안 컨텍스트를 나타냅니다. 역할 기반 보안을 구현하는 애플리케이션에서는 Principal 개체와 관련된 역할에 따라 권한을 부여합니다. Identity 개체와 마찬가지로,.NET Framework에서 제공 된 <xref:System.Security.Principal.GenericPrincipal> 개체 및 <xref:System.Security.Principal.WindowsPrincipal> 개체입니다. 또한 고유한 사용자 지정 principal 클래스를 정의할 수도 있습니다.  
  
 <xref:System.Security.Principal.IPrincipal> 인터페이스는 연결에 액세스 하기 위한 속성을 정의 **Identity** 개체를 구분 하는지 여부를 결정 하기 위한 메서드를 **주** 개체의 멤버인를 지정 된 역할입니다. 모든 **Principal** 클래스는 **IPrincipal** 인터페이스와 필요한 추가 속성 및 메서드를 모두 구현합니다. 예를 들어, 공용 언어 런타임에서는 Windows NT 또는 Windows 2000 그룹 멤버를 역할에 매핑하기 위한 추가 기능을 구현하는 **WindowsPrincipal** 클래스를 제공합니다.  
  
 A **주체** 개체가 호출 컨텍스트가 바인딩된 (<xref:System.Runtime.Remoting.Messaging.CallContext>) 응용 프로그램 도메인 내에서 개체 (<xref:System.AppDomain>). 기본 호출 컨텍스트는 항상 각각의 새로운 **AppDomain**을 사용하여 만들어지므로 **Principal** 개체를 허용하는 데 사용할 수 있는 호출 컨텍스트가 항상 있습니다. 새로운 스레드가 만들어지면 해당 스레드에 대한 **CallContext** 개체도 만들어집니다. **Principal** 개체 참조는 만드는 스레드에서 새로운 스레드의 **CallContext**로 자동 복사됩니다. 런타임에서 어떤 **Principal** 개체가 해당 스레드의 작성자에 속하는지 확인할 수 없는 경우에는 **Principal** 및 **Identity** 개체 작성을 위한 기본 정책을 따릅니다.  
  
 구성 가능한 애플리케이션의 도메인 관련 정책을 사용하여 새 애플리케이션 도메인과 연결할 **Principal** 개체의 형식을 결정하기 위한 규칙을 정의할 수 있습니다. 보안 정책이 허용하는 경우 런타임에서 현재 실행 스레드와 관련된 운영 체제 시스템 토큰을 반영하는 **Principal** 개체 및 **Identity** 개체를 만들 수 있습니다. 기본적으로 런타임에서는 인증되지 않은 사용자를 나타내는 **Principal** 및 **Identity** 개체를 사용하며, 코드에서 기본 **Principal** 및 **Identity** 개체에 액세스하려고 시도할 때까지는 이러한 개체들을 만들지 않습니다.  
  
 애플리케이션 도메인을 만드는 트러스트된 코드를 사용하여 기본 **Principal** 및 **Identity** 개체의 생성을 제어하는 애플리케이션 도메인 정책을 설정할 수 있습니다. 이 애플리케이션 도메인 관련 정책은 해당 애플리케이션 도메인에 있는 모든 실행 스레드에 적용됩니다. 관리 되지 않는, 신뢰할 수 있는 호스트에는 기본적으로이 정책을 설정 하는 기능에는 없지만이 정책을 설정 하는 관리 코드 해야는 <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType> 도메인 정책을 제어 하기 위한 합니다.  
  
 여러 애플리케이션 도메인 간에, 동일한 프로세스(즉, 동일한 컴퓨터)에서 **Principal** 개체를 전송하는 경우, 원격 인프라에서 호출자의 컨텍스트와 관련된 **Principal** 개체에 대한 참조를 호출 수신자의 컨텍스트에 복사합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: WindowsPrincipal 개체 만들기](../../../docs/standard/security/how-to-create-a-windowsprincipal-object.md)
- [방법: GenericPrincipal 및 GenericIdentity 개체 만들기](../../../docs/standard/security/how-to-create-genericprincipal-and-genericidentity-objects.md)
- [Principal 개체 바꾸기](../../../docs/standard/security/replacing-a-principal-object.md)
- [가장 및 되돌리기](../../../docs/standard/security/impersonating-and-reverting.md)
- [역할 기반 보안](../../../docs/standard/security/role-based-security.md)
- [주요 보안 개념](../../../docs/standard/security/key-security-concepts.md)
