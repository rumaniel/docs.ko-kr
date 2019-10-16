---
title: <linkedConfiguration> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding/linkedConfiguration
- http://schemas.microsoft.com/.NetConfiguration/v2.0#linkedConfiguration
helpviewer_keywords:
- configuration files [.NET Framework],linked configuration files
- <linkedConfiguration> element
- including configuration files
- linked configuration files
- linkedConfiguration Element
ms.assetid: 8eb34f3b-427e-4288-a7ff-c73f489deb45
ms.openlocfilehash: a0b56ac66302f11c59c149197a84bb96691282a5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921008"
---
# <a name="linkedconfiguration-element"></a>\<linkedConfiguration > 요소

포함할 구성 파일을 지정합니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp;[ **\<assemblyBinding>** ](assemblybinding-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp; **\<linkedConfiguration>**

## <a name="syntax"></a>구문

```xml
<linkedConfiguration href="URL of linked configuration file" />
```

## <a name="attribute"></a>특성

|           | Description |
| --------- | ----------- |
| **href**  | 필수 특성입니다.<br><br>포함할 구성 파일의 URL입니다. **Href** 특성 `file://`에 대해 지원 되는 유일한 형식은입니다. 로컬 파일 및 UNC 파일이 지원 됩니다. |

## <a name="parent-element"></a>부모 요소

|     | Description |
| --- | ----------- |
| [assemblybinding > 요소  **\<** ](assemblybinding-element-for-configuration.md) | 구성 수준에서 어셈블리 바인딩 정책을 지정합니다. |

## <a name="child-elements"></a>자식 요소

없음

## <a name="remarks"></a>설명

**\<LinkedConfiguration >** 요소는 구성 요소 어셈블리에 대 한 서비스를 간소화 합니다. 하나 이상의 응용 프로그램에서 잘 알려진 위치에 있는 구성 파일이 있는 어셈블리를 사용 하는 경우 해당 어셈블리를 사용 하는 응용 프로그램의 구성 파일은  **\<linkedConfiguration >** 요소를 사용 하 여 구성 정보를 직접 포함 하는 것이 아니라 어셈블리 구성 파일입니다. 구성 요소 어셈블리를 서비스할 때 공통 구성 파일을 업데이트 하면 어셈블리를 사용 하는 모든 응용 프로그램에 업데이트 된 구성 정보가 제공 됩니다.

> [!NOTE]
> LinkedConfiguration > 요소는 Windows side-by-side 매니페스트를 사용 하는 응용 프로그램에 대해 지원 되지 않습니다.  **\<**

다음 규칙은 연결 된 구성 파일의 사용을 제어 합니다.

- 포함 된 구성 파일의 설정은 로더 바인딩 정책에만 영향을 주며 로더에서 사용 됩니다. 포함 된 구성 파일에는 바인딩 정책 이외의 설정이 있을 수 있지만 이러한 설정은 적용 되지 않습니다.

- `href` 특성에 대해 지원 되는 유일한 형식은 입니다.`file://` 로컬 파일 및 UNC 파일이 지원 됩니다.

- 구성 파일당 연결 된 구성 수에는 제약 조건이 없습니다.

- C/ `#include` C++에서 지시문의 동작과 유사 하 게 모든 연결 된 구성 파일을 병합 하 여 하나의 파일을 구성 합니다.

- **\<LinkedConfiguration >** 요소는 응용 프로그램 구성 파일 에서만 사용할 수 있으며 *machine.config*에서 무시 됩니다.

- 순환 참조가 감지 되 고 종료 됩니다. 즉, 일련의 구성 파일에 있는  **\<linkedConfiguration >** 요소가 루프를 형성 하면 루프가 검색 되 고 중지 됩니다.

## <a name="example"></a>예제

다음 예제에서는 로컬 하드 디스크의 구성 파일을 포함 하는 방법을 보여 줍니다.

```xml
<configuration>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml"/>
  </assemblyBinding>
</configuration>
```

## <a name="see-also"></a>참고자료

- [assemblybinding > 요소  **\<** ](assemblybinding-element-for-configuration.md)
- [.NET Framework에 대 한 구성 파일 스키마](index.md)
