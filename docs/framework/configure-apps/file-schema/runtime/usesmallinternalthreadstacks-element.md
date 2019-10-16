---
title: <UseSmallInternalThreadStacks> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- UseSmallInternalThreadStacks element
- <UseSmallInternalThreadStacks> element
ms.assetid: 1e3f6ec0-1cac-4e1c-9c81-17d948ae5874
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 515ea076c5eaead50b41e45e415725d0439914bc
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252214"
---
# <a name="usesmallinternalthreadstacks-element"></a>\<UseSmallInternalThreadStacks > 요소
CLR (공용 언어 런타임)이 해당 스레드에 대 한 기본 스택 크기를 사용 하는 대신 내부적으로 사용 하는 특정 스레드를 만들 때 명시적 스택 크기를 지정 하 여 메모리 사용을 줄이도록 요청 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<UseSmallInternalThreadStacks>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<UseSmallInternalThreadStacks enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|사용|필수 특성입니다.<br /><br /> 내부적으로 사용 하는 특정 스레드를 만들 때 CLR에서 기본 스택 크기 대신 명시적 스택 크기를 사용 하도록 요청할 것인지 여부를 지정 합니다. 명시적 스택 크기는 1mb의 기본 스택 크기 보다 작습니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|true|명시적 스택 크기를 요청 합니다.|  
|False|기본 스택 크기를 사용 합니다. .NET Framework 4의 기본값입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 이 구성 요소는 CLR이 내부 스레드에 사용 하는 명시적 스레드 크기 (요청이 적용 되는 경우)가 기본 크기 보다 작기 때문에 프로세스에서 축소 된 가상 메모리 사용을 요청 하는 데 사용 됩니다.  
  
> [!IMPORTANT]
> 이 구성 요소는 절대 요구 사항이 아닌 CLR에 대 한 요청입니다. .NET Framework 4에서 요청은 x86 아키텍처에만 적용 됩니다. 이 요소는 CLR의 이후 버전에서 완전히 무시 되거나 선택한 내부 스레드에 항상 사용 되는 명시적 스택 크기로 대체 될 수 있습니다.  
  
 이 구성 요소를 지정 하면 CLR에서 요청을 지 원하는 경우 더 작은 가상 메모리 사용에 대 한 안정성을 유지 합니다 .이로 인해 스택 크기가 작을수록 스택 오버플로가 발생할 가능성이 높아집니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 CLR에서 내부적으로 사용 하는 특정 스레드에 대해 명시적 스택 크기를 사용 하도록 요청 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <UseSmallInternalThreadStacks enabled="true" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
