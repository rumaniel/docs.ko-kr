---
title: <trace> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace
- http://schemas.microsoft.com/.NetConfiguration/v2.0#trace
helpviewer_keywords:
- <trace> element
- listeners
- trace element
- trace listener, <trace> element
ms.assetid: 7931c942-63c1-47c3-a045-9d9de3cacdbf
ms.openlocfilehash: 02fd794eb7b7b7f46f7f7bc4e43036cb4a4758ed
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699177"
---
# <a name="trace-element"></a>\<trace > 요소
추적 메시지를 수집하고 저장하고 라우팅하는 수신기가 포함되어 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<trace >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<trace autoflush="true|false"   
       indentsize="indent value"  
       useGlobalLock="true| false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`autoflush`|선택적 특성입니다.<br /><br /> 모든 쓰기 작업 후 추적 수신기가 출력 버퍼를 자동으로 플러시하지 여부를 지정 합니다.|  
|`indentsize`|선택적 특성입니다.<br /><br /> 들여쓸 공백의 수를 지정 합니다.|  
|`useGlobalLock`|선택적 특성입니다.<br /><br /> 전역 잠금을 사용 해야 하는지 여부를 나타냅니다.|  
  
## <a name="autoflush-attribute"></a>autoflush 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|는 출력 버퍼를 자동으로 플러시하지 않습니다. 이 값이 기본값입니다.|  
|`true`|출력 버퍼를 자동으로 플러시합니다.|  
  
## <a name="usegloballock-attribute"></a>useGlobalLock 특성  
  
|값|설명|  
|-----------|-----------------|  
|`false`|수신기가 스레드로부터 안전 하 게 보호 되는 경우 전역 잠금을 사용 하지 않습니다. 그렇지 않으면 전역 잠금을 사용 합니다.|  
|`true`|수신기가 스레드로부터 안전한 지 여부에 관계 없이 전역 잠금을 사용 합니다. 이 값이 기본값입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<listeners>](listeners-element-for-trace.md)|메시지를 수집, 저장 및 라우팅하는 수신기를 지정 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<trace>` 요소를 사용 하 여 수신기 `MyListener`을 `Listeners` 컬렉션에 추가 하는 방법을 보여 줍니다. `MyListener`은 `MyListener.log` 이라는 파일을 만들고 출력을 파일에 씁니다. @No__t-0 특성은 `false`로 설정 되어 있으며,이로 인해 추적 수신기가 스레드로부터 안전 하 게 보호 되는 경우 전역 잠금이 사용 되지 않습니다. @No__t-0 특성은 <xref:System.Diagnostics.Trace.Flush%2A?displayProperty=nameWithType> 메서드가 호출 되었는지 여부에 관계 없이 추적 수신기가 파일에 쓰도록 하는 `true`로 설정 됩니다. @No__t-0 특성은 0 (영)으로 설정 되며,이는 <xref:System.Diagnostics.Trace.Indent%2A?displayProperty=nameWithType> 메서드를 호출할 때 수신기가 0 공백을 들여씁니다.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace useGlobalLock="false" autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.TraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- [추적 및 디버그 설정 스키마](index.md)
