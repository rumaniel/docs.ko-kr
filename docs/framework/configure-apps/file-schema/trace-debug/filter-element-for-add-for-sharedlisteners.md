---
title: <sharedListeners>에 대 한 <add>에 대 한 <filter> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners/add/filter
helpviewer_keywords:
- filter element for <add> for <sharedListeners>
- initializeData attribute
- <filter> element for <add> for <sharedListeners>
- filters, trace listeners
- trace listeners, filters
ms.assetid: 7d4e7faa-2e4e-4379-ac76-f6cd7f2f8fac
ms.openlocfilehash: 4e92f80e9f6069b5fa70501e13a55d5a6fe95e7a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697318"
---
# <a name="filter-element-for-add-for-sharedlisteners"></a>@no__t에 대 한 \<filter > @no__t 요소 >-2sharedListeners에 대 한 > 추가
`sharedListeners` 컬렉션에 있는 수신기에 필터를 추가합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<sharedListeners >** ](sharedlisteners-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<add >** ](add-element-for-sharedlisteners.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<filter >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<filter type="System.Diagnostics.EventTypeFilter"   
  initializeData="Warning" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**type**|필수 특성입니다.<br /><br /> 필터의 유형을 지정 합니다. 형식의 전체 이름 (<xref:System.Type.FullName%2A?displayProperty=nameWithType> 속성 형식)만 사용할 수도 있고, 어셈블리 정보 (<xref:System.Type.AssemblyQualifiedName%2A?displayProperty=nameWithType> 속성의 형식)를 포함 하 여 정규화 된 형식 이름을 사용할 수도 있습니다. 정규화 된 형식 이름을 만드는 방법에 대 한 자세한 내용은 정규화 된 [형식 이름 지정](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)을 참조 하세요.|  
|**initializeData**|선택적 특성입니다.<br /><br /> 지정 된 클래스의 생성자에 전달 된 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|`sharedListeners`|모든 소스 또는 추적 요소가 참조할 수 있는 수신기의 컬렉션입니다.|  
|`add`|**Sharedlisteners** 컬렉션에 수신기를 추가 합니다.|  
  
## <a name="remarks"></a>설명  
 수신기가 `<sharedListeners>` 요소의 `<add>` 요소에 정의 된 경우 해당 수신기의 필터는 `<add>` 요소의 자식인 `<filter>` 요소에 정의 되어야 합니다.  
  
 이 요소는 컴퓨터 구성 파일 (machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<filter>` 요소를 사용 하 여 `sharedListeners` 컬렉션의 추적 @no__t 수신기에 필터를 추가 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="myTraceSource" >  
        <listeners>  
          <add name="console" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="console"   
        type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"   
          initializeData="Error" />  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.TraceFilter>
- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.TraceSource>
- [추적 및 디버그 설정 스키마](index.md)
