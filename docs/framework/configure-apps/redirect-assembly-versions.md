---
title: 어셈블리 버전 리디렉션
ms.date: 03/30/2017
helpviewer_keywords:
- assembly binding, redirection
- redirecting assembly binding to earlier version
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], binding redirection
ms.assetid: 88fb1a17-6ac9-4b57-8028-193aec1f727c
ms.openlocfilehash: c43ba119b92d4dc1a50b03d6359555ad25f37d08
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971564"
---
# <a name="redirecting-assembly-versions"></a>어셈블리 버전 리디렉션

.NET Framework 어셈블리, 타사 어셈블리 또는 고유의 앱 어셈블리로 컴파일 타임 바인딩 참조를 리디렉션할 수 있습니다. 게시자 정책, 응용 프로그램 구성 파일 또는 컴퓨터 구성 파일 등을 통한 다양한 방법으로 여러 버전의 어셈블리를 사용하도록 응용 프로그램을 리디렉션할 수 있습니다. 이 문서에서는 .NET Framework에서 어셈블리 바인딩의 작동 방식과 구성 방법에 대해 설명합니다.

<a name="BKMK_Assemblyunificationanddefaultbinding"></a>
## <a name="assembly-unification-and-default-binding"></a>어셈블리 통합 및 기본 바인딩
 .NET Framework 어셈블리에 대한 바인딩은 *어셈블리 통합*이라고 하는 프로세스를 통해 리디렉션되는 경우가 있습니다. .NET Framework는 공용 언어 런타임 버전과 형식 라이브러리를 구성하는 약 24개의 .NET Framework 어셈블리로 이루어져 있습니다. 이러한 .NET Framework 어셈블리는 런타임에서 하나의 단위로 처리됩니다. 기본적으로, 응용 프로그램이 시작되면 런타임으로 실행되는 코드의 형식에 대한 모든 참조는 프로세스에서 로드되는 런타임과 버전 번호가 같은 .NET Framework 어셈블리로 이동됩니다. 이 모델에서 발생하는 리디렉션은 런타임에 대한 기본 동작입니다.

 예를 들어 앱이 SYSTEM.XML 네임 스페이스의 형식을 참조 하 고 .NET Framework 4.5를 사용 하 여 빌드된 경우, 런타임 버전 4.5과 함께 제공 되는 SYSTEM.XML 어셈블리에 대 한 정적 참조를 포함 합니다. .NET Framework 4와 함께 제공되는 System.XML 어셈블리를 가리키도록 바인딩 참조를 리디렉션하려는 경우에는 응용 프로그램 구성 파일에 리디렉션 정보를 넣을 수 있습니다. 통합된 .NET Framework 어셈블리에 대한 구성 파일에서 바인딩 리디렉션은 해당 어셈블리에 대한 통합을 취소합니다.

 또한 여러 버전을 사용할 수 있는 경우 타사 어셈블리에 대해 어셈블리 바인딩을 수동으로 리디렉션할 수 있습니다.

<a name="BKMK_Redirectingassemblyversionsbyusingpublisherpolicy"></a>
## <a name="redirecting-assembly-versions-by-using-publisher-policy"></a>게시자 정책을 사용하여 어셈블리 버전 리디렉션
 어셈블리 공급업체는 새 어셈블리와 함께 게시자 정책 파일을 포함하여 최신 버전의 어셈블리로 응용 프로그램을 유도할 수 있습니다. 전역 어셈블리 캐시에 있는 게시자 정책 파일에는 어셈블리 리디렉션 설정이 포함되어 있습니다.

 각 *주*.*부* 버전의 어셈블리에는 자체 게시자 정책 파일이 있습니다. 예를 들어 버전 2.0.2.222에서 2.0.3.000으로 리디렉션과 버전 2.0.2.321에서 2.0.3.000으로 리디렉션은 버전 2.0과 연관되기 때문에 동일한 파일로 이동됩니다. 그러나 버전 3.0.0.999에서 4.0.0.000으로 리디렉션은 버전 3.0.999용 파일로 이동됩니다. .NET Framework의 각 주 버전에는 자체 게시자 정책 파일이 있습니다.

 어셈블리에 대한 게시자 정책 파일이 있으면, 런타임에서 어셈블리의 매니페스트 및 응용 프로그램 구성 파일을 확인한 후 이 파일을 확인합니다. 공급업체는 새 어셈블리가 리디렉션되는 어셈블리와 역호환되는 경우에만 게시자 정책 파일을 사용해야 합니다.

 [게시자 정책 무시 섹션](#bypass_PP)에 설명된 대로, 앱 구성 파일에서 설정을 지정하여 응용 프로그램의 게시자 정책을 무시할 수 있습니다.

<a name="BKMK_Redirectingassemblyversionsattheapplevel"></a>
## <a name="redirecting-assembly-versions-at-the-app-level"></a>앱 수준에서 어셈블리 버전 리디렉션
 앱 구성 파일을 통해 앱의 바인딩 동작을 변경하는 몇 가지 방법이 있습니다. 즉, 파일을 수동으로 편집하거나, 자동 바인딩 리디렉션을 사용하거나, 게시자 정책을 무시하여 바인딩 동작을 지정할 수 있습니다.

### <a name="manually-editing-the-app-config-file"></a>앱 프로그램 구성 파일을 수동으로 편집
 앱 프로그램 구성 파일을 수동으로 편집하여 어셈블리 문제를 해결할 수 있습니다. 예를 들어, 공급업체가 게시자 정책을 제공하지 않고 앱에서 사용되는 어셈블리의 최신 버전을 출시하는 경우에는 역호환성이 보장되지 않으므로 다음과 같이 앱의 구성 파일에 어셈블리 바인딩 정보를 배치하여 새 버전의 어셈블리를 사용하도록 앱을 유도할 수 있습니다.

```xml
<dependentAssembly>
  <assemblyIdentity name="someAssembly"
    publicKeyToken="32ab4ba45e0a69a1"
    culture="en-us" />
  <bindingRedirect oldVersion="7.0.0.0" newVersion="8.0.0.0" />
</dependentAssembly>
```

### <a name="relying-on-automatic-binding-redirection"></a>자동 바인딩 리디렉션 사용

.NET Framework 4.5.1 이상 버전을 대상으로 하는 Visual Studio에서 데스크톱 앱을 만드는 경우 앱에서 자동 바인딩 리디렉션을 사용 합니다. 즉, 두 구성 요소가 강력한 이름의 동일한 어셈블리의 다른 버전을 참조하는 경우 런타임에서 출력 앱 구성 파일(app.config)에 최신 버전의 어셈블리에 바인딩 리디렉션을 자동으로 추가한다는 의미입니다. 이 리디렉션은 그 밖에 발생할 수 있는 어셈블리 통합을 재정의합니다. 소스 app.config 파일은 수정되지 않습니다. 예를 들어, 앱에서 대역 외 .NET Framework 구성 요소를 직접 참조하지만 동일한 구성 요소의 이전 버전을 대상으로 하는 타사 라이브러리를 사용한다고 가정해 보겠습니다. 앱을 컴파일하면, 최신 버전의 구성 요소에 대한 바인딩 리디렉션이 포함되도록 출력 앱 구성 파일이 수정됩니다. 웹앱을 만드는 경우, 바인딩 충돌에 대한 빌드 경고가 표시된 후에 소스 웹 구성 파일에 필요한 바인딩 리디렉션을 추가할 수 있는 옵션이 제공됩니다.

컴파일 시에 소스 app.config 파일에 바인딩 리디렉션을 수동으로 추가 하는 경우 Visual Studio는 추가 된 바인딩 리디렉션을 기준으로 어셈블리를 통합 하려고 시도 합니다. 예를 들어, 어셈블리에 대해 다음과 같은 바인딩 리디렉션을 삽입한다고 가정해 보겠습니다.

`<bindingRedirect oldVersion="3.0.0.0" newVersion="2.0.0.0" />`

앱에 있는 다른 프로젝트가 동일한 어셈블리의 버전 1.0.0.0을 참조하는 경우, 자동 바인딩 리디렉션은 다음 항목을 출력 app.config 파일에 추가하여 이 어셈블리의 2.0.0.0 버전에 앱이 통합되도록 합니다.

`<bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />`

앱이 이전 버전의 .NET Framework를 대상으로 하는 경우 자동 바인딩 리디렉션을 사용 하도록 설정할 수 있습니다. 어셈블리에 대 한 app.config 파일에 바인딩 리디렉션 정보를 제공 하거나 바인딩 리디렉션 기능을 해제 하 여이 기본 동작을 재정의할 수 있습니다. 이 기능을 설정 하거나 해제 [하는 방법에 대 한 자세한 내용은 방법: 자동 바인딩 리디렉션 사용 설정 및 해제](how-to-enable-and-disable-automatic-binding-redirection.md)를 참조하세요.

<a name="bypass_PP"></a>
### <a name="bypassing-publisher-policy"></a>게시자 정책 무시
 필요에 따라 앱 구성 파일에서 게시자 정책을 무시할 수 있습니다. 예를 들어, 역호환성이 있다고 하는 최신 버전의 어셈블리가 앱을 중단시킬 수 있습니다. 게시자 정책을 무시 하려면 앱 구성 파일의 [ \<dependentAssembly >](./file-schema/runtime/dependentassembly-element.md) 요소에 [ \<y apply >](./file-schema/runtime/publisherpolicy-element.md) 요소를 추가 하 고 **적용** 특성을 **아니요**로 설정 합니다. 모든 이전 **예** 설정을 재정의 합니다.

 `<publisherPolicy apply="no" />`

 사용자에 대해 실행 중인 앱을 유지하려면 게시자 정책을 무시할 수 있지만, 문제가 발생할 경우 어셈블리 공급업체에 보고해야 합니다. 어셈블리에 게시자 정책 파일이 있는 경우, 공급업체는 해당 어셈블리가 역호환되는지 확인하고 클라이언트에서 가능하면 최신 버전을 사용할 수 있도록 해야 합니다.

<a name="BKMK_Redirectingassemblyversionsatthemachinelevel"></a>
## <a name="redirecting-assembly-versions-at-the-machine-level"></a>컴퓨터 수준에서 어셈블리 버전 리디렉션
 드문 경우이지만 시스템 관리자가 컴퓨터의 모든 앱에서 특정 버전의 어셈블리를 사용해야 하는 경우도 있습니다. 예를 들어, 관리자는 모든 앱에서 보안 허점을 해결하는 특정 어셈블리 버전을 사용해야 할 수 있습니다. 컴퓨터의 구성 파일에서 어셈블리가 리디렉션되면, 이전 버전을 사용하는 컴퓨터의 모든 앱이 새 버전을 사용하도록 유도됩니다. 컴퓨터 구성 파일은 앱 구성 파일 및 게시자 정책 파일을 재정의합니다. 이 파일은 %*런타임 설치 경로*%\Config 디렉터리에 있습니다. 일반적으로 .NET Framework는 %drive%\Windows\Microsoft.NET\Framework 디렉터리에 설치됩니다.

<a name="BKMK_Specifyingassemblybindinginconfigurationfiles"></a>
## <a name="specifying-assembly-binding-in-configuration-files"></a>구성 파일에 어셈블리 바인딩 지정
 동일한 XML 형식을 사용하여 앱 구성 파일, 컴퓨터 구성 파일 또는 게시자 정책 파일에 있는 바인딩 리디렉션을 지정할 수 있습니다. 한 어셈블리 버전을 다른 버전으로 리디렉션하려면 [ \<bindingRedirect >](./file-schema/runtime/bindingredirect-element.md) 요소를 사용 합니다. **oldVersion** 특성은 단일 어셈블리 버전 또는 다양한 버전을 지정할 수 있습니다. `newVersion` 특성은 단일 버전을 지정해야 합니다.  예를 들어, `<bindingRedirect oldVersion="1.1.0.0-1.2.0.0" newVersion="2.0.0.0"/>` 은 런타임에서 1.1.0.0 - 1.2.0.0 버전의 어셈블리 대신 2.0.0.0 버전을 사용하도록 지정합니다.

 다음 코드 예제는 다양한 바인딩 리디렉션 시나리오를 보여줍니다. 이 예제에서는 `myAssembly`에 대해 다양한 버전의 리디렉션을 지정하고, `mySecondAssembly`에 대해 단일 바인딩 리디렉션을 지정합니다. 또한 이 예제에서는 게시자 정책 파일이 `myThirdAssembly`에 대한 바인딩 리디렉션을 재정의하지 않도록 지정합니다.

 어셈블리를 바인딩하려면 [ \<assemblybinding >](./file-schema/runtime/assemblybinding-element-for-runtime.md) 태그에서 xmlns 특성을 사용 하 여 "urn: 스키마-microsoft-com: **x x x** " 문자열을 지정 해야 합니다.

```xml
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="myAssembly"
          publicKeyToken="32ab4ba45e0a69a1"
          culture="en-us" />
        <!-- Assembly versions can be redirected in app,
          publisher policy, or machine configuration files. -->
        <bindingRedirect oldVersion="1.0.0.0-2.0.0.0" newVersion="3.0.0.0" />
      </dependentAssembly>
  <dependentAssembly>
        <assemblyIdentity name="mySecondAssembly"
          publicKeyToken="32ab4ba45e0a69a1"
          culture="en-us" />
             <bindingRedirect oldVersion="1.0.0.0" newVersion="2.0.0.0" />
      </dependentAssembly>
      <dependentAssembly>
      <assemblyIdentity name="myThirdAssembly"
        publicKeyToken="32ab4ba45e0a69a1"
        culture="en-us" />
        <!-- Publisher policy can be set only in the app
          configuration file. -->
        <publisherPolicy apply="no" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration>
```

### <a name="limiting-assembly--bindings-to-a-specific-version"></a>특정 버전에 대한 어셈블리 바인딩 제한
 응용 프로그램 구성 파일에서 [ \<assemblybinding >](./file-schema/runtime/assemblybinding-element-for-runtime.md) 요소에 대 한 **appliesTo** 특성을 사용 하 여 특정 버전의 .NET Framework에 대 한 어셈블리 바인딩 참조를 리디렉션할 수 있습니다. 이 선택적 특성은 .NET Framework 버전 번호를 사용하여 특성이 적용되는 버전을 지정합니다. **appliesTo** 특성이 지정되지 않으면 [\<assemblyBinding>](./file-schema/runtime/assemblybinding-element-for-runtime.md) 요소는 .NET Framework의 모든 버전에 적용됩니다.

 예를 들어 .NET Framework 버전 3.5 어셈블리에 대한 어셈블리 바인딩을 리디렉션하려면 앱 구성 파일에 다음 XML 코드를 포함합니다.

```xml
<runtime>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1"
    appliesTo="v3.5">
    <dependentAssembly>
      <!-- assembly information goes here -->
    </dependentAssembly>
  </assemblyBinding>
</runtime>
```

 버전 순서대로 리디렉션 정보를 입력해야 합니다. 예를 들어, .NET Framework 3.5 어셈블리에 대한 어셈블리 바인딩 리디렉션 정보를 입력한 후에 .NET Framework 4.5 어셈블리에 대한 해당 정보를 입력합니다. 마지막으로 **appliesTo** 특성을 사용하지 않으므로 모든 .NET Framework 버전에 적용되는 .NET Framework 어셈블리 리디렉션에 대한 어셈블리 바인딩 리디렉션 정보를 입력합니다. 리디렉션 시 충돌이 발생하면 구성 파일에서 일치하는 첫 번째 리디렉션 문이 사용됩니다.

 예를 들어 한 참조를 .NET Framework 버전 3.5 어셈블리로 리디렉션하고 다른 참조를 .NET Framework 버전 4 어셈블리로 리디렉션하려면 다음 의사 코드에 표시된 패턴을 사용합니다.

```xml
<assemblyBinding xmlns="..." appliesTo="v3.5 ">
  <!--.NET Framework version 3.5 redirects here -->
</assemblyBinding>

<assemblyBinding xmlns="..." appliesTo="v4.0.30319">
  <!--.NET Framework version 4.0 redirects here -->
</assemblyBinding>

<assemblyBinding xmlns="...">
  <!-- redirects meant for all versions of the runtime -->
</assemblyBinding>
```

## <a name="see-also"></a>참고자료

- [방법: 자동 바인딩 리디렉션 사용 설정 및 해제](how-to-enable-and-disable-automatic-binding-redirection.md)
- [\<bindingRedirect > 요소](./file-schema/runtime/bindingredirect-element.md)
- [어셈블리 바인딩 리디렉션 보안 권한](assembly-binding-redirection-security-permission.md)
- [.NET 어셈블리](../../standard/assembly/index.md)
- [어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [응용 프로그램 구성](index.md)
- [런타임 설정 스키마](./file-schema/runtime/index.md)
- [구성 파일 스키마](./file-schema/index.md)
- [방법: 게시자 정책 만들기](how-to-create-a-publisher-policy.md)
