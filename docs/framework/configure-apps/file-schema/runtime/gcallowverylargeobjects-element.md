---
title: <gcAllowVeryLargeObjects> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- gcAllowVeryLargeObjects element
- <gcAllowVeryLargeObjects> element
ms.assetid: 5c7ea24a-39ac-4e5f-83b7-b9f9a1b556ab
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3f638a880aaa21bc41d2575f3609dabae158c1a0
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252579"
---
# <a name="gcallowverylargeobjects-element"></a>\<Gcallowverylargeobjects> > 요소
64비트 플랫폼에서 총 크기가 2GB보다 큰 배열을 사용하도록 설정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<gcAllowVeryLargeObjects>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<gcAllowVeryLargeObjects    
   enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`enabled`|필수 특성입니다.<br /><br /> 총 크기에서 2gb 보다 큰 배열을 64 비트 플랫폼에서 사용할 수 있는지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|전체 크기의 2gb 보다 큰 배열은 사용할 수 없습니다. 이 값이 기본값입니다.|  
|`true`|총 크기가 2gb 보다 큰 배열은 64 비트 플랫폼에서 사용 하도록 설정 됩니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|런타임 초기화 옵션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 응용 프로그램 구성 파일에서이 요소를 사용 하면 크기가 2gb 보다 큰 배열은 가능 하지만 개체 크기나 배열 크기에 대 한 다른 제한은 변경 되지 않습니다.  
  
- 배열의 최대 요소 수는 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>입니다.  
  
- 단일 차원의 최대 인덱스는 바이트 배열 및 단일 바이트 구조의 배열에 대해 2147483591 (0x7FFFFFC7)이 고 다른 형식의 경우 2146435071 (0X7FEFFFFF)입니다.  
  
- 문자열 및 기타 배열 이외의 개체에 대 한 최대 크기는 변경 되지 않습니다.  
  
> [!CAUTION]
> 이 기능을 사용 하도록 설정 하기 전에 모든 배열이 2gb 보다 작은 것으로 가정 하는 안전 하지 않은 코드가 응용 프로그램에 포함 되지 않도록 합니다. 예를 들어 배열을 버퍼로 사용 하는 안전 하지 않은 코드는 배열이 2gb를 초과 하지 않는다는 가정 하에 작성 되는 경우 버퍼 오버런에 취약할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 응용 프로그램에 대해이 기능을 사용 하도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <runtime>  
    <gcAllowVeryLargeObjects enabled="true" />  
  </runtime>  
</configuration>  
```  
  
## <a name="supported-in"></a>다음에서 지원:

.NET Framework 4.5 이상 버전

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
