---
title: Visual Basic 프로그램의 구조
ms.date: 07/20/2015
helpviewer_keywords:
- conditional compilation [Visual Basic], Visual Basic
- program structure [Visual Basic], Visual Basic
- procedures [Visual Basic], structure
- Visual Basic code, program structure
ms.assetid: ad0c6531-d762-4c77-a700-de16b07b6119
ms.openlocfilehash: 4f4136a2c8fb7ca98ff22aa6a5fc676f30cd1c5d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624307"
---
# <a name="structure-of-a-visual-basic-program"></a>Visual Basic 프로그램의 구조
Visual Basic 프로그램은 표준 구성 요소에서 빌드됩니다. A *솔루션* 하나 이상의 프로젝트를 구성 합니다. A *프로젝트* 에 하나 이상의 어셈블리를 포함할 수 있습니다. 각 *어셈블리* 하나 이상의 소스 파일에서 컴파일됩니다. A *소스 파일* 정의와 클래스, 구조체, 모듈 및 궁극적으로 모든 코드를 포함 하는 인터페이스의 구현을 제공 합니다.  
  
 Visual Basic 프로그램의 이러한 구성 요소에 대 한 자세한 내용은 참조 하세요 [솔루션 및 프로젝트](/visualstudio/ide/solutions-and-projects-in-visual-studio) 하 고 [.net에서 어셈블리](../../../standard/assembly/index.md)합니다.  
  
## <a name="file-level-programming-elements"></a>파일-수준 프로그래밍 요소  
 프로젝트 또는 파일을 시작 하 고 코드 편집기를 열고 올바른 순서에 이미 있는 코드가 표시 됩니다. 모든 코드를 작성할 때는 다음 순서 대로 수행 해야 합니다.  
  
1. `Option` 문  
  
2. `Imports` 문  
  
3. `Namespace` 문 및 네임 스페이스 수준 요소  
  
 문을 다른 순서로 입력 하면 컴파일 오류가 발생할 수 있습니다.  
  
 프로그램에 조건부 컴파일 문에 포함할 수도 있습니다. 이전 시퀀스의 문 함께 소스 파일에서 이러한 중간에 삽입할 수 있습니다.  
  
### <a name="option-statements"></a>문 옵션  
 `Option` 문은 후속 코드, 구문 및 논리 오류를 방지 하기 위해 노력에 대 한 기본 규칙을 구성 합니다. 합니다 [Option Explicit 문](../../../visual-basic/language-reference/statements/option-explicit-statement.md) 모든 변수 선언 하면 되며 확인 철자가 디버깅 시간을 줄입니다. 합니다 [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md) 서로 다른 데이터 형식의 변수 사이 작업할 때 발생할 수 있는 논리 오류 및 데이터 손실을 최소화 하는 데 도움이 됩니다. 합니다 [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md) 서로 기준 방식으로 문자열 비교 지정 해당 `Binary` 또는 `Text` 값입니다.  
  
### <a name="imports-statements"></a>Imports 문  
 포함할 수 있습니다는 [Imports 문 (.NET Namespace 및 형식)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 프로젝트 외부에 정의 된 이름을 가져올 수 있습니다. `Imports` 문 클래스를 한정 하지 않고는 가져온된 네임 스페이스 내에서 정의 된 다른 형식을 참조 하도록 코드를 허용 합니다. 만큼 사용할 수 있습니다 `Imports` 문을 적절 하 게 합니다. 자세한 내용은 [참조 및 Imports 문](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)합니다.  
  
### <a name="namespace-statements"></a>Namespace 문  
 네임 스페이스 도움말 구성 하 고 그룹화 하 고 액세스 하는 편의 위해 프로그래밍 요소를 분류 합니다. 사용할 합니다 [Namespace 문](../../../visual-basic/language-reference/statements/namespace-statement.md) 특정 네임 스페이스 내에서 다음 명령문을 분류 합니다. 자세한 내용은 [Visual Basic의 네임스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)를 참조하세요.  
  
### <a name="conditional-compilation-statements"></a>조건부 컴파일 문은  
 조건부 컴파일 문을 소스 파일의 거의 모든 곳에 나타날 수 있습니다. 특정 조건에 따라 컴파일 시 제외 되거나 포함 된 코드의 일부 문제를 일으킬 있습니다. 이용할 수 있습니다 이러한 응용 프로그램 디버깅에 대 한 조건부 코드 디버깅 모드 에서만 실행 되기 때문입니다. 자세한 내용은 [조건부 컴파일](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)합니다.  
  
## <a name="namespace-level-programming-elements"></a>Namespace 수준 프로그래밍 요소  
 클래스, 구조체 및 모듈 원본 파일의 모든 코드를 포함 합니다. 이들은 *네임 스페이스 수준* 요소 네임 스페이스 내에서 또는 소스 파일 수준에서 표시 될 수 있습니다. 다른 모든 프로그래밍 요소 선언을 포함 됩니다. 인터페이스 요소 서명을 정의 하지만 구현이 제공 하는 모듈 수준에서도 나타납니다. 모듈 수준 요소에 대 한 자세한 내용은 다음을 참조 하세요.  
  
- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)  
  
- [Structure 문](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
- [Module 문](../../../visual-basic/language-reference/statements/module-statement.md)  
  
- [Interface 문](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 네임 스페이스 수준에서 데이터 요소는 열거형 및 대리자입니다.  
  
## <a name="module-level-programming-elements"></a>모듈 수준 프로그래밍 요소  
 프로시저, 연산자, 속성 및 이벤트는 실행 코드 (런타임 시 작업을 수행 하는 문)을 보유할 수 있는 유일한 프로그래밍 요소입니다. 이들은 합니다 *모듈 수준* 프로그램의 요소입니다. 프로시저 수준 요소에 대 한 자세한 내용은 다음을 참조 하세요.  
  
- [Function 문](../../../visual-basic/language-reference/statements/function-statement.md)  
  
- [Sub 문](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
- [Declare 문](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
- [Operator 문](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
- [Property 문](../../../visual-basic/language-reference/statements/property-statement.md)  
  
- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 모듈 수준에서 데이터 요소에는 변수, 상수, 열거형 및 대리자는입니다.  
  
## <a name="procedure-level-programming-elements"></a>프로시저 수준 프로그래밍 요소  
 내용의 대부분 *프로시저 수준* 요소는 프로그램의 런타임 코드를 구성 하는 문을 실행 합니다. 모든 실행 코드는 몇 가지 절차에 있어야 합니다. (`Function`, `Sub`, `Operator`, `Get`를 `Set`를 `AddHandler`를 `RemoveHandler`, `RaiseEvent`). 자세한 내용은 [문](../../../visual-basic/programming-guide/language-features/statements.md)을 참조하세요.  
  
 프로시저 수준에서 데이터 요소는 로컬 변수 및 상수에 제한 됩니다.  
  
## <a name="the-main-procedure"></a>Main 프로시저  
 `Main` 프로시저는 응용 프로그램 로드 되었을 때 실행할 첫 번째 코드입니다. `Main` 시작 지점 및 응용 프로그램에 대 한 전체 제어 사용 됩니다. 네 가지가 있습니다 `Main`:  
  
- `Sub Main()`  
  
- `Sub Main(ByVal cmdArgs() As String)`  
  
- `Function Main() As Integer`  
  
- `Function Main(ByVal cmdArgs() As String) As Integer`  
  
 이 절차의 가장 일반적인 것은 `Sub Main()`합니다. 자세한 내용은 [Visual Basic의 Main 프로시저](../../../visual-basic/programming-guide/program-structure/main-procedure.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 main 프로시저](../../../visual-basic/programming-guide/program-structure/main-procedure.md)
- [Visual Basic 명명 규칙](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
- [Visual Basic 제한 사항](../../../visual-basic/programming-guide/program-structure/limitations.md)
