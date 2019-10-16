---
title: <codeBase> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#codeBase
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/runtime/assemblyBinding/dependentAssembly/codeBase
helpviewer_keywords:
- <codeBase> element
- container tags, <codeBase> element
- codeBase element
ms.assetid: d48a3983-2297-43ff-a14d-1f29d3995822
ms.openlocfilehash: 475b7df55ed509157c1da0aeb8f979de238c72b5
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971880"
---
# <a name="codebase-element"></a>\<codeBase > 요소

공용 언어 런타임에서 어셈블리를 찾을 수 있는 위치를 지정 합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<런타임 >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<assemblyBinding >** ](assemblybinding-element-for-runtime.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<dependentAssembly >** ](dependentassembly-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<codeBase>**

## <a name="syntax"></a>구문

```xml
   <codeBase
        version="Assembly version"
        href="URL of assembly"/>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

|특성|설명|
|---------------|-----------------|
|`href`|필수 특성입니다.<br /><br /> 런타임이 지정 된 버전의 어셈블리를 찾을 수 있는 URL을 지정 합니다.|
|`version`|필수 특성입니다.<br /><br /> 코드 베이스가 적용 되는 어셈블리의 버전을 지정 합니다. 어셈블리 버전 번호의 형식은 주 버전. *부 버전. 빌드. 수정 버전*입니다.|

## <a name="version-attribute"></a>version 특성

|값|설명|
|-----------|-----------------|
|버전 번호의 각 부분에 대해 유효한 값은 0에서 65535입니다.|해당 사항 없음.|

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|`buildproviders`|사용자 지정 리소스 파일의 컴파일에 사용되는 빌드 공급자의 컬렉션을 정의합니다. 빌드 공급자 수에는 제한이 없습니다.|
|`compilation`|ASP.NET에서 사용 하는 모든 컴파일 설정을 구성 합니다.|
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|
|`System.web`|ASP.NET 구성 섹션의 루트 요소를 지정합니다.|

## <a name="remarks"></a>설명

런타임이 컴퓨터 구성 파일 또는 게시자 정책 파일의  **\<codeBase >** 설정을 사용 하려면 파일도 어셈블리 버전을 리디렉션해야 합니다. 응용 프로그램 구성 파일에는 어셈블리 버전을 리디렉션하지 않고 codebase 설정이 있을 수 있습니다. 사용할 어셈블리 버전을 확인 한 후 런타임은 버전을 결정 하는 파일의 codebase 설정을 적용 합니다. 코드 베이스가 표시 되지 않는 경우 런타임은 일반적인 방법으로 어셈블리를 검색 합니다.

어셈블리에 강력한 이름이 있는 경우 코드 베이스 설정은 로컬 인트라넷 또는 인터넷의 어디에 나 있을 수 있습니다. 어셈블리가 전용 어셈블리인 경우 codebase 설정은 응용 프로그램 디렉터리에 대 한 상대 경로 여야 합니다.

강력한 이름이 없는 어셈블리의 경우 버전은 무시 되 고 로더에서는 dependentAssembly > 내 \< \<에서 코드 베이스의 첫 번째 모양을 사용 > 합니다. 응용 프로그램 구성 파일에 바인딩을 다른 어셈블리로 리디렉션하는 항목이 있는 경우 어셈블리 버전이 바인딩 요청과 일치 하지 않는 경우에도 리디렉션이 우선적으로 적용 됩니다.

## <a name="example"></a>예제

다음 예제에서는 런타임에서 어셈블리를 찾을 수 있는 위치를 지정 하는 방법을 보여 줍니다.

```xml
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="myAssembly"
                              publicKeyToken="32ab4ba45e0a69a1"
                              culture="neutral" />
            <codeBase version="2.0.0.0"
                      href="http://www.litwareinc.com/myAssembly.dll"/>
         </dependentAssembly>
      </assemblyBinding>
   </runtime>
</configuration>
```

## <a name="see-also"></a>참고자료

- [런타임 설정 스키마](index.md)
- [구성 파일 스키마](../index.md)
- [어셈블리 위치 지정](../../../../standard/assembly/location.md)
- [런타임에서 어셈블리를 찾는 방법](../../../deployment/how-the-runtime-locates-assemblies.md)
