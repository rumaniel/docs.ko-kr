---
title: '방법: 강력한 이름 건너뛰기 기능 비활성화'
ms.date: 03/30/2017
helpviewer_keywords:
- strong-name bypass feature
- strong-named assemblies, loading into trusted application domains
ms.assetid: 234e088c-3b11-495a-8817-e0962be79d82
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 628bc1f89e5e09b47c70e39e107987753697cdb4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198330"
---
# <a name="how-to-disable-the-strong-name-bypass-feature"></a>방법: 강력한 이름 건너뛰기 기능 비활성화
.NET Framework 버전 3.5 SP1(서비스 팩 1)부터는 어셈블리가 완전 신뢰 <xref:System.AppDomain> 개체(예: `MyComputer` 영역의 기본 <xref:System.AppDomain>)에 로드될 때 강력한 이름 시그니처의 유효성을 검사하지 않습니다. 이를 강력한 이름 건너뛰기 기능이라고 합니다. 완전 신뢰 환경에서는 <xref:System.Security.Permissions.StrongNameIdentityPermission>에 대한 요청이 해당 시그니처와 관계없이 서명된 완전 신뢰 어셈블리에 대해 항상 성공합니다. 유일한 제한 사항은 어셈블리 영역이 완전히 신뢰되므로 어셈블리도 완전히 신뢰할 수 있어야 한다는 것입니다. 강력한 이름은 이러한 조건에서 결정적인 요소가 아니므로 유효성을 검사할 이유가 없습니다. 강력한 이름 시그니처의 유효성 검사를 건너뛰면 상당한 성능 개선 효과가 있습니다.  
  
 건너뛰기 기능은 지연 서명되지 않았으며 <xref:System.AppDomainSetup.ApplicationBase%2A> 속성으로 지정된 디렉터리에서 완전 신뢰 <xref:System.AppDomain>에 로드된 모든 완전 신뢰 어셈블리에 적용됩니다.  
  
 레지스트리 키 값을 설정하여 컴퓨터의 모든 응용 프로그램에 대해 건너뛰기 기능을 재정의할 수 있습니다. 응용 프로그램 구성 파일을 사용하여 단일 응용 프로그램에 대한 설정을 재정의할 수 있습니다. 레지스트리 키를 통해 사용하지 않도록 설정된 경우 단일 응용 프로그램에 대해 건너뛰기 기능을 복원할 수 없습니다.  
  
 건너뛰기 기능을 재정의하면 정확성에 대해서만 강력한 이름의 유효성이 검사되고 <xref:System.Security.Permissions.StrongNameIdentityPermission>에 대해서는 검사되지 않습니다. 특정 강력한 이름을 확인하려면 해당 확인을 별도로 수행해야 합니다.  
  
> [!IMPORTANT]
>  강력한 이름 유효성 검사를 강제 적용하는 기능은 다음 절차에 설명된 대로 레지스트리 키에 따라 달라집니다. 응용 프로그램이 해당 레지스트리 키에 액세스할 수 있는 ACL(액세스 제어 목록) 권한이 없는 계정으로 실행되는 경우에는 설정이 적용되지 않습니다. 모든 어셈블리에서 읽을 수 있도록 이 키에 대해 ACL 권한이 구성되어 있는지 확인해야 합니다.  
  
### <a name="to-disable-the-strong-name-bypass-feature-for-all-applications"></a>모든 응용 프로그램에 대해 강력한 이름 건너뛰기 기능을 사용하지 않도록 설정하려면  
  
-   32비트 컴퓨터에서는 시스템 레지스트리의 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 키 아래에 값이 0인 `AllowStrongNameBypass`라는 DWORD 항목을 만듭니다.  
  
-   64비트 컴퓨터에서는 시스템 레지스트리의 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework 및 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework 아래에 값이 0인 `AllowStrongNameBypass`라는 DWORD 항목을 만듭니다.  
  
### <a name="to-disable-the-strong-name-bypass-feature-for-a-single-application"></a>단일 응용 프로그램에 대해 강력한 이름 건너뛰기 기능을 사용하지 않도록 설정하려면  
  
1.  응용 프로그램 구성 파일을 열거나 만듭니다.  
  
     이 파일에 대한 자세한 내용은 [앱 구성](../../../docs/framework/configure-apps/index.md)에서 응용 프로그램 구성 파일 섹션을 참조하세요.  
  
2.  다음 항목을 추가합니다.  
  
    ```xml  
    <configuration>  
      <runtime>  
        <bypassTrustedAppStrongNames enabled="false" />  
      </runtime>  
    </configuration>  
    ```  
  
 구성 파일 설정을 제거하거나 특성을 "true"로 설정하여 응용 프로그램에 대한 건너뛰기 기능을 복원할 수 있습니다.  
  
> [!NOTE]
>  컴퓨터에서 건너뛰기 기능이 사용되는 경우에만 응용 프로그램에 대해 강력한 이름 유효성 검사를 켜고 끌 수 있습니다. 컴퓨터에서 건너뛰기 기능이 해제된 경우 모든 응용 프로그램에 대해 강력한 이름 유효성이 검사되며, 단일 응용 프로그램에 대해 유효성 검사를 건너뛸 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
- [Sn.exe(강력한 이름 도구)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)  
- [\<bypassTrustedAppStrongNames> 요소](../../../docs/framework/configure-apps/file-schema/runtime/bypasstrustedappstrongnames-element.md)  
- [강력한 이름의 어셈블리 만들기 및 사용](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
