---
title: <sharedListeners> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#sharedListeners
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sharedListeners
helpviewer_keywords:
- <sharedListeners> element
- listeners
- shared listeners
- trace listeners, <sharedListeners> element
- sharedListeners element
ms.assetid: de200534-19dd-4156-86cf-c50521802c4c
ms.openlocfilehash: b419ecf451b79808e545525c7b8761175f390200
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699298"
---
# <a name="sharedlisteners-element"></a>\<sharedListeners > 요소
소스 또는 추적 요소가 참조할 수 있는 수신기가 포함되어 있습니다.  이러한 수신기는 기본적으로 추적을 수신 하지 않으며 런타임에 이러한 수신기를 검색할 수 없습니다. 공유 수신기로 식별 된 수신기는 이름으로 원본 또는 추적에 추가할 수 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<sharedListeners >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<sharedListeners>   
  <add>...</add>  
</sharedListeners>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<add>](add-element-for-listeners-for-trace.md)|`sharedListeners` 컬렉션에 수신기를 추가합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`Configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|ASP.NET 구성 섹션의 루트 요소를 지정합니다.|  
  
## <a name="remarks"></a>설명  
 수신기를 공유 수신기 컬렉션에 추가 해도 활성 수신기로 설정 되지 않습니다. 해당 추적 요소에 대 한 `Listeners` 컬렉션에 추가 하 여 추적 소스 나 추적에 추가 해야 합니다. .NET Framework의 수신기 클래스는 <xref:System.Diagnostics.TraceListener> 클래스에서 파생 됩니다.  
  
 이 요소는 컴퓨터 구성 파일 (machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<sharedListeners>` 요소를 사용 하 여 <xref:System.Diagnostics.TraceSource> 및 <xref:System.Diagnostics.Trace> 클래스 모두에 대 한 `Listeners` 컬렉션에 수신기 `console`을 추가 하는 방법을 보여 줍니다. 콘솔 추적 수신기는 <xref:System.Diagnostics.TraceSource> 또는 <xref:System.Diagnostics.Trace>을 호출 하 여 추적 정보를 콘솔에 씁니다.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sharedListeners>  
      <add name="console" type="System.Diagnostics.ConsoleTraceListener" >  
        <filter type="System.Diagnostics.EventTypeFilter"  
          initializeData="Warning" />  
      </add>  
    </sharedListeners>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch"  >  
        <listeners>  
          <add name="console" />  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="sourceSwitch" value="Verbose"/>  
    </switches>  
    <trace>  
      <listeners>  
        <add name="console" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.TraceListener>
- [추적 및 디버그 설정 스키마](index.md)
- [추적 수신기](../../../debug-trace-profile/trace-listeners.md)
