---
title: 어셈블리 바인딩 리디렉션 구성
ms.date: 03/30/2017
helpviewer_keywords:
- side-by-side execution, assembly binding redirection
- assemblies [.NET Framework], binding redirection
ms.assetid: d266cbd8-bf91-41d1-baf0-afbc481a741f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3abf42790757708b235b3eab82ea9a11ff545215
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50182868"
---
# <a name="configuring-assembly-binding-redirection"></a>어셈블리 바인딩 리디렉션 구성
기본적으로 응용 프로그램에서는 응용 프로그램을 컴파일하는 데 사용된 런타임 버전과 함께 제공된 .NET Framework 어셈블리 집합을 사용합니다. 응용 프로그램 구성 파일에서 [\<assemblyBinding>](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md) 요소에 대해 **appliesTo** 특성을 사용하여 어셈블리 바인딩 참조를 .NET Framework 어셈블리의 특정 버전으로 리디렉션할 수 있습니다. 이 선택적 특성은 .NET Framework 버전을 사용하여 특성이 적용되는 버전을 지정합니다. **appliesTo** 특성이 지정되지 않으면 **\<assemblyBinding>** 요소는 .NET Framework의 모든 버전에 적용됩니다.  
  
 **appliesTo** 특성은 .NET Framework 버전 1.1에서 도입되었고 .NET Framework 버전 1.0에서는 무시됩니다. 즉, .NET Framework 버전 1.0을 사용할 때는 **appliesTo** 특성을 지정해도 모든 **\<assemblyBinding>** 요소가 적용됩니다.  
  
> [!NOTE]
>  **appliesTo** 특성을 사용하여 특정 런타임 버전으로 리디렉션되는 어셈블리 바인딩을 제한합니다.  
  
 예를 들어 .NET Framework 버전 1.0 어셈블리에 대한 어셈블리 바인딩을 리디렉션하려면 응용 프로그램 구성 파일에 다음 XML 코드를 포함합니다.  
  
```xml  
<runtime>  
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1" appliesTo="v1.0.3705">  
            <dependentAssembly>   
               * assembly information goes here *  
            </dependentAssembly>  
       </assemblyBinding>  
</runtime>  
```  
  
 **\<assemblyBinding>** 요소는 순서를 구분합니다. 먼저 .NET Framework 버전 1.0 어셈블리에 대한 어셈블리 바인딩 리디렉션 정보를 입력하고 .NET Framework 버전 1.1 어셈블리에 대한 어셈블리 바인딩 리디렉션 정보를 입력합니다. 마지막으로 **appliesTo** 특성을 사용하지 않으므로 모든 .NET Framework 버전에 적용되는 .NET Framework 어셈블리 리디렉션에 대한 어셈블리 바인딩 리디렉션 정보를 입력합니다. 리디렉션 시 충돌이 발생하면 구성 파일에서 일치하는 첫 번째 리디렉션 문이 사용됩니다.  
  
 예를 들어 한 참조를 .NET Framework 버전 1.0 어셈블리로 리디렉션하고 다른 참조를 .NET Framework 버전 1.1 어셈블리로 리디렉션하려면 다음 의사 코드에 표시된 패턴을 사용합니다.  
  
```xml  
<assemblyBinding xmlns="..." appliesTo="v1.0.3705">   
<! — .NET Framework version 1.0 redirects here. -->   
</assemblyBinding>   
  
<assemblyBinding xmlns="..." appliesTo="v1.1.4322">   
    <! — .NET Framework version 1.1 redirects here. -->   
</assemblyBinding>   
  
<assemblyBinding xmlns="...">   
<!-- Redirects meant for all versions of the .NET Framework. -->   
</assemblyBinding>  
```  
  
## <a name="debugging-configuration-file-errors"></a>구성 파일 오류 디버깅  
 런타임에서는 응용 프로그램이 만들어질 때 구성 파일을 한 번 구문 분석하고 코드를 해당 응용 프로그램 도메인으로 로드합니다. 공용 언어 런타임에서는 입력을 무시하는 방식으로 구성 파일의 오류를 처리합니다. 형식이 잘못된 XML이 포함된 런타임에서는 전체 구성 파일을 무시합니다. 잘못된 XML의 경우 잘못된 섹션만 무시됩니다.  
  
 어셈블리 바인딩이 리디렉션이 발생하는지를 확인하여 구성 파일이 사용되고 있는지를 확인할 수 있습니다. [어셈블리 바인딩 로그 뷰어(Fuslogvw.exe)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md)를 사용하여 로드되고 있는 어셈블리를 확인합니다. 모든 어셈블리 바인드를 확인하려면 레지스트리에서 **ForceLog**에 대한 항목을 설정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
- [방법: 자동 바인딩 리디렉션 사용 설정 및 해제](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)
