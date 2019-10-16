---
title: Enum 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Enum
helpviewer_keywords:
- enumerated constants [Visual Basic]
- Enum statement [Visual Basic]
- Private keyword [Visual Basic], Enum statements
- Public keyword [Visual Basic], in Enum statement
- variables [Visual Basic], enumeration
- constants [Visual Basic], enumerated
ms.assetid: a45e51f1-65ff-48e1-bf32-79130f137377
ms.openlocfilehash: 0a761c39b51a8d71919a84cbbbf6739fc1f5bcea
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754625"
---
# <a name="enum-statement-visual-basic"></a>Enum 문(Visual Basic)

열거형을 선언 하 고 해당 멤버의 값을 정의 합니다.

## <a name="syntax"></a>구문

```
[ <attributelist> ] [ accessmodifier ]  [ Shadows ]
Enum enumerationname [ As datatype ]
   memberlist
End Enum
```

## <a name="parts"></a>요소

- `attributelist`

  선택 사항입니다. 이 열거형에 적용 되는 특성 목록입니다. 묶어야 합니다 [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md) 꺾쇠 괄호에서 ("`<`"및"`>`").

  <xref:System.FlagsAttribute> 열거형 인스턴스에 값이 여러 열거형 멤버를 포함할 수 있으며 각 멤버가 나타내는 열거형 값의 비트 필드 특성을 나타냅니다.

- `accessmodifier`

  선택 사항입니다. 이 열거형에 액세스할 수 있는 코드를 지정 합니다. 다음 중 하나일 수 있습니다.

  - [공용](../../../visual-basic/language-reference/modifiers/public.md)

  - [보호됨](../../../visual-basic/language-reference/modifiers/protected.md)

  - [Friend](../../../visual-basic/language-reference/modifiers/friend.md)

  - [전용](../../../visual-basic/language-reference/modifiers/private.md)

  - [Protected Friend](../../language-reference/modifiers/protected-friend.md)

  - [Private Protected](../../language-reference/modifiers/private-protected.md)

- `Shadows`

  선택 사항입니다. 이 열거형을 동일 하 게 명명 된 프로그래밍 요소 또는 기본 클래스에서 오버 로드 된 요소 집합을 다시 선언 하 고 숨기도록 지정 합니다. 지정할 수 있습니다 [그림자](../../../visual-basic/language-reference/modifiers/shadows.md) 열거형 자체에, 해당 멤버 중 하나에 없습니다.

- `enumerationname`

  필수 요소. 열거형의 이름입니다. 유효한 이름에 대 한 자세한 내용은 [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)합니다.

- `datatype`

  선택 사항입니다. 열거형 및 모든 해당 멤버의 데이터 형식입니다.

- `memberlist`

  필수 요소. 이 문에서 선언 되는 멤버 상수 목록입니다. 여러 멤버는 개별 소스 코드 줄에 표시 됩니다.

  각 `member` 다음 구문과 구성 요소는: `[<attribute list>] member name [ = initializer ]`

  |파트|설명|
  |---|---|
  |`membername`|필수 요소. 이 멤버의 이름입니다.|
  |`initializer`|선택 사항입니다. 컴파일 시 계산 되 고이 멤버에 할당 되는 식입니다.|

- `End` `Enum`

  `Enum` 블록을 종료합니다.

## <a name="remarks"></a>설명

서로 논리적으로 관련 된 변경 되지 않는 값 집합에 있는 경우 열거형의 함께 정의할 수 있습니다. 열거형 및 해당 값 보다 쉽게 기억할 수 있는 해당 멤버에 대 한 의미 있는 이름을 제공 합니다. 다음 코드에서 여러 위치에서 열거형 멤버를 사용할 수 있습니다.

열거형을 사용 하는 이점은 다음과 같습니다.

- 숫자를 잘못 입력 하 여 발생 한 오류를 줄입니다.

- 에서는 값을 나중에 변경 하기가 쉽습니다.

- 에서는 오류가 도입 될 가능성이 더 낮아집니다 것을 의미 하는 코드를 쉽게 읽을 수 있습니다.

- 이후 버전과 호환성을 확인합니다. 열거형을 사용 하는 경우 코드는 멤버 이름에 해당 하는 값을 나중에 변경 되 면 실패할 가능성이 적습니다.

열거형에는 이름, 내부 데이터 형식 및 멤버 집합을 합니다. 각 멤버에는 상수를 나타냅니다.

클래스, 구조체, 모듈 또는 인터페이스 수준에서 다른 프로시저 외부에서 선언 된 열거형은는 *열거형 멤버*합니다. 클래스, 구조체, 모듈 또는 이벤트를 선언 하는 인터페이스의 멤버 임

멤버 열거 액세스할 수 있습니다에서 아무 곳 이나 해당 클래스, 구조체, 모듈 또는 인터페이스 내에서. 코드 클래스 이외에 구조체 또는 모듈 이름을 한 정해야 멤버 열거형의 해당 클래스, 구조체 또는 모듈의 이름입니다. 추가 하 여 정규화 된 이름을 사용할 필요를 방지할 수 있습니다는 [Imports](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 문을 소스 파일에 있습니다.

클래스, 구조체, 모듈 또는 인터페이스 외부 네임 스페이스 수준에서 선언 된 열거형이 표시 되는 네임 스페이스의 멤버 임

합니다 *선언 컨텍스트* 열거형 소스 파일, 네임 스페이스, 클래스, 구조체, 모듈 또는 인터페이스를 이어야 하며 프로시저일 수는 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.

특성 적용을 전체적으로 열거형이 아니라 해당 멤버 개별적으로 합니다. 특성이는 어셈블리의 메타 데이터에 대 한 정보를 제공합니다.

## <a name="data-type"></a>데이터 형식

`Enum` 문은 데이터 형식의 열거형을 선언할 수 있습니다. 각 멤버는 열거형의 데이터 형식을 사용 합니다. 지정할 수 있습니다 `Byte`, `Integer`, `Long`, `SByte`를 `Short`를 `UInteger`를 `ULong`, 또는 `UShort`합니다.

지정 하지 않는 경우 `datatype` 열거형에 대 한 각 멤버는 데이터 형식의 해당 `initializer`합니다. 둘 다 지정 하는 경우 `datatype` 하 고 `initializer`, 데이터 형식 `initializer` 변환할 수 있어야 합니다 `datatype`합니다. 모두 `datatype` 나 `initializer` 가 있는 경우 데이터 형식이 기본값으로 `Integer`합니다.

## <a name="initializing-members"></a>멤버 초기화

`Enum` 문은 선택한 멤버의 내용을 초기화할 수 `memberlist`입니다. 사용할 `initializer` 멤버에 할당할 식을 제공 합니다.

지정 하지 않는 경우 `initializer` 멤버에 대 한 Visual Basic 초기화 하거나 0 (첫 번째 경우 `member` 에 `memberlist`), 또는 바로 이전 보다 1만 큼 값 `member`합니다.

각 지정 된 식은 `initializer` 리터럴, 이미 정의 되어 있는 다른 상수 및 이미 정의 되어 있는,이 열거형의 이전 멤버를 포함 하 여 열거형 멤버의 조합일 수 있습니다. 이러한 요소를 결합 하 여 산술 및 논리 연산자를 사용할 수 있습니다.

변수 또는 함수에서 사용할 수 없습니다 `initializer`합니다. 와 같은 변환 키워드를 사용할 수는 있지만 `CByte` 고 `CShort`입니다. 사용할 수도 있습니다 `AscW` 상수를 사용 하 여 호출 하는 경우 `String` 또는 `Char` 인수를 컴파일 타임에 평가할 수 있는 때문입니다.

열거형 부동 소수점 값을 가질 수 없습니다. 멤버는 부동 소수점 값에 할당 된 경우 및 `Option Strict` 가 on으로 설정 하면 컴파일러 오류가 발생 합니다. 하는 경우 `Option Strict` 꺼져, 값을 자동으로 변환 되며는 `Enum` 형식입니다.

기본 데이터 형식에 대해 허용 되는 범위를 초과 하는 멤버의 값 또는 기본 데이터 형식에 의해 허용 되는 최대값에 멤버를 초기화 하면 컴파일러 오류를 보고 합니다.

## <a name="modifiers"></a>한정자

클래스, 구조체, 모듈 및 인터페이스 멤버의 열거형 기본적으로 공용 액세스 합니다. 액세스 한정자를 사용 하 여 해당 액세스 수준을 조정할 수 있습니다. Namespace 멤버 열거는 기본적으로 대 한 friend 액세스 합니다. 공용이 아니라 private 또는 protected 액세스 수준을 조정할 수 있습니다. 자세한 내용은 [액세스 수준을 Visual Basic의](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)합니다.

모든 열거형 멤버에는 공용 액세스가 있고에 액세스 한정자를 사용할 수 없습니다. 그러나에서 열거형 자체로 좀 더 제한 된 액세스 수준이 지정 된 열거형의 액세스 수준이 우선 적용 됩니다.

기본적으로 모든 열거형 형식이 며 해당 필드는 상수입니다. 따라서 합니다 `Shared`, `Static`, 및 `ReadOnly` 열거형 또는 해당 멤버를 선언 하는 경우에 키워드를 사용할 수 없습니다.

## <a name="assigning-multiple-values"></a>여러 값 할당

열거형은 일반적으로 상호 배타적인 값을 나타냅니다. 포함 하 여 합니다 <xref:System.FlagsAttribute> 특성을 `Enum` 선언 하면 대신 여러 값을 할당할 수 열거형의 인스턴스. <xref:System.FlagsAttribute> 특성 열거형 플래그 집합 즉, 비트 필드로 처리 되도록 지정 합니다. 이러한 이라고 *비트* 열거형입니다.

사용 하 여 열거형을 선언 하는 <xref:System.FlagsAttribute> 특성인 것이 좋습니다는 2, 1, 2, 4, 8, 16, 및 등의 거듭제곱 값을 사용 하는 합니다. 값이 0 인 멤버의 이름을 "None" 되도록 하는 것이 좋습니다. 추가 지침을 참조 하세요 <xref:System.FlagsAttribute> 고 <xref:System.Enum>입니다.

## <a name="example"></a>예제

다음 예제에서는 `Enum` 문을 사용하는 방법을 보여 줍니다. 멤버 라고 보면 `EggSizeEnum.Medium`, 아니라 `Medium`합니다.

[!code-vb[VbEnumsTask#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#41)]

## <a name="example"></a>예제

다음 예제에서 메서드는 외부는 `Egg` 클래스입니다. 따라서 `EggSizeEnum` 으로 정규화 `Egg.EggSizeEnum`합니다.

[!code-vb[VbEnumsTask#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#42)]

## <a name="example"></a>예제

다음 예제에서는 `Enum` 명명 된 상수 값을 관련된 집합을 정의 합니다. 이 경우 값은 색을 데이터베이스에 대 한 데이터 입력 폼 디자인 하도록 선택할 수 있습니다.

[!code-vb[VbEnumsTask#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#30)]

## <a name="example"></a>예제

다음 예제에서는 양수와 음수 모두를 포함 하는 값을 보여 줍니다.

[!code-vb[VbEnumsTask#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#31)]

## <a name="example"></a>예제

다음 예제에서는 `As` 절을 사용 하 여를 지정 합니다 `datatype` 열거형의 합니다.

[!code-vb[VbEnumsTask#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#6)]

## <a name="example"></a>예제

다음 예제에서는 비트 열거형을 사용 하는 방법을 보여 줍니다. 여러 값의 비트 열거형 인스턴스에 할당할 수 있습니다. `Enum` 선언에 포함 된 <xref:System.FlagsAttribute> 열거형 플래그 집합으로 처리할 수 있음을 나타내는 특성입니다.

[!code-vb[VbEnumsTask#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#61)]

## <a name="example"></a>예제

다음 예제에서는 열거형을 반복합니다. 사용 된 <xref:System.Enum.GetNames%2A> 열거형의 멤버 이름의 배열을 검색 하는 방법 및 <xref:System.Enum.GetValues%2A> 멤버 값의 배열을 검색 하 합니다.

[!code-vb[VbEnumsTask#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#51)]

## <a name="see-also"></a>참고자료

- <xref:System.Enum>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- [Const 문](../../../visual-basic/language-reference/statements/const-statement.md)
- [Dim 문](../../../visual-basic/language-reference/statements/dim-statement.md)
- [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [상수 및 열거형](../../../visual-basic/language-reference/constants-and-enumerations.md)
