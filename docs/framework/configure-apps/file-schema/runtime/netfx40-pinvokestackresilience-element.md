---
title: <NetFx40_PInvokeStackResilience> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_PInvokeStackResilience> element
- NetFx40_PInvokeStackResilience element
ms.assetid: 39fb1588-72a4-4479-af74-0605233b68bd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8f4dffe5428ccb7541055fa4f3f335f57deaf2ec
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252437"
---
# <a name="netfx40_pinvokestackresilience-element"></a>\<NetFx40_PInvokeStackResilience > 요소

런타임이 잘못된 플랫폼 호출 선언을 실행 시간에 자동으로 수정할지를 지정합니다. 자동 수정을 수행하는 경우 관리 코드와 비관리 코드 간 전환 속도가 느려집니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<NetFx40_PInvokeStackResilience >**  

## <a name="syntax"></a>구문

```xml
<NetFx40_PInvokeStackResilience  enabled="1|0"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`enabled`|필수 특성입니다.<br /><br /> 런타임이 잘못 된 플랫폼 호출 선언을 검색 하 고 런타임에 32 비트 플랫폼에서 스택을 자동으로 수정 하는지 여부를 지정 합니다.|

## <a name="enabled-attribute"></a>enabled 특성

|값|Description|
|-----------|-----------------|
|`0`|런타임은 잘못 된 플랫폼 호출 선언을 검색 하 고 수정 하지 않는 .NET Framework 4에서 도입 된 더 빠른 interop 마샬링 아키텍처를 사용 합니다. 기본값입니다.|
|`1`|런타임에서는 잘못 된 플랫폼 호출 선언을 검색 하 고 수정 하는 느린 전환을 사용 합니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|

## <a name="remarks"></a>설명

이 요소를 사용 하면 잘못 된 플랫폼 호출 선언에 대해 런타임 복원 력을 더 빠르게 수행할 수 있습니다.

.NET Framework 4부터, 간소화 된 interop 마샬링 아키텍처는 관리 코드에서 비관리 코드로의 전환을 위한 상당한 성능 향상을 제공 합니다. 이전 버전의 .NET Framework에서는 마샬링 계층이 32 비트 플랫폼에서 잘못 된 플랫폼 호출 선언을 검색 하 고 스택을 자동으로 수정 했습니다. 새 마샬링 아키텍처는이 단계를 제거 합니다. 결과적으로 전환은 매우 빠르지만 잘못 된 플랫폼 호출 선언으로 인해 프로그램 오류가 발생할 수 있습니다.

개발 하는 동안 잘못 된 선언을 쉽게 검색할 수 있도록 Visual Studio 디버깅 환경이 개선 되었습니다. [PINVOKESTACKIMBALANCE](../../../debug-trace-profile/pinvokestackimbalance-mda.md) MDA (관리 디버깅 도우미)는 디버거가 연결 된 상태에서 응용 프로그램을 실행할 때 잘못 된 플랫폼 호출 선언이 있음을 알려 줍니다.

응용 프로그램에서 다시 컴파일할 수 없는 구성 요소를 사용 하 고 잘못 된 플랫폼 호출 선언이 있는 시나리오를 해결 하기 위해 요소 `NetFx40_PInvokeStackResilience` 를 사용할 수 있습니다. Opts를 사용 하 여 `enabled="1"` 이 요소를 응용 프로그램 구성 파일에 추가 하는 것은 이전 버전의 .NET Framework 동작을 사용 하 여 호환성 모드로 전환 하는 것이 더 느린 전환의 비용입니다. 이전 버전의 .NET Framework에 대해 컴파일된 어셈블리는 자동으로이 호환 모드로 옵트인 되며이 요소가 필요 하지 않습니다.

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일에만 사용할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 관리 코드와 비관리 코드 간의 느린 전환으로 인해 응용 프로그램에 대 한 잘못 된 플랫폼 호출 선언에 대해 늘어난 복원 력을 옵트인 (opt in) 하는 방법을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <NetFx40_PInvokeStackResilience enabled="1"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [pInvokeStackImbalance](../../../debug-trace-profile/pinvokestackimbalance-mda.md)
