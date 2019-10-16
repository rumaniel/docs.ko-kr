---
title: 보안 및 레지스트리(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- security [Visual Basic], registry
- registry [Visual Basic], security issues
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
ms.openlocfilehash: 2fdb8003365841a4eef298eb853765dd3bc4587d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916525"
---
# <a name="security-and-the-registry-visual-basic"></a>보안 및 레지스트리(Visual Basic)
이 페이지에서는 레지스트리에 데이터를 저장할 경우 보안에 미치는 영향을 설명합니다.  
  
## <a name="permissions"></a>사용 권한  
 레지스트리 키가 ACL(액세스 제어 목록)로 보호된 경우에도 비밀(예: 암호)을 레지스트리에 일반 텍스트로 저장하는 것은 안전하지 않습니다.  
  
 레지스트리로 작업하면 시스템 리소스나 보호된 정보에 부적절하게 액세스하여 보안이 손상될 수 있습니다. 이러한 속성을 사용하려면 레지스트리 변수에 대한 액세스를 제어하는 <xref:System.Security.Permissions.RegistryPermissionAccess> 열거형의 읽기 및 쓰기 권한이 있어야 합니다. 완전 신뢰로 실행되는 코드(기본 보안 정책에서 사용자의 로컬 하드 디스크에 설치된 모든 코드)에는 레지스트리에 액세스하는 데 필요한 권한이 있습니다. 자세한 내용은 <xref:System.Security.Permissions.RegistryPermission> 클래스를 참조하세요.  
  
 <xref:System.Security.Permissions.RegistryPermission> 없이 코드에서 액세스할 수 있는 메모리 위치에 레지스트리 변수를 저장하면 안 됩니다. 마찬가지로, 사용 권한을 부여하는 경우 작업을 완료하는 데 필요한 최소 권한을 부여합니다.  
  
 레지스트리 권한 액세스 값은 <xref:System.Security.Permissions.RegistryPermissionAccess> 열거형에 의해 정의됩니다. 다음 표에서는 해당 멤버를 자세히 설명합니다.  
  
|값|레지스트리 변수에 대한 액세스 권한|  
|-----------|----------------------------------|  
|`AllAccess`|만들기, 읽기, 쓰기|  
|`Create`|만들기|  
|`NoAccess`|액세스 권한 없음|  
|`Read`|읽기|  
|`Write`|Write|  
  
## <a name="checking-values-in-registry-keys"></a>레지스트리 키의 값 검사  
 레지스트리 값을 만들 때 해당 값이 이미 있는 경우 수행할 작업을 결정해야 합니다. 다른 악성 프로세스에서 값을 이미 만들고 액세스했을 수도 있습니다. 레지스트리 값에 데이터를 넣으면 다른 프로세스에서 해당 데이터를 사용할 수 있습니다. 이를 방지하려면 `GetValue` 메서드를 사용합니다. 키가 아직 없는 경우 `Nothing`이 반환됩니다.  
  
> [!IMPORTANT]
> 웹 애플리케이션에서 레지스트리를 읽는 경우 현재 사용자의 ID는 웹 애플리케이션에 구현된 인증 및 가장에 따라 결정됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [레지스트리 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
