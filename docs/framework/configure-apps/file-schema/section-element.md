---
title: <section> element
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/section
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/sectionGroup/section
helpviewer_keywords:
- section Element
- <section> Element
ms.assetid: ec7d4110-2403-47ac-8218-499bfe9d5ddb
author: rpetrusha
ms.author: mairaw
ms.openlocfilehash: 94f7709f4bd273515d9fcdd727354ec579c46207
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927221"
---
# <a name="section-element"></a>\<section > 요소

구성 섹션 선언을 포함 합니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<section>**

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<configSections>** ](configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<sectionGroup>** ](sectiongroup-element-for-configsections.md)   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<section>**

## <a name="syntax"></a>구문

```xml
<section name="section name"
         type="configuration section handler class, assembly"
         allowDefinition="Everywhere|MachineOnly|MachineToApplication" 
         allowLocation="true|false" />
```

## <a name="required-attributes"></a>필수 특성

|           | 설명 |
| --------- | ----------- |
| **name**  | 구성 섹션의 이름을 지정 합니다. |
| **type**  | 구성 파일에서 섹션을 읽는 구성 섹션 처리기 클래스의 이름을 지정 합니다. 형식 값의 구문은 "정규화 된 섹션-클래스 이름, 단순 어셈블리 이름"입니다. 단순 어셈블리 이름은 *.dll* 파일 확장명이 없는 루트 파일 이름입니다. |

## <a name="optional-attributes"></a>선택적 특성

다음 특성은 ASP.NET 응용 프로그램에만 적용 됩니다. 구성 시스템에서는 다른 응용 프로그램 유형에 대 한 이러한 특성을 무시 합니다.

|                     | Description |
| ------------------- | ----------- |
| **allowDefinition** | 섹션을 사용할 수 있는 구성 파일을 지정 합니다. 다음 값 중 하나를 사용합니다.<br><br>**마다**<br>섹션을 모든 구성 파일에서 사용할 수 있습니다. 기본값입니다.<br>**MachineOnly**<br>컴퓨터 구성 파일 (machine.config) 에서만 섹션을 사용할 수 있습니다.<br>**MachineToApplication**<br>컴퓨터 구성 파일 또는 응용 프로그램 구성 파일에서 섹션을 사용할 수 있습니다. |
| **allowLocation**   | 위치 > 요소 내에서  **\<** 섹션을 사용할 수 있는지 여부를 확인 합니다. 다음 값 중 하나를 사용합니다.<br><br>**true**<br>Location > 요소 내  **\<** 에 섹션을 사용할 수 있습니다. 기본값입니다.<br>**false**<br>에서는  **\<location >** 요소 내에서 섹션을 사용 하는 것을 허용 하지 않습니다. |

## <a name="parent-elements"></a>부모 요소

|     | Description |
| --- | ----------- |
| [configsections > 요소  **\<** ](configsections-element-for-configuration.md) | 구성 섹션과 네임 스페이스 선언을 포함 합니다. |
| [ **sectionGroup>\<** 요소](sectiongroup-element-for-configsections.md) | 구성 섹션에 대 한 네임 스페이스를 정의 합니다. |

> [!NOTE]
> 섹션 > 요소는  **\<configsections >** 또는  **\<sectionGroup >** 의 자식 요소 이지만 둘 다는 아닙니다.  **\<**

## <a name="child-elements"></a>자식 요소

없음

## <a name="remarks"></a>설명

구성 섹션을 선언 하는 것은 기본적으로 구성 파일에 대 한 새 요소를 정의 합니다. 새 요소는 구성 섹션 처리기 (즉, <xref:System.Configuration.IConfigurationSectionHandler> 인터페이스를 구현 하는 클래스)가 읽는 설정을 포함 합니다. 사용자가 정의 하는 섹션의 특성 및 자식 요소는 설정을 읽는 데 사용 하는 섹션 처리기에 따라 달라 집니다.

Machine.config 파일에서 구성 섹션 처리기를 선언 하면 **allowDefinition** 특성이 달리 지정 되지 않는 한 해당 컴퓨터의 모든 응용 프로그램 구성 파일에서 구성 섹션을 사용할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 구성 섹션을 정의 하 고 해당 섹션에 대 한 설정을 정의 하는 방법을 보여 줍니다.

```xml
<configuration>
  <configSections>
    <section name="sampleSection"
             type="System.Configuration.SingleTagSectionHandler" 
             allowLocation="false" />
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
