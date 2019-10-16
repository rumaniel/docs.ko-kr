---
title: -publicsign(C# 컴파일러 옵션)
ms.date: 05/15/2018
f1_keywords:
- /publicsign
helpviewer_keywords:
- -publicsign compiler option [C#]
- publicsign compiler option [C#]
- /publicsign compiler option [C#]
ms.openlocfilehash: de7d9c98b0f279b52bc93711c5b986a2b2e57215
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54738068"
---
# <a name="-publicsign-c-compiler-options"></a>-publicsign(C# 컴파일러 옵션)

이 옵션을 사용하면 컴파일러는 공개 키를 적용하지만 실제로 어셈블리에 서명하지 않습니다. 또한 **-publicsign** 옵션은 파일이 실제로 서명되었음을 런타임에 알리는 비트를 어셈블리에 설정합니다.

## <a name="syntax"></a>구문

```console
-publicsign
```

## <a name="arguments"></a>인수

없음

## <a name="remarks"></a>주의

**-publicsign** 옵션에는 [-keyfile](keyfile-compiler-option.md) 또는 [-keycontainer](keycontainer-compiler-option.md)를 사용해야 합니다. **keyfile** 또는 **keycontainer** 옵션은 공개 키를 지정합니다.

**-publicsign** 및 **-delaysign** 옵션은 함께 사용할 수 없습니다.

“모조 서명” 또는 “OSS 서명”이라고도 하는 공개 서명은 출력 어셈블리에 공개 키를 포함하고 “서명된” 플래그를 설정하지만 개인 키를 사용하여 어셈블리에 실제로 서명하지는 않습니다. 이 서명은 릴리스된 “완전히 서명된” 어셈블리와 호환되지만 어셈블리 서명에 사용된 개인 키에는 액세스할 수 없는 어셈블리를 빌드하려는 오픈 소스 프로젝트에 유용합니다. 어셈블리가 완전히 서명되었는지 실제로 확인해야 하는 소비자는 거의 없으므로 완전히 서명된 어셈블리가 사용되는 거의 모든 시나리오에서 이러한 공개적으로 빌드된 어셈블리를 사용할 수 있습니다.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면

1. 프로젝트의 **속성** 페이지를 엽니다.
1. **서명만 연기** 속성을 수정합니다.

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 -delaysign 옵션](delaysign-compiler-option.md)
- [C# 컴파일러 -keyfile 옵션](keyfile-compiler-option.md)
- [C# 컴파일러 -keycontainer 옵션](keycontainer-compiler-option.md)
- [C# 컴파일러 옵션](index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
