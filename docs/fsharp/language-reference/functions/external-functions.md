---
title: 외부 함수
description: 네이티브 코드에서 F# 함수를 호출 하는 언어 지원에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: 3c8edaba25e07b6ca2c44a58c4b55dc98a13b4fc
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968723"
---
# <a name="external-functions"></a>외부 함수

이 항목에서는 F# 네이티브 코드에서 함수를 호출 하는 언어 지원에 대해 설명 합니다.

## <a name="syntax"></a>구문

```fsharp
[<DllImport( arguments )>]
extern declaration
```

## <a name="remarks"></a>설명

이전 구문에서 *인수* 는 `System.Runtime.InteropServices.DllImportAttribute` 특성에 제공 되는 인수를 나타냅니다. 첫 번째 인수는이 함수가 포함 된 DLL의 이름을 나타내는 문자열이 며 .dll 확장명은 사용 하지 않습니다. `System.Runtime.InteropServices.DllImportAttribute` 클래스의 public 속성 (예: 호출 규칙)에 대 한 추가 인수를 제공할 수 있습니다.

다음 내보낸 함수를 포함 C++ 하는 네이티브 DLL이 있다고 가정 합니다.

```cpp
#include <stdio.h>
extern "C" void __declspec(dllexport) HelloWorld()
{
    printf("Hello world, invoked by F#!\n");
}
```

다음 코드를 사용 하 여 F# 에서이 함수를 호출할 수 있습니다.

```fsharp
open System.Runtime.InteropServices

module InteropWithNative =
    [<DllImport(@"C:\bin\nativedll", CallingConvention = CallingConvention.Cdecl)>]
    extern void HelloWorld()

InteropWithNative.HelloWorld()
```

네이티브 코드와의 상호 운용성은 *플랫폼 호출* 이라고 하며 CLR의 기능입니다. 자세한 내용은 [비관리 코드 상호 운용](../../../framework/interop/index.md)을 참조하세요. 해당 섹션의 정보는에 F#적용 됩니다.

## <a name="see-also"></a>참고자료

- [함수](index.md)
