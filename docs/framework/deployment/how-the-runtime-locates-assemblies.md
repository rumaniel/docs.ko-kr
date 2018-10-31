---
title: 런타임에서 어셈블리를 찾는 방법
ms.date: 03/30/2017
helpviewer_keywords:
- app.config files, assembly locations
- deploying applications [.NET Framework], assembly locations
- application configuration files, locating assemblies
- .NET Framework application deployment, locating assemblies
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 772ac6f4-64d2-4cfb-92fd-58096dcd6c34
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 54ca80e83511d6120669df634ae34ca0bf486bf3
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453452"
---
# <a name="how-the-runtime-locates-assemblies"></a>런타임에서 어셈블리를 찾는 방법
.NET Framework 응용 프로그램을 성공적으로 배포하려면 공용 언어 런타임이 응용 프로그램을 구성하는 어셈블리를 찾아서 바인딩하는 방법을 이해해야 합니다. 기본적으로 런타임은 응용 프로그램 빌드 시 사용된 정확한 버전의 어셈블리로 바인딩을 시도합니다. 이 기본 동작은 구성 파일 설정으로 재정의할 수 있습니다.  
  
 공용 언어 런타임은 어셈블리를 찾아서 어셈블리 참조를 확인하려고 할 때 다양 한 단계를 수행합니다. 각 단계는 다음 섹션에서 설명합니다. 검색이라는 용어는 대개 런타임에서 어셈블리를 찾는 방법을 설명할 때 사용됩니다. 해당 이름 및 문화권에 따라 어셈블리를 찾는 데 사용되는 추론 집합을 가리킵니다.  
  
> [!NOTE]
>  [에 포함된](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md)어셈블리 바인딩 로그 뷰어(Fuslogvw.exe) [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]를 사용하여 로그 파일의 바인딩 정보를 볼 수 있습니다.  
  
## <a name="initiating-the-bind"></a>바인딩 시작  
 런타임에서 다른 어셈블리에 대한 참조를 확인하려고 시도하면 어셈블리를 찾아서 바인딩하는 프로세스가 시작됩니다. 이 참조는 정적이거나 동적일 수 있습니다. 컴파일러는 빌드 타임에 정적 참조를 어셈블리 매니페스트 메타데이터에 기록합니다. 동적 참조는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>와 같은 다양한 메서드의 호출 결과로 즉석에서 생성됩니다.  
  
 어셈블리를 참조할 때는 어셈블리 이름, 버전, 문화권 및 공개 키 토큰(있는 경우)을 포함하여 전체 참조를 사용하는 것이 좋습니다. 런타임은 이 섹션의 뒷부분에 설명된 단계에 따라 이 정보를 사용하여 어셈블리를 찾습니다. 런타임은 정적 또는 동적 어셈블리에 대한 참조인지에 관계없이 동일한 확인 프로세스를 사용합니다.  
  
 어셈블리 이름만 지정하는 등 호출 메서드에 어셈블리에 대한 부분 정보만 제공하여 어셈블리에 대한 동적 참조를 만들 수도 있습니다. 이 경우 응용 프로그램 디렉터리에서만 어셈블리가 검색되고 다른 검사는 수행되지 않습니다. <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 또는 <xref:System.AppDomain.Load%2A?displayProperty=nameWithType>와 같은 다양한 어셈블리 로드 메서드 중 하나를 사용하여 부분 참조를 만듭니다.  
  
 <xref:System.Reflection.Assembly.Load*?displayProperty=nameWithType> 등의 메서드를 사용하여 동적 참조를 만들고 부분 정보만 제공할 수 있습니다. 그런 다음 응용 프로그램 구성 파일에서 [\<qualifyAssembly>](../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md) 요소를 사용하여 참조를 한정할 수 있습니다. 코드 대신 응용 프로그램 구성 파일에서 이 요소를 통해 전체 참조 정보(이름, 버전, 문화권 및 해당하는 경우 공개 키 토큰)를 제공할 수 있습니다. 응용 프로그램 디렉터리 외부의 어셈블리에 대한 참조를 정규화하려는 경우 또는 전역 어셈블리 캐시에서 어셈블리를 참조하려고 하지만 코드 대신 구성 파일에서 전체 참조를 편리하게 지정하려는 경우 이 기술을 사용합니다.  
  
> [!NOTE]
>  이 형식의 부분 참조는 여러 응용 프로그램 간에 공유되는 어셈블리와 함께 사용하면 안 됩니다. 어셈블리 단위가 아니라 응용 프로그램 단위로 구성 설정이 적용되기 때문에 이 형식의 부분 참조를 사용하는 공유 어셈블리에서는 공유 어셈블리를 사용하는 각 응용 프로그램의 구성 파일에 적격한 정보가 있어야 합니다.  
  
 런타임은 다음 단계를 사용하여 어셈블리 참조를 확인합니다.  
  
1.  응용 프로그램 구성 파일, 게시자 정책 파일 및 컴퓨터 구성 파일을 비롯한 해당 구성 파일을 검사하여[올바른 어셈블리 버전을 결정](#step1) 합니다. 구성 파일이 원격 컴퓨터에 있는 경우 런타임에서 먼저 응용 프로그램 구성 파일을 찾아서 다운로드해야 합니다.  
  
2.  [어셈블리 이름이 이전에 바인딩되었는지 여부를 확인](#step2) 하고, 바인딩된 경우 이전에 로드된 어셈블리를 사용합니다. 이전의 어셈블리 로드 요청이 실패한 경우 어셈블리 로드를 시도하지 않고 요청이 즉시 실패합니다.  
  
    > [!NOTE]
    >  어셈블리 바인딩 실패 캐싱은 .NET Framework 버전 2.0의 새로운 기능입니다.  
  
3.  [전역 어셈블리 캐시를 확인](#step3)합니다. 어셈블리가 있으면 런타임에서 이 어셈블리를 사용합니다.  
  
4.  다음 단계를 사용하여[어셈블리를 검색](#step4) 합니다.  
  
    1.  구성 및 게시자 정책이 원래 참조 영향을 주지 않고 바인딩 요청이 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드를 사용하여 만들어진 경우 런타임에서 위치 힌트를 확인합니다.  
  
    2.  구성 파일에 코드베이스가 있을 경우 런타임에서 이 위치만 확인합니다. 이 검색이 실패하면 런타임에서 바인딩 요청이 실패했다고 결정하며 다른 검색이 수행되지 않습니다.  
  
    3.  [검색 섹션](#step4)에서 설명한 추론을 사용하여 어셈블리를 검색합니다. 검색 후에도 어셈블리가 발견되지 않으면 런타임에서 Windows Installer에 어셈블리를 제공하도록 요청합니다. 이는 주문형 설치 기능으로 작동합니다.  
  
        > [!NOTE]
        >  강력한 이름이 없는 어셈블리에 대한 버전 검사는 없으며, 강력한 이름이 없는 어셈블리에 대한 런타임 검사도 전역 어셈블리 캐시에 없습니다.  
  
<a name="step1"></a>   
## <a name="step-1-examining-the-configuration-files"></a>단계 1: 구성 파일 검토  
 세 개의 XML 파일을 기준으로 다양한 수준에서 어셈블리 바인딩 동작을 구성할 수 있습니다.  
  
-   응용 프로그램 구성 파일  
  
-   게시자 정책 파일  
  
-   컴퓨터 구성 파일  
  
 이러한 파일은 동일한 구문을 따르며 바인딩 리디렉션, 코드 위치 및 특정 어셈블리에 대한 바인딩 모드와 같은 정보를 제공합니다. 각 구성 파일에는 바인딩 프로세스를 리디렉션하는 [\<assemblyBinding> 요소](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)가 포함될 수 있습니다. [\<assemblyBinding> 요소](../../../docs/framework/configure-apps/file-schema/runtime/assemblybinding-element-for-runtime.md)의 자식 요소에는 [\<dependentAssembly> 요소](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md)가 포함됩니다. [\<dependentAssembly> 요소](../../../docs/framework/configure-apps/file-schema/runtime/dependentassembly-element.md)의 자식 요소에는 [\<assemblyIdentity> 요소](/visualstudio/deployment/assemblyidentity-element-clickonce-deployment), [\<bindingRedirect> 요소](../../../docs/framework/configure-apps/file-schema/runtime/bindingredirect-element.md) 및 [\<codeBase> 요소](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md)가 포함됩니다.  
  
> [!NOTE]
>  세 개의 구성 파일에서 구성 정보를 확인할 수 있습니다. 모든 요소가 모든 구성 파일에서 유효한 것은 아닙니다. 예를 들어 바인딩 모드 및 전용 경로 정보는 응용 프로그램 구성 파일에만 포함될 수 있습니다. 각 파일에 포함된 정보의 전체 목록은 [구성 파일을 사용하여 앱 구성](../../../docs/framework/configure-apps/index.md)을 참조하세요.  
  
### <a name="application-configuration-file"></a>응용 프로그램 구성 파일  
 첫째, 공용 언어 런타임은 응용 프로그램 구성 파일에서 호출 어셈블리의 매니페스트에 저장된 버전 정보를 재정의하는 정보를 확인합니다. 응용 프로그램 구성 파일은 응용 프로그램과 함께 배포될 수 있지만 응용 프로그램 실행에 필요하지는 않습니다. 일반적으로 이 파일은 즉시 검색되지만 Internet Explorer 웹 기반 시나리오와 같이 응용 프로그램 기준 위치가 원격 컴퓨터에 있는 경우 구성 파일을 다운로드해야 합니다.  
  
 클라이언트 실행 파일의 경우 응용 프로그램 구성 파일이 응용 프로그램 실행 파일과 동일한 디렉터리에 있으며 .config 확장명을 가진 실행 파일과 동일한 기본 이름을 사용합니다. 예를 들어 C:\Program Files\Myapp\Myapp.exe의 구성 파일은 C:\Program Files\Myapp\Myapp.exe.config입니다. 브라우저 기반 시나리오에서 HTML 파일은 **\<link>** 요소를 사용하여 구성 파일을 명시적으로 가리켜야 합니다.  
  
 다음 코드는 응용 프로그램 구성 파일의 간단한 예를 제공합니다. 이 예제에서는 <xref:System.Diagnostics.TextWriterTraceListener> 컬렉션에 <xref:System.Diagnostics.Debug.Listeners%2A> 를 추가하여 파일에 디버그 정보를 기록할 수 있게 합니다.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
### <a name="publisher-policy-file"></a>게시자 정책 파일  
 둘째, 런타임은 게시자 정책 파일을 검사합니다(있는 경우). 게시자 정책 파일은 구성 요소 게시자에 의해 공유 구성 요소에 대한 수정 프로그램이나 업데이트로 배포됩니다. 이 파일에는 어셈블리 참조를 새 버전으로 보내는 공유 구성 요소의 게시자에 의해 발급된 호환성 정보가 포함되어 있습니다. 응용 프로그램 및 컴퓨터 구성 파일과 달리 게시자 정책 파일은 전역 어셈블리 캐시에 설치되어야 하는 고유한 어셈블리에 포함됩니다.  
  
 다음은 게시자 정책 구성 파일의 예입니다.  
  
```xml  
<configuration>  
    <runtime>  
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
  
            <dependentAssembly>  
                <assemblyIdentity name="asm6" publicKeyToken="c0305c36380ba429" />   
                <bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0"/>    
            </dependentAssembly>  
  
        </assemblyBinding>  
    </runtime>  
</configuration>  
```  
  
 어셈블리를 만들려면 다음과 같은 명령과 함께 [Al.exe(어셈블리 링커)](../../../docs/framework/tools/al-exe-assembly-linker.md) 도구를 사용할 수 있습니다.  
  
```  
Al.exe /link:asm6.exe.config /out:policy.3.0.asm6.dll /keyfile: compatkey.dat /v:3.0.0.0  
```  
  
 `compatkey.dat` 는 강력한 이름의 키 파일입니다. 이 명령은 전역 어셈블리 캐시에 배치할 수 있는 강력한 이름의 어셈블리를 만듭니다.  
  
> [!NOTE]
>  게시자 정책은 공유 구성 요소를 사용하는 모든 응용 프로그램에 영향을 줍니다.  
  
 게시자 정책 구성 파일은 응용 프로그램(즉, 어셈블리 매니페스트 또는 응용 프로그램 구성 파일)에서 제공되는 버전 정보를 재정의합니다. 어셈블리 매니페스트에 지정된 버전을 리디렉션하는 문이 응용 프로그램 구성 파일에 없는 경우 게시자 정책 파일이 어셈블리 매니페스트에 지정된 버전을 재정의합니다. 그러나 응용 프로그램 구성 파일에 리디렉션 문이 있으면 게시자 정책이 매니페스트에 지정된 버전 대신 해당 버전을 재정의합니다.  
  
 게시자 정책 파일은 공유 구성 요소가 업데이트되고 해당 구성 요소를 사용하는 모든 응용 프로그램이 새 버전의 공유 구성 요소를 선택할 때 사용됩니다. 응용 프로그램 구성 파일이 안전 모드를 적용하지 않는 한 게시자 정책 파일의 설정이 응용 프로그램 구성 파일의 설정을 재정의합니다.  
  
#### <a name="safe-mode"></a>안전 모드  
 게시자 정책 파일은 일반적으로 서비스 팩이나 프로그램 업데이트의 일부로 명시적으로 설치됩니다. 업그레이드된 공유 구성 요소에 문제가 있는 경우 안전 모드를 사용하여 게시자 정책 파일의 재정의를 무시할 수 있습니다. 안전 모드는 **\<publisherPolicy apply="yes**&#124;**no"/>** 요소에 의해 결정되며, 이 요소는 응용 프로그램 구성 파일에만 있습니다. 바인딩 프로세스에서 게시자 정책 구성 정보를 제거할지 여부를 지정합니다.  
  
 전체 응용 프로그램이나 선택한 어셈블리에 대해 안전 모드를 설정할 수 있습니다. 즉, 응용 프로그램을 구성하는 모든 어셈블리에 대해 정책을 해제하거나 다른 어셈블리는 제외하고 일부 어셈블리에 대해서만 설정할 수 있습니다. 응용 프로그램을 구성하는 어셈블리에 게시자 정책을 선택적으로 적용하려면, **\<publisherPolicy apply\=no/>** 를 설정한 다음 \<**dependentAssembly**> 요소를 사용하여 정책을 적용하려는 어셈블리를 지정합니다. 응용 프로그램을 구성하는 모든 어셈블리에 게시자 정책을 적용하려면 종속 어셈블리 요소 없이 **\<publisherPolicy apply\=no/>** 를 설정합니다. 구성에 대한 자세한 내용은 [구성 파일을 사용하여 앱 구성](../../../docs/framework/configure-apps/index.md)을 참조하세요.  
  
### <a name="machine-configuration-file"></a>컴퓨터 구성 파일  
 셋째, 런타임은 컴퓨터 구성 파일을 검사합니다. Machine.config라는 이 파일은 로컬 컴퓨터에서 런타임이 설치된 루트 디렉터리의 Config 하위 디렉터리에 상주합니다. 관리자는 이 파일을 사용하여 해당 컴퓨터에 로컬로 적용되는 어셈블리 바인딩 제한 사항을 지정할 수 있습니다. 컴퓨터 구성 파일의 설정은 다른 모든 구성 설정보다 우선합니다. 그러나 모든 구성 설정을 이 파일에 넣어야 한다는 의미는 아닙니다. 관리자 정책 파일에서 결정된 버전이 최종 버전이며 재정의할 수 없습니다. Machine.config 파일에서 지정된 재정의는 모든 응용 프로그램에 영향을 줍니다. 구성 파일에 대한 자세한 내용은 [구성 파일을 사용하여 앱 구성](../../../docs/framework/configure-apps/index.md)을 참조하세요.  
  
<a name="step2"></a>   
## <a name="step-2-checking-for-previously-referenced-assemblies"></a>단계 2: 이전에 참조된 어셈블리 확인  
 요청된 어셈블리가 이전 호출에서도 요청된 경우 공용 언어 런타임은 이미 로드된 어셈블리를 사용합니다. 이 경우 응용 프로그램을 구성하는 어셈블리의 이름을 바꿀 때 영향을 받을 수 있습니다. 어셈블리 이름 지정에 대한 자세한 내용은 [어셈블리 이름](../../../docs/framework/app-domains/assembly-names.md)을 참조하세요.  
  
 이전의 어셈블리 요청이 실패한 경우 어셈블리 로드를 시도하지 않고 어셈블리에 대한 이후 요청이 즉시 실패합니다. .NET Framework 버전 2.0부터 어셈블리 바인딩 실패가 캐시되며 캐시된 정보는 어셈블리 로드를 시도할지 여부를 확인하는 데 사용됩니다.  
  
> [!NOTE]
>  바인딩 실패를 캐시하지 않은 .NET Framework 버전 1.0 및 1.1의 동작으로 되돌리려면 [\<disableCachingBindingFailures> 요소](../../../docs/framework/configure-apps/file-schema/runtime/disablecachingbindingfailures-element.md)를 구성 파일에 포함합니다.  
  
<a name="step3"></a>   
## <a name="step-3-checking-the-global-assembly-cache"></a>단계 3: 전역 어셈블리 캐시 확인  
 강력한 이름의 어셈블리에 대한 바인딩 프로세스는 계속해서 전역 어셈블리 캐시를 확인합니다. 전역 어셈블리 캐시는 컴퓨터의 여러 응용 프로그램에서 사용할 수 있는 어셈블리를 저장합니다. 전역 어셈블리 캐시의 모든 어셈블리에 강력한 이름이 있어야 합니다.  
  
<a name="step4"></a>   
## <a name="step-4-locating-the-assembly-through-codebases-or-probing"></a>단계 4: 코드베이스나 조사를 통해 어셈블리 찾기  
 호출 어셈블리 참조와 구성 파일의 정보를 사용하여 올바른 어셈블리 버전을 확인하고 전역 어셈블리 캐시를 검사한 후(강력한 이름의 어셈블리에만 해당) 공용 언어 런타임이 어셈블리를 찾으려고 시도합니다. 어셈블리를 찾는 프로세스는 다음 단계로 구성됩니다.  
  
1.  응용 프로그램 구성 파일에 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 있을 경우 런타임은 지정한 위치를 확인합니다. 일치 항목이 있으면 해당 어셈블리가 사용되고 검색이 수행되지 않습니다. 어셈블리가 없으면 바인딩 요청이 실패합니다.  
  
2.  그런 다음 런타임은 이 섹션의 뒷부분에 지정된 규칙을 사용하여 참조된 어셈블리를 검색합니다.  
  
> [!NOTE]
>  같은 디렉터리에 여러 버전의 어셈블리가 있고 그중에서 특정 버전을 참조하려는 경우 [\<probing>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) 요소의 `privatePath` 특성 대신 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소를 사용해야 합니다. [\<probing>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) 요소를 사용할 경우 참조되는 단순 어셈블리 이름에 일치하는 어셈블리를 런타임에서 처음 찾았으면 정확하게 일치하는지 여부에 관계없이 검색이 중지됩니다. 정확하게 일치하는 항목이면 해당 어셈블리가 사용됩니다. 정확하게 일치하는 항목이 아니면 검색이 중지되고 바인딩이 실패합니다.  
  
### <a name="locating-the-assembly-through-codebases"></a>코드베이스를 통해 어셈블리 찾기  
 구성 파일의 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소를 사용하여 코드베이스 정보를 제공할 수 있습니다. 이 코드베이스는 항상 런타임이 참조된 어셈블리를 검색하기 전에 확인됩니다. 최종 버전 리디렉션이 포함된 게시자 정책 파일에도 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 포함되어 있으면, [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 사용됩니다. 예를 들어 응용 프로그램 구성 파일에서 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 지정되고 응용 프로그램 정보를 재정의하는 게시자 정책 파일에서도 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 지정되면 게시자 정책 파일의 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 사용됩니다.  
  
 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소에서 지정한 위치에 일치하는 항목이 없을 경우 바인드 요청은 실패하며 더 이상 다음 단계가 수행되지 않습니다. 런타임에서 어셈블리가 호출 어셈블리의 조건과 일치한다고 결정하면 해당 어셈블리가 사용됩니다. 지정한 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소에서 지정된 파일이 로드되면 런타임은 해당 이름, 버전, 문화권 및 공개 키가 호출하는 어셈블리의 참조와 일치하는지 확인합니다.  
  
> [!NOTE]
>  응용 프로그램의 루트 디렉터리 외부에 있는 참조된 어셈블리는 강력한 이름이 있어야 하며 전역 어셈블리 캐시에 설치되거나 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소를 사용하여 지정되어야 합니다.  
  
### <a name="locating-the-assembly-through-probing"></a>검색을 통해 어셈블리 찾기  
 응용 프로그램 구성 파일에 [\<codeBase>](../../../docs/framework/configure-apps/file-schema/runtime/codebase-element.md) 요소가 없을 경우 런타임에서는 다음 네 가지 기준을 사용하여 어셈블리를 조사합니다.  
  
-   응용 프로그램이 실행되는 루트 위치인 응용 프로그램 기준 위치  
  
-   참조되는 어셈블리의 문화권 특성인 문화권  
  
-   참조되는 어셈블리의 이름인 이름  
  
-   [\<probing>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) 요소의 `privatePath` 특성으로서, 루트 위치 아래의 하위 디렉터리에 대해 사용자가 정의한 목록입니다. 이 위치는 응용 프로그램 구성 파일과 관리 코드에서 응용 프로그램 도메인에 대한 <xref:System.AppDomainSetup.PrivateBinPath?displayProperty=nameWithType> 속성을 사용하여 지정할 수 있습니다. 관리 코드에서 지정된 경우 관리 코드 `privatePath` 가 먼저 검색된 다음 응용 프로그램 구성 파일에 지정된 경로가 검색됩니다.  
  
#### <a name="probing-the-application-base-and-culture-directories"></a>응용 프로그램 기준 위치 및 문화권 디렉터리 검색  
 런타임은 항상 URL이나 컴퓨터의 응용 프로그램 루트 디렉터리일 수 있는 응용 프로그램 기준 위치에서 검색을 시작합니다. 참조된 어셈블리가 응용 프로그램 기준 위치에 없고 문화권 정보가 제공되지 않은 경우 런타임은 어셈블리 이름을 사용하여 하위 디렉터리를 모두 검색합니다. 검색되는 디렉터리는 다음과 같습니다.  
  
 [응용 프로그램 기준 위치] / [어셈블리 이름].dll  
  
 [응용 프로그램 기준 위치] / [어셈블리 이름] / [어셈블리 이름].dll  
  
 참조된 어셈블리에 대한 문화권 정보가 지정된 경우 다음 디렉터리만 검색됩니다.  
  
 [응용 프로그램 기준 위치] / [문화권] / [어셈블리 이름].dll  
  
 [응용 프로그램 기준 위치] / [문화권] / [어셈블리 이름] / [어셈블리 이름].dll  
  
#### <a name="probing-with-the-privatepath-attribute"></a>PrivatePath 특성을 사용하여 검색  
 문화권 하위 디렉터리와 참조된 어셈블리에 대해 명명된 하위 디렉터리 외에도 런타임은 [\<probing>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) 요소의 `privatePath` 특성을 사용하여 지정한 디렉터리를 조사합니다. `privatePath` 특성을 사용하여 지정된 디렉터리는 응용 프로그램 루트 디렉터리의 하위 디렉터리여야 합니다. 검색되는 디렉터리는 참조된 어셈블리 요청에 문화권 정보가 포함되었는지 여부에 따라 달라집니다.  
  
 참조되는 단순 어셈블리 이름에 일치하는 어셈블리를 런타임에서 처음 찾았을 때는 정확하게 일치하는지 여부에 관계없이 검색이 중지됩니다. 정확하게 일치하는 항목이면 해당 어셈블리가 사용됩니다. 정확하게 일치하는 항목이 아니면 검색이 중지되고 바인딩이 실패합니다.  
  
 문화권이 포함된 경우 다음 디렉터리가 검색됩니다.  
  
 [응용 프로그램 기준 위치] / [binpath] / [문화권] / [어셈블리 이름].dll  
  
 [응용 프로그램 기준 위치] / [binpath] / [문화권] / [어셈블리 이름] / [어셈블리 이름].dll  
  
 문화권 정보가 포함되지 않은 경우 다음 디렉터리가 검색됩니다.  
  
 [응용 프로그램 기준 위치] / [binpath] / [어셈블리 이름].dll  
  
 [응용 프로그램 기준 위치] / [binpath] / [어셈블리 이름] / [어셈블리 이름].dll  
  
#### <a name="probing-examples"></a>검색 예제  
 다음과 같은 정보가 제공됩니다.  
  
-   참조된 어셈블리 이름: myAssembly  
  
-   응용 프로그램 루트 디렉터리: `http://www.code.microsoft.com`  
  
-   구성 파일의 [\<probing>](../../../docs/framework/configure-apps/file-schema/runtime/probing-element.md) 요소가 지정하는 것: bin  
  
-   문화권: de  
  
 이 경우 런타임은 다음과 같은 URL을 검색합니다.  
  
 `http://www.code.microsoft.com/de/myAssembly.dll`
  
 `http://www.code.microsoft.com/de/myAssembly/myAssembly.dll`
  
 `http://www.code.microsoft.com/bin/de/myAssembly.dll`
  
 `http://www.code.microsoft.com/bin/de/myAssembly/myAssembly.dll`
  
##### <a name="multiple-assemblies-with-the-same-name"></a>동일한 이름을 가진 여러 어셈블리  
 다음 예제에서는 여러 어셈블리를 동일한 이름으로 구성하는 방법을 보여 줍니다.  
  
```xml  
<dependentAssembly>  
   <assemblyIdentity name="Server" publicKeyToken="c0305c36380ba429" />   
   <codeBase version="1.0.0.0" href="v1/Server.dll" />  
   <codeBase version="2.0.0.0" href="v2/Server.dll" />  
</dependentAssembly>  
```  
  
#### <a name="other-locations-probed"></a>검색되는 기타 위치  
 현재 바인딩 컨텍스트를 사용하여 어셈블리 위치를 결정할 수도 있습니다. 이러한 경우는 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> 메서드가 사용될 때 및 COM interop 시나리오에서 자주 발생합니다. 어셈블리가 <xref:System.Reflection.Assembly.LoadFrom%2A> 메서드를 사용하여 다른 어셈블리를 참조하는 경우 호출 어셈블리의 위치는 참조된 어셈블리를 찾을 수 있는 위치에 대한 힌트로 간주됩니다. 일치 항목이 있으면 해당 어셈블리가 로드됩니다. 일치 항목이 없으면 런타임이 해당 검색 의미 체계를 계속하고 Windows Installer에 어셈블리를 제공하도록 쿼리합니다. 바인딩 요청과 일치하는 어셈블리가 제공되지 않으면 예외가 발생합니다. 이 예외는 형식이 참조된 경우 관리 코드의 <xref:System.TypeLoadException> 이거나, 로드되는 어셈블리가 없는 경우 <xref:System.IO.FileNotFoundException> 입니다.  
  
 예를 들어 Assembly1이 Assembly2를 참조하고 Assembly1이 `http://www.code.microsoft.com/utils`에서 다운로드된 경우 해당 위치는 Assembly2.dll을 찾을 수 있는 위치에 대한 힌트로 간주됩니다. 런타임은 `http://www.code.microsoft.com/utils/Assembly2.dll`과 `http://www.code.microsoft.com/utils/Assembly2/Assembly2.dll`의 어셈블리를 탐지합니다. Assembly2가 이러한 위치 중 하나에  없으면 런타임에서 Windows Installer를 쿼리합니다.  
  
## <a name="see-also"></a>참고 항목  
- [최선의 어셈블리 로드 방법](../../../docs/framework/deployment/best-practices-for-assembly-loading.md)  
- [배포](../../../docs/framework/deployment/index.md)
