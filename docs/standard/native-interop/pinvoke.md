---
title: P/Invoke(플랫폼 호출)
description: .NET에서 P/Invoke를 통해 네이티브 함수를 호출하는 방법을 알아봅니다.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: cda738a173cbe61cf49f79ceef78c533a5a879d9
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106792"
---
# <a name="platform-invoke-pinvoke"></a>P/Invoke(플랫폼 호출)

P/Invoke는 관리 코드에서 비관리형 라이브러리의 구조체, 콜백 및 함수에 액세스할 수 있는 기술입니다. P/Invoke API는 대부분 `System` 및 `System.Runtime.InteropServices`라는 두 네임스페이스에 포함되어 있습니다. 이러한 두 네임스페이스를 사용하면 기본 구성 요소와 통신하는 방법을 설명하는 도구가 제공됩니다.

관리 코드에서 관리되지 않는 함수를 호출하는 가장 일반적인 예제에서 시작하겠습니다. 명령줄 애플리케이션에서 메시지 상자를 표시하겠습니다.

[!code-csharp[MessageBox](~/samples/snippets/standard/interop/pinvoke/messagebox.cs)]

앞의 예제는 간단하지만 관리 코드에서 관리되지 않는 함수를 호출하는 데 필요한 사항을 보여 줍니다. 예제를 단계별로 살펴보겠습니다.

- 줄 #1에서는 필요한 항목이 모두 포함되어 있는 `System.Runtime.InteropServices` 네임스페이스에 대한 using 문을 보여 줍니다.
- 줄 #7에서는 `DllImport` 특성을 도입합니다. 이 특성은 관리되지 않는 DLL을 로드하도록 런타임에 지정하므로 중요합니다. 전달된 문자열은 대상 함수가 있는 DLL입니다. 또한 문자열을 마샬링하는 데 사용할 [문자 집합](./charset.md)을 지정합니다. 마지막으로 이 함수가 [SetLastError](/windows/desktop/api/errhandlingapi/nf-errhandlingapi-setlasterror)를 호출하고 사용자가 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error?displayProperty=nameWithType>을 통해 검색할 수 있게 런타임이 이 오류 코드를 캡처하도록 지정합니다.
- 줄 #8은 P/Invoke 작업의 핵심입니다. 관리되지 않는 메서드와 **동일한 시그니처**가 있는 관리되는 메서드를 정의합니다. 선언에서 확인할 수 있는 새 키워드 `extern`은 이 메서드가 외부 메서드이며 호출 시 런타임이 `DllImport` 특성에 지정된 DLL에서 찾도록 런타임에 지정합니다.

예제의 나머지 부분에서는 단순히 다른 관리되는 메서드와 마찬가지로 메서드를 호출합니다.

macOS에 대한 샘플도 이와 비슷합니다. macOS에서는 다른 동적 라이브러리 명명 체계를 사용하므로 `DllImport` 특성의 라이브러리 이름을 변경해야 합니다. 다음 샘플에서는 `getpid(2)` 함수를 사용하여 애플리케이션의 프로세스 ID를 가져오고 콘솔에 출력합니다.

[!code-csharp[getpid macOS](~/samples/snippets/standard/interop/pinvoke/getpid-macos.cs)]

Linux에서도 이와 비슷합니다. `getpid(2)`는 표준 [POSIX](https://en.wikipedia.org/wiki/POSIX) 시스템 호출이기 때문에 함수 이름이 같습니다.

[!code-csharp[getpid Linux](~/samples/snippets/standard/interop/pinvoke/getpid-linux.cs)]

## <a name="invoking-managed-code-from-unmanaged-code"></a>비관리 코드에서 관리 코드 호출

런타임에서 양방향 통신을 허용하므로 함수 포인터를 사용하여 네이티브 함수에서 관리 코드로 콜백할 수 있습니다. 관리 코드에서 함수 포인터와 가장 가까운 것은 **대리자**이므로, 대리자를 사용하여 네이티브 코드에서 관리 코드로의 콜백을 허용합니다.

이 기능을 사용하는 방법은 앞에서 설명한 관리 코드에서 네이티브 코드로의 프로세스와 비슷합니다. 지정된 콜백에 대해 시그니처와 일치하는 대리자를 정의하고 외부 메서드에 전달합니다. 다른 모든 작업은 런타임에서 수행합니다.

[!code-csharp[EnumWindows](~/samples/snippets/standard/interop/pinvoke/enumwindows.cs)]

예제를 살펴보기 전에 작업해야 하는 관리되지 않는 함수의 시그니처를 검토하는 것이 좋습니다. 모든 창을 열거하기 위해 호출할 함수에는 다음과 같은 시그니처가 있습니다. `BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`

첫 번째 매개 변수는 콜백입니다. 이 콜백에는 다음과 같은 시그니처가 있습니다. `BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`

이제 예제를 살펴보겠습니다.

- 예제의 줄 #9에서는 비관리 코드의 콜백 시그니처와 일치하는 대리자를 정의합니다. 관리 코드에서 `IntPtr`을 사용하여 LPARAM 및 HWND 형식을 나타내는 방법을 확인합니다.
- 줄 #13 및 #14에서는 user32.dll 라이브러리의 `EnumWindows` 함수를 도입합니다.
- 줄 #17-20에서는 대리자를 구현합니다. 이 간단한 예제에서는 단순히 핸들을 콘솔에 출력하려고 합니다.
- 마지막으로, 줄 #24에서는 외부 메서드를 호출하고 대리자에 전달합니다.

Linux 및 macOS 예제는 다음과 같습니다. 해당 예제에서는 C 라이브러리 `libc`에 있는 `ftw` 함수를 사용합니다. 이 함수는 디렉터리 계층 구조를 트래버스하는 데 사용되며, 함수에 대한 포인터를 해당 매개 변수 중 하나로 사용합니다. 이 함수에는 다음과 같은 시그니처가 있습니다. `int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`.

[!code-csharp[ftw Linux](~/samples/snippets/standard/interop/pinvoke/ftw-linux.cs)]

macOS 예제에서는 동일한 함수를 사용하며, macOS에서 `libc`가 다른 위치에 유지되므로 `DllImport` 특성에 대한 인수만 다릅니다.

[!code-csharp[ftw macOS](~/samples/snippets/standard/interop/pinvoke/ftw-macos.cs)]

앞의 두 예제에서는 매개 변수를 사용하며, 두 경우 모두 매개 변수가 관리형 형식으로 지정됩니다. 런타임에서 “올바른 작업”을 수행하고 다른 쪽의 해당 항목으로 처리합니다. [형식 마샬링](type-marshaling.md) 페이지에서 형식이 네이티브 코드로 마샬링되는 방법을 알아봅니다.

## <a name="more-resources"></a>추가 리소스

- [PInvoke.net wiki](https://www.pinvoke.net/)는 일반적인 Windows API 및 호출 방법에 대한 정보가 포함된 우수한 Wiki입니다.
- [C++/CLI의 P/Invoke](/cpp/dotnet/native-and-dotnet-interoperability)
- [P/Invoke에 대한 Mono 설명서](https://www.mono-project.com/docs/advanced/pinvoke/)
