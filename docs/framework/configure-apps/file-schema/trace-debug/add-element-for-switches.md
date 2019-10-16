---
title: <switches>에 대한 <add> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/switches/add
helpviewer_keywords:
- <add> element for <switches>
- add element for <switches>
ms.assetid: 712ac3a7-7abf-4a9e-8db4-acd241c2f369
ms.openlocfilehash: 2edc890049d62913d693ad61d8d814d012c0f482
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697192"
---
# <a name="add-element-for-switches"></a>\<add-1switches에 대 한 > 요소를 추가 >
추적 스위치를 설정하는 수준을 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\< >** ](system-diagnostics-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<switches >** ](switches-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<> 추가**  
  
## <a name="syntax"></a>구문  
  
```xml  
<add name="switch name"  
     value="value"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**name**|필수 특성입니다.<br /><br /> 스위치의 이름을 지정 합니다. 이 특성의 값은 switch 생성자에 전달 되는 *displayName* 매개 변수에 해당 합니다.|  
|**value**|필수 특성입니다.<br /><br /> 스위치의 수준을 지정 합니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`switches`|추적 스위치 및 추적 스위치가 설정된 수준이 포함되어 있습니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 구성 파일에 배치 하 여 추적 스위치의 수준을 변경할 수 있습니다. 스위치가 <xref:System.Diagnostics.BooleanSwitch> 인 경우 설정 및 해제할 수 있습니다. 스위치가 <xref:System.Diagnostics.TraceSwitch> 인 경우 다른 수준을 할당 하 여 응용 프로그램에서 출력 하는 추적 또는 디버그 메시지의 형식을 지정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **\<add >** 요소를 사용 하 여 @no__t 2 추적 스위치를 @no__t 3 수준으로 설정 하 고 `Data` 부울 추적 스위치를 사용 하도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <switches>  
         <add name="General" value="4" />  
         <add name="Data" value="1" />  
      </switches>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- <xref:System.Diagnostics.Switch>
- <xref:System.Diagnostics.TraceSwitch>
- <xref:System.Diagnostics.BooleanSwitch>
- [추적 및 디버그 설정 스키마](index.md)
