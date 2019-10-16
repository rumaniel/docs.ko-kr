---
title: <configuration>에 대한 <assemblyBinding> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/assemblyBinding
helpviewer_keywords:
- assemblyBinding Element
- <assemblyBinding> Element
ms.assetid: 6cc55983-b894-449b-8e26-b258e53939cd
ms.openlocfilehash: e0b83c4b3573ab6819654e72cac1bf3e4a0ba637
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921269"
---
# <a name="assemblybinding-element-for-configuration"></a>\<구성 >에 대 한 \<assemblybinding > 요소

구성 수준에서 어셈블리 바인딩 정책을 지정합니다.

[ **\<configuration>** ](configuration-element.md)   
&nbsp;&nbsp; **\<assemblyBinding>**

## <a name="syntax"></a>구문

```xml
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
  <!-- Configuration files to include. -->
</assemblyBinding>
```

## <a name="attribute"></a>특성

|           | 설명 |
| --------- | ----------- |
| **xmlns** | 필수 특성입니다.<br><br>어셈블리 바인딩에 필요한 XML 네임스페이스를 지정합니다. 문자열 string "urn:schemas-microsoft-com:asm.v1"을 값으로 사용합니다. |

## <a name="parent-element"></a>부모 요소

|     | 설명 |
| --- | ----------- |
| [ **\<configuration>** ](configuration-element.md) | 공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다. |

## <a name="child-element"></a>자식 요소

|     | 설명 |
| --- | ----------- |
| [ **\<linkedConfiguration>** ](linkedconfiguration-element.md) | 포함할 구성 파일을 지정합니다. |

## <a name="remarks"></a>설명

[ **\<LinkedConfiguration >** ](linkedconfiguration-element.md) 요소는 응용 프로그램 구성 파일에서 어셈블리를 복제 하는 대신 잘 알려진 위치에 어셈블리 구성 파일을 포함 하도록 허용 하 여 구성 요소 어셈블리의 관리를 간소화 합니다. 구성 설정.

> [!NOTE]
> LinkedConfiguration > 요소는 Windows side-by-side 매니페스트를 사용 하는 응용 프로그램에 대해 지원 되지 않습니다.  **\<**

## <a name="example"></a>예제

다음 예제에서는 로컬 하드 디스크에 구성 파일을 포함 하는 방법을 보여 줍니다.

```xml
<configuration>
  <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
    <linkedConfiguration href="file://c:\Program Files\Contoso\sharedConfig.xml" />
  </assemblyBinding>
</configuration>
```

## <a name="see-also"></a>참고자료

- [.NET Framework에 대 한 구성 파일 스키마](index.md)
