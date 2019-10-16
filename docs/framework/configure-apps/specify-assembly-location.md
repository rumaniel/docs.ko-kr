---
title: 어셈블리 위치 지정
ms.date: 03/30/2017
helpviewer_keywords:
- configuration [.NET Framework], applications
- application configuration [.NET Framework]
- assemblies [.NET Framework], specifying location
ms.assetid: 1cb92bd7-6bab-44cf-8fd3-36303ce84fea
ms.openlocfilehash: f13b19dcd0aceac969d9639e6230ad33c6cd8d84
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971542"
---
# <a name="specifying-an-assemblys-location"></a>어셈블리 위치 지정
어셈블리 위치를 지정 하는 방법에는 두 가지가 있습니다.  
  
- CodeBase > 요소 사용. [ \<](./file-schema/runtime/codebase-element.md)  
  
- 검색 > 요소 사용. [ \<](./file-schema/runtime/probing-element.md)  
  
 또한 [.NET Framework 구성 도구 (mscorcfg.msc)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/2bc0cxhc(v=vs.100)) 를 사용 하 여 어셈블리 위치를 지정 하거나 어셈블리를 검색할 공용 언어 런타임에 대 한 위치를 지정할 수 있습니다.  
  
## <a name="using-the-codebase-element"></a>\<CodeBase > 요소 사용  
 코드 베이스 > 요소는 어셈블리 버전을 리디렉션하는 컴퓨터 구성 또는 게시자 정책 파일에만 사용할  **\<** 수 있습니다. 런타임에서 사용할 어셈블리 버전을 결정 하면 버전을 결정 하는 파일의 코드 베이스 설정을 적용 합니다. 코드 베이스가 표시 되지 않는 경우 런타임은 일반적인 방법으로 어셈블리를 검색 합니다. 자세한 내용은 [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)을 참조 하세요.  
  
 다음 예제에서는 어셈블리의 위치를 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
       <dependentAssembly>  
         <assemblyIdentity name="myAssembly"  
                           publicKeyToken="32ab4ba45e0a69a1"  
                           culture="en-us" />  
         <codeBase version="2.0.0.0"  
                   href="http://www.litwareinc.com/myAssembly.dll"/>  
       </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **Version** 특성은 강력한 이름의 어셈블리에 필요 하지만 강력한 이름이 아닌 어셈블리의 경우 생략 해야 합니다. **\<코드베이스>** 요소에 필요 합니다 **href** 특성입니다. **\<CodeBase >** 요소에는 버전 범위를 지정할 수 없습니다.  
  
> [!NOTE]
> 강력한 이름의 어셈블리에 대 한 코드 베이스 힌트를 제공 하는 경우 힌트는 응용 프로그램 기본 디렉터리의 하위 디렉터리 또는 응용 프로그램을 가리켜야 합니다.  
  
## <a name="using-the-probing-element"></a>\<검색 > 요소 사용  
 런타임은 코드 베이스가 없는 어셈블리를 검색 하 여 찾습니다. 검색에 대 한 자세한 내용은 [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)을 참조 하세요.  
  
 응용 프로그램 구성 파일에서 검색 [ \<>](./file-schema/runtime/probing-element.md) 요소를 사용 하 여 런타임에서 어셈블리를 찾을 때 검색 해야 하는 하위 디렉터리를 지정할 수 있습니다. 다음 예제에서는 런타임에서 검색할 디렉터리를 지정 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <probing privatePath="bin;bin2\subbin;bin3"/>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
 **PrivatePath** 특성은 런타임에서 어셈블리를 검색 해야 하는 디렉터리를 포함 합니다. 응용 프로그램이 C:\Program 런타임에 files\myapp에 있는 경우 런타임은 C:\Program Files\MyApp\Bin, C:\Program Files\MyApp\Bin2\Subbin 및 C:\Program Files\MyApp\Bin3.에서 코드 베이스를 지정 하지 않는 어셈블리를 검색 합니다. **PrivatePath** 에 지정 된 디렉터리는 응용 프로그램 기본 디렉터리의 하위 디렉터리 여야 합니다.  
  
## <a name="see-also"></a>참고자료

- [.NET 어셈블리](../../standard/assembly/index.md)
- [어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [구성 파일을 사용 하 여 앱 구성](index.md)
