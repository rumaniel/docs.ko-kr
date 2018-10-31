---
title: 강력한 이름의 어셈블리
ms.date: 03/30/2017
helpviewer_keywords:
- strong-named assemblies, about strong-named assemblies
- assemblies [.NET Framework], strong-named
ms.assetid: d4a80263-f3e0-4d81-9b61-f0cbeae3797b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6fe3847d9ee4530a776f43c67ac17085a9cd9d7b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50190907"
---
# <a name="strong-named-assemblies"></a>강력한 이름의 어셈블리
강력한 이름의 어셈블리는 어셈블리에 대한 고유한 ID를 만들어 어셈블리 충돌을 방지할 수 있습니다.  
  
## <a name="what-makes-a-strong-named-assembly"></a>강력한 이름의 어셈블리를 만드는 방법은?  
 강력한 이름의 어셈블리는 어셈블리와 함께 배포된 공개 키에 대응하는 개인 키와 어셈블리 자체를 사용하여 생성됩니다. 어셈블리에는 어셈블리를 구성하는 모든 파일의 이름과 해시가 포함된 어셈블리 매니페스트가 포함되어 있습니다. 같은 강력한 이름을 가진 어셈블리는 동일합니다.  
  
 Visual Studio나 명령줄 도구를 사용하여 강력한 이름의 어셈블리를 만들 수 있습니다. 자세한 내용은 [방법: 강력한 이름으로 어셈블리 서명](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md) 또는 [Sn.exe(강력한 이름 도구)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)를 참조하세요.  
  
 강력한 이름의 어셈블리가 만들어지면 그 어셈블리에는 어셈블리에 대한 간단한 텍스트 이름, 버전 번호, 문화권 정보(제공된 경우), 디지털 서명 및 서명에 사용된 개인 키에 대응하는 공개 키가 포함되어 있습니다.  
  
> [!WARNING]
>  강력한 이름을 보안용으로 사용하지 마세요. 강력한 이름은 고유한 ID를 제공할 뿐입니다.  
  
## <a name="why-strong-name-your-assemblies"></a>강력한 이름의 어셈블리를 사용해야 하는 이유는?  
 강력한 이름의 어셈블리를 참조하면 버전 관리나 이름 보호와 같은 이점이 있습니다. 강력한 이름의 어셈블리는 일부 시나리오를 수행하는 데 필요한 전역 어셈블리 캐시에서 설치할 수 있습니다.  
  
 강력한 이름의 어셈블리는 다음과 같은 시나리오에 유용합니다.  
  
-   강력한 이름의 어셈블리가 어셈블리를 참조할 수 있도록 설정하거나 다른 강력한 이름의 어셈블리에서 어셈블리에 대해 `friend` 액세스 권한을 제공하려는 경우  
  
-   앱이 동일 어셈블리의 다른 버전에 액세스해야 하는 경우. 즉, 같은 앱 도메인 내에서 여러 어셈블리 버전을 충돌 없이 함께 로드해야 하는 경우입니다. 예를 들어 여러 API 확장이 단순한 동일 이름의 어셈블리에 존재하는 경우 강력한 이름을 통해 각 어셈블리 버전에 대한 고유 ID가 제공됩니다.  
  
-   어셈블리를 사용하는 앱의 성능 저하를 방지하기 위해 어셈블리를 도메인 중립으로 설정하려는 경우. 도메인 중립 어셈블리는 전역 어셈블리 캐시에 설치해야 하므로 이렇게 하려면 강력한 이름을 지정해야 합니다.  
  
-   게시자 정책을 적용하여 앱 서비스를 한 위치에서 제공하려는 경우. 이렇게 하려면 어셈블리를 전역 어셈블리 캐시에 설치해야 합니다.  
  
 강력한 이름의 어셈블리가 제공하는 ID 이점을 원하는 오픈 소스 개발자의 경우 어셈블리와 연관된 개인 키를 소스 제어 시스템에 체크 인할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
- [전역 어셈블리 캐시](../../../docs/framework/app-domains/gac.md)  
- [방법: 강력한 이름으로 어셈블리 서명](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)  
- [Sn.exe(강력한 이름 도구)](../../../docs/framework/tools/sn-exe-strong-name-tool.md)  
- [강력한 이름의 어셈블리 만들기 및 사용](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)
