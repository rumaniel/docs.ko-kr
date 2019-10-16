---
title: .NET에서 쉽게 디버깅할 수 있도록 이미지 만들기
description: IDE 스위치 및 명령줄 옵션을 사용 하 여 디버깅을 용이 하 게 하기 위해 실행 가능한 이미지를 구성 하는 방법을 알아봅니다.
ms.date: 08/30/2018
helpviewer_keywords:
- images [.NET Framework], debugging
- executable image for debugging
- debugging [.NET Framework], executable images for
ms.assetid: 7d90ea7a-150f-4f97-98a7-f9c26541b9a3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1b64bd1e112932f394bb473a21642d37e28e39d3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052509"
---
# <a name="making-an-image-easier-to-debug-in-net"></a>.NET에서 쉽게 디버깅할 수 있도록 이미지 만들기

비관리 코드를 컴파일할 때 IDE 스위치 또는 명령줄 옵션을 설정하여 디버깅할 실행 가능 이미지를 구성할 수 있습니다. 예를 들어 Visual C++에서 /**Zi** 명령줄 옵션을 사용하여 디버그 기호 파일(확장 확장자는 .pdb)을 생성하도록 요청할 수 있습니다. 마찬가지로 /**Od** 명령줄 옵션을 사용하면 최적화를 사용하지 않게 설정하도록 컴파일러에 지시합니다. 결과 코드는 더 느리게 실행 되지만 디버그 하는 것이 필요 합니다.

.NET Framework 관리 코드를 컴파일하는 경우 Visual C++등의 컴파일러는 Visual Basic 하 C# 고 소스 프로그램을 MSIL (Microsoft 중간 언어)로 컴파일합니다. MSIL은 실행 직전에 네이티브 기계어 코드로 JIT 컴파일됩니다. 비관리 코드와 함께 IDE 스위치 또는 명령줄 옵션을 설정하여 디버깅할 실행 가능 이미지를 구성할 수 있습니다. 동일한 방식으로 디버깅을 위해 JIT 컴파일을 구성할 수도 있습니다.

JIT 구성에는 두 가지 요소가 있습니다.

- JIT 컴파일러에서 추적 정보를 생성 하도록 요청할 수 있습니다. 그러면 디버거에서 MSIL 체인을 대응하는 기계어 코드와 일치시키고 지역 변수와 함수 인수가 저장된 위치를 추적할 수 있습니다. .NET Framework 버전 2.0부터 JIT 컴파일러는 항상 추적 정보를 생성 하므로 요청할 필요가 없습니다.

- 결과 기계어 코드를 최적화 하지 않도록 JIT 컴파일러를 요청할 수 있습니다.

일반적으로 MSIL을 생성 하는 컴파일러는 사용자가 지정 하는 IDE 스위치 또는 명령줄 옵션 (예:/**Od**)에 따라 이러한 JIT 컴파일러 옵션을 적절 하 게 설정 합니다.

경우에 따라 생성되는 기계어 코드를 더 쉽게 디버깅할 수 있도록 JIT 컴파일러의 동작을 변경하는 것이 좋습니다. 예를 들어, 정품 빌드 또는 제어 최적화를 위해 JIT 추적 정보를 생성할 수 있습니다. 초기화(.ini) 파일을 사용해서도 수행할 수 있습니다.

예를 들어 디버그 하려는 어셈블리를 *myapp.exe*라고 하는 경우 다음 세 줄을 포함 하는 *myapp.exe*와 동일한 폴더에 *myapp.exe*라는 텍스트 파일을 만들 수 있습니다.

```ini
[.NET Framework Debugging Control]
GenerateTrackingInfo=1
AllowOptimize=0
```

각 옵션의 값은 0 또는 1로 설정되고 비어 있는 옵션은 기본값으로 0으로 설정됩니다. `GenerateTrackingInfo`를 1로 설정하고 `AllowOptimize`를 0으로 설정하면 디버깅이 가장 쉬워집니다.

.NET Framework 버전 2.0부터 JIT 컴파일러는의 `GenerateTrackingInfo`값에 관계 없이 항상 추적 정보를 생성 하지만 값은 `AllowOptimize` 여전히 효과가 있습니다. [Ngen.exe(네이티브 이미지 생성기)](../tools/ngen-exe-native-image-generator.md)를 사용하여 최적화하지 않고 네이티브 이미지를 사전 컴파일하는 경우 Ngen.exe가 실행될 때 `AllowOptimize=0`인 대상 폴더에 .ini 파일이 있어야 합니다. 최적화 하지 않고 어셈블리를 미리 컴파일한 경우 Ngen.exe를 다시 실행 하 여 최적화 된 상태로 코드를 미리 컴파일하려면 ngen.exe **/uninstall** 옵션을 사용 하 여 미리 컴파일된 코드를 제거 해야 합니다. .Ini 파일이 폴더에 없는 경우 기본적으로 Ngen.exe는 최적화 된 상태로 코드를 미리 컴파일합니다.

<xref:System.Diagnostics.DebuggableAttribute?displayProperty=nameWithType>을 통해 어셈블리의 설정을 제어합니다. **DebuggableAttribute** 에는 JIT 컴파일러가 추적 정보를 최적화 하 고 생성 해야 하는지 여부를 제어 하는 두 개의 필드가 포함 됩니다. .NET Framework 버전 2.0부터 JIT 컴파일러는 항상 추적 정보를 생성 합니다.

소매 빌드의 경우 컴파일러는 **DebuggableAttribute**를 설정 하지 않습니다. 기본적으로 JIT 컴파일러는 컴퓨터 코드를 디버그 하는 데 가장 큰 성능을 생성 합니다. JIT 추적을 사용하면 성능이 약간 저하되지만 최적화를 사용하지 않게 설정하면 성능이 상당히 저하됩니다.

**DebuggableAttribute**는 어셈블리에 있는 개별 모듈이 아니라 한 번에 전체 어셈블리에 적용됩니다. 따라서 개발 도구에서 사용자 지정 특성을 어셈블리 메타데이터 토큰에 연결하거나, 어셈블리가 이미 생성된 경우 **System.Runtime.CompilerServices.AssemblyAttributesGoHere**라는 클래스에 연결해야 합니다. 그런 다음 ALink 도구는 이러한 **DebuggableAttribute** 특성을 각 모듈에서 일부가 될 어셈블리로 승격 합니다. 충돌이 발생 하면 ALink 작업이 실패 합니다.

> [!NOTE]
> .NET Framework 버전 1.0에서 **/clr** 및 **/Zi** 컴파일러 옵션이 지정된 경우 Microsoft Visual C++ Compiler에서 **DebuggableAttribute**를 추가합니다. .NET Framework 버전 1.1에서 코드에 수동으로 **DebuggableAttribute** 을 추가 하거나 **/ASSEMBLYDEBUG** 링커 옵션을 사용 해야 합니다.

## <a name="see-also"></a>참고자료

- [디버깅, 추적 및 프로파일링](index.md)
- [JIT 연결 디버깅 설정](enabling-jit-attach-debugging.md)
- [프로파일링 설정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/s5ec0es1(v=vs.100))
