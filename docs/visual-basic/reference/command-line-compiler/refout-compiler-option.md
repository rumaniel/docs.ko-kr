---
title: -refout (Visual Basic)
ms.date: 03/16/2018
f1_keywords:
- /refout
helpviewer_keywords:
- refout compiler option [Visual Basic]
- /refout compiler option [Visual Basic]
- -refout compiler option [Visual Basic]
ms.openlocfilehash: f2cdd228d8ce1912abbbe888c29c42f29299ebba
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61788793"
---
# <a name="-refout-visual-basic"></a>-refout (Visual Basic)

**-refout** 옵션은 참조 어셈블리가 출력되어야 하는 파일 경로를 지정합니다.

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]

## <a name="syntax"></a>구문

```console
-refout:filepath
```

## <a name="arguments"></a>인수

 `filepath` 경로 및 참조 어셈블리의 이름입니다. 일반적으로 주 어셈블리의 하위 폴더에는 것이 있어야 합니다. 권장되는 규칙(MSBuild에서 사용됨)은 주 어셈블리에 상대적으로 “ref/” sub-폴더에 참조 어셈블리를 배치하는 것입니다. 모든 폴더 `filepath` ; 있어야 컴파일러에서 만들 하지 않습니다. 

## <a name="remarks"></a>설명

Visual Basic 지원은 `-refout` 버전 15.3부터 전환 합니다.

참조 어셈블리는 구현 코드가 없는 메타 데이터를 포함 하는 메타 데이터 전용 어셈블리입니다. 익명 형식을 제외한 모든 항목에 대 한 형식 및 멤버 정보가 포함 됩니다. 메서드 본문은 단일 바뀝니다 `throw null` 문입니다. 사용 하는 이유 `throw null` (달리 본문이 없는) 메서드 본문은 PEVerify 실행 하 고 (따라서 메타 데이터의 완전성을 검증)를 전달할 수 있도록 합니다.

참조 어셈블리는 어셈블리 수준 포함 [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) 특성입니다. 이 특성을 소스에서 지정할 수 있습니다. 이렇게 하면 컴파일러가 특성을 합성할 필요가 없습니다. 이 특성으로 인해 런타임은 실행에 대 한 참조 어셈블리를 로드 하지 않습니다 (하지만 여전히 있을 수 있습니다 리플렉션 전용 컨텍스트에 로드). 어셈블리에 반영 되는 도구를 참조 어셈블리를 리플렉션 전용으로 로드를 확인 해야 합니다. 그렇지 않으면 런타임에서 throw 된 <xref:System.BadImageFormatException>합니다.

`-refout` 및 [`-refonly`](refonly-compiler-option.md) 옵션은 함께 사용할 수 없습니다.

## <a name="see-also"></a>참고자료

- [/refonly](refonly-compiler-option.md)
- [Visual Basic 명령줄 컴파일러](index.md)
- [샘플 컴파일 명령줄](sample-compilation-command-lines.md)
