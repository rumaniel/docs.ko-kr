---
title: <GCCpuGroup> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- GCCpuGroup element
- <GCCpuGroup> element
ms.assetid: c1fc7d6c-7220-475c-a312-5b8b201f66e0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9ff646f13c5619b0bfca1b61c86013a981c274e3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252560"
---
# <a name="gccpugroup-element"></a>\<GCCpuGroup > 요소

가비지 수집에서 여러 CPU 그룹을 지원할지를 지정합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<GCCpuGroup>**  

## <a name="syntax"></a>구문

```xml
<GCCpuGroup
   enabled="true|false"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`enabled`|필수 특성입니다.<br /><br /> 가비지 수집에서 여러 CPU 그룹을 지원할지를 지정합니다.|

## <a name="enabled-attribute"></a>enabled 특성

|값|설명|
|-----------|-----------------|
|`false`|가비지 수집은 여러 CPU 그룹을 지원 하지 않습니다. 이 값이 기본값입니다.|
|`true`|서버 가비지 수집을 사용 하는 경우 가비지 수집은 여러 CPU 그룹을 지원 합니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|

## <a name="remarks"></a>설명

컴퓨터에 여러 cpu 그룹이 있고 서버 가비지 수집이 사용 되는 경우 ( [ \<gcServer >](gcserver-element.md) 요소 참조)이 요소를 사용 하도록 설정 하면 모든 CPU 그룹에서 가비지 수집을 확장 하 고를 만들 때 모든 코어를 고려 합니다. 힙 분산.

> [!NOTE]
> 이 요소는 가비지 수집 스레드에만 적용 됩니다. 런타임이 모든 CPU 그룹에 사용자 스레드를 배포할 수 있도록 하려면 [ \<Thread_UseAllCpuGroups >](thread-useallcpugroups-element.md) 요소도 사용 하도록 설정 해야 합니다.

## <a name="example"></a>예제

다음 예제에서는 여러 CPU 그룹에 대해 가비지 수집을 사용 하도록 설정 하는 방법을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <GCCpuGroup enabled="true"/>
      <gcServer enabled="true"/>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [동시 가비지 수집을 사용 하지 않도록 설정 하려면](gcconcurrent-element.md#to-disable-background-garbage-collection)
- [워크스테이션 및 서버 가비지 수집](../../../../standard/garbage-collection/fundamentals.md#workstation_and_server_garbage_collection)
