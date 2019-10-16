---
title: -appconfig(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /appconfig
helpviewer_keywords:
- /appconfig compiler option [C#]
- -appconfig compiler option [C#]
- appconfig compiler option [C#]
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
ms.openlocfilehash: 7a7e8e61f65704a2e99385a1be320048d950324c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922516"
---
# <a name="-appconfig-c-compiler-options"></a>-appconfig(C# 컴파일러 옵션)
**-appconfig** 컴파일러 옵션을 사용하면 C# 애플리케이션이 어셈블리 바인딩 시간에 어셈블리의 애플리케이션 구성(app.config) 파일 위치를 CLR(공용 언어 런타임)에 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-appconfig:file  
```  
  
## <a name="arguments"></a>인수  
 `file`  
 필수 요소. 어셈블리 바인딩 설정이 포함된 애플리케이션 구성 파일입니다.  
  
## <a name="remarks"></a>설명  
 **-appconfig**의 한 가지 용도는 어셈블리가 특정 참조 어셈블리의 .NET Framework 버전과 .NET Framework for Silverlight 버전을 동시에 둘 다 참조해야 하는 고급 시나리오입니다. 예를 들어 WPF(Windows Presentation Foundation)로 작성된 XAML 디자이너는 디자이너의 사용자 인터페이스를 위한 WPF 데스크톱 및 Silverlight에 포함된 WPF 하위 집합을 둘 다 참조해야 할 수도 있습니다. 같은 디자이너 어셈블리가 두 어셈블리에 모두 액세스해야 합니다. 기본적으로, 어셈블리 바인딩 시 두 어셈블리가 동등한 것으로 간주되기 때문에 서로 다른 참조를 사용할 경우 컴파일러 오류가 발생합니다.  
  
 **-appconfig** 컴파일러 옵션을 사용하면 다음 예제와 같이 `<supportPortability>` 태그를 사용하여 기본 동작을 비활성화하는 app.config 파일의 위치를 지정할 수 있습니다.  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 컴파일러는 이 파일 위치를 CLR의 어셈블리 바인딩 논리에 전달합니다.  
  
> [!NOTE]
> Microsoft Build Engine(MSBuild)을 사용하여 애플리케이션을 빌드하는 경우 .csproj 파일에 속성 태그를 추가하여 **-appconfig** 컴파일러 옵션을 설정할 수 있습니다. 프로젝트에 이미 설정된 app.config 파일을 사용하려면 속성 태그 `<UseAppConfigForCompiler>`를 .csproj 파일에 추가하고 해당 값을 `true`로 설정합니다. 다른 app.config 파일을 지정하려면 속성 태그 `<AppConfigForCompiler>`를 추가하고 해당 값을 파일 위치로 설정합니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 애플리케이션이 두 구현에 모두 있는 .NET Framework 어셈블리의 .NET Framework for Silverlight 구현과 .NET Framework 구현 둘 다에 대한 참조를 사용할 수 있도록 하는 app.config 파일을 보여 줍니다. **-appconfig** 컴파일러 옵션은 이 app.config 파일의 위치를 지정합니다.  
  
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
  
## <a name="see-also"></a>참고 항목

- [\<supportPortability> 요소](../../../framework/configure-apps/file-schema/runtime/supportportability-element.md)
- [사전순 C# 컴파일러 옵션 목록](./listed-alphabetically.md)
