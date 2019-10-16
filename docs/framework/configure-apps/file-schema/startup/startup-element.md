---
title: <startup> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup
- http://schemas.microsoft.com/.NetConfiguration/v2.0#startup
helpviewer_keywords:
- container tags, <startup> element
- <startup> element
- startup element
ms.assetid: 536acfd8-f827-452f-838a-e14fa3b87621
ms.openlocfilehash: 634d9c5248c33619abec50d441d95c111febdcbf
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699409"
---
# <a name="startup-element"></a>\<startup > 요소

공용 언어 런타임 시작 정보를 지정 합니다.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp; **\<startup>**  

## <a name="syntax"></a>구문

```xml
<startup useLegacyV2RuntimeActivationPolicy="true|false" > 
</startup>
```

## <a name="attributes-and-elements"></a>특성 및 요소

 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`useLegacyV2RuntimeActivationPolicy`|선택적 특성입니다.<br /><br /> .NET Framework 2.0 런타임 활성화 정책 사용 여부를 지정 하거나 .NET Framework 4 활성화 정책을 사용할지 여부를 지정 합니다.|

## <a name="uselegacyv2runtimeactivationpolicy-attribute"></a>useLegacyV2RuntimeActivationPolicy 특성

|값|설명|
|-----------|-----------------|
|`true`|[CorBindToRuntimeEx 함수](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)등의 레거시 런타임 활성화 기법을 CLR에서 50, 하는 대신 구성 파일에서 선택한 런타임에 바인딩하는 .NET Framework 2.0 런타임 활성화 정책을 사용 하도록 설정 합니다. 버전 2.0. 따라서 구성 파일에서 CLR 버전 4 이상을 선택한 경우 이전 버전의 .NET Framework을 사용 하 여 만든 혼합 모드 어셈블리는 선택한 CLR 버전과 함께 로드 됩니다. 이 값을 설정 하면 CLR 버전 1.1 또는 CLR 버전 2.0이 동일한 프로세스로 로드 되지 않으므로 in-process side-by-side 기능을 효과적으로 사용 하지 않습니다.|
|`false`|.NET Framework 4 이상에 대 한 기본 활성화 정책을 사용 합니다 .이는 레거시 런타임 활성화 기술을 통해 CLR 버전 1.1 또는 2.0을 프로세스에 로드할 수 있습니다. 이 값을 설정 하면 .NET Framework 4 이상에서 빌드된 경우를 제외 하 고 혼합 모드 어셈블리를 .NET Framework 4 이상으로 로드할 수 없습니다. 이 값은 기본값입니다.|

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[\<requiredRuntime>](requiredruntime-element.md)|애플리케이션에서 1.0 버전의 공용 언어 런타임만 지원하도록 지정합니다. 런타임 버전 1.1 이상을 사용 하 여 빌드된 응용 프로그램은 **\<supportedRuntime >** 요소를 사용 해야 합니다.|
|[\<supportedRuntime>](supportedruntime-element.md)|애플리케이션이 지원하는 공용 언어 런타임 버전을 지정합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|

## <a name="remarks"></a>설명

 **@No__t-1supportedRuntime >** 요소는 버전 1.1 이상을 사용 하 여 빌드된 모든 응용 프로그램에서 사용 해야 합니다. 버전 1.0의 런타임을 지원 하도록 빌드된 응용 프로그램은 **\<requiredRuntime >** 요소를 사용 해야 합니다.

 Microsoft Internet Explorer에서 호스트 되는 응용 프로그램의 시작 코드는 **\<startup >** 요소 및 해당 자식 요소를 무시 합니다.

## <a name="the-uselegacyv2runtimeactivationpolicy-attribute"></a>UseLegacyV2RuntimeActivationPolicy 특성

 이 특성은 [CorBindToRuntimeEx 함수와](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)같은 레거시 활성화 경로를 사용 하는 응용 프로그램에서 이전 버전이 아닌 CLR 버전 4를 활성화 하거나 응용 프로그램을 .net으로 빌드하는 경우에 유용 합니다. 프레임 워크 4 이지만 이전 버전의 .NET Framework로 빌드된 혼합 모드 어셈블리에 대 한 종속성이 있습니다. 이러한 시나리오에서는 특성을 `true`으로 설정 합니다.

> [!NOTE]
> 특성을 `true`으로 설정 하면 CLR 버전 1.1 또는 CLR 버전 2.0이 동일한 프로세스로 로드 되지 않으므로 in-process side-by-side 기능이 효과적으로 사용 되지 않습니다 ( [COM Interop에 대 한 Side-by-side 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100))참조).

## <a name="example"></a>예제

 다음 예제에서는 구성 파일의 런타임 버전을 지정 하는 방법을 보여 줍니다.

```xml
<!-- When used with version 1.0 of the .NET Framework runtime -->
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
<!-- When used with version 1.1 (or later) of the runtime -->
<configuration>
   <startup>
      <supportedRuntime version="v1.1.4322"/>
      <supportedRuntime version="v1.0.3705"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>참조

- [시작 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [방법: .NET Framework 4 이상 버전을 지원하도록 앱 구성](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [COM Interop에 대 한 side-by-side 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100))
- [In-Process Side-by-Side 실행](../../../deployment/in-process-side-by-side-execution.md)
