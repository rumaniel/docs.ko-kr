---
title: Visual Studio용 개발자 명령 프롬프트
ms.date: 08/14/2018
helpviewer_keywords:
- command prompt, Windows SDK
- Visual Studio command prompt
- command prompt, Visual Studio
- SDK command prompt
- tools [.NET Framework], setting environment variables
- environment variables, setting for tools
- developer command prompt
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 59af252967a18eca858035fb0a3465d909734ddf
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044736"
---
# <a name="developer-command-prompt-for-visual-studio"></a>Visual Studio용 개발자 명령 프롬프트

Visual Studio에 대한 개발자 명령 프롬프트를 통해 .NET Framework 도구를 더 쉽게 사용할 수 있습니다. 이는 특정 환경 변수를 자동으로 설정하는 명령 프롬프트입니다.

> [!div class="button"]
> [Visual Studio 다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019)

## <a name="search-for-the-command-prompt-on-your-machine"></a>머신에서 명령 프롬프트 검색

설치한 Visual Studio의 버전과 추가 SDK에 따라 여러 개의 명령 프롬프트가 표시될 수 있습니다. 예를 들어 64비트 버전의 Visual Studio는 32비트 및 64비트 명령 프롬프트를 모두 제공합니다. (32비트 및 64비트 버전의 도구는 대부분 동일하지만, 몇 가지 도구는 32비트 및 64비트 환경에 맞게 변경됩니다.) 다음 단계가 작동하지 않는 경우 [머신에서 수동으로 파일 찾기](#manually-locate-the-files-on-your-machine) 또는 [Visual Studio 내에서 명령 프롬프트 실행](#run-the-command-prompt-from-inside-visual-studio)을 시도해 볼 수 있습니다.

### <a name="in-windows-10"></a>Windows 10

1. 작업 표시줄의 검색 상자에 `dev` 또는 `developer command prompt`와 같은 도구 이름을 입력합니다. 그러면 검색 패턴과 일치하는 설치된 앱의 목록이 표시됩니다. 다른 명령 프롬프트를 찾으려면 `prompt`와 같은 다른 검색어를 입력해 봅니다.

2. **Visual Studio용 개발자 명령 프롬프트**(또는 사용할 명령 프롬프트)를 선택합니다.

### <a name="in-windows-81"></a>Windows 8.1에서

1. Windows 로고 키 ![키보드에서 Windows 로고 키](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)를 눌러 **시작** 화면으로 이동합니다. 예를 들어 키보드에서

2. **시작** 화면에서 **Ctrl**+**Tab**을 눌러 **앱** 목록을 열고 `V`를 입력합니다. 그러면 설치된 모든 Visual Studio 명령 프롬프트가 포함된 목록을 가져옵니다.

3. **개발자 명령 프롬프트**(또는 사용할 명령 프롬프트)를 선택합니다.

### <a name="in-windows-8"></a>Windows 8에서

1. Windows 로고 키 ![키보드에서 Windows 로고 키](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)를 눌러 **시작** 화면으로 이동합니다. 예를 들어 키보드에서

2. **시작** 화면에서 Windows 로고 키 ![키보드에서 로고 키](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)를 누릅니다. `+ Z`.

3. 화면 아래쪽에서 **앱 보기** 아이콘을 선택하고 `V` 키를 누릅니다. 그러면 설치된 모든 Visual Studio 명령 프롬프트가 포함된 목록을 가져옵니다.

4. **개발자 명령 프롬프트**(또는 사용할 명령 프롬프트)를 선택합니다.

### <a name="in-windows-7"></a>Windows 7에서

1. **시작**을 선택하고 **모든 프로그램**, **Microsoft Visual Studio**를 차례로 확장합니다.

2. 설치한 Visual Studio 버전에 따라 **Visual Studio Tools**, **Visual Studio 명령 프롬프트** 또는 사용할 명령 프롬프트를 선택합니다.

[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 또는 [이전 버전](https://developer.microsoft.com/windows/downloads/sdk-archive)과 같은 다른 SDK를 설치한 경우 ARM, x86 또는 x64 아키텍처에 대한 추가 명령 프롬프트가 표시될 수 있습니다. 각 도구의 설명서를 확인하여 사용할 명령 프롬프트 버전을 결정합니다.

## <a name="manually-locate-the-files-on-your-machine"></a>머신에서 수동으로 파일 찾기

일반적으로 설치한 명령 프롬프트의 바로 가기는 C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Visual Studio 2017\Visual Studio Tools와 같이 Visual Studio에 대한 **시작 메뉴** 폴더에 배치됩니다. 하지만 어떤 이유로 명령 프롬프트를 검색했는데 예상된 결과가 나타나지 않는 경우, 컴퓨터에서 수동으로 바로 가기를 찾을 수 있습니다. *VsDevCmd.bat*와 같은 명령 프롬프트 파일의 이름 검색을 시도하거나 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools와 같은 도구 폴더로 이동합니다(경로는 Visual Studio 버전, 에디션 및 설치 위치에 따라 바뀜).

## <a name="run-the-command-prompt-from-inside-visual-studio"></a>Visual Studio 내에서 명령 프롬프트 실행

Visual Studio 개발자 명령 프롬프트 또는 다른 명령 프롬프트를 Visual Studio의 **도구** 메뉴에 추가하면 쉽게 액세스할 수 있습니다. 도구를 사용 가능하도록 하려면 외부 도구 목록에 추가합니다. 단계는 다음과 같습니다.

1. Visual Studio를 엽니다.

2. **도구** 메뉴를 선택한 다음, **외부 도구**를 선택합니다.

3. **외부 도구** 대화 상자에서 **추가** 단추를 선택합니다. 새 항목이 표시됩니다.

4. `Command Prompt`와 같은 새 메뉴 항목에 대해 **제목**을 입력합니다.

5. **명령** 필드에서 `%comspec%` 또는 `C:\Windows\System32\cmd.exe` 등의 시작하려는 파일을 지정합니다.

6. **인수** 필드에서 `/k "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools\VsDevCmd.bat"`과 같이 사용할 특정 명령 프롬프트가 있는 위치를 지정합니다(이 명령은 Visual Studio 2017 Enterprise와 함께 설치된 개발자 명령 프롬프트를 시작함). Visual Studio 버전, 에디션 및 설치 위치에 따라 이 값을 변경합니다.

7. **프로젝트 디렉터리**와 같은 **초기 디렉터리** 필드에 대한 값을 선택합니다.

8. **확인** 단추를 선택합니다.

   새 메뉴 항목이 추가되고 **도구** 메뉴에서 명령 프롬프트에 액세스할 수 있습니다.

   ![Visual Studio의 명령 프롬프트 메뉴 항목](./media/command-prompt-vs-menu.png)

## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [외부 도구 관리](/visualstudio/ide/managing-external-tools)
