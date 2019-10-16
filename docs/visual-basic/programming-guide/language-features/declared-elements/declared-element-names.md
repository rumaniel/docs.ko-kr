---
title: 선언된 요소 이름(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], case sensitivity
- names [Visual Basic], Visual Basic rules
- naming conventions [Visual Basic]
- element names [Visual Basic]
- declared elements [Visual Basic], identifiers
- declarations [Visual Basic], elements
- declared elements [Visual Basic], valid names
- '[] escape characters [Visual Basic]'
- names [Visual Basic], elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- identifiers [Visual Basic], declared elements
- case sensitivity, declared element names
- escape characters [Visual Basic]
- names [Visual Basic], declared elements
- declared elements [Visual Basic], about declared elements
- escaped names [Visual Basic]
- declared elements [Visual Basic], names
- names [Visual Basic], naming conventions
- identifiers [Visual Basic], elements
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
ms.openlocfilehash: 8a1b4869588c8dd030cf6276969063ec99b79e33
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046593"
---
# <a name="declared-element-names-visual-basic"></a>선언된 요소 이름(Visual Basic)
선언 된 모든 요소에는 *식별자*라고도 하는 이름이 있습니다 .이 이름은 코드에서이를 참조 하는 데 사용 됩니다.  
  
## <a name="rules"></a>규칙  
 Visual Basic의 요소 이름은 다음 규칙을 따라야 합니다.  
  
- 알파벳 문자 또는 밑줄 (`_`)로 시작 해야 합니다.  
  
- 영문자, 10 진수 및 밑줄만 포함 해야 합니다.  
  
- 밑줄로 시작 하는 경우 하나 이상의 알파벳 문자 또는 10 진수가 포함 되어야 합니다.  
  
- 길이는 1023 자이 하 여야 합니다.  
  
 1023 문자의 길이 제한은와 `outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement`같이 정규화 된 이름의 전체 문자열에도 적용 됩니다.  
  
 다음 예제에서는 몇 가지 유효한 요소 이름을 보여 줍니다.  
  
 `aB123__45`  
  
 `_567`  
  
 다음 예제에서는 일부 잘못 된 요소 이름을 보여 줍니다. 첫 번째에는 밑줄만 포함 되 고, 두 번째는 10 진수로 시작 하 고, 세 번째에는 잘못 된 문자 ($)가 포함 됩니다.  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
> 밑줄 (`_`)로 시작 하는 요소 이름은 [언어 독립성 및 언어 독립적 구성 요소](../../../../standard/language-independence-and-language-independent-components.md) (cls)의 일부가 아니므로 cls 규격 코드는 이러한 이름을 정의 하는 구성 요소를 사용할 수 없습니다. 그러나 요소 이름에서 다른 위치의 밑줄은 CLS 규격입니다.  
  
### <a name="name-length-guidelines"></a>이름 길이 지침  
 실제로는 요소의 특성을 명확 하 게 식별 하는 동시에 이름을 최대한 짧게 지정 해야 합니다. 이렇게 하면 코드의 가독성을 높이고 줄 길이와 소스 파일 크기를 줄입니다.  
  
 반면에 요소는 요소가 나타내는 내용과 코드에서 사용 하는 방법을 적절 하 게 설명 하지는 않습니다. 이는 코드의 가독성을 높이기 위해 중요 합니다. 다른 사용자가이를 이해 하려고 하거나 사용자가 작성 한 후 오랜 시간을 확인 하는 경우 적절 한 요소 이름을 통해 상당한 시간을 절약할 수 있습니다.  
  
## <a name="escaped-names"></a>이스케이프 된 이름  
 일반적으로 요소 이름은 Visual Basic에 예약 된 키워드 (예: `Case` 또는 `Friend`)와 일치 하지 않아야 합니다. 그러나 대괄호 (`[ ]`)로 묶인 *이스케이프 된 이름을*정의할 수 있습니다. 괄호는 모호성을 제거 하므로 이스케이프 된 이름은 모든 Visual Basic 키워드와 일치할 수 있습니다. 또한 코드에서 나중에 이름을 참조할 때 괄호를 사용 합니다.  
  
 일반적으로 다음과 같은 경우에만 이스케이프 된 이름을 사용 해야 합니다.  
  
- 코드를 이름으로 사용 되는 키워드를 예약 하지 않은 Visual Basic 이전 버전에서 마이그레이션 했습니다. 디스크나  
  
- 지정 된 키워드가 예약 되지 않은 다른 언어로 작성 된 코드로 작업 하 고 있습니다.  
  
 그렇지 않으면 요소의 이름이 키워드와 충돌 하는 경우 요소의 이름을 바꾸는 것을 고려해 야 합니다. IDE (통합 개발 환경)는이 작업을 수행 하는 쉬운 방법을 제공 합니다. 자세한 내용은 [리팩터링](/visualstudio/vb-ide/refactoring-vb)을 참조 하세요.  
  
## <a name="case-sensitivity-in-names"></a>이름에서 대/소문자 구분  
 Visual Basic의 요소 이름은 대/소문자를 구분 하지 않습니다. 즉, 컴파일러에서 알파벳 대/소문자만 다른 두 이름을 비교할 때 동일한 이름으로 해석 합니다. 예를 들어, `ABC` 와 `abc` 는 동일한 선언 요소를 참조하는 것으로 간주합니다.  
  
 그러나 CLR (공용 언어 런타임)에서는 대/소문자를 구분 하는 바인딩을 사용 합니다. 그러므로, 어셈블리나 DLL을 작성하여 다른 어셈블리에서 이를 사용하게 되면 이름의 대/소문자가 구분됩니다. 예를 들어, `ABC`라는 이름의 요소를 포함하는 클래스를 정의하고 다른 어셈블리에서 공용 언어 런타임을 통해 이 클래스를 사용할 경우 해당 어셈블리에서 이 요소를 `ABC`로 참조해야 합니다. 이후에 클래스를 다시 컴파일하고 요소 이름을로 `abc`변경 하는 경우 클래스를 사용 하는 다른 어셈블리에서 해당 요소에 더 이상 액세스할 수 없습니다. 따라서, 어셈블리를 업데이트하여 릴리스하는 경우 공용 요소의 알파벳 대/소문자를 변경하지 않아야 합니다.  
  
## <a name="names-and-locales"></a>이름 및 로캘  
 이름 비교는 로캘과 무관 합니다. 한 로캘에서 두 이름이 일치 하는 경우 모든 로캘에서 일치 하도록 보장 됩니다.  
  
## <a name="see-also"></a>참고자료

- [선언 요소](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)
- [선언 요소의 특징](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [선언된 요소 참조](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [문(C++)](../../../../visual-basic/language-reference/statements/index.md)
