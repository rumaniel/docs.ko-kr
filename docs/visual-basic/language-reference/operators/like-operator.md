---
title: Like 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 795ecc2e80d57af29ccd50c50d2dd209c6425e40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701130"
---
# <a name="like-operator-visual-basic"></a>Like 연산자(Visual Basic)
문자열과 패턴을 비교 합니다.  

> [!IMPORTANT]
> @No__t-0 연산자는 현재 .NET Core 및 .NET Standard 프로젝트에서 지원 되지 않습니다.

## <a name="syntax"></a>구문  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>요소  
 `result`  
 필수. 모든 `Boolean` 변수입니다. 결과는 `string`이 `pattern`를 충족 하는지 여부를 나타내는 0 @no__t 값입니다.  
  
 `string`  
 필수. 임의의 `String` 식입니다.  
  
 `pattern`  
 필수. "주의"에 설명 된 패턴 일치 규칙을 따르는 `String` 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0의 값이 `pattern`에 포함 된 패턴을 충족 하는 경우 `result`는-3 @no__t. 문자열이 패턴을 충족 하지 않는 경우 `result`은-1 @no__t. @No__t-0과 `pattern`이 모두 빈 문자열이 면 결과는-2 @no__t 됩니다.  
  
## <a name="comparison-method"></a>비교 방법  
 @No__t-0 연산자의 동작은 [Option Compare 문에](../../../visual-basic/language-reference/statements/option-compare-statement.md)따라 달라 집니다. 각 소스 파일에 대 한 기본 문자열 비교 메서드는 `Option Compare Binary`입니다.  
  
## <a name="pattern-options"></a>패턴 옵션  
 기본 제공 패턴 일치는 문자열 비교를 위한 다양 한 도구를 제공 합니다. 패턴 일치 기능을 사용 하면 `string`의 각 문자를 특정 문자, 와일드 카드 문자, 문자 목록 또는 문자 범위에 대해 일치 시킬 수 있습니다. 다음 표에서는 `pattern`에서 허용 되는 문자 및 일치 하는 문자를 보여 줍니다.  
  
|@No__t의 문자-0|@No__t의 일치-0|  
|-----------------------------|-------------------------|  
|`?`|단일 문자|  
|`*`|0 개 이상의 문자|  
|`#`|임의의 단일 숫자 (0-9)|  
|`[charlist]`|@No__t의 단일 문자-0|  
|`[!charlist]`|@No__t에 없는 모든 단일 문자-0|  
  
## <a name="character-lists"></a>문자 목록  
 대괄호 (`[ ]`)로 묶인 하나 이상의 문자 (`charlist`) 그룹을 사용 하 여 `string`의 단일 문자를 일치 시키고, 숫자를 포함 하 여 거의 모든 문자 코드를 포함할 수 있습니다.  
  
 @No__t-1의 시작 부분에서 느낌표 (`!`)는 `charlist`의 문자를 제외한 문자를 `string`에서 찾을 수 있으면 일치가 수행 됨을 의미 합니다. 대괄호 외부에서 사용 하는 경우 느낌표는 자체와 일치 합니다.  
  
## <a name="special-characters"></a>특수 문자  
 특수 문자 왼쪽 대괄호 (`[`), 물음표 (`?`), 숫자 기호 (`#`) 및 별표 (`*`)를 일치 시키려면 대괄호로 묶습니다. 오른쪽 대괄호 (`]`)는 자신을 일치 시키기 위해 그룹 내에서 사용할 수 없지만 그룹 외부에서 개별 문자로 사용할 수 있습니다.  
  
 문자 시퀀스 `[]`은 길이가 0 인 문자열 (`""`)로 간주 됩니다. 그러나 대괄호로 묶은 문자 목록의 일부일 수는 없습니다. @No__t-0의 위치에 문자 그룹 중 하나가 포함 되어 있거나 문자가 없는지를 확인 하려는 경우에는 `Like`을 두 번 사용할 수 있습니다. 예는 [방법: 문자열을 @ no__t-0 패턴과 일치 시킵니다.  
  
## <a name="character-ranges"></a>문자 범위  
 하이픈 (`–`)을 사용 하 여 범위의 하 한 및 상한을 구분 하면-1 @no__t는 문자 범위를 지정할 수 있습니다. 예를 들어 `string`의 해당 문자 위치에 `A` – `Z` 사이에 있는 문자가 포함 된 경우 의 해당 문자 위치에 일치 하는 항목이 있으면 일치 항목이 반환 되 고, `[!H–L]`는 해당 문자 위치에 범위 `H` – `L`입니다.  
  
 문자 범위를 지정 하는 경우 오름차순 정렬 순서로 표시 되어야 합니다. 따라서 `[A–Z]`은 유효한 패턴 이지만 `[Z–A]`은 그렇지 않습니다.  
  
### <a name="multiple-character-ranges"></a>여러 문자 범위  
 동일한 문자 위치에 여러 범위를 지정 하려면 구분 기호 없이 동일한 대괄호 안에 배치 합니다. 예를 들어 `string` @no__t의 해당 문자 위치에 `A` – `C`의 범위 또는-4 – `Z` 범위의 문자가 포함 된 경우-0은 일치 항목을 반환 합니다.  
  
### <a name="usage-of-the-hyphen"></a>하이픈 사용  
 하이픈 (`–`)은 시작 부분 (느낌표 뒤에) 또는 `charlist`의 끝에 표시 될 수 있습니다. 다른 위치에서 하이픈은 하이픈 양쪽의 문자로 구분 되는 문자 범위를 식별 합니다.  
  
## <a name="collating-sequence"></a>데이터 정렬 순서  
 지정 된 범위의 의미는 런타임에 문자 순서에 따라 달라 지 며, `Option Compare` 및 코드를 실행 하는 시스템의 로캘 설정에 따라 결정 됩니다. @No__t-0 `[A–E]`은 `A`, `B`, `C`, `D`, `E`과 일치 합니다. @No__t-0 `[A–E]`은 `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, 0, 1, 2, 3과 일치 합니다. 범위는 `Ê` 또는 `ê`과 일치 하지 않습니다.  
  
## <a name="digraph-characters"></a>D i g 문자  
 일부 언어에는 두 개의 개별 문자를 나타내는 영문자가 있습니다. 예를 들어 여러 언어에서 `æ` 문자를 사용 하 여 문자 `a`을 나타내고 `e`를 함께 표시 합니다. @No__t-0 연산자는 단일 d i g 문자 및 두 개의 개별 문자가 동일 하다는 것을 인식 합니다.  
  
 D i g 문자를 사용 하는 언어가 시스템 로캘 설정에 지정 된 경우 `pattern` 또는 `string`의 단일 d i g 문자가 다른 문자열의 두 문자 시퀀스와 일치 합니다. 마찬가지로 `pattern`에서 대괄호 (자체, 목록 또는 범위)로 묶인 d i g 문자는 `string`에서 해당 하는 두 문자 시퀀스와 일치 합니다.  
  
## <a name="overloading"></a>오버로딩  
 연산자를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체의 동작을 다시 정의할 수 있습니다. `Like` 코드가 이러한 클래스 또는 구조체에서이 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 이 예제에서는 `Like` 연산자를 사용 하 여 문자열을 다양 한 패턴과 비교 합니다. 결과는 각 문자열이 패턴을 충족 하는지 여부를 나타내는 0 @no__t 변수로 이동 합니다.  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>참조

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [비교 연산자](../../../visual-basic/language-reference/operators/comparison-operators.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [연산자 및 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [방법: @ No__t 패턴에 대해 문자열 일치
