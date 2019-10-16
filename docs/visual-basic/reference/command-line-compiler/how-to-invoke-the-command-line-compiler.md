---
title: '방법: 명령줄 컴파일러 호출 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- command-line arguments
- vbc.exe
- Visual Basic compiler, starting
- command line [Visual Basic], arguments
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
ms.openlocfilehash: a81d5b4f4eae76b0306e2d27475cb8527bda0ff2
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054225"
---
# <a name="how-to-invoke-the-command-line-compiler-visual-basic"></a>방법: 명령줄 컴파일러 호출 (Visual Basic)

명령줄에서 실행 파일의 이름을 입력 하 여 명령줄 컴파일러를 호출할 수 있습니다 .이는 MS-DOS 프롬프트 라고도 합니다. 기본 Windows 명령 프롬프트에서 컴파일하는 경우 실행 파일의 정규화 된 경로를 입력 해야 합니다. 이 기본 동작을 재정의 하려면 Visual Studio 용 개발자 명령 프롬프트를 사용 하거나 PATH 환경 변수를 수정할 수 있습니다. 둘 다 컴파일러 이름을 입력 하기만 하면 모든 디렉터리에서 컴파일할 수 있습니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-invoke-the-compiler-using-the-developer-command-prompt-for-visual-studio"></a>Visual Studio에 대 한 개발자 명령 프롬프트를 사용 하 여 컴파일러를 호출 하려면

1. Microsoft Visual Studio 프로그램 그룹 내에서 Visual Studio Tools 프로그램 폴더를 엽니다.

2. Visual studio가 설치 되어 있는 경우 Visual Studio 용 개발자 명령 프롬프트를 사용 하 여 컴퓨터의 모든 디렉터리에서 컴파일러에 액세스할 수 있습니다.

3. Visual Studio에 대 한 개발자 명령 프롬프트를 호출 합니다.

4. 명령줄에 *sourcefilename* 을 입력 `vbc.exe` 한 다음 enter 키를 누릅니다.

    예를 들어, 라는 `SourceFiles`디렉터리에 소스 코드를 저장 한 경우 명령 프롬프트를 열고를 입력 `cd SourceFiles` 하 여 해당 디렉터리로 변경 합니다. 디렉터리에 라는 `Source.vb`원본 파일이 있는 경우를 입력 `vbc.exe Source.vb`하 여 컴파일할 수 있습니다.

## <a name="to-set-the-path-environment-variable-to-the-compiler-for-the-windows-command-prompt"></a>PATH 환경 변수를 Windows 명령 프롬프트의 컴파일러로 설정 하려면

1. Windows 검색 기능을 사용 하 여 로컬 디스크에서 Vbc.exe를 찾습니다.

    컴파일러가 있는 디렉터리의 정확한 이름은 Windows 디렉터리의 위치와 설치 된 ".NET Framework"의 버전에 따라 달라 집니다. ".NET Framework" 버전이 둘 이상 설치 되어 있는 경우 사용할 버전 (일반적으로 최신 버전)을 결정 해야 합니다.

2. **시작** 메뉴에서 **내 컴퓨터**를 마우스 오른쪽 단추로 클릭 한 다음 바로 가기 메뉴에서 **속성** 을 클릭 합니다.

3. **고급** 탭을 클릭 한 다음 **환경 변수**를 클릭 합니다.

4. **시스템** 변수 창의 목록에서 **경로** 를 선택 하 고 **편집**을 클릭 합니다.

5. 시스템 변수 **편집** 대화 상자에서 **변수 값** 필드에 있는 문자열의 끝 부분으로 삽입 지점을 이동 하 고 세미콜론 (;)을 입력 합니다. 다음에 1 단계에서 찾은 전체 디렉터리 이름을 입력 합니다.

6. **확인** 을 클릭 하 여 편집 내용을 확인 하 고 대화 상자를 닫습니다.

     PATH 환경 변수를 변경한 후에는 컴퓨터의 모든 디렉터리에서 Windows 명령 프롬프트에서 Visual Basic 컴파일러를 실행할 수 있습니다.

## <a name="to-invoke-the-compiler-using-the-windows-command-prompt"></a>Windows 명령 프롬프트를 사용 하 여 컴파일러를 호출 하려면

1. **시작** 메뉴에서 **보조 프로그램** 폴더를 클릭 하 고 **Windows 명령 프롬프트**를 엽니다.

2. 명령줄에 *sourcefilename* 을 입력 `vbc.exe`한 다음 enter 키를 누릅니다.

     예를 들어, 라는 `SourceFiles`디렉터리에 소스 코드를 저장 한 경우 명령 프롬프트를 열고를 입력 `cd SourceFiles` 하 여 해당 디렉터리로 변경 합니다. 디렉터리에 라는 `Source.vb`원본 파일이 있는 경우를 입력 `vbc.exe Source.vb`하 여 컴파일할 수 있습니다.

## <a name="see-also"></a>참고자료

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
