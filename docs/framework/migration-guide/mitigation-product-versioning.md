---
title: '완화: 제품 버전 관리'
ms.date: 03/30/2017
ms.assetid: 1c4de9d7-9aba-427a-8f38-0ab9bfb8f85e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 91db9d8c6fccf75bc9025a9487517e8c55d016cc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779214"
---
# <a name="mitigation-product-versioning"></a>완화: 제품 버전 관리

.NET Framework 4.6 이상에서, 제품 버전 관리가 .NET Framework(.NET Framework 4, 4.5, 4.5.1 및 4.5.2)의 이전 릴리스에서 변경되었습니다.

## <a name="product-versioning-changes"></a>제품 버전 관리 변경 내용

자세한 변경 내용은 다음과 같습니다.

- `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`키에서 `Version` 항목의 값은 .NET Framework 4.6 및 해당 포인트 릴리스에 대해 `4.6.`*xxxxx*로, .NET Framework 4.7에 대해 `4.7.`*xxxxx*로 변경되었습니다. .NET Framework 4.5, 4.5.1 및 4.5.2에서는 `4.5.`*xxxxx* 형식이었습니다.

- .NET Framework 파일에 대한 파일 및 제품 버전 관리는 이전 버전 관리 체계의 `4.0.30319.x`에서 .NET Framework 4.6 및 해당 포인트 릴리스에 대해 `4.6.X.0`로, .NET Framework 4.7 및 해당 포인트에 대해 `4.7.X.0`로 변경되었습니다. 파일을 마우스 오른쪽 단추로 클릭한 후 파일의 **속성**을 보면 이러한 새 값을 확인할 수 있습니다.

- 관리되는 어셈블리의 <xref:System.Reflection.AssemblyFileVersionAttribute> 및 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 특성은 .NET Framework 4.6 및 해당 포인트 릴리스의 경우 `4.6.X.0` 형식, 그리고 .NET Framework 4.7의 경우에는 `4.7.X.0` 형식의 <xref:System.Version> 값을 포함합니다.

- .NET Framework 4.6부터 <xref:System.Environment.Version%2A?displayProperty=nameWithType> 속성은 최종 버전 문자열 `4.0.30319.42000`을 반환합니다. .NET Framework 4, 4.5, 4.5.1 및 4.5.2에서는 `xxxxx`가 42000보다 작은 `4.0.30319.xxxxx` 형식의 버전 문자열을 반환합니다(예: "4.0.30319.18010"). <xref:System.Environment.Version%2A?displayProperty=nameWithType> 속성에서 새 종속성을 취하는 애플리케이션 코드는 권장하지 않습니다.

### <a name="handling-the-product-versioning-changes"></a>제품 버전 관리 변경 내용 처리

일반적으로 애플리케이션은 .NET Framework 및 설치 디렉터리 검색의 런타임 버전과 같은 항목 검색을 위한 권장 기술에 의존해야 합니다.

- .NET Framework의 런타임 버전을 검색하려면 [방법: 설치된 .NET Framework 버전 확인](how-to-determine-which-versions-are-installed.md)을 참조하세요.

- .NET Framework의 설치 경로를 확인하려면`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full` 키의 `InstallPath` 항목 값을 사용합니다.

  > [!IMPORTANT]
  > 하위 키 이름은 `.NET Framework Setup`이 아니라 `NET Framework Setup`입니다.

- .NET Framework 공용 언어 런타임에 대한 디렉터리 경로를 확인하려면 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory%2A?displayProperty=nameWithType> 메서드를 호출합니다.

- CLR 버전을 알아보려면 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion%2A?displayProperty=nameWithType> 메서드를 호출합니다.   .NET Framework 4 및 해당 지점 릴리스(.NET Framework 4.5, 4.5.1, 4.5.2 및 .NET Framework 4.6, 4.6.1, 4.6.2 및 4.7)의 경우 문자열 `v4.0.30319`를 반환합니다.

## <a name="see-also"></a>참고 항목

- [런타임 변경 내용](runtime-changes-in-the-net-framework-4-6.md)
