---
title: <configSections>에 대한 <remove> 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/remove
helpviewer_keywords:
- remove Element
- <remove> Element
ms.assetid: ae4d82e0-e8fe-468c-81ab-46d63c4d66a8
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: 4ff9bb537a31e28dbd4b878c1bc04c96262f85ac
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927466"
---
# <a name="remove-element-for-configsections"></a>\<configsections에 대 \<한 > 요소를 제거 >

미리 정의 된 섹션 또는 섹션 그룹을 제거 합니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<remove>**

## <a name="syntax"></a>구문

```xml
<remove name="section name or section group name" />
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

Remove > 요소를 사용  **\<** 하 여 구성 파일 계층 구조에서 상위 수준에 정의 된 섹션 및 섹션 그룹을 응용 프로그램에서 제거할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 응용 프로그램 구성 파일에서  **\<remove >** 요소를 사용 하 여 컴퓨터 구성 파일에 이전에 정의 된 섹션을 제거 하는 방법을 보여 줍니다.

다음 컴퓨터 구성 파일 코드는  **\<sampleSection >** 섹션을 선언 합니다.

```xml
<!-- Machine.config file -->
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

다음 응용 프로그램 구성 파일 코드는  **\<sampleSection >** 섹션을 제거 합니다. 제거 후 응용 프로그램은  **\<sampleSection >** 에서 설정을 검색할 수 없습니다.

```xml
<!-- Application configuration file -->
<configuration>
  <configSections>
    <remove name="sampleSection"/>
  </configSections>
</configuration>
```

## <a name="configuration-file"></a>구성 파일

이 요소는 응용 프로그램 구성 파일, 컴퓨터 구성 파일 (machine.config) 및응용 프로그램 디렉터리 수준에 없는 web.config 파일에서 사용할 수 있습니다.

## <a name="see-also"></a>참고자료

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
