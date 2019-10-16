---
title: -subsystemversion (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- /subsystemversion compiler option [Visual Basic]
- -subsystemversion compiler option [Visual Basic]
- subsystemversion compiler option [Visual Basic]
ms.assetid: 08be22b2-f447-4cd3-8203-120b1b920b54
ms.openlocfilehash: e42501a002d808f31dc3d599dc030e96c573a22f
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66380315"
---
# <a name="-subsystemversion-visual-basic"></a>-subsystemversion (Visual Basic)

생성된 실행 파일을 실행할 수 있는 하위 시스템의 최소 버전을 지정하여 실행 파일을 실행할 수 있는 Windows 버전을 결정합니다. 가장 일반적으로, 이 옵션은 실행 파일이 이전 버전의 Windows에서 사용할 수 없는 특정 보안 기능을 활용할 수 있도록 합니다.

> [!NOTE]
> 하위 시스템 자체를 지정하려면 [-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 컴파일러 옵션을 사용합니다.

## <a name="syntax"></a>구문

```vb
-subsystemversion:major.minor
```

## <a name="parameters"></a>매개 변수

`major.minor`

주 버전과 부 버전의 점 표기법으로 표현된 필수 최소 버전의 하위 시스템입니다. 예를 들어 이 항목의 뒷부분에 나오는 표의 설명에 따라 이 옵션의 값을 6.01로 설정하는 경우 Windows 7 이전 운영 체제에서는 애플리케이션을 실행할 수 없도록 지정할 수 있습니다. `major` 및 `minor`의 값을 정수로 지정해야 합니다.

`minor` 버전에서 선행 0은 버전을 변경하지 않지만 후행 0은 버전을 변경합니다. 예를 들어 6.1과 6.01은 동일한 버전을 가리키지만 6.10은 다른 버전을 가리킵니다. 혼동을 피하기 위해 부 버전을 두 자리로 표현하는 것이 좋습니다.

## <a name="remarks"></a>설명

다음 표에는 Windows의 일반적인 하위 시스템 버전이 나와 있습니다.

|Windows 버전|하위 시스템 버전|
|---------------------|-----------------------|
|Windows 2000|5.00|
|Windows XP|5.01|
|Windows Server 2003|5.02|
|Windows Vista|6.00|
|Windows 7|6.01|
|Windows Server 2008|6.01|
|[!INCLUDE[win8](~/includes/win8-md.md)]|6.02|

## <a name="default-values"></a>기본값

**-subsystemversion** 컴파일러 옵션의 기본값은 다음 목록의 조건에 따라 달라집니다.

- 다음 목록의 컴파일러 옵션이 설정된 경우 기본값은 6.02입니다.

  - [/target:appcontainerexe](../../../visual-basic/reference/command-line-compiler/target.md)

  - [/target:winmdobj](../../../visual-basic/reference/command-line-compiler/target.md)

  - [-platform:arm](../../../visual-basic/reference/command-line-compiler/platform.md)

- MSBuild를 사용 하는.NET Framework 4.5를 대상으로 하는,이 목록의 앞부분에서 지정 된 컴파일러 옵션 중 하나를 설정 하지 않은 경우 기본값은 6.00입니다.

- 앞의 조건이 하나도 true가 아닌 경우 기본값은 4.00입니다.

## <a name="setting-this-option"></a>이 옵션 설정

설정 하는 **-subsystemversion** 컴파일러 옵션 Visual Studio에서.vbproj 파일을 열 및 값을 지정 해야 합니다는 `SubsystemVersion` MSBuild XML에서 속성입니다. Visual Studio IDE에서는 이 옵션을 설정할 수 없습니다. 자세한 내용은 이 항목의 앞부분에 나오는 "기본값"이나 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties)을 참조하세요.

## <a name="see-also"></a>참고자료

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)

- [MSBuild 속성](/visualstudio/msbuild/msbuild-properties)
