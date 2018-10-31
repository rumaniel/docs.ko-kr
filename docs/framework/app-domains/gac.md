---
title: 전역 어셈블리 캐시
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache)
- ACLs [.NET Framework]
- global assembly cache
- cache [.NET Framework], global assembly cache
- global assembly cache, about
- access control lists [.NET Framework]
ms.assetid: cf5eacd0-d3ec-4879-b6da-5fd5e4372202
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0508e9291b089ec7af6a0b41bbc231fdb0701ad6
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49452992"
---
# <a name="global-assembly-cache"></a>전역 어셈블리 캐시
공용 언어 런타임이 설치된 각 컴퓨터에는 전역 어셈블리 캐시라는 컴퓨터 수준의 코드 캐시가 있습니다. 전역 어셈블리 캐시에는 컴퓨터의 여러 응용 프로그램에서 공유하도록 특별히 지정된 어셈블리가 저장됩니다.  
  
 필요할 경우에만 어셈블리를 전역 어셈블리 캐시에 설치하여 어셈블리를 공유해야 합니다. 일반적으로 어셈블리 공유가 명시적으로 필요하지 않은 경우에는 어셈블리 종속성은 pirvate으로 유지하고 어셈블리를 응용 프로그램 디렉터리에 저장해야 합니다. 또한 어셈블리가 COM interop 또는 비관리 코드에 액세스 가능하게 설정하기 위해 어셈블리를 전역 어셈블리 캐시에 설치할 필요는 없습니다.  
  
> [!NOTE]
>  어셈블리를 전역 어셈블리 캐시에 명시적으로 설치하지 않으려고 하는 시나리오가 있습니다. 응용 프로그램을 구성하는 어셈블리 중 하나를 전역 어셈블리 캐시에 배치하면 **xcopy** 명령을 사용하여 응용 프로그램 디렉터리를 복사하는 방식으로 응용 프로그램을 더 이상 복제하거나 설치할 수 없습니다. 전역 어셈블리 캐시의 어셈블리도 이동해야 합니다.  
  
 어셈블리를 전역 어셈블리 캐시에 배포하는 다음 두 가지 방법이 있습니다.  
  
-   전역 어셈블리 캐시와 함께 사용하도록 디자인된 설치 관리자를 사용합니다. 이것은 어셈블리를 전역 어셈블리 캐시에 설치하기 위한 기본 설정된 옵션입니다.  
  
-   [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]에서 제공된 [전역 어셈블리 캐시 도구(Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)라는 개발자 도구를 사용합니다.  
  
    > [!NOTE]
    >  배포 시나리오에서는 전역 어셈블리 캐시에 어셈블리를 설치할 때 Windows Installer를 사용해야 합니다. 전역 어셈블리 캐시 도구는 개발 시나리오에서만 사용합니다. 그 이유는 이 도구가 어셈블리 참조 계산 및 Windows Installer를 사용할 때 제공되는 기타 기능을 제공하지 않기 때문입니다.  
  
 .NET Framework 4부터 전역 어셈블리 캐시의 기본 위치는 **%windir%\Microsoft.NET\assembly**입니다. .NET Framework의 이전 버전에서 기본 위치는 **%windir%\assembly**입니다.  
  
 관리자는 대부분 쓰기 및 실행 액세스를 제어하기 위해 ACL(액세스 제어 목록)을 사용하여 systemroot 디렉터리를 보호합니다. 전역 어셈블리 캐시는 systemroot 디렉터리의 하위 디렉터리에 설치되므로 해당 디렉터리의 ACL을 상속합니다. 관리자 권한을 가진 사용자만 전역 어셈블리 캐시에서 파일을 삭제하도록 허용하는 것이 좋습니다.  
  
 전역 어셈블리 캐시에 배포된 어셈블리에 강력한 이름이 있어야 합니다. 어셈블리가 전역 어셈블리 캐시에 추가되면 어셈블리를 구성하는 모든 파일에 대한 무결성 검사가 수행됩니다. 예를 들어 파일이 변경되었지만 매니페스트가 변경을 반영하지 않는 경우 캐시는 이러한 무결성 검사를 수행하여 어셈블리가 변조되지 않았는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
- [공용 언어 런타임의 어셈블리](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)  
- [어셈블리 및 전역 어셈블리 캐시 사용](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
- [강력한 이름의 어셈블리](../../../docs/framework/app-domains/strong-named-assemblies.md)
