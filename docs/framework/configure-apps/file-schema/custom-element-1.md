---
title: SingleTagSectionHandler에 대 한 사용자 지정 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName
helpviewer_keywords:
- custom element
ms.assetid: e62056c6-b351-40eb-afc0-cc13fc44e45e
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: 8fae3673fe72d036802cb1a8366aaa2430c38884
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927496"
---
# <a name="custom-element-for-singletagsectionhandler"></a>SingleTagSectionHandler에 대 한 사용자 지정 요소

\<섹션 > 요소에 정의 되 고 클래스를 <xref:System.Configuration.SingleTagSectionHandler> 사용 하는 사용자 지정 구성 섹션의 설정을 정의 합니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp; *\<sectionName>*

## <a name="syntax"></a>구문

```xml
<sectionName key="value" key2="value2" ... />
```

## <a name="attributes"></a>특성

특성 및 특성 값은 사용자 정의 됩니다.

## <a name="parent-element"></a>부모 요소

|     | 설명 |
| --- | ----------- |
| [ **\<configuration>** ](configuration-element.md) | 공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다. |

## <a name="child-elements"></a>자식 요소

없음

## <a name="remarks"></a>설명

섹션 이름 > 요소는 [**configsections > 요소의 section > 태그에 의해 정의 되는 사용자 지정 요소입니다. \<** ](configsections-element-for-configuration.md) [ **\<** ](section-element.md)  **\<** 를 호출할 <xref:System.Collections.IDictionary> <xref:System.Configuration.Configuration.GetSection(System.String)?displayProperty=nameWithType>때 구성 시스템에서 개체를 반환 합니다.

## <a name="example"></a>예제

다음 예제에서는 <xref:System.Configuration.SingleTagSectionHandler> 클래스에서 읽은 설정을 포함 하는  **\<sampleSection >** 이라는 사용자 지정 요소를 선언 합니다.

```xml
<configuration>
  <configSections>
    <section name="sampleSection" 
             type="System.Configuration.SingleTagSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일, 컴퓨터 구성 파일 (machine.config) 및응용 프로그램 디렉터리 수준에 없는 web.config 파일에서 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
