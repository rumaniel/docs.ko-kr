---
title: <supportPortability> 요소
ms.date: 03/30/2017
helpviewer_keywords:
- supportPortability element
- <supportPortability> element
ms.assetid: 6453ef66-19b4-41f3-b712-52d0c2abc9ca
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 011793006f2aff32486fbe4537b46517e0a2b888
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252300"
---
# <a name="supportportability-element"></a>\<Supportportability> > 요소
애플리케이션 이식성을 위해 어셈블리를 동일하게 간주하는 기본 동작을 사용하지 않도록 설정함으로써, 애플리케이션이 .NET Framework의 서로 다른 두 구현에서 같은 어셈블리를 참조할 수 있도록 지정합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<assemblyBinding >** ](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<Supportportability> >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<supportPortability PKT="public_key_token" enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|PKT|필수 특성입니다.<br /><br /> 영향을 받는 어셈블리의 공개 키 토큰을 문자열로 지정 합니다.|  
|사용|선택적 특성입니다.<br /><br /> 지정 된 .NET Framework 어셈블리의 구현 간 이식성에 대 한 지원을 사용 하도록 설정할지 여부를 지정 합니다.|  
  
## <a name="enabled-attribute"></a>enabled 특성  
  
|값|설명|  
|-----------|-----------------|  
|true|지정 된 .NET Framework 어셈블리의 구현 간 이식성에 대 한 지원을 사용 하도록 설정 합니다. 이 값이 기본값입니다.|  
|False|지정 된 .NET Framework 어셈블리의 구현 간 이식성에 대 한 지원을 사용 하지 않도록 설정 합니다. 이렇게 하면 응용 프로그램에서 지정 된 어셈블리의 여러 구현에 대 한 참조를 사용할 수 있습니다.|  
  
### <a name="child-elements"></a>자식 요소  

없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`runtime`|어셈블리 바인딩 및 가비지 컬렉션에 대한 정보를 포함합니다.|  
|`assemblyBinding`|어셈블리 버전 리디렉션 및 어셈블리 위치에 대한 정보를 포함합니다.|  
  
## <a name="remarks"></a>설명  

.NET Framework 4부터 .NET Framework의 두 구현 중 하나를 사용할 수 있는 응용 프로그램에 대 한 지원이 자동으로 제공 됩니다 (예: .NET Framework 구현 또는 Silverlight 구현을 위한 .NET Framework). 특정 .NET Framework 어셈블리의 두 구현은 어셈블리 바인더에 의해 동등 하 게 표시 됩니다. 일부 시나리오에서는이 응용 프로그램 이식성 기능으로 인해 문제가 발생 합니다. 이러한 시나리오 `<supportPortability>` 에서는 요소를 사용 하 여 기능을 사용 하지 않도록 설정할 수 있습니다.  
  
이러한 시나리오 중 하나는 .NET Framework 구현과 특정 참조 어셈블리의 Silverlight 구현에 대 한 .NET Framework를 모두 참조 해야 하는 어셈블리입니다. 예를 들어 Windows Presentation Foundation (WPF)로 작성 된 XAML 디자이너는 WPF 데스크톱 구현, 디자이너의 사용자 인터페이스 및 Silverlight 구현에 포함 된 WPF의 하위 집합을 모두 참조 해야 할 수 있습니다. 기본적으로, 어셈블리 바인딩 시 두 어셈블리가 동등한 것으로 간주되기 때문에 서로 다른 참조를 사용할 경우 컴파일러 오류가 발생합니다. 이 요소는 기본 동작을 사용 하지 않도록 설정 하 고 컴파일이 성공 하도록 허용 합니다.  
  
> [!IMPORTANT]
> 컴파일러가 정보를 공용 언어 런타임의 어셈블리 바인딩 논리에 전달 하도록 하려면 `/appconfig` 컴파일러 옵션을 사용 하 여이 요소를 포함 하는 app.config 파일의 위치를 지정 해야 합니다.  
  
## <a name="example"></a>예제  

다음 예제에서는 응용 프로그램에 두 구현 모두에 존재 하는 모든 .NET Framework 어셈블리의 Silverlight 구현에 대 한 .NET Framework 구현 및 .NET Framework에 대 한 참조를 사용할 수 있도록 합니다. 이 app.config 파일의 위치를 지정 하려면 컴파일러옵션을사용해야합니다.`/appconfig`  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding>  
         <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
         <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- [/appconfig (C# 컴파일러 옵션)](../../../../csharp/language-reference/compiler-options/appconfig-compiler-option.md)
- [.NET Framework 어셈블리 통합 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/db7849ey(v=vs.100))
