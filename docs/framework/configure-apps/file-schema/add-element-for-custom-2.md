---
title: <add>NameValueSectionHandler 및 DictionarySectionHandler에 대 한 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/sectionName/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 0d4ddb53-eb2b-49c0-9c33-a8dec5c39b46
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: ec6d5045580e887de5f05a05c8f39fa62c6e3f2e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921321"
---
# <a name="add-element-for-namevaluesectionhandler-and-dictionarysectionhandler"></a>\<NameValueSectionHandler 및 DictionarySectionHandler에 대 한 > 요소 추가

사용자 지정 응용 프로그램 설정을 추가 합니다. **각\<추가 >** 태그에는 키/값 쌍이 포함 되어 있습니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<sectionName>** ](custom-element-2.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<add>**

## <a name="syntax"></a>구문

```xml
<add key="key" value="value" />
```

## <a name="attributes"></a>특성

| 특성 | 설명 |
| --------- | ----------- |
| **key**   | 필수 특성입니다.<br><br>설정의 이름을 지정 합니다. |
| **value** | 필수 특성입니다.<br><br>설정 값을 지정 합니다. |

## <a name="parent-element"></a>부모 요소

| 요소 | Description |
| ------- | ------------|
| [섹션 이름 > 요소  **\<** ](custom-element-2.md) | <xref:System.Configuration.NameValueSectionHandler> 및<xref:System.Configuration.DictionarySectionHandler> 클래스를 사용 하는 사용자 지정 구성 섹션에 대 한 설정을 정의 합니다. |

## <a name="child-elements"></a>자식 요소

없음

## <a name="example"></a>예제

다음 예제에서는 사용자 지정 구성 섹션을 정의 하 고  **\<add >** 요소를 사용 하 여 설정을 섹션에 배치 하는 방법을 보여 줍니다.

```xml
<configuration>
  <configSections>
    <section name="dictionarySample" type="System.Configuration.DictionarySectionHandler,System" />
  </configSections>
  <dictionarySample>
    <add key="myKey" value="myValue" />
  </dictionarySample>
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일, 컴퓨터 구성 파일 (machine.config) 및응용 프로그램 디렉터리 수준에 없는 web.config 파일에서 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
