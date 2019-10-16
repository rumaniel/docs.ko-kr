---
title: <requiredRuntime> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#requiredRuntime
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup/requiredRuntime
helpviewer_keywords:
- requiredRuntime element
- <requiredRuntime> element
- container tags, <requiredRuntime> element
ms.assetid: 9fa1639e-beb8-43be-b7a4-12f7b229c34b
ms.openlocfilehash: fe96673b95f48cb75d36662a680bf56a59363f9f
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697496"
---
# <a name="requiredruntime-element"></a>\<requiredRuntime > 요소

애플리케이션에서 1.0 버전의 공용 언어 런타임만 지원하도록 지정합니다. 이 요소는 사용 되지 않으며 더 이상 사용 되지 않습니다. [@No__t-1](supportedruntime-element.md) 요소를 대신 사용 해야 합니다.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<startup >** ](startup-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<requiredRuntime >**  

## <a name="syntax"></a>구문

```xml
   <requiredRuntime  
version="runtime version"
safemode="true|false"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`version`|선택적 특성입니다.<br /><br /> 이 응용 프로그램에서 지 원하는 .NET Framework 버전을 지정 하는 문자열 값입니다. 문자열 값은 .NET Framework 설치 루트 아래에 있는 디렉터리 이름과 일치 해야 합니다. 문자열 값의 내용은 구문 분석 되지 않습니다.|
|`safemode`|선택적 특성입니다.<br /><br /> 런타임 시작 코드가 레지스트리를 검색 하 여 런타임 버전을 확인할 지 여부를 지정 합니다.|

## <a name="safemode-attribute"></a>안전 안전 특성

|값|설명|
|-----------|-----------------|
|`false`|런타임 시작 코드는 레지스트리에서 찾습니다. 기본값입니다.|
|`true`|런타임 시작 코드는 레지스트리에 표시 되지 않습니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`startup`|요소를 `<requiredRuntime>` 포함 합니다.|

## <a name="remarks"></a>설명
 버전 1.0의 런타임을 지원 하도록 빌드된 응용 프로그램은 `<requiredRuntime>` 요소를 사용 해야 합니다. 버전 1.1 이상을 사용 하 여 빌드된 응용 프로그램은 `<supportedRuntime>` 요소를 사용 해야 합니다.

> [!NOTE]
> [CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md) 함수를 사용 하 여 구성 파일을 지정 하는 경우 모든 버전의 런타임에 대해 `<requiredRuntime>` 요소를 사용 해야 합니다. [CorBindToRuntimeByCfg](../../../unmanaged-api/hosting/corbindtoruntimebycfg-function.md)를 사용 하는 경우 `<supportedRuntime>` 요소는 무시 됩니다.

 @No__t-0 특성 문자열은 지정 된 .NET Framework 버전의 설치 폴더 이름과 일치 해야 합니다. 이 문자열은 해석 되지 않습니다. 런타임 시작 코드에서 일치 하는 폴더를 찾지 못하면 런타임은 로드 되지 않습니다. 시작 코드는 오류 메시지를 표시 하 고 종료 됩니다.

> [!NOTE]
> Microsoft Internet Explorer에서 호스트 되는 응용 프로그램의 시작 코드는 `<requiredRuntime>` 요소를 무시 합니다.

## <a name="example"></a>예제

다음 예제에서는 구성 파일의 런타임 버전을 지정 하는 방법을 보여 줍니다.

```xml
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>참조

- [시작 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [방법: .NET Framework 4 이상 버전을 지원하도록 앱 구성](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
