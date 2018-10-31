---
title: 어셈블리 및 Side-by-Side 실행
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution [.NET Framework]
- assemblies [.NET Framework], side-by-side execution
ms.assetid: e42036ee-7590-47d1-b884-cc856e39bd5d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e192266aa7b98637cb05f400901f51afd3046a72
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "49415206"
---
# <a name="assemblies-and-side-by-side-execution"></a>어셈블리 및 Side-by-Side 실행
Side-by-side 실행은 같은 컴퓨터에 여러 버전의 응용 프로그램이나 구성 요소를 저장하고 실행할 수 있는 기능입니다. 다시 말해 동시에 같은 컴퓨터에서 여러 런타임 버전을 사용할 수 있으며 특정 런타임 버전을 바탕으로 하는 여러 버전의 응용 프로그램 및 구성 요소를 사용할 수 있습니다. Side-by-Side 실행을 사용하면 응용 프로그램이 바인딩되는 구성 요소 버전과 응용 프로그램에서 사용되는 런타임 버전을 보다 효과적으로 관리할 수 있습니다.  
  
 동일한 어셈블리의 서로 다른 버전을 side-by-side 방식으로 저장하고 실행하는 기능은 강력한 이름 지정의 매우 중요한 부분으로서, 런타임의 인프라에 빌드됩니다. 강력한 이름의 어셈블리 버전 번호는 어셈블리 ID의 일부이기 때문에 런타임에서는 동일한 어셈블리의 여러 버전을 전역 어셈블리 캐시에 저장하고 이들 어셈블리를 런타임에 로드할 수 있습니다.  
  
 런타임에서는 동시 응용 프로그램을 만들 수 있는 기능을 제공하지만, Side-by-Side 실행 기능을 자동으로 적용되지 않습니다. Side-by-Side 실행용 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [Side-by-Side 실행용 구성 요소를 만들기 위한 지침](../../../docs/framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
- [런타임에서 어셈블리를 찾는 방법](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
- [공용 언어 런타임의 어셈블리](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)
