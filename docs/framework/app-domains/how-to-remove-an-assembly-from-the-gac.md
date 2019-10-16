---
title: '방법: 글로벌 어셈블리 캐시에서 어셈블리 제거'
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- global assembly cache, removing assemblies
- strong-named assemblies, global assembly cache
- removing assemblies from global assembly cache
- deleting assemblies in global assembly cache
- Global Assembly Cache tool
- GAC (global assembly cache), removing assemblies
ms.assetid: acdcc588-b458-436d-876c-726de68244c1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7a085ff6955f706bcd90f895c42e6405a28d408a
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834047"
---
# <a name="how-to-remove-an-assembly-from-the-global-assembly-cache"></a>방법: 글로벌 어셈블리 캐시에서 어셈블리 제거

GAC(전역 어셈블리 캐시)에서 어셈블리를 제거하는 다음 두 가지 방법이 있습니다.

- [전역 어셈블리 캐시 도구(Gacutil.exe)](../tools/gacutil-exe-gac-tool.md) 사용. 개발 및 테스트 중 GAC에 배치한 어셈블리를 제거하려면 이 옵션을 사용할 수 있습니다.

- [Windows Installer](/windows/desktop/Msi/windows-installer-portal) 사용. 설치 패키지를 테스트할 때 및 프로덕션 시스템에 대해 어셈블리를 제거하려면 이 옵션을 사용해야 합니다.

## <a name="removing-an-assembly-with-gacutilexe"></a>Gacutil.exe를 사용하여 어셈블리 제거

명령 프롬프트에 다음 명령을 입력합니다.

**gacutil –u** \<*assembly name*>

이 명령에서 *assembly name*은 전역 어셈블리 캐시에서 제거할 어셈블리의 이름입니다.

> [!WARNING]
> 어셈블리가 일부 애플리케이션에서 여전히 필요할 수 있으므로 프로덕션 시스템에서 어셈블리를 제거하려는 경우 Gacutil.exe를 사용하면 안 됩니다. 대신, GAC에 설치하는 각 어셈블리에 대한 참조 횟수를 유지 관리하는 Windows Installer를 사용해야 합니다.

다음 예제에서는 전역 어셈블리 캐시에서 `hello.dll` 이라는 어셈블리를 제거 합니다.

```console
gacutil -u hello
```

## <a name="removing-an-assembly-with-windows-installer"></a>Windows Installer를 사용하여 어셈블리 제거

**제어판**의 **프로그램 및 기능** 앱에서 제거할 앱을 선택합니다. 설치 패키지가 GAC에 어셈블리를 배치한 경우 다른 애플리케이션에서 사용되지 않으면 Windows Installer가 해당 어셈블리를 제거합니다.

> [!NOTE]
> Windows Installer는 GAC에 설치된 어셈블리에 대한 참조 횟수를 유지 관리합니다. 참조 횟수가 0에 도달하여 Windows Installer 패키지를 통해 설치된 애플리케이션에서 사용되지 않음을 나타내는 경우에만 어셈블리가 GAC에서 제거됩니다.

## <a name="see-also"></a>참조

- [어셈블리 및 전역 어셈블리 캐시 사용](working-with-assemblies-and-the-gac.md)
- [방법: 글로벌 어셈블리 캐시에 어셈블리 설치](install-assembly-into-gac.md)
- [Gacutil.exe(전역 어셈블리 캐시 도구)](../tools/gacutil-exe-gac-tool.md)
