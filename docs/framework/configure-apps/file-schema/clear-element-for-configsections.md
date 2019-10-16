---
title: <configSections>에 대한 <clear> 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/clear
helpviewer_keywords:
- clear Element
- <clear> Element
ms.assetid: 77f1d761-ff45-4001-8f36-3a3e5c41fa63
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: c06fca8b83638fb47bedb21863cb9b200cd211f3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927737"
---
# <a name="clear-element-for-configsections"></a>\<configsections에 대 \<한 > 요소를 지웁니다 >

이전에 정의 된 모든 섹션과 섹션 그룹을 지웁니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<clear>**

## <a name="syntax"></a>구문

```xml
<clear/>
```

## <a name="attribute"></a>특성

|           | 설명 |
| --------- | ----------- |
| **name**  | 필수 특성입니다.<br><br>제거할 섹션 또는 섹션 그룹의 이름을 지정 합니다. |

## <a name="parent-element"></a>부모 요소

|     | Description |
| --- | ----------- |
| [configsections > 요소  **\<** ](configsections-element-for-configuration.md) | 구성 섹션과 네임 스페이스 선언을 포함 합니다. |

## <a name="child-elements"></a>자식 요소

없음

## <a name="remarks"></a>설명

**\<Clear >** 요소는 이전에 현재 구성 파일에 정의 되어 있거나 구성 파일 계층 구조에서 상위 수준에 정의 된 응용 프로그램에서 모든 섹션과 섹션 그룹을 제거 합니다.

## <a name="example"></a>예제

이 예제에서는 컴퓨터 구성 파일 및 응용 프로그램 구성 파일을 정의 하 고, 응용 프로그램 구성 파일에서  **\<clear >** 요소를 사용 하 여 이전에 컴퓨터 구성에 정의 된 섹션을 지우는 방법을 보여 줍니다. 파일과.

다음 컴퓨터 구성 파일 코드는 응용 프로그램 구성 파일 앞에서 읽은 두 섹션인  **\<sampleSection >** 및  **\<anotherSampleSection >** 를 선언 합니다.

```xml
<!-- Machine.config file -->
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" />
    <section name="anotherSampleSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <sampleSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

다음 응용 프로그램 구성 파일 코드는 이전에 선언 된 섹션을 모두 지웁니다. 응용 프로그램은 컴퓨터 구성 파일에 선언 된 섹션 중 하나에서 설정을 사용 하거나 검색할 수 없습니다. **그러나 \<clear >** 요소 뒤에 있기 때문에  **\<>** 의 설정을 사용할 수 있습니다.

```xml
<!-- Application configuration file -->
<configuration>
  <configSections>
    <clear/>
    <section name="anotherSection"
             type="System.Configuration.NameValueSectionHandler" />
  </configSections>
  <anotherSection setting1="Value1" 
                 setting2="value two" 
                 setting3="third value" />
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일, 컴퓨터 구성 파일 (machine.config) 및응용 프로그램 디렉터리 수준에 없는 web.config 파일에서 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
