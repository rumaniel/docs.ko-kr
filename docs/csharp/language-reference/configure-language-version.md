---
title: C# 언어 버전 관리 - C# 가이드
description: 프로젝트에 따라 C# 언어 버전이 결정되는 방법과 수동으로 조정할 수 있는 다양한 값에 대해 알아봅니다.
ms.date: 07/10/2019
ms.openlocfilehash: aa4f16d91b38fec7f5d4cd0b2632e62552b64eb7
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698799"
---
# <a name="c-language-versioning"></a>C# 언어 버전 관리

최신 C# 컴파일러는 프로젝트의 대상 프레임워크를 기반으로 기본 언어 버전을 결정합니다. C# 언어는 모든 .NET 구현에서 사용할 수 없는 유형 또는 런타임 구성 요소를 사용하는 기능이 있을 수 있기 때문입니다. 또한 프로젝트가 빌드된 대상에 상관없이 기본적으로 가장 호환성이 높은 언어 버전을 제공합니다.

이 문서의 규칙은 Visual Studio 2019 또는 .NET Core 3.0 SDK와 함께 제공되는 컴파일러에 적용됩니다. Visual Studio 2017 설치 또는 이전 .NET Core SDK 버전의 일부인 C# 컴파일러는 기본적으로 C# 7.0을 대상으로 합니다. 

## <a name="defaults"></a>기본값

컴파일러는 다음 규칙에 따라 기본값을 결정합니다.

|대상 프레임워크|버전|C# 언어 버전 기본값|
|----------------|-------|---------------------------|
|.NET Core|3.x|C# 8.0|
|.NET Core|2.x|C# 7.3|
|.NET Standard|2.1|C# 8.0|
|.NET Standard|2.0|C# 7.3|
|.NET Standard|1.x|C# 7.3|
|.NET Framework|모두|C# 7.3|

## <a name="default-for-previews"></a>미리 보기에 대한 기본값

프로젝트가 해당 미리 보기 언어 버전이 있는 미리 보기 프레임워크를 대상으로 하는 경우 사용되는 언어 버전은 미리 보기 언어 버전입니다. 이렇게 하면 릴리스된 .NET Core 버전을 대상으로 하는 프로젝트에 영향을 주지 않고 모든 환경에서 해당 미리 보기로 작업할 수 있는 최신 기능을 사용할 수 있습니다.

## <a name="override-a-default"></a>기본값 재정의

C# 버전을 명시적으로 지정해야 하는 경우 다음과 같은 여러 가지 방법으로 수행할 수 있습니다.

- [프로젝트 파일](#edit-the-project-file)을 수동으로 편집합니다.
- [하위 디렉터리에 있는 여러 프로젝트의](#configure-multiple-projects) 언어 버전을 설정합니다.
- [`-langversion` 컴파일러 옵션](compiler-options/langversion-compiler-option.md) 구성

### <a name="edit-the-project-file"></a>프로젝트 파일 편집

프로젝트 파일에서 언어 버전을 설정할 수 있습니다. 예를 들어 미리 보기 기능에 명시적으로 액세스하려는 경우 다음과 같은 요소를 추가합니다.

```xml
<PropertyGroup>
   <LangVersion>preview</LangVersion>
</PropertyGroup>
```

값 `preview`는 컴파일러에서 지원하는 사용 가능한 최신 미리 보기 C# 언어를 사용합니다.

### <a name="configure-multiple-projects"></a>여러 프로젝트 구성

`<LangVersion>` 요소를 포함하는 **Directory.Build.props** 파일을 만들어 여러 디렉터리를 구성할 수 있습니다. 일반적으로 솔루션 디렉터리에서 이 작업을 수행합니다. 솔루션 디렉터리의 **Directory.Build.props** 파일에 다음을 추가합니다.

```xml
<Project>
 <PropertyGroup>
   <LangVersion>preview</LangVersion>
 </PropertyGroup>
</Project>
```

이제 해당 파일을 포함하는 디렉터리의 모든 하위 디렉터리에 있는 빌드는 미리 보기 C# 버전을 사용합니다. 자세한 내용은 [빌드 사용자 지정](/visualstudio/msbuild/customize-your-build)에 대한 문서를 참조하세요.

## <a name="c-language-version-reference"></a>C# 언어 버전 참조

모든 표는 현재 C# 언어 버전을 보여줍니다. 컴파일러가 오래된 것이라면 모든 값을 반드시 파악하지 못할 수도 있습니다. .NET Core 3.0을 설치하면 나열된 모든 항목에 액세스할 수 있습니다.

|값|의미|
|------------|-------------|
|미리 보기|컴파일러가 최신 미리 보기 버전의 유효한 언어 구문을 모두 허용합니다.|
|latest|컴파일러가 최신 릴리스 버전(부 버전 포함)의 구문을 허용합니다.|
|latestMajor|컴파일러가 최신 릴리스 주 버전의 구문을 허용합니다.|
|8.0|컴파일러는 C# 8.0 이하에 포함된 구문만 허용합니다.|
|7.3|컴파일러는 C# 7.3 이하에 포함된 구문만 허용합니다.|
|7.2|컴파일러는 C# 7.2 이하에 포함된 구문만 허용합니다.|
|7.1|컴파일러는 C# 7.1 이하에 포함된 구문만 허용합니다.|
|7|컴파일러는 C# 7.0 이하에 포함된 구문만 허용합니다.|
|6|컴파일러는 C# 6.0 이하에 포함된 구문만 허용합니다.|
|5|컴파일러는 C# 5.0 이하에 포함된 구문만 허용합니다.|
|4|컴파일러는 C# 4.0 이하에 포함된 구문만 허용합니다.|
|3|컴파일러는 C# 3.0 이하에 포함된 구문만 허용합니다.|
|ISO-2|컴파일러는 ISO/IEC 23270:2006 C#(2.0)에 포함된 구문만 허용합니다. |
|ISO-1|컴파일러는 ISO/IEC 23270:2003 C#(1.0/1.2)에 포함된 구문만 허용합니다. |
