---
title: -delaysign(C# 컴파일러 옵션)
ms.date: 05/15/2018
f1_keywords:
- /delaysign
helpviewer_keywords:
- -delaysign compiler option [C#]
- delaysign compiler option [C#]
- /delaysign compiler option [C#]
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
ms.openlocfilehash: 9fdc02c22d9d8c8a709155e43a17ebf0d86dfd69
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970440"
---
# <a name="-delaysign-c-compiler-options"></a>-delaysign(C# 컴파일러 옵션)

이 옵션을 사용하면 나중에 디지털 시그니처를 추가할 수 있도록 컴파일러가 출력 파일에 공간을 예약합니다.

## <a name="syntax"></a>구문

```console
-delaysign[ + | - ]
```

## <a name="arguments"></a>인수

`+` &#124; `-`

완전히 서명된 어셈블리가 필요하면 **-delaysign-** 를 사용합니다. 어셈블리에 공개 키만 배치하려면 **-delaysign+** 를 사용합니다. 기본값은 **-delaysign-** 입니다.

## <a name="remarks"></a>설명

**-delaysign** 옵션은 [-keyfile](./keyfile-compiler-option.md) 또는 [-keycontainer](./keycontainer-compiler-option.md)와 함께 사용하지 않으면 효과가 없습니다.

**-delaysign** 및 **-publicsign** 옵션은 함께 사용할 수 없습니다.

완전히 서명된 어셈블리를 요청할 경우 컴파일러는 매니페스트(어셈블리 메타데이터)가 포함된 파일을 해시하고 프라이빗 키로 해당 해시에 서명합니다. 해당 작업으로 디지털 시그니처가 생생되어 매니페스트가 포함된 파일에 저장됩니다. 어셈블리 서명이 연기된 경우 컴파일러는 서명을 컴퓨팅하거나 저장하지 않고 나중에 서명을 추가할 수 있도록 파일에 공간을 예약합니다.

예를 들어 **-delaysign+** 를 사용하면 테스터를 통해 전역 캐시에 어셈블리를 넣을 수 있습니다. 테스트를 마친 후 [어셈블리 링커](../../../framework/tools/al-exe-assembly-linker.md) 유틸리티를 통해 어셈블리에 프라이빗 키를 배치하여 어셈블리에 완전히 서명할 수 있습니다.

자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../standard/assembly/create-use-strong-named.md) 및 [어셈블리 서명 지연](../../../standard/assembly/delay-sign.md)을 참조하세요.

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면

1. 프로젝트의 **속성** 페이지를 엽니다.
1. **서명만 연기** 속성을 수정합니다.

이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# -publicsign 옵션](publicsign-compiler-option.md)
- [C# 컴파일러 옵션](index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
