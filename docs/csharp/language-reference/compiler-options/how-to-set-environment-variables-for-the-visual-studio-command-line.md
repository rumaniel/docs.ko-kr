---
title: '방법: Visual Studio 명령줄에 필요한 환경 변수 설정'
ms.date: 09/29/2017
f1_keywords:
- cs.build.commandline
helpviewer_keywords:
- csc.exe, command-line builds
- Visual C#, command-line builds
- command-line compilers, Visual C#
- Vsvars32.bat
- builds [C#], command-line
- compilers, invoking from command line
- Vcvars32.bat file
- command line [C#], building from
- Visual C# compiler, enabling
- compiling source code, from command line
ms.assetid: 7ec09480-5612-4f6a-8d00-ad90ea9bca5d
ms.openlocfilehash: 9b26f6b80488ad4043054cd23f0f351773e8d6d1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602861"
---
# <a name="how-to-set-environment-variables-for-the-visual-studio-command-line"></a>방법: Visual Studio 명령줄에 필요한 환경 변수 설정

VsDevCmd.bat 파일은 명령줄 빌드를 사용하도록 적절한 환경 변수를 설정합니다.

> [!NOTE]
> VsDevCmd.bat 파일은 Visual Studio 2017과 함께 제공되는 새로운 파일입니다. Visual Studio 2015 및 이전 버전에서도 VSVARS32.bat가 같은 용도로 사용됩니다. 이 파일은 \Program Files\Microsoft Visual Studio\\*Version*\Common7\Tools 또는 Program Files (x86)\Microsoft Visual Studio\\*Version*\Common7\Tools에 저장되었습니다.

Visual Studio의 이전 버전이 설치된 컴퓨터에 Visual Studio의 최신 버전을 설치한 경우 동일한 명령 프롬프트 창에서 다른 버전의 VsDevCmd.bat 또는 VSVARS32.BAT를 실행해서는 안 됩니다. 대신 별도 창에서 각 버전에 대해 명령을 실행해야 합니다.

### <a name="to-run-vsdevcmdbat"></a>VsDevCmd.BAT를 실행하려면

1. **시작** 메뉴에서 **VS 2017용 개발자 명령 프롬프트**를 엽니다.  **Visual Studio 2017** 폴더에 있습니다.

2. 설치 경로를 \Program Files\Microsoft Visual Studio\\*Version*\\*Offering*\Common7\Tools or \Program Files (x86)\Microsoft Visual Studio\\*Version*\\*Offering*\Common7\Tools 하위 디렉터리로 변경합니다.  (*Version*은 현재 버전용인 *2017*입니다. *Offering*은 *Enterprise*, *Professional* 또는 *Community* 중 하나입니다.)

3. **VsDevCmd**를 입력하여 VsDevCmd.bat을 실행합니다.

    > [!CAUTION]
    > VsDevCmd.bat는 컴퓨터마다 다를 수 있습니다. 누락되거나 손상된 VsDevCmd.bat 파일을 다른 컴퓨터의 VsDevCmd.bat 파일로 바꾸지 마세요. 대신 설치 프로그램을 다시 실행하여 누락된 파일을 교체하십시오.

### <a name="available-options-for-vsdevcmdbat"></a>VsDevCmd.BAT에 사용 가능한 옵션

VsDevCmd.BAT에 사용 가능한 옵션을 보려면 `-help` 옵션을 사용하여 명령을 실행하세요.

```console
VsDevCmd.bat -help
```

## <a name="see-also"></a>참고 항목

- [csc.exe를 사용한 명령줄 빌드](./command-line-building-with-csc-exe.md)
