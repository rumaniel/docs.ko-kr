---
title: bypasslist의 <remove> 요소(네트워크 설정)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: 97b49a8a520d6a4f72945366874991d2deb18710
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697903"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>\<remove > 요소 bypasslist (네트워크 설정)

프록시 바이패스 목록에서 IP 주소 또는 DNS 이름을 제거 합니다.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4c.net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<defaultProxy >** ](defaultproxy-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<bypasslist >** ](bypasslist-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<remove >**  

## <a name="syntax"></a>구문

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|**특성**|**설명**|
|-------------------|---------------------|
|`address`|IP 주소 또는 DNS 이름을 설명 하는 정규식입니다.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|**요소**|**설명**|
|-----------------|---------------------|
|[bypasslist](bypasslist-element-network-settings.md)|프록시를 사용 하지 않는 주소를 설명 하는 정규식 집합을 제공 합니다.|

## <a name="remarks"></a>설명

@No__t-0 요소는 프록시 서버를 우회 하는 주소 목록에서 IP 주소 또는 DNS 서버 이름을 설명 하는 정규식을 제거 합니다. 주소가 구성 파일에서 이전에 정의 되었거나 구성 계층 구조의 상위 수준에 정의 되어 있습니다.

@No__t-0 특성의 값은 IP 주소 또는 호스트 이름 집합을 설명 하는 정규식 이어야 합니다.

정규식에 대 한 자세한 내용은을 참조 하십시오. [정규식을 .NET Framework](../../../../standard/base-types/regular-expressions.md)합니다.

## <a name="configuration-files"></a>구성 파일

이 요소는 애플리케이션 구성 파일 또는 컴퓨터 구성 파일(Machine.config)에서 사용할 수 있습니다.

## <a name="example"></a>예제

다음 예에서는 adventure-works.com 도메인에 대 한 이전 정의를 제거 하 고 contoso.com 도메인을 바이패스 목록에 추가 합니다.

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>참조

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [네트워크 설정 스키마](index.md)
