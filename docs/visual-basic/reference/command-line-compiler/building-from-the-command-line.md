---
title: 명령줄에서 빌드(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers [Visual Basic], invoking from command line
- command-line builds
- compiling source code
- command-line compilers [Visual Basic], Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
ms.openlocfilehash: 719ca45403ea56a655f06dbfea7c0fb7e32b34f7
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046437"
---
# <a name="building-from-the-command-line-visual-basic"></a>명령줄에서 빌드(Visual Basic)

Visual Basic 프로젝트는 하나 이상의 개별 소스 파일로 구성 됩니다. 컴파일 프로세스 중에 이러한 파일은 하나의 패키지로 함께 가져와 응용 프로그램으로 실행할 수 있는 단일 실행 파일입니다.

Visual Basic는 Visual Studio IDE (통합 개발 환경) 내에서 프로그램을 컴파일하는 대신 명령줄 컴파일러를 제공 합니다. 명령줄 컴파일러는 시스템 메모리 나 저장소 공간이 제한 된 컴퓨터를 사용 하거나 쓰는 경우와 같이 IDE에서 전체 기능 집합이 필요 하지 않은 상황을 위해 설계 되었습니다.

Visual Studio IDE 내에서 소스 파일을 컴파일하려면 **빌드** 메뉴에서 **빌드** 명령을 선택 합니다.

> [!TIP]
> Visual Studio IDE를 사용 하 여 프로젝트 파일을 빌드할 때 출력 창에 연결 된 **vbc** 명령 및 해당 스위치에 대 한 정보를 표시할 수 있습니다. 이 정보를 표시 하려면 [옵션 대화 상자, 프로젝트 및 솔루션, 빌드 및 실행](/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)을 연 다음 **MSBuild 프로젝트 빌드 출력의 자세한 정도** 를 **보통** 또는 높은 수준의 자세한 표시로 설정 합니다. 자세한 내용은 [방법: 빌드 로그 파일](/visualstudio/ide/how-to-view-save-and-configure-build-log-files)보기, 저장 및 구성

MSBuild를 사용 하 여 명령 프롬프트에서 프로젝트 (.vbproj) 파일을 컴파일할 수 있습니다. 자세한 내용은 [명령줄 참조](/visualstudio/msbuild/msbuild-command-line-reference) 및 [연습: MSBuild 사용](/visualstudio/msbuild/walkthrough-using-msbuild)을 참조하세요.

## <a name="in-this-section"></a>섹션 내용

[방법: 명령줄 컴파일러 호출](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md) \
MS-DOS 프롬프트에서 또는 특정 하위 디렉터리에서 명령줄 컴파일러를 호출 하는 방법을 설명 합니다.

[샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md) \
사용자 고유의 용도에 맞게 수정할 수 있는 샘플 명령줄 목록을 제공 합니다.

## <a name="related-sections"></a>관련 단원

[Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md) \
사전순 또는 용도별로 구성 된 컴파일러 옵션 목록을 제공 합니다.

[조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md) \
특정 코드 섹션을 컴파일하는 방법을 설명 합니다.

[Visual Studio에서 프로젝트 및 솔루션 빌드 및 정리](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio) \
서로 다른 빌드에 포함할 항목을 구성 하 고, 프로젝트 속성을 선택 하 고, 프로젝트를 올바른 순서로 빌드해야 하는지 설명 합니다.
