---
title: Visual Basic 언어 버전 선택
description: 컴파일러가 특정 컴파일러 버전을 사용 하 여 구문 유효성 검사를 수행 하도록 구성 합니다.
ms.date: 05/24/2018
ms.openlocfilehash: 4768d59a37d168b2883396f1dea4d0c1a0ff4ca7
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268272"
---
# <a name="select-the-visual-basic-language-version"></a>Visual Basic 언어 버전 선택

Visual Basic 컴파일러 기본값은 해제 된 언어의 최신 주 버전입니다. 언어의 새 포인트 릴리스를 사용하여 모든 프로젝트를 컴파일하도록 선택할 수 있습니다. 최신 버전의 언어를 선택하면 프로젝트에서 최신 언어 기능을 사용할 수 있습니다. 다른 시나리오에서는 이전 버전의 언어를 사용할 때 프로젝트가 깨끗하게 컴파일되는지 확인해야 할 수 있습니다.

이 기능은 개발 환경에서 SDK 및 도구의 새 버전을 설치하는 결정과 프로젝트의 새 언어 기능을 통합하는 결정을 분리합니다. 빌드 컴퓨터에 최신 SDK 및 도구를 설치할 수 있습니다. 각 프로젝트는 해당 빌드에 대해 특정 버전의 언어를 사용하도록 구성될 수 있습니다.

언어 버전을 설정 하는 방법은 세 가지가 있습니다.

- 수동으로 편집 하 여 [ **.vbproj** 파일](#edit-the-vbproj-file)
- 언어 버전을 설정 [하위 디렉터리에 여러 프로젝트에 대 한](#configure-multiple-projects)
- 구성 된 [ `-langversion` 컴파일러 옵션](#set-the-langversion-compiler-option)

## <a name="edit-the-vbproj-file"></a>Vbproj 파일 편집

언어 버전을 설정할 수 있습니다 하 **.vbproj** 파일입니다. 다음 요소를 추가 합니다.

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

값 `latest` Visual Basic 언어의 최신 부 버전을 사용 합니다. 올바른 값은 다음과 같습니다.

|값|의미|
|------------|-------------|
|default|컴파일러는 지원할 수 있는 최신 주 버전의 유효한 언어 구문을 모두 허용합니다.|
|9|컴파일러 또는 Visual Basic 9.0에 포함 된 구문만을 허용 합니다.|
|10|컴파일러 또는 Visual Basic 10.0의 포함 된 구문만을 허용 합니다.|
|11|컴파일러 또는 Visual Basic 11.0에 포함 된 구문만을 허용 합니다.|
|12|컴파일러 또는 Visual Basic 12.0에 포함 된 구문만을 허용 합니다.|
|14|컴파일러 또는 Visual Basic 14.0에 포함 된 구문만을 허용 합니다.|
|15|컴파일러 또는 Visual Basic 15.0에 포함 된 구문만을 허용 합니다.|
|15.3|컴파일러 또는 Visual Basic 15.3에 포함 된 구문만을 허용 합니다.|
|15.5|컴파일러 또는 Visual Basic 15.5에 포함 된 구문만을 허용 합니다.|
|15.8|컴파일러 또는 Visual Basic 15.8에 포함 된 구문만을 허용 합니다.|
|latest|컴파일러가 지원할 수 있는 유효한 언어 구문을 모두 허용합니다.|

특수한 문자열 `default` 및 `latest`는 각각 빌드 컴퓨터에 설치된 최신 주 및 부 언어 버전을 확인합니다.

## <a name="configure-multiple-projects"></a>여러 프로젝트 구성

`<LangVersion>` 요소를 포함하는 **Directory.build.props** 파일을 생성하여 여러 디렉터리를 구성할 수 있습니다. 일반적으로 솔루션 디렉터리에서 이 작업을 수행합니다. 솔루션 디렉터리의 **Directory.build.props** 파일에 다음을 추가합니다.

```xml
<Project>
 <PropertyGroup>
   <LangVersion>15.5</LangVersion>
 </PropertyGroup>
</Project>
```

이제 해당 파일을 포함 하는 디렉터리의 모든 하위 디렉터리에 빌드는 Visual Basic 버전 15.5 구문을 사용 합니다. 자세한 내용은 [빌드 사용자 지정](/visualstudio/msbuild/customize-your-build)에 대한 문서를 참조하세요.

## <a name="set-the-langversion-compiler-option"></a>langversion 컴파일러 옵션 설정

`-langversion` 명령줄 옵션을 사용할 수 있습니다. 자세한 내용은 [-langversion](../reference/command-line-compiler/langversion.md) 컴파일러 옵션에 대한 문서를 참조하세요. 유효한 값 목록을 입력 하 여 보이는 `vbc -langversion:?` 합니다.
