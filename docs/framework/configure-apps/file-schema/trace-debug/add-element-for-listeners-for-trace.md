---
title: <trace>에 대 한 <listeners>에 대 한 <add> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/add
helpviewer_keywords:
- initializeData attribute
- <add> element for <listeners>
- add element for <listeners>
ms.assetid: 81e804a3-ef11-4d39-bbde-bfa012c179e2
ms.openlocfilehash: d89a77107e7aff65b007a69c23af34771146570c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697329"
---
# <a name="add-element-for-listeners-for-trace"></a>\< @no__t-> 1listeners에 대 한 > 요소 추가 \<trace >
**수신기 컬렉션에** 수신기를 추가 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<trace >** ](trace-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<listeners >** ](listeners-element-for-trace.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> 추가**  
  
## <a name="syntax"></a>구문  
  
```xml  
<add name="name"   
     type="trace listener class name, Version, Culture, PublicKeyToken"  
     initializeData="data"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**type**|필수 특성입니다.<br /><br /> 수신기의 유형을 지정 합니다. 정규화 된 [형식 이름 지정](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)에 지정 된 요구 사항을 충족 하는 문자열을 사용 해야 합니다.|  
|**initializeData**|선택적 특성입니다.<br /><br /> 지정 된 클래스의 생성자에 전달 된 문자열입니다.|  
|**name**|선택적 특성입니다.<br /><br /> 수신기의 이름을 지정 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<filter>](filter-element-for-add-for-listeners-for-trace.md)|추적에 대 한 `Listeners` 컬렉션의 수신기에 필터를 추가 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`listeners`|메시지를 수집, 저장 및 라우팅하는 수신기를 지정 합니다. 수신기는 추적 출력을 적절 한 대상으로 보냅니다.|  
|`system.diagnostics`|ASP.NET 구성 섹션의 루트 요소를 지정합니다.|  
|`trace`|추적 메시지를 수집하고 저장하고 라우팅하는 수신기가 포함되어 있습니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 및 <xref:System.Diagnostics.Trace> 클래스는 동일한 **Listeners** 컬렉션을 공유 합니다. 이러한 클래스 중 하나에서 컬렉션에 수신기 개체를 추가 하는 경우 다른 클래스는 동일한 수신기를 사용 합니다. 수신기 클래스는 <xref:System.Diagnostics.TraceListener>에서 파생 됩니다.  
  
 추적 수신기의 `name` 특성을 지정 하지 않는 경우 추적 수신기의 @no__t 1은 빈 문자열 ("")로 설정 됩니다. 응용 프로그램에 수신기가 하나만 있는 경우 이름을 지정 하지 않고 수신기를 추가 하 고 이름에 대해 빈 문자열을 지정 하 여 제거할 수 있습니다. 그러나 응용 프로그램에 둘 이상의 수신기가 있는 경우 각 추적 수신기에 고유한 이름을 지정 하 여 <xref:System.Diagnostics.Debug.Listeners%2A> 및 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션 내에서 개별 추적 수신기를 식별 하 고 관리할 수 있습니다.  
  
> [!NOTE]
> 동일한 형식의 추적 수신기를 둘 이상 추가 하 고 이름이 동일한 경우 해당 형식 및 이름에 대 한 추적 수신기는 `Listeners` 컬렉션에 추가 됩니다. 그러나 `Listeners` 컬렉션에 여러 개의 동일한 수신기를 프로그래밍 방식으로 추가할 수 있습니다.  
  
 **Initializedata** 특성의 값은 사용자가 만드는 수신기의 유형에 따라 달라 집니다. 모든 추적 수신기에서 **Initializedata**를 지정 해야 하는 것은 아닙니다.  
  
> [!NOTE]
> @No__t-0 특성을 사용 하는 경우 컴파일러 경고 "' initializeData ' 특성이 선언 되지 않았습니다." 라는 메시지가 표시 될 수 있습니다. 이 경고는 `initializeData` 특성을 인식 하지 않는 추상 기본 클래스 <xref:System.Diagnostics.TraceListener>에 대해 구성 설정의 유효성을 검사 하기 때문에 발생 합니다. 일반적으로 매개 변수를 사용 하는 생성자가 있는 추적 수신기 구현에 대해서는이 경고를 무시할 수 있습니다.  
  
 다음 표에서는 .NET Framework에 포함 된 추적 수신기를 보여 주고 해당 **Initializedata** 특성의 값을 설명 합니다.  
  
|추적 수신기 클래스|initializeData 특성 값|  
|--------------------------|------------------------------------|  
|<xref:System.Diagnostics.ConsoleTraceListener?displayProperty=nameWithType>|@No__t-1 생성자의 @no__t 0 값입니다.  @No__t-0 특성을 "`true`"로 설정 하 여 추적 및 디버그 출력을 <xref:System.Console.Error%2A?displayProperty=nameWithType>에 기록 합니다. @no__t에 쓸 "`false`"입니다.|  
|<xref:System.Diagnostics.DelimitedListTraceListener?displayProperty=nameWithType>|파일의 이름을 합니다 <xref:System.Diagnostics.DelimitedListTraceListener> 를 씁니다.|  
|<xref:System.Diagnostics.EventLogTraceListener?displayProperty=nameWithType>|기존 이벤트 로그 원본의 이름입니다.|  
|<xref:System.Diagnostics.EventSchemaTraceListener?displayProperty=nameWithType>|@No__t-0에서 쓸 파일의 이름입니다.|  
|<xref:System.Diagnostics.TextWriterTraceListener?displayProperty=nameWithType>|@No__t-0에서 쓸 파일의 이름입니다.|  
|<xref:System.Diagnostics.XmlWriterTraceListener?displayProperty=nameWithType>|@No__t-0에서 쓸 파일의 이름입니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 **\<add >** 요소를 사용 하 여 **수신기 컬렉션에** `MyListener` 및 `MyEventListener` 수신기를 추가 하는 방법을 보여 줍니다. `MyListener` `MyListener.log` 이라는 파일을 만들고 출력을 파일에 씁니다. `MyEventListener`은 이벤트 로그에 항목을 만듭니다.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
            <add name="MyEventListener"  
                 type="System.Diagnostics.EventLogTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"                 initializeData="MyConfigEventLog"/>  
            <add name="configConsoleListener"  
                 type="System.Diagnostics.ConsoleTraceListener, system, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
         </listeners>  
      </trace>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.EventLogTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.TextWriterTraceListener>
- [추적 및 디버그 설정 스키마](index.md)
- [추적 수신기](../../../debug-trace-profile/trace-listeners.md)
