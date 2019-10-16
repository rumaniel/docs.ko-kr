---
title: 다중 파일 어셈블리
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- command-line compilers
- assembly manifest, multifile assemblies
- code modules
- multifile assemblies
ms.assetid: 13509e73-db77-4645-8165-aad8dfaedff6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b4c288a54194e89eb90b6ac512cf45184376e952
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971871"
---
# <a name="multifile-assemblies"></a>다중 파일 어셈블리

명령줄 컴파일러 또는 Visual Studio를 Visual C++와 함께 사용하여 .NET Framework를 대상으로 하는 다중 파일 어셈블리를 만들 수 있습니다. 어셈블리의 한 파일에 어셈블리 매니페스트가 포함되어 있어야 합니다. 애플리케이션을 시작하는 어셈블리에는 `Main` 또는 `WinMain` 메서드와 같은 진입점도 포함되어 있어야 합니다.

예를 들어 두 개의 코드 모듈 *Client.cs* 및 *Stringer.cs*를 포함하는 애플리케이션이 있다고 가정해 보세요. *Stringer.cs*는 *Client.cs*의 코드에서 참조하는 `myStringer` 네임스페이스를 만듭니다. *Client.cs*에는 애플리케이션의 진입점인 `Main` 메서드가 포함되어 있습니다. 이 예제에서는 두 개의 코드 모듈을 컴파일한 다음 애플리케이션을 시작하는 어셈블리 매니페스트가 포함된 세 번째 파일을 만듭니다. 어셈블리 매니페스트는 *Client* 및 *Stringer*모듈을 모두 참조합니다.

> [!NOTE]
> 다중 파일 어셈블리는 어셈블리에 여러 개의 코드 모듈이 있는 경우에도 진입점을 하나만 포함할 수 있습니다.

다중 파일 어셈블리를 만드는 것이 좋은 몇 가지 이유는 다음과 같습니다.

- 서로 다른 언어로 작성된 모듈을 결합하기 위해. 다중 파일 어셈블리를 만드는 가장 일반적인 이유입니다.

- 필요할 때만 다운로드되는 모듈에 거의 사용하지 않는 형식을 삽입하여 애플리케이션 다운로드를 최적화하기 위해.

    > [!NOTE]
    > Microsoft Internet Explorer와 함께 `<object>` 태그를 사용하여 다운로드되는 애플리케이션을 만드는 경우 다중 파일 어셈블리를 만드는 것이 중요합니다. 이 시나리오에서는 코드 모듈과 별도로 어셈블리 매니페스트만 포함된 파일을 만듭니다. Internet Explorer는 어셈블리 매니페스트를 먼저 다운로드한 다음 필요한 추가 모듈이나 어셈블리를 다운로드할 작업자 스레드를 만듭니다. 어셈블리 매니페스트가 포함된 파일을 다운로드하는 동안 Internet Explorer는 사용자 입력에 응답하지 않습니다. 어셈블리 매니페스트가 포함된 파일이 작을수록 Internet Explorer가 응답하지 않는 시간이 줄어듭니다.

- 여러 개발자가 작성한 코드 모듈을 결합하기 위해. 각 개발자가 각 코드 모듈을 어셈블리로 컴파일할 수 있지만 이 경우 모든 모듈을 다중 파일 어셈블리에 포함할 경우 노출되지 않는 일부 형식이 강제로 공개될 수 있습니다.

어셈블리를 만든 후 어셈블리 매니페스트가 포함된 파일(따라서 어셈블리)에 서명하거나 파일 및 어셈블리에 강력한 이름을 지정하고 전역 어셈블리 캐시에 넣을 수 있습니다.

## <a name="see-also"></a>참고 항목

- [방법: 다중 파일 어셈블리 빌드](build-multifile-assembly.md)
- [어셈블리를 사용한 프로그램](../../standard/assembly/program.md)
