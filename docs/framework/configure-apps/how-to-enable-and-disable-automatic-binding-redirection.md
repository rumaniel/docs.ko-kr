---
title: 자동 생성 바인딩 리디렉션 사용 또는 사용 안 함
ms.date: 10/30/2018
helpviewer_keywords:
- side-by-side execution, assembly binding redirection
- assemblies [.NET Framework], binding redirection
ms.assetid: 5fca42f3-bdce-4b81-a704-61e42c89d3ba
ms.openlocfilehash: 178d5070dd7018bbc0fce474cdd0b31ba3d17f77
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "69913042"
---
# <a name="how-to-enable-and-disable-automatic-binding-redirection"></a>방법: 자동 바인딩 리디렉션 사용 설정 및 해제

.NET Framework 4.5.1 이상 버전을 대상으로 하는 Visual Studio에서 앱을 컴파일하면 어셈블리 통합을 재정의 하기 위해 바인딩 리디렉션이 앱 구성 파일에 자동으로 추가 될 수 있습니다. 수동으로 바인딩 리디렉션을 응용 프로그램의 구성 파일에 지정할 지라도 응용 프로그램 또는 해당 구성 요소가 동일 어셈블리의 두 개 이상의 버전을 참조할 경우 바인딩 리디렉션을 추가합니다. 자동 바인딩 리디렉션 기능은 .NET Framework 4.5.1 이상 버전을 대상으로 하는 데스크톱 앱 및 웹 앱에 영향을 주지만 웹 앱에 대해서는 동작이 약간 다릅니다. 이전 버전의 .NET Framework를 대상으로 하는 기존 앱이 있는 경우 자동 바인딩 리디렉션을 사용 하도록 설정 하거나 수동으로 바인딩 리디렉션을 작성 하려는 경우이 기능을 사용 하지 않도록 설정할 수 있습니다.

## <a name="disable-automatic-binding-redirects-in-desktop-apps"></a>데스크톱 앱에서 자동 바인딩 리디렉션 사용 안 함

자동 바인딩 리디렉션은 .NET Framework 4.5.1 이상 버전을 대상으로 하는 Windows 데스크톱 앱에 대해 기본적으로 사용 하도록 설정 됩니다. 바인딩 리디렉션은 앱이 컴파일될 때 출력 구성 (**app.config**) 파일에 추가 되 고, 그렇지 않으면 발생 될 수 있는 어셈블리 통합을 재정의 합니다. 원본 **app.config** 파일은 수정 되지 않습니다. 앱에 대 한 프로젝트 파일을 수정 하거나 Visual Studio의 프로젝트 속성에서 확인란의 선택을 취소 하 여이 기능을 사용 하지 않도록 설정할 수 있습니다.

### <a name="disable-through-project-properties"></a>프로젝트 속성을 통해 사용 안 함

Visual Studio 2017 버전 15.7 이상이 있는 경우 프로젝트의 속성 페이지에서 자동 생성 된 바인딩 리디렉션을 쉽게 사용 하지 않도록 설정할 수 있습니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.

2. **응용 프로그램** 페이지에서 **바인딩 리디렉션 자동 생성** 옵션을 선택 취소 합니다.

3. **Ctrl**+**S** 를 눌러 변경 내용을 저장 합니다.

### <a name="disable-manually-in-the-project-file"></a>프로젝트 파일에서 수동으로 사용 안 함

1. 다음 방법 중 하나를 사용 하 여 프로젝트 파일을 편집용으로 엽니다.

   - Visual Studio의 **솔루션 탐색기**에서 프로젝트를 선택한 다음 바로 가기 메뉴에서 **파일 탐색기에서 폴더 열기** 를 선택 합니다. 파일 탐색기에서 프로젝트 (.csproj 또는 .vbproj) 파일을 찾아서 메모장에서 엽니다.
   - Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 언로드**를 선택 합니다. 언로드된 프로젝트를 다시 마우스 오른쪽 단추로 클릭 한 다음 **편집 [projectname. .csproj]** 을 선택 합니다.

2. 프로젝트 파일에서 다음 속성 항목을 찾습니다.

   ```xml
   <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
   ```

3. `true`를 `false`로 변경합니다.

   ```xml
   <AutoGenerateBindingRedirects>false</AutoGenerateBindingRedirects>
   ```

## <a name="enable-automatic-binding-redirects-manually"></a>수동으로 자동 바인딩 리디렉션 사용

이전 버전의 .NET Framework를 대상으로 하는 기존 앱에서 자동 바인딩 리디렉션을 사용 하도록 설정 하거나, 리디렉션을 추가 하 라는 메시지가 자동으로 표시 되지 않는 경우에 사용할 수 있습니다. 최신 버전의 프레임 워크를 대상으로 하지만 리디렉션을 추가 하 라는 메시지가 자동으로 표시 되지 않는 경우 어셈블리 다시 매핑을 제안 하는 빌드 출력이 표시 될 가능성이 높습니다.

1. 다음 방법 중 하나를 사용 하 여 프로젝트 파일을 편집용으로 엽니다.

   - Visual Studio의 **솔루션 탐색기**에서 프로젝트를 선택한 다음 바로 가기 메뉴에서 **파일 탐색기에서 폴더 열기** 를 선택 합니다. 파일 탐색기에서 프로젝트 (.csproj 또는 .vbproj) 파일을 찾아서 메모장에서 엽니다.
   - Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 언로드**를 선택 합니다. 언로드된 프로젝트를 다시 마우스 오른쪽 단추로 클릭 한 다음 **편집 [projectname. .csproj]** 을 선택 합니다.

2. 다음 요소를 첫 번째 구성 속성 그룹 ( \<PropertyGroup > 태그 아래)에 추가 합니다.

   ```xml
   <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
   ```

   다음은 요소가 삽입 된 예제 프로젝트 파일을 보여 줍니다.

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project ToolsVersion="12.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" />
     <PropertyGroup>
       <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
       <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
       <ProjectGuid>{123334}</ProjectGuid>
       ...
       <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
     </PropertyGroup>
     ...
   </Project>
   ```

3. 응용 프로그램을 컴파일합니다.

## <a name="enable-automatic-binding-redirects-in-web-apps"></a>웹 앱에서 자동 바인딩 리디렉션 사용

자동 바인딩 리디렉션은 웹 응용 프로그램마다 다르게 구현됩니다. 웹 앱에 대해 원본**구성 (web.config**) 파일을 수정 해야 하기 때문에 바인딩 리디렉션은 구성 파일에 자동으로 추가 되지 않습니다. 하지만 Visual Studio는 바인딩 충돌을 경고하고 충돌 해결을 위해 바인딩 리디렉션을 추가할 수 있습니다. 항상 바인딩 리디렉션을 추가 하 라는 메시지가 표시 되므로 웹 앱에 대해이 기능을 명시적으로 사용 하지 않도록 설정할 필요가 없습니다.

**Web.config** 파일에 바인딩 리디렉션을 추가 하려면:

1. Visual Studio에서 응용 프로그램을 컴파일하고 빌드 경고를 확인합니다.

   ![어셈블리 참조 충돌에 대 한 빌드 경고](./media/clr-assemblyrefwarning.png "CLR_AssemblyRefWarning")

2. 어셈블리 바인딩 충돌이 있을 경우 경고가 나타납니다. 경고를 두 번 클릭 하거나 경고를 선택 하 고 enter **키를**누릅니다.

   필요한 바인딩 **리디렉션을 소스 web.config** 파일에 자동으로 추가할 수 있는 대화 상자가 나타납니다.

   ![바인딩 리디렉션 권한 대화 상자](./media/clr-addbindingredirect.png "CLR_AddBindingRedirect")

## <a name="see-also"></a>참고 항목

- [\<bindingRedirect > 요소](./file-schema/runtime/bindingredirect-element.md)
- [어셈블리 버전 리디렉션](redirect-assembly-versions.md)
