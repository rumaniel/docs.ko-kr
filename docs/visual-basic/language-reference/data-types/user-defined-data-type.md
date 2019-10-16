---
title: 사용자 정의 데이터 형식 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- UserDefined
- UDT
- vb.UDT
- User-Defined
- vb.UserDefined
- vb.User-Defined
helpviewer_keywords:
- user-defined data types [Visual Basic], Visual Basic
- user-defined types
- structures [Visual Basic], as user-defined data types
- user-defined types [Visual Basic], Visual Basic
- user-defined types [Visual Basic], structure declaration
- user-defined types [Visual Basic], structures in Visual Basic
- user-defined data types [Visual Basic], structure declaration
- data types [Visual Basic], assigning
- Structure statement [Visual Basic]
- data types [Visual Basic], user-defined
- user-defined data types [Visual Basic], structures in Visual Basic
- user-defined data types
- types [Visual Basic], user-defined
ms.assetid: be913dca-a364-4a51-96a1-549a1b390b0a
ms.openlocfilehash: d95feec3a976a38c92a215f6da58ae6324085fe8
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696861"
---
# <a name="user-defined-data-type"></a>사용자 정의 데이터 형식

사용자가 정의한 형식으로 데이터를 저장 합니다. @No__t-0 문은 형식을 정의 합니다.

이전 버전의 Visual Basic에서는 UDT (사용자 정의 형식)를 지원 합니다. 현재 버전은 UDT를 *구조체로*확장 합니다. 구조는 다양 한 데이터 형식에 대 한 하나 이상의 *멤버* 를 연결 하는 것입니다. Visual Basic는 구조체를 단일 단위로 처리 하지만 해당 멤버에 개별적으로 액세스할 수도 있습니다.

## <a name="remarks"></a>설명

구조 데이터 형식을 정의 하 고 사용 하 여 다양 한 데이터 형식을 단일 단위로 결합 해야 하거나 모든 기본 데이터 형식이 필요 하지 않은 경우에 사용 합니다.

구조체 데이터 형식의 기본값은 각 멤버의 기본값 조합으로 구성 됩니다.

## <a name="declaration-format"></a>선언 형식

구조체 선언은 [Structure 문으로](../../../visual-basic/language-reference/statements/structure-statement.md) 시작 하 고 `End Structure` 문으로 끝납니다. @No__t-0 문은 구조체에서 정의 하는 데이터 형식의 식별자 이기도 한 구조 이름을 제공 합니다. 코드의 다른 부분은이 식별자를 사용 하 여 변수, 매개 변수 및 함수 반환 값을이 구조체의 데이터 형식으로 선언할 수 있습니다.

@No__t-0과 `End Structure` 문 사이의 선언은 구조체의 멤버를 정의 합니다.

## <a name="member-access-levels"></a>멤버 액세스 수준

[Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md) 또는 [Public](../../../visual-basic/language-reference/modifiers/public.md), [Friend](../../../visual-basic/language-reference/modifiers/friend.md)또는 [Private](../../../visual-basic/language-reference/modifiers/private.md)와 같은 액세스 수준을 지정 하는 문을 사용 하 여 모든 멤버를 선언 해야 합니다. @No__t-0 문을 사용 하는 경우 액세스 수준 기본값은 public입니다.

## <a name="programming-tips"></a>프로그래밍 팁

- **메모리 소비** 모든 복합 데이터 형식과 마찬가지로 해당 멤버의 명목상 저장소 할당을 함께 추가 하 여 구조의 총 메모리 소비량을 안전 하 게 계산할 수 없습니다. 또한 메모리의 저장소 순서가 선언 순서와 동일 하다는 것을 안전 하 게 가정할 수 없습니다. 구조의 저장소 레이아웃을 제어 해야 하는 경우 <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성을 `Structure` 문에 적용할 수 있습니다.

- **Interop 고려 사항** .NET Framework 용으로 작성 되지 않은 구성 요소 (예: Automation 또는 COM 개체)와 상호 작용 하는 경우 다른 환경의 사용자 정의 형식은 Visual Basic 구조체 형식과 호환 되지 않는다는 점에 유의 하세요.

- **넓혀.** 구조체 데이터 형식과의 자동 변환은 없습니다. [연산자 문을](../../../visual-basic/language-reference/statements/operator-statement.md)사용 하 여 구조체에 변환 연산자를 정의할 수 있으며 각 변환 연산자를 `Widening` 또는 `Narrowing`로 선언할 수 있습니다.

- **문자를 입력 합니다.** 구조체 데이터 형식에는 리터럴 형식 문자 또는 식별자 형식 문자가 없습니다.

- **프레임 워크 형식입니다.** .NET Framework에 해당 형식이 없습니다. 모든 구조체는 .NET Framework 클래스 <xref:System.ValueType?displayProperty=nameWithType>에서 상속 하지만 개별 구조는 <xref:System.ValueType?displayProperty=nameWithType>에 해당 하지 않습니다.

## <a name="example"></a>예제

다음 패러다임에서는 구조체의 선언에 대 한 개요를 보여 줍니다.

```vb
[Public | Protected | Friend | Protected Friend | Private] Structure structname
    {Dim | Public | Friend | Private} member1 As datatype1
    ' ...
    {Dim | Public | Friend | Private} memberN As datatypeN
End Structure
```

## <a name="see-also"></a>참조

- <xref:System.ValueType>
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- [데이터 형식](../../../visual-basic/language-reference/data-types/index.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [변환 요약](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)
- [확장](../../../visual-basic/language-reference/modifiers/widening.md)
- [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [데이터 형식의 효율적 사용](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
