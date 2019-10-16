---
title: <NetFx40_LegacySecurityPolicy> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- <NetFx40_LegacySecurityPolicy> element
- NetFx40_LegacySecurityPolicy element
ms.assetid: 07132b9c-4a72-4710-99d7-e702405e02d4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2cd6f937811ae503dd4de7ff989510c4eb8b8933
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252442"
---
# <a name="netfx40_legacysecuritypolicy-element"></a>\<Y > 요소

런타임이 레거시 CAS(코드 액세스 보안) 정책을 사용할지를 지정합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<Y >**  

## <a name="syntax"></a>구문

```xml
<NetFx40_LegacySecurityPolicy
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`enabled`|필수 특성입니다.<br /><br /> 런타임이 레거시 CAS 정책을 사용 하는지 여부를 지정 합니다.|

## <a name="enabled-attribute"></a>enabled 특성

|값|설명|
|-----------|-----------------|
|`false`|런타임은 레거시 CAS 정책을 사용 하지 않습니다. 이 값이 기본값입니다.|
|`true`|런타임은 레거시 CAS 정책을 사용 합니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|

## <a name="remarks"></a>설명

.NET Framework 버전 3.5 및 이전 버전에서는 CAS 정책이 항상 적용 됩니다. .NET Framework 4에서 CAS 정책을 사용 하도록 설정 해야 합니다.

CAS 정책은 버전별 정책입니다. 이전 버전의 .NET Framework에 존재 하는 사용자 지정 CAS 정책은 .NET Framework 4에서 respecified 해야 합니다.

.NET Framework 4 어셈블리에 `<NetFx40_LegacySecurityPolicy>` 요소를 적용해도 [보안 투명코드](../../../misc/security-transparent-code.md)에는 영향을 주지않습니다. 투명성 규칙은 여전히 적용됩니다.

> [!IMPORTANT]
> 요소를 `<NetFx40_LegacySecurityPolicy>` 적용 하면 [전역 어셈블리 캐시](../../../app-domains/gac.md)에 설치 되지 않은 [네이티브 이미지 생성기 (ngen.exe)](../../../tools/ngen-exe-native-image-generator.md) 에서 생성 되는 네이티브 이미지 어셈블리에 대해 상당한 성능 저하가 발생할 수 있습니다. 성능이 저하 되는 이유는 특성이 적용 될 때 런타임이 네이티브 이미지로 어셈블리를 로드할 수 없어 just-in-time 어셈블리로 로드 되는 경우에 발생 합니다.

> [!NOTE]
> Visual Studio 프로젝트에 대 한 프로젝트 설정에서 .NET Framework 4 이전의 대상 .NET Framework 버전을 지정 하는 경우 해당 버전에 대해 지정한 모든 사용자 지정 CAS 정책을 포함 하 여 CAS 정책이 사용 됩니다. 그러나 새 .NET Framework 4 형식 및 멤버를 사용할 수는 없습니다. [응용 프로그램 구성 파일](../../index.md)에서 시작 설정 스키마의 [ \<supportedruntime> > 요소](../startup/supportedruntime-element.md) 를 사용 하 여 .NET Framework의 이전 버전을 지정할 수도 있습니다.

> [!NOTE]
> 구성 파일 구문은 대/소문자를 구분 합니다. 구문 및 예제 섹션에서 제공 하는 구문을 사용 해야 합니다.

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일에만 사용할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 응용 프로그램에 대해 레거시 CAS 정책을 사용 하도록 설정 하는 방법을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <NetFx40_LegacySecurityPolicy enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
