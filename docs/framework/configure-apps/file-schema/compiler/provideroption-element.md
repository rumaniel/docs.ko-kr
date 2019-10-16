---
title: <providerOption> 요소
ms.date: 03/30/2017
f1_keywords:
- provideroption
helpviewer_keywords:
- <provideroption> element
- providerOptions
- provideroption element
ms.assetid: 014f2e0b-c0b5-4fc4-92d3-73f02978b2a1
ms.openlocfilehash: 8d90364e34aa15bbd38e82ec70ec44616d7360f8
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70167663"
---
# <a name="provideroption-element"></a>\<providerOption > 요소
언어 공급자에 대 한 컴파일러 버전 특성을 지정 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp;[ **\<시스템 codedom >** ](system-codedom-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<컴파일러 >** ](compilers-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<컴파일러 >** ](compiler-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<providerOption >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<providerOption  
  name="option-name"  
  value="option-value"  
/>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`name`|필수 특성입니다.<br /><br /> 옵션의 이름을 지정 합니다. 예를 들면 "찾고 compilerversion"입니다.|  
|`value`|필수 특성입니다.<br /><br /> 옵션의 값을 지정 합니다. 예를 들면 "v 3.5"입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<configuration> 요소](../configuration-element.md)|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|[\<system.object > 요소](system-codedom-element.md)|사용 가능한 언어 공급자에 대한 컴파일러 구성 설정을 지정합니다.|  
|[\<컴파일러 > 요소](compilers-element.md)|컴파일러 구성 요소에 대 한 컨테이너입니다. 0 개 이상의 `<compiler>` 요소를 포함 합니다.|  
|[\<compiler> 요소](compiler-element.md)|언어 공급자에 대한 컴파일러 구성 특성을 지정합니다.|  
  
## <a name="remarks"></a>설명  
 .NET Framework 버전 3.5에서 CodeDOM (코드 문서 개체 모델) 코드 공급자는 요소를 `<providerOption>` 사용 하 여 공급자별 옵션을 지원할 수 있습니다.  
  
 .NET Framework 3.5에는 업데이트 된 .NET Framework 2.0 어셈블리가 포함 되어 있으며 새 버전 3.5 어셈블리에는 새 형식이 포함 되어 있습니다. Microsoft C# 및 Visual Basic 코드 공급자는 .NET Framework 2.0 어셈블리에 포함 되어 있지만 버전 3.5 컴파일러를 지원 하도록 업데이트 되었습니다. 기본적으로 업데이트 된 코드 공급자는 버전 2.0 컴파일러에 대 한 코드를 생성 합니다. `<providerOption>` 요소를 사용 하 여 대상 컴파일러 버전을 3.5으로 변경할 수 있습니다. 이렇게 하려면 특성에 대해 `name` "찾고 compilerversion"를 지정 하 고 특성에는 `value` "v 3.5"를 지정 합니다. 버전 번호 앞에는 소문자 "v"가와 야 합니다.  
  
 .NET Framework 2.0 machine.config 또는 루트 web.config 파일에 `<providerOption>` 요소를 추가 하 여 버전 사양을 전역적으로 지정할 수 있습니다. Machine.config 파일에서 기본 컴파일러 버전을 3.5로 업데이트 하는 경우 응용 프로그램 구성 파일의 `<providerOption>` 요소를 사용 하 여 응용 프로그램 별로 다시 2.0로 변경할 수 있습니다.  
  
 CodeDOM 코드 공급자 구현자는 형식의 `providerOptions` <xref:System.Collections.Generic.IDictionary%602>매개 변수를 사용 하는 생성자를 제공 하 여 사용자 지정 옵션을 처리할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 C# 코드 공급자의 버전 3.5을 사용 하도록 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler  
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,   
          Version=2.0.3600.0, Culture=neutral,   
          PublicKeyToken=b77a5c561934e089"  
        compilerOptions="/optimize"  
        warningLevel="1" >  
          <providerOption  
            name="CompilerVersion"  
            value="v3.5" />  
      </compiler>  
    </compilers>  
  </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [구성 파일 스키마](../index.md)
- [\<컴파일러 > 요소](compilers-element.md)
- [정규화된 형식 이름 지정](../../../reflection-and-codedom/specifying-fully-qualified-type-names.md)
- [컴파일에 대 한 컴파일러의 컴파일러 요소 (ASP.NET Settings 스키마)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/a15ebt6c(v=vs.100))
