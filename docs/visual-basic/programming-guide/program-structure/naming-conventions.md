---
title: Visual Basic 명명 규칙
ms.date: 07/20/2015
helpviewer_keywords:
- names [Visual Basic], Visual Basic rules
- naming conventions
- naming conventions [Visual Basic], Visual Basic
- Visual Basic code, naming conventions
- conventions [Visual Basic], Visual Basic coding
- names [Visual Basic], naming conventions
- naming conventions [Visual Basic], classes
ms.assetid: 164949a4-2a7c-4736-9d82-9c3078e2e56c
ms.openlocfilehash: ce8d4c5ede0d722d2c1768b9c2cd7929f296114e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651246"
---
# <a name="visual-basic-naming-conventions"></a>Visual Basic 명명 규칙
Visual Basic 응용 프로그램의 요소에 이름을 지정할 때 해당 이름의 첫 번째 문자는 영문자 또는 밑줄 이어야 합니다. 단, 밑줄로 시작 하는 이름에 맞지 않는 합니다 [Language Independence and Language-independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS).  
  
 다음 제안 이름에 적용 됩니다.  
  
- 와 같이 대문자를 사용 하 여 이름에 별도 각 단어를 시작할 `FindLastRecord` 고 `RedrawMyForm`입니다.  
  
- 함수 및 메서드 이름이 동사를 사용 하 여 시작 `InitNameArray` 또는 `CloseDialog`합니다.  
  
- 시작 클래스, 구조체, 모듈 및 명사가 포함 된 속성 이름으로 `EmployeeName` 또는 `CarAccessory`합니다.  
  
- 인터페이스 이름 접두사를 사용 하 여 시작 "I", 명사 또는 명사구를 같은 뒤 `IComponent`, 또는 형용사와 같은 인터페이스의 동작을 설명 하는 `IPersistable`합니다. 약어에 혼동을 일으킬 수 있으므로 약어를 제한적으로 사용 및 밑줄을 사용 하지 않는 수행 합니다.  
  
- 이벤트 처리기 이름은 뒤에 이벤트의 형식을 설명 하는 명사를 사용 하 여 시작 된 "`EventHandler`"접미사를와 같이"`MouseEventHandler`"입니다.  
  
- 이벤트 인수 클래스 이름에 포함 된 "`EventArgs`" 접미사.  
  
- 있으면 이벤트의 개념을 "before" 또는 "after"의 접미사를 사용 또는 과거 시제 에서처럼 "`ControlAdd`"또는"`ControlAdded`"입니다.  
  
- Long 또는 자주 사용 되는 용어에 대 한 예를 들어, "HTML", "Hypertext Markup Language" 대신 이름 길이 적합 하 게 되도록 약어를 사용 합니다. 일반적으로 변수 이름은 32 자 보다 긴 낮은 해상도로 설정 된 모니터에서 읽기 어렵습니다. 또한 프로그램 약어 전체 응용 프로그램 전체에서 일관 되는지 확인 합니다. 임의로 "HTML"과 "Hypertext Markup Language" 프로젝트에서 전환 혼란이 발생할 수 있습니다.  
  
- 내부 범위에서 외부 범위에서 이름으로 동일한 이름을 사용 하지 마십시오. 잘못 된 변수에 액세스 하는 경우 오류가 발생할 수 있습니다. 변수와 이름이 같은 키워드 간에 충돌이 발생할 경우 적절 한 형식 라이브러리를 사용 하 여 앞에 키워드를 식별 해야 합니다. 예를 들어 호출 이라는 변수가 있다고 `Date`, 내장 함수를 사용할 수 있습니다 `Date` 함수를 호출 하 여만 <xref:System.DateTime.Date%2A?displayProperty=nameWithType>합니다.  
  
## <a name="see-also"></a>참고자료

- [코드에서 요소 이름으로 사용되는 키워드](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)
- [Me, My, MyBase 및 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
- [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [프로그램 구조 및 코드 규칙](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)
- [Visual Basic 언어 참조](../../../visual-basic/language-reference/index.md)
