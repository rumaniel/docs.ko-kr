---
title: -refonly (Visual Basic)
ms.date: 03/16/2018
f1_keywords:
- -refonly
helpviewer_keywords:
- /refonly compiler option [Visual Basic]
- -refonly compiler option [Visual Basic]
- refonly compiler option [Visual Basic]
ms.openlocfilehash: b22fb9ae24a04d9fe530811bf764352199c31813
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200812"
---
# <a name="-refonly-visual-basic"></a>-refonly (Visual Basic)

합니다 **-refonly** 옵션 컴파일 기본 출력은 구현 어셈블리 대신 참조 어셈블리를 함을 나타냅니다. `-refonly` 매개 변수는 참조 어셈블리가 실행될 수 없을 때 PDB 출력을 자동으로 사용하지 않도록 설정합니다.

[!INCLUDE[compiler-options](~/includes/compiler-options.md)]

## <a name="syntax"></a>구문

```console
-refonly
```

## <a name="remarks"></a>설명

Visual Basic 지원은 `-refout` 버전 15.3부터 전환 합니다.

참조 어셈블리는 구현 코드가 없는 메타 데이터를 포함 하는 메타 데이터 전용 어셈블리입니다. 익명 형식을 제외한 모든 항목에 대 한 형식 및 멤버 정보가 포함 됩니다. 본문이 없는 경우와 대조적으로 `throw null` 본문을 사용하는 이유는 PEVerify가 실행 및 전달될 수 있도록 하여 메타데이터의 완전성을 검증하기 위한 것입니다.

참조 어셈블리는 어셈블리 수준 포함 [ReferenceAssembly](xref:System.Runtime.CompilerServices.ReferenceAssemblyAttribute) 특성입니다. 이 특성을 소스에서 지정할 수 있습니다. 이렇게 하면 컴파일러가 특성을 합성할 필요가 없습니다. 이 특성으로 인해 런타임 실행을 위한 참조 어셈블리 로드를 거부 되지만 리플렉션 전용 컨텍스트에서 로드 될 여전히 수 있습니다. 어셈블리에 반영 되는 도구를 참조 어셈블리를 리플렉션 전용으로 로드를 확인 해야 합니다. 그렇지 않으면 런타임에서 throw 된 <xref:System.BadImageFormatException>합니다.

`-refonly` 및 [`-refout`](refout-compiler-option.md) 옵션은 함께 사용할 수 없습니다.

## <a name="see-also"></a>참고자료
[-refout](refout-compiler-option.md)   
[Visual Basic 명령줄 컴파일러](index.md)  
[샘플 컴파일 명령줄](sample-compilation-command-lines.md)   
