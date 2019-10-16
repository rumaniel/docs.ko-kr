---
title: Declare 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Declare
- vb.Lib
- vb.Any
helpviewer_keywords:
- Lib keyword [Visual Basic]
- declaring procedures [Visual Basic], Declare statement
- functions [Visual Basic], function procedures
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- procedures [Visual Basic], external
- Alias keyword [Visual Basic]
- external references [Visual Basic], Visual Basic
- DLLs, declaring procedures
- Declare statement [Visual Basic]
- declarations [Visual Basic], external
- Visual Basic code, Function procedures
- As keyword [Visual Basic], in Declare statement
- resources [Visual Basic], declaring
- Public keyword [Visual Basic], Declare statement
- platform invoke, Visual Basic external references
- Sub procedures [Visual Basic], declarations
- APIs, declaring API functions
- Visual Basic code, Sub procedures
- Function procedures [Visual Basic], declaring
ms.assetid: d3f21fb0-b804-4c99-97ed-583b23894cf1
ms.openlocfilehash: e839fe14c360229fbe0350fd7878c7a844056e8b
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005097"
---
# <a name="declare-statement"></a>Declare Statement

외부 파일에 구현 된 프로시저에 대 한 참조를 선언 합니다.

## <a name="syntax"></a>구문

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Sub ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ]
' -or-
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _
Declare [ charsetmodifier ] [ Function ] name Lib "libname" _
[ Alias "aliasname" ] [ ([ parameterlist ]) ] [ As returntype ]
```

## <a name="parts"></a>요소

|용어|정의|
|---|---|
|`attributelist`|(선택 사항) [특성 목록](../../../visual-basic/language-reference/statements/attribute-list.md)을 참조 하십시오.|
|`accessmodifier`|(선택 사항) 다음 중 하나일 수 있습니다.<br /><br /> -   [공용](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [보호](../../../visual-basic/language-reference/modifiers/protected.md) 됨<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [개인](../../../visual-basic/language-reference/modifiers/private.md)<br />- 으로[보호 된 Friend](../../language-reference/modifiers/protected-friend.md)<br />- [개인 보호](../../language-reference/modifiers/private-protected.md) 됨<br /><br /> [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)을 참조하세요.|
|`Shadows`|(선택 사항) [그림자](../../../visual-basic/language-reference/modifiers/shadows.md)를 참조 하세요.|
|`charsetmodifier`|(선택 사항) 문자 집합 및 파일 검색 정보를 지정 합니다. 다음 중 하나일 수 있습니다.<br /><br /> -   [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md) (기본값)<br />-   [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)<br />-   [자동](../../../visual-basic/language-reference/modifiers/auto.md)|
|`Sub`|선택 사항 이지만 `Sub` 또는 `Function` 중 하나 여야 합니다. 외부 프로시저에서 값을 반환 하지 않음을 나타냅니다.|
|`Function`|선택 사항 이지만 `Sub` 또는 `Function` 중 하나 여야 합니다. 외부 프로시저에서 값을 반환 함을 나타냅니다.|
|`name`|필수. 이 외부 참조의 이름입니다. 자세한 내용은 [선언 된 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조 하세요.|
|`Lib`|필수. 외부 프로시저를 포함 하는 외부 파일 (DLL 또는 코드 리소스)을 식별 하는 `Lib` 절을 소개 합니다.|
|`libname`|필수. 선언 된 프로시저를 포함 하는 파일의 이름입니다.|
|`Alias`|(선택 사항) 선언 되는 프로시저를 파일 내에서 `name`에 지정 된 이름으로 식별할 수 없음을 나타냅니다. @No__t-0에서 해당 id를 지정 합니다.|
|`aliasname`|@No__t-0 키워드를 사용 하는 경우 필수 사항입니다. 다음 두 가지 방법 중 하나로 프로시저를 식별 하는 문자열입니다.<br /><br /> 파일 내에 있는 프로시저의 진입점 이름 (따옴표 포함) (`""`)<br /><br /> 또는<br /><br /> 숫자 기호 (`#`) 다음에 해당 파일 내에서 프로시저 진입점의 서 수 번호를 지정 하는 정수입니다.|
|`parameterlist`|프로시저에서 매개 변수를 사용 하는 경우 필수입니다. [매개 변수 목록](../../../visual-basic/language-reference/statements/parameter-list.md)을 참조 하세요.|
|`returntype`|@No__t-0이 지정 되 고 `Option Strict`이 `On` 인 경우 필수 사항입니다. 프로시저에서 반환 하는 값의 데이터 형식입니다.|

## <a name="remarks"></a>설명

프로젝트 외부의 파일 (예: DLL 또는 코드 리소스)에 정의 된 프로시저를 호출 해야 하는 경우가 있습니다. 이 작업을 수행 하는 경우 Visual Basic 컴파일러는 프로시저를 올바르게 호출 하는 데 필요한 정보 (프로시저의 위치, 식별 방법, 호출 시퀀스 및 반환 형식, 사용 하는 문자열 문자 집합)에 액세스할 수 없습니다. @No__t-0 문은 외부 프로시저에 대 한 참조를 만들고이 필요한 정보를 제공 합니다.

`Declare`는 모듈 수준에서만 사용할 수 있습니다. 즉, 외부 참조의 *선언 컨텍스트* 는 클래스, 구조체 또는 모듈 이어야 하며 소스 파일, 네임 스페이스, 인터페이스, 프로시저 또는 블록일 수 없습니다. 자세한 내용은 [선언 컨텍스트 및 기본 액세스 수준](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)을 참조하세요.

외부 참조의 기본값은 [공용](../../../visual-basic/language-reference/modifiers/public.md) 액세스입니다. 액세스 한정자를 사용 하 여 액세스 수준을 조정할 수 있습니다.

## <a name="rules"></a>규칙

- **특성.** 외부 참조에 특성을 적용할 수 있습니다. 적용 하는 모든 특성은 외부 파일이 아닌 프로젝트에만 적용 됩니다.

- **수정자.** 외부 프로시저는 암시적으로 [공유](../../../visual-basic/language-reference/modifiers/shared.md)됩니다. 외부 참조를 선언할 때 `Shared` 키워드를 사용할 수 없으며, 공유 상태를 변경할 수 없습니다.

  외부 프로시저는 재정의, 인터페이스 멤버 구현 또는 이벤트 처리에 참여할 수 없습니다. 따라서 `Declare` 문에서 `Overrides`, `Overridable`, `NotOverridable`, `MustOverride`, `Handles` 키워드를 사용할 수 없습니다.

- **외부 프로시저 이름입니다.** 이 외부 참조는 외부 파일 (`aliasname`) 내의 프로시저의 진입점 이름과 동일한 이름 (`name`)을 제공할 필요가 없습니다. @No__t-0 절을 사용 하 여 진입점 이름을 지정할 수 있습니다. 이는 외부 프로시저의 이름이 Visual Basic 예약 된 한정자, 변수, 프로시저 또는 동일한 범위에 있는 다른 프로그래밍 요소와 동일한 경우에 유용할 수 있습니다.

  > [!NOTE]
  > 대부분의 Dll에서 진입점 이름은 대/소문자를 구분 합니다.

- **외부 프로시저 번호입니다.** 또는 `Alias` 절을 사용 하 여 외부 파일의 내보내기 테이블에 있는 진입점의 서 수를 지정할 수 있습니다. 이 작업을 수행 하려면 숫자 기호 (`#`)로 `aliasname`을 시작 합니다. 이는 Visual Basic에서 외부 프로시저 이름에 있는 모든 문자를 사용할 수 없거나 외부 파일이 프로시저를 이름 없이 내보내는 경우에 유용 합니다.

## <a name="data-type-rules"></a>데이터 형식 규칙

- **매개 변수 데이터 형식입니다.** @No__t-0 `On` 인 경우에는 `parameterlist`에서 각 매개 변수의 데이터 형식을 지정 해야 합니다. 모든 데이터 형식 또는 열거형, 구조체, 클래스 또는 인터페이스의 이름일 수 있습니다. @No__t-0에서 `As` 절을 사용 하 여 각 매개 변수에 전달할 인수의 데이터 형식을 지정 합니다.

  > [!NOTE]
  > .NET Framework에 대해 외부 프로시저가 작성 되지 않은 경우에는 데이터 형식이 일치 하는지 주의 해야 합니다. 예를 들어 `Integer` 매개 변수 (Visual Basic 6.0의 16 비트)를 사용 하 여 Visual Basic 6.0 프로시저에 대 한 외부 참조를 선언 하는 경우 `Declare` 문에서 해당 인수를 `Short`로 식별 해야 합니다. Visual Basic. 마찬가지로 `Long` Visual Basic 6.0에는 서로 다른 데이터 너비가 있고 `Date`은 다르게 구현 됩니다.

- **반환 데이터 형식입니다.** 외부 프로시저가 `Function`이 고 `Option Strict`이 `On` 인 경우 호출 코드에 반환 되는 값의 데이터 형식을 지정 해야 합니다. 모든 데이터 형식 또는 열거형, 구조체, 클래스 또는 인터페이스의 이름일 수 있습니다.

  > [!NOTE]
  > Visual Basic 컴파일러는 데이터 형식이 외부 프로시저의 데이터 형식과 호환 되는지 확인 하지 않습니다. 일치 하지 않는 경우 공용 언어 런타임은 런타임에 <xref:System.Runtime.InteropServices.MarshalDirectiveException> 예외를 생성 합니다.

- **기본 데이터 형식입니다.** @No__t-0이-1 @no__t `parameterlist`에 매개 변수의 데이터 형식을 지정 하지 않으면 Visual Basic 컴파일러는 해당 인수를 [Object 데이터 형식](../../../visual-basic/language-reference/data-types/object-data-type.md)으로 변환 합니다. 마찬가지로 `returntype`을 지정 하지 않으면 컴파일러는 반환 데이터 형식을-1로 @no__t 합니다.

  > [!NOTE]
  > 다른 플랫폼에서 작성 되었을 수 있는 외부 프로시저를 처리 하기 때문에 데이터 형식에 대 한 가정을 하거나 기본값을 허용 하는 것이 위험 합니다. 모든 매개 변수의 데이터 형식과 반환 값 (있는 경우)을 지정 하는 것이 훨씬 안전 합니다. 또한 코드의 가독성을 향상 시킵니다.

## <a name="behavior"></a>동작

- **범위.** 외부 참조는 해당 클래스, 구조체 또는 모듈 전체의 범위에 있습니다.

- **수명.** 외부 참조는 선언 된 클래스, 구조체 또는 모듈과 수명이 동일 합니다.

- **외부 프로시저를 호출 합니다.** @No__t-0 또는 `Sub` 프로시저를 호출 하는 것과 같은 방식으로 외부 프로시저를 호출 합니다 .이 프로시저는 값을 반환 하는 경우 식에서 사용 하 고, 값을 반환 하지 않을 경우 [Call 문에](../../../visual-basic/language-reference/statements/call-statement.md) 지정 하 여 호출 합니다.

  @No__t-1 문에서 `parameterlist`에 지정 된 대로 외부 프로시저에 인수를 정확 하 게 전달 합니다. 매개 변수가 외부 파일에서 원래 선언 된 방식을 고려 하지 마십시오. 마찬가지로 반환 값이 있는 경우에는 `Declare` 문에서 `returntype`에 지정 된 그대로 사용 합니다.

- **문자 집합.** @No__t에서 Visual Basic 외부 프로시저를 호출할 때 문자열을 마샬링하는 방법을 지정할 수 있습니다. @No__t-0 한정자는 모든 문자열을 ANSI 값으로 마샬링할 Visual Basic를 전달 하 고, `Unicode` 한정자는 모든 문자열을 유니코드 값으로 마샬링하는 것으로 지시 합니다. @No__t-0 한정자는 외부 참조 `name`을 기반으로 .NET Framework 규칙에 따라 문자열을 마샬링할 Visual Basic 하거나 지정 된 경우 `aliasname`를 전달 합니다. 기본값은 `Ansi`입니다.

  `charsetmodifier`은 Visual Basic 외부 파일 내에서 외부 프로시저를 조회 하는 방법을 지정 하기도 합니다. `Ansi` 및 @no__t-Visual Basic 1을 사용 하 여 검색 중에 이름을 수정 하지 않고 조회 합니다. `Auto`은 런타임 플랫폼의 기본 문자 집합을 결정 하 고 다음과 같이 외부 프로시저 이름을 수정할 수 Visual Basic를 지시 합니다.

  - ANSI 플랫폼 (예: Windows 95, Windows 98 또는 Windows Millennium Edition)에서 먼저 이름 수정 없이 외부 프로시저를 조회 합니다. 실패 하면 외부 프로시저 이름의 끝에 "A"를 추가 하 고 다시 확인 합니다.

  - Windows NT, Windows 2000 또는 Windows XP와 같은 유니코드 플랫폼에서는 먼저 이름 수정 없이 외부 프로시저를 조회 합니다. 실패 하면 외부 프로시저 이름의 끝에 "W"를 추가 하 고 다시 확인 합니다.

- **방법일.** Visual Basic는 PInvoke (.NET Framework *platform invoke* ) 메커니즘을 사용 하 여 외부 프로시저를 확인 하 고 액세스 합니다. @No__t-0 문과 <xref:System.Runtime.InteropServices.DllImportAttribute> 클래스는 모두이 메커니즘을 자동으로 사용 하 고 PInvoke에 대 한 지식이 필요 하지 않습니다. 자세한 내용은 [연습: Windows Api @ no__t-0을 호출 합니다.

> [!IMPORTANT]
> 외부 프로시저가 CLR (공용 언어 런타임) 외부에서 실행 되는 경우 *관리 되지 않는 코드*입니다. 이러한 프로시저 (예: Windows API 함수 또는 COM 메서드)를 호출 하는 경우 응용 프로그램을 보안 위험에 노출 시킬 수 있습니다. 자세한 내용은 [비관리 코드에 대 한 보안 코딩 지침](../../../framework/security/secure-coding-guidelines-for-unmanaged-code.md)을 참조 하세요.

## <a name="example"></a>예제

다음 예에서는 현재 사용자 이름을 반환 하는 `Function` 프로시저에 대 한 외부 참조를 선언 합니다. 그런 다음 `getUser` 프로시저의 일부로 `GetUserNameA` 외부 프로시저를 호출 합니다.

[!code-vb[VbVbalrStatements#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#15)]

## <a name="example"></a>예제

@No__t-0은 비관리 코드에서 함수를 사용 하는 대체 방법을 제공 합니다. 다음 예에서는 `Declare` 문을 사용 하지 않고 가져온 함수를 선언 합니다.

[!code-vb[VbVbalrStatements#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#16)]

[!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]

## <a name="see-also"></a>참조

- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [Imports 문(.NET 네임스페이스 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [AddressOf 연산자](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)
- [매개 변수 목록](../../../visual-basic/language-reference/statements/parameter-list.md)
- [Call 문](../../../visual-basic/language-reference/statements/call-statement.md)
- [연습: Windows API 호출](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
