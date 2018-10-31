---
title: 전역 어셈블리 캐시에서 서비스되는 구성 요소 사용
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4fe5edb7c09d0f850b142aba5062a36bfc6d87c1
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50184239"
---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>전역 어셈블리 캐시에서 서비스되는 구성 요소 사용
서비스되는 구성 요소(관리 코드 COM+ 구성 요소)는 전역 어셈블리 캐시에 저장해야 합니다. 일부 시나리오에서 공용 언어 런타임과 COM+ 서비스에서 전역 어셈블리 캐시에 없는 서비스되는 구성 요소를 처리할 수 있지만, 다른 시나리오에서는 그렇게 할 수 없습니다. 다음 시나리오에서 이러한 예에 대해 설명합니다.  
  
-   COM+ 서버 응용 프로그램에 있는 서비스되는 구성 요소의 경우, 서비스되는 구성 요소가 포함된 디렉터리와 동일한 디렉터리에서 Dllhost.exe가 실행되지 않기 때문에 구성 요소가 포함된 어셈블리는 전역 어셈블리 캐시에 있어야 합니다.  
  
-   COM+ 라이브러리 응용 프로그램에 있는 서비스되는 구성 요소의 경우 런타임 및 COM+ 서비스에서 현재 디렉터리를 검색하여 구성 요소가 포함된 어셈블리에 대한 참조를 확인할 수 있습니다. 이 경우 어셈블리가 전역 어셈블리 캐시에 있을 필요가 없습니다.  
  
-   ASP.NET 응용 프로그램에 있는 서비스되는 구성 요소의 경우 상황이 다릅니다. 서비스되는 구성 요소가 포함된 어셈블리를 응용 프로그램 기준 위치의 bin 디렉터리에 저장하고 요청 시 등록을 사용하는 경우, ASP.NET에서 런타임의 섀도 기능을 사용하므로 다운로드 캐시에 어셈블리를 섀도 복사합니다.  
  
## <a name="see-also"></a>참고 항목  
- [어셈블리 및 전역 어셈블리 캐시 사용](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
- [Gacutil.exe(전역 어셈블리 캐시 도구)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)
