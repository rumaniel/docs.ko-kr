---
title: 위험한 권한 및 정책 관리
ms.date: 03/30/2017
helpviewer_keywords:
- permissions [.NET Framework], policy administration
- security [.NET Framework], dangerous permissions
- code security, dangerous permissions
- secure coding, dangerous permissions
- permissions [.NET Framework], dangerous
ms.assetid: 1929e854-23a0-4bb1-94be-e8aa3b609e32
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ffe4f3e000c80610d5a105dddef90f9cfd51f0dc
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205593"
---
# <a name="dangerous-permissions-and-policy-administration"></a>위험한 권한 및 정책 관리
.NET Framework가 권한을 제공하는 보호되는 몇몇 작업은 보안 시스템의 보안을 손상시킬 수 있습니다. 이렇게 위험한 권한은 필요한 경우에만, 그리고 신뢰할 수 있는 코드에만 제공되어야 합니다. 일반적으로 이러한 권한이 부여되면 악성 코드를 방어할 수 없습니다.  
  
> [!NOTE]
> .NET Framework 4에서는 .NET Framework 보안 모델 및 용어에 대 한 중요 한 변경 내용이 있습니다. 이러한 변경 내용에 대 한 자세한 내용은 [보안 변경 내용](../security/security-changes.md)을 참조 하세요.  
  
 위험한 권한은 다음 표에 설명되어 있습니다.  
  
|사용 권한|잠재적 위험|  
|----------------|--------------------|  
|<xref:System.Security.Permissions.SecurityPermission>||  
|<xref:System.Security.Permissions.SecurityPermissionFlag.UnmanagedCode>|관리 코드에서 비관리 코드를 호출하도록 허용하므로 위험할 수 있습니다.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SkipVerification>|이 코드는 유효성 검사가 없어도 모든 작업을 수행할 수 있습니다.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlEvidence>|잘못된 증명 정보로 보안 정책을 속일 수 있습니다.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPolicy>|보안 정책을 수정하는 기능으로 보안을 해제할 수 있습니다.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.SerializationFormatter>|직렬화를 사용하면 접근성 메커니즘을 피할 수 있습니다. 자세한 내용은 [보안 및 직렬화](security-and-serialization.md)를 참조하세요.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlPrincipal>|현재 보안 주체를 설정하는 기능은 역할 기반 보안을 속일 수 있습니다.|  
|<xref:System.Security.Permissions.SecurityPermissionFlag.ControlThread>|스레드 조작은 스레드와 관련된 보안 상태로 인해 위험합니다.|  
|<xref:System.Security.Permissions.ReflectionPermission>||  
|<xref:System.MemberAccessException>|접근성 메커니즘을 무력화하는 데 전용 멤버를 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
