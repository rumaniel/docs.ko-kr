---
title: '방법: DEVPATH를 사용하여 어셈블리 찾기'
ms.date: 03/30/2017
helpviewer_keywords:
- DEVPATH
- .NET Framework application configuration, assemblies
- application configuration files, specifying assembly's location
- app.config files, assembly locations
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 44d2eadf-7eec-443c-a2ac-d601fd919e17
ms.openlocfilehash: 6fa864f814d6a9ce04f2bce92c61cd0075ab5145
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912996"
---
# <a name="how-to-locate-assemblies-by-using-devpath"></a>방법: DEVPATH를 사용하여 어셈블리 찾기
개발자는 빌드하는 공유 어셈블리가 여러 응용 프로그램에서 올바르게 작동 하는지 확인 하는 것이 좋습니다. 개발자는 개발 주기 동안 어셈블리를 전역 어셈블리 캐시에 지속적으로 배치 하는 대신 어셈블리의 빌드 출력 디렉터리를 가리키는 DEVPATH 환경 변수를 만들 수 있습니다.  
  
 예를 들어 MySharedAssembly 라는 공유 어셈블리를 빌드하고 출력 디렉터리는 C:\MySharedAssembly\Debug. 라고 가정 합니다. C:\MySharedAssembly\Debug를 DEVPATH 변수에 넣을 수 있습니다. 그런 다음 컴퓨터 구성 파일에서 [ \<developmentMode >](./file-schema/runtime/developmentmode-element.md) 요소를 지정 해야 합니다. 이 요소는 공용 언어 런타임에 DEVPATH를 사용 하 여 어셈블리를 찾도록 지시 합니다.  
  
 공유 어셈블리는 런타임에서 검색할 수 있어야 합니다.  어셈블리 참조를 확인 하기 위한 전용 디렉터리를 지정 하려면 [어셈블리의 위치 지정](specify-assembly-location.md)에 설명 된 대로 [ \<코드 베이스 > 요소](./file-schema/runtime/codebase-element.md) 를 사용 하거나 [ \<](./file-schema/runtime/probing-element.md) 구성 파일에서 > 요소를 검색 합니다.  응용 프로그램 디렉터리의 하위 디렉터리에 어셈블리를 배치할 수도 있습니다. 자세한 내용은 [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)을 참조하세요.  
  
> [!NOTE]
> 이는 개발용으로 제공 되는 고급 기능입니다.  
  
 다음 예제에서는 런타임이 DEVPATH 환경 변수로 지정 된 디렉터리에서 어셈블리를 검색 하도록 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
  
```xml  
<configuration>  
  <runtime>  
    <developmentMode developerInstallation="true"/>  
  </runtime>  
</configuration>  
```  
  
 이 설정의 기본값은 false입니다.  
  
> [!NOTE]
> 이 설정은 개발 시에만 사용 합니다. 런타임은 DEVPATH에서 찾은 강력한 이름의 어셈블리에 대 한 버전을 확인 하지 않습니다. 단순히 찾은 첫 번째 어셈블리를 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- [구성 파일을 사용 하 여 앱 구성](index.md)
