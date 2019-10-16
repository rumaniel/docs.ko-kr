---
title: -refonly(C# 컴파일러 옵션)
ms.date: 07/08/2017
f1_keywords:
- /refonly
helpviewer_keywords:
- /refonly compiler option [C#]
- -refonly compiler option [C#]
- refonly compiler option [C#]
ms.openlocfilehash: eb62f98c5d548fe3583d3422eb7b6020a82c296a
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606490"
---
# <a name="-refonly-c-compiler-options"></a>-refonly(C# 컴파일러 옵션)

**-refonly** 옵션은 구현 어셈블리 대신 참조 어셈블리가 기본 출력으로 출력되어야 함을 나타냅니다. `-refonly` 매개 변수는 참조 어셈블리가 실행될 수 없을 때 PDB 출력을 자동으로 사용하지 않도록 설정합니다. 이 옵션은 MSBuild의 [ProduceOnlyReferenceAssembly](/visualstudio/msbuild/common-msbuild-project-properties) 프로젝트 속성에 해당합니다.

## <a name="syntax"></a>구문

```console
-refonly
```

## <a name="remarks"></a>설명

메타데이터 전용 어셈블리에는 단일 `throw null` 본문으로 대체되는 메서드 본문이 있지만 익명 형식을 제외한 모든 멤버가 포함됩니다. 본문이 없는 경우와 대조적으로 `throw null` 본문을 사용하는 이유는 PEVerify가 실행 및 전달될 수 있도록 하여 메타데이터의 완전성을 검증하기 위한 것입니다.

참조 어셈블리에는 어셈블리 수준 `ReferenceAssembly` 특성이 포함됩니다. 이 특성을 소스에서 지정할 수 있습니다. 이렇게 하면 컴파일러가 특성을 합성할 필요가 없습니다. 이 특성으로 인해 런타임은 실행용 참조 어셈블리 로드를 거부합니다. 그러나 리플렉션 전용 모드에서 계속 로드할 수 있습니다. 어셈블리에 반영되는 도구는 참조 어셈블리를 리플렉션 전용으로 로드하는지, 아니면 런타임에서 typeload 오류가 발생하는지 확인해야 합니다.

참조 어셈블리는 메타데이터 프라이빗 어셈블리에서 메타데이터(전용 멤버)를 추가로 제거합니다.

- 참조 어셈블리에는 API 화면에 있어야 하는 항목에 대한 참조만 포함됩니다. 실제 어셈블리에는 특정 구현에 관련된 추가 참조가 포함될 수 있습니다. 예를 들어 `class C { private void M() { dynamic d = 1; ... } }`에 대한 참조 어셈블리는 `dynamic`에 필요한 형식을 참조하지 않습니다.
- 제거가 컴파일에 눈에 띄는 영향을 미치지 않을 경우 전용 함수-멤버(메서드, 속성 및 이벤트)가 제거됩니다. <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성이 없는 경우 내부 함수-멤버에 대해 동일한 작업을 수행합니다.
- 그러나 모든 형식(전용 또는 중첩 형식 포함)은 참조 어셈블리에서 유지됩니다. 모든 특성이 유지됩니다(내부 특성인 경우에도).
- 모든 가상 메서드가 유지됩니다. 명시적 인터페이스 구현이 유지됩니다. 명시적으로 구현된 속성 및 이벤트가 유지됩니다. 해당 접근자가 가상이므로 유지됩니다.
- 구조체의 모든 필드가 유지됩니다. 이것은 post-C#-7.1 개선의 후보입니다.

`-refonly` 및 [`-refout`](refout-compiler-option.md) 옵션은 함께 사용할 수 없습니다.

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
