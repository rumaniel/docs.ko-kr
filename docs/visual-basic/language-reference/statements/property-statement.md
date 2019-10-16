---
title: Property 문 (Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.PropertySet
- vb.Property
- vb.PropertyGet
helpviewer_keywords:
- Property statement [Visual Basic]
- default modifier
- property procedures [Visual Basic], Property statements
- Property keyword [Visual Basic]
ms.assetid: 3155edaf-8ebd-45c6-9cef-11d5d2dc8d38
ms.openlocfilehash: 2c3e417aad404171a43342dc92773615ec350ef5
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332741"
---
# <a name="property-statement"></a>Property Statement

속성의 이름과 속성 값을 저장 하 고 검색 하는 데 사용 되는 속성 프로시저를 선언 합니다.

## <a name="syntax"></a>구문

```vb
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ] [ Iterator ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
    [ <attributelist> ] [ accessmodifier ] Get
        [ statements ]
    End Get
    [ <attributelist> ] [ accessmodifier ] Set ( ByVal value As returntype [, parameterlist ] )
        [ statements ]
    End Set
End Property
- or -
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
```

## <a name="parts"></a>요소

- `attributelist`

  (선택 사항) 이 속성 또는 `Get` 또는 @no__t 프로시저에 적용 되는 특성의 목록입니다. [특성 목록](attribute-list.md)을 참조 하십시오.

- `Default`

  (선택 사항) 이 속성이 정의 된 클래스 또는 구조체에 대 한 기본 속성 임을 지정 합니다. 기본 속성은 매개 변수를 허용 해야 하며 속성 이름을 지정 하지 않고 설정 하 고 검색할 수 있습니다. 속성을 `Default`으로 선언 하는 경우 속성 또는 속성 프로시저 중 하나에서 `Private`을 사용할 수 없습니다.

- `accessmodifier`

  @No__t-0 문과 `Get` 및 `Set` 문 중 하나 이상에 대 한 선택 사항입니다. 다음 중 하나일 수 있습니다.

  - [공개](../modifiers/public.md)

  - [보호됨](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [전용](../modifiers/private.md)

  - [Protected Friend](../modifiers/protected-friend.md)

  - [Private Protected](../modifiers/private-protected.md)

  [Access levels in Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.

- `propertymodifiers`

  (선택 사항) 다음 중 하나일 수 있습니다.

  - [오버로드](../modifiers/overloads.md)

  - [재정의](../modifiers/overrides.md)

  - [재정의 가능](../modifiers/overridable.md)

  - [NotOverridable](../modifiers/notoverridable.md)

  - [MustOverride](../modifiers/mustoverride.md)

  - `MustOverride Overrides`

  - `NotOverridable Overrides`

- `Shared`

  (선택 사항) [공유](../modifiers/shared.md)를 참조 하세요.

- `Shadows`

  (선택 사항) [그림자](../modifiers/shadows.md)를 참조 하세요.

- `ReadOnly`

  (선택 사항) [ReadOnly](../modifiers/readonly.md)를 참조 하세요.

- `WriteOnly`

  (선택 사항) [WriteOnly](../modifiers/writeonly.md)를 참조 하세요.

- `Iterator`

  (선택 사항) [반복기](../modifiers/iterator.md)를 참조 하세요.

- `name`

  필수. 속성의 이름입니다. [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.

- `parameterlist`

  (선택 사항) 이 속성의 매개 변수를 나타내는 지역 변수 이름과 `Set` 프로시저의 가능한 추가 매개 변수를 나타내는 목록입니다. [매개 변수 목록](parameter-list.md)을 참조 하세요.

- `returntype`

  필요한 경우 `Option Strict` 는 `On`합니다. 이 속성에서 반환 하는 값의 데이터 형식입니다.

- `Implements`

  (선택 사항) 이 속성이이 속성의 포함 클래스 또는 구조체에서 구현 하는 인터페이스에 각각 정의 된 하나 이상의 속성을 구현 함을 나타냅니다. [Implements 문](implements-statement.md)을 참조 하세요.

- `implementslist`

  `Implements`가 제공된 경우 필수입니다. 구현 중인 속성의 목록입니다.

  `implementedproperty [ , implementedproperty ... ]`

  각 `implementedproperty`에는 다음과 같은 구문과 요소가 있습니다.

  `interface.definedname`

  |부분|설명|
  |---|---|
  |`interface`|필수. 이 속성에 포함 된 클래스 또는 구조체에 의해 구현 된 인터페이스의 이름입니다.|
  |`definedname`|필수. @No__t-0에서 속성을 정의 하는 이름입니다.|

- `Get`

  (선택 사항) 속성이-0 @no__t 표시 되는 경우 필수입니다. 속성의 값을 반환 하는 데 사용 되는 `Get` 속성 프로시저를 시작 합니다.  @No__t-0 문은 [자동으로 구현 된 속성과](../../programming-guide/language-features/procedures/auto-implemented-properties.md)함께 사용 되지 않습니다.

- `statements`

  (선택 사항) @No__t-0 또는 `Set` 프로시저 내에서 실행할 문 블록입니다.

- `End Get`

  @No__t-0 속성 프로시저를 종료 합니다.

- `Set`

  (선택 사항) 속성이-0 @no__t 표시 되는 경우 필수입니다. 속성의 값을 저장 하는 데 사용 되는 `Set` 속성 프로시저를 시작 합니다.  @No__t-0 문은 [자동으로 구현 된 속성과](../../programming-guide/language-features/procedures/auto-implemented-properties.md)함께 사용 되지 않습니다.

- `End Set`

  @No__t-0 속성 프로시저를 종료 합니다.

- `End Property`

  이 속성의 정의를 종료 합니다.

## <a name="remarks"></a>설명

@No__t-0 문은 속성의 선언을 소개 합니다. 속성에는 `Get` 프로시저 (읽기 전용), @no__t 1 프로시저 (쓰기 전용) 또는 두 가지 모두 (읽기/쓰기)를 사용할 수 있습니다. 자동 구현 속성을 사용 하는 경우 `Get` 및 `Set` 프로시저를 생략할 수 있습니다. 자세한 내용은 [자동으로 구현된 속성](../../programming-guide/language-features/procedures/auto-implemented-properties.md)을 참조하세요.

@No__t-0은 클래스 수준 에서만 사용할 수 있습니다. 즉, 속성에 대 한 *선언 컨텍스트* 는 클래스, 구조체, 모듈 또는 인터페이스 여야 하며 소스 파일, 네임 스페이스, 프로시저 또는 블록일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](declaration-contexts-and-default-access-levels.md)을 참조하세요.

기본적으로 속성은 공용 액세스를 사용 합니다. @No__t-0 문에서 액세스 한정자를 사용 하 여 속성의 액세스 수준을 조정 하 고 필요에 따라 속성 프로시저 중 하나를 더 제한적인 액세스 수준으로 조정할 수 있습니다.

Visual Basic는 속성을 할당 하는 동안 매개 변수를 `Set` 프로시저에 전달 합니다. @No__t-0에 대 한 매개 변수를 제공 하지 않으면 IDE (통합 개발 환경)에서 `value` 이라는 암시적 매개 변수를 사용 합니다. 이 매개 변수는 속성에 할당 되는 값을 포함 합니다. 일반적으로이 값을 전용 지역 변수에 저장 하 고 `Get` 프로시저가 호출 될 때마다 반환 합니다.

## <a name="rules"></a>규칙

- **혼합 액세스 수준.** 읽기/쓰기 속성을 정의 하는 경우 선택적으로 `Get` 또는 `Set` 프로시저 중 하나에 대해 다른 액세스 수준을 지정할 수 있습니다. 이 작업을 수행 하는 경우 프로시저 액세스 수준이 속성의 액세스 수준 보다 더 제한적 이어야 합니다. 예를 들어 속성이-0 @no__t로 선언 된 경우-2 @no__t-@no__t 2 @no__t 프로시저를 선언할 수 있습니다.

  @No__t-0 또는 `WriteOnly` 속성을 정의 하는 경우, 단일 속성 프로시저 (`Get` 또는 `Set`)는 모든 속성을 나타냅니다. 속성에 대해 두 개의 액세스 수준을 설정 하므로 프로시저에 대해 다른 액세스 수준을 선언할 수 없습니다.

- **반환 형식입니다.** @No__t-0 문은 반환 하는 값의 데이터 형식을 선언할 수 있습니다. 모든 데이터 형식 또는 열거형, 구조체, 클래스 또는 인터페이스의 이름을 지정할 수 있습니다.

  @No__t-0을 지정 하지 않을 경우 속성은-1 @no__t 반환 합니다.

- **구현이.** 이 속성에서 `Implements` 키워드를 사용 하는 경우 포함 하는 클래스 또는 구조체에 `Class` 또는 `Structure` 문 바로 뒤에 `Implements` 문이 있어야 합니다. @No__t-0 문은 `implementslist`에 지정 된 각 인터페이스를 포함 해야 합니다. 그러나 인터페이스가 @no__t (`definedname`)를 정의 하는 이름은이 속성의 이름과 같을 필요가 없습니다 (`name`).

## <a name="behavior"></a>동작

- **속성 프로시저에서 반환** @No__t-0 또는 `Set` 프로시저가 호출 코드에 반환 되 면 호출 된 문 다음에 오는 문으로 계속 실행 됩니다.

  @No__t-0 및 `Return` 문은 속성 프로시저에서 즉각적인 종료를 발생 시킵니다. @No__t-0 및 `Return` 문은 프로시저의 어디에 나 나타날 수 있으며, `Exit Property` 및 `Return` 문을 혼합할 수 있습니다.

- **반환 값입니다.** @No__t-0 프로시저에서 값을 반환 하려면 속성 이름에 값을 할당 하거나 `Return` 문에 포함할 수 있습니다. 다음 예에서는 반환 값을 속성 이름 `quoteForTheDay`에 할당 한 다음 `Exit Property` 문을 사용 하 여를 반환 합니다.

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#28)]

  값을 `name`에 할당 하지 않고 `Exit Property`을 사용 하는 경우 `Get` 프로시저는 속성의 데이터 형식에 대 한 기본값을 반환 합니다.

  @No__t-0 문은 `Get` 프로시저 반환 값을 할당 하 고 프로시저를 종료 합니다. 다음 예제에서는이를 보여 줍니다.

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#29)]

## <a name="example"></a>예제

다음 예제에서는 클래스의 속성을 선언 합니다.

[!code-vb[VbVbalrStatements#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#51)]

## <a name="see-also"></a>참조

- [자동으로 구현된 속성](../../programming-guide/language-features/procedures/auto-implemented-properties.md)
- [개체 및 클래스](../../programming-guide/language-features/objects-and-classes/index.md)
- [Get 문](get-statement.md)
- [Set 문](set-statement.md)
- [매개 변수 목록](parameter-list.md)
- [Default](../modifiers/default.md)
