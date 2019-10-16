---
title: <trace>에 대 한 <listeners>에 대 한 <remove> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/remove
helpviewer_keywords:
- remove element
- <remove> element
ms.assetid: 9a5cd1b5-be1a-485f-8f0c-2890ad3ef3e0
ms.openlocfilehash: 56d1e56514aed98d5f3b9f7363e461af6ac68a8c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697214"
---
# <a name="remove-element-for-listeners-for-trace"></a>\< \< 수신기 >에 대 한 > 요소 제거 \<trace >
**수신기 컬렉션에서** 수신기를 제거 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<trace >** ](trace-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5[ **\<listeners >** ](listeners-element-for-trace.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<remove >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<remove name="listener name" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**name**|필수 특성입니다.<br /><br /> **Listeners** 컬렉션에서 제거할 수신기의 이름입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`listeners`|메시지를 수집, 저장 및 라우팅하는 수신기를 지정 합니다. 수신기는 추적 출력을 적절 한 대상으로 보냅니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|`trace`|ASP.NET 추적 서비스를 구성합니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> @No__t-1 컬렉션에서 <xref:System.Diagnostics.DefaultTraceListener>을 제거 하면 <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType>, <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> 및 @no__t 방법의 동작이 변경 됩니다. @No__t-0 또는 `Fail` 메서드를 호출 하면 일반적으로 메시지 상자가 표시 되지만 <xref:System.Diagnostics.DefaultTraceListener>가 `Listeners` 컬렉션에 없으면 메시지 상자가 표시 되지 않습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 추적 **수신기** 컬렉션에서 기본 추적 수신기를 제거 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <trace autoflush="true" indentsize="0">  
         <listeners>  
            <remove name="Default" />  
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
