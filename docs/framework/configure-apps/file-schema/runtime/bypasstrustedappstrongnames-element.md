---
title: <bypassTrustedAppStrongNames> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- strong-name bypass feature
- bypassTrustedAppStrongNames element
- strong-named assemblies, loading into trusted application domains
- <bypassTrustedAppStrongNames> element
ms.assetid: 71b2ebf6-3843-41e2-ad52-ffa5cd083a40
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 35b4c6201b5181b8d7241906f60a731e4175d523
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991233"
---
# <a name="bypasstrustedappstrongnames-element"></a>\<bypassTrustedAppStrongNames> 요소

완전 신뢰 <xref:System.AppDomain>로 로드 된 완전 신뢰 어셈블리의 강력한 이름에 대 한 유효성 검사를 건너뛸지 여부를 지정 합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<bypassTrustedAppStrongNames>**

## <a name="syntax"></a>구문

```xml
<bypassTrustedAppStrongNames
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`enabled`|필수 특성입니다.<br /><br /> 완전 신뢰 어셈블리의 강력한 이름 유효성 검사를 방지 하는 바이패스 기능을 사용 하도록 설정할지 여부를 지정 합니다. 이 기능을 사용 하는 경우 어셈블리가 로드 될 때 강력한 이름의 유효성이 검사 되지 않습니다. 기본값은 `true`입니다.|

## <a name="enabled-attribute"></a>enabled 특성

|값|설명|
|-----------|-----------------|
|`true`|완전 신뢰 어셈블리의 강력한 이름 서명은 어셈블리가 완전 신뢰 <xref:System.AppDomain>로 로드 될 때 유효성이 검사 되지 않습니다. 이 값이 기본값입니다.|
|`false`|완전 신뢰 어셈블리의 강력한 이름 서명은 어셈블리가 완전 신뢰 <xref:System.AppDomain>로 로드 될 때 유효성이 검사 됩니다. 강력한 이름 시그니처는 서명 정확성에 대해서만 확인 됩니다. 일치 항목에 대 한 다른 강력한 이름과 비교 되지 않습니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|

## <a name="remarks"></a>설명

강력한 이름 건너뛰기 기능을 사용 하면 완전 신뢰 어셈블리의 강력한 이름 서명 확인의 오버 헤드가 방지 됩니다.

건너뛰기 기능은 강력한 이름으로 서명되었으며 다음과 같은 특징이 있는 모든 어셈블리에 적용됩니다.

- <xref:System.Security.Policy.StrongName> 증명 정보 없이 완전히 신뢰할 수 있는 경우 (예 `MyComputer` : 영역 증명 정보 포함)

- 완전히 신뢰할 수 있는 <xref:System.AppDomain>에 로드됨

- 해당 <xref:System.AppDomain>의 <xref:System.AppDomainSetup.ApplicationBase%2A> 속성 아래에 있는 위치에서 로드됨

- 서명이 연기되지 않음

> [!NOTE]
> 레지스트리 키를 사용 하 여 컴퓨터의 모든 응용 프로그램에 대해 바이패스 기능이 꺼져 있는 경우이 구성 파일 설정은 적용 되지 않습니다. 자세한 내용은 [방법: 강력한 이름 건너뛰기 기능 비활성화](../../../app-domains/how-to-disable-the-strong-name-bypass-feature.md)

## <a name="example"></a>예제

다음 예제에서는 완전 신뢰 어셈블리에서 강력한 이름 서명의 유효성을 검사 하는 동작을 지정 하는 방법을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <bypassTrustedAppStrongNames enabled="false"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [방법: 강력한 이름 건너뛰기 기능을 사용 하지 않도록 설정](../../../../standard/assembly/disable-strong-name-bypass-feature.md)
