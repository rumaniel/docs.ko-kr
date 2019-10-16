---
title: 루트 네임스페이스 <namespacename>의 이름 <fullnamespacename>이(가) CLS 규격이 아닙니다.
ms.date: 07/20/2015
f1_keywords:
- vbc40039
- bc40039
helpviewer_keywords:
- BC40039
ms.assetid: c5bd5914-ae71-416a-8bed-f76f644f78be
ms.openlocfilehash: faed46eaf21513945ef4eb0c76d36780e960d380
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592033"
---
# <a name="name-namespacename-in-the-root-namespace-fullnamespacename-is-not-cls-compliant"></a>이름을 \<namespacename > 루트 네임 스페이스에서 \<fullnamespacename > CLS 규격이 아님
로 어셈블리 표시 됩니다 `<CLSCompliant(True)>`에 요소의 루트 네임 스페이스 이름 밑줄로 시작 하지만 (`_`).  
  
 프로그래밍 요소를 호환 되어야 하지만 하나 이상의 밑줄을 포함할 수 있습니다 합니다 [Language Independence and Language-independent Components](../../../standard/language-independence-and-language-independent-components.md) (CLS) 시작 하지 않아야 밑줄을 사용 하 여 합니다. [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)을 참조하세요.  
  
 <xref:System.CLSCompliantAttribute>를 프로그래밍 요소에 적용하는 경우 특성의 `isCompliant` 매개 변수를 `True` 또는 `False`로 설정하여 준수 여부를 나타냅니다. 이 매개 변수에는 기본값이 없으며 값을 제공해야 합니다.  
  
 요소에 <xref:System.CLSCompliantAttribute> 를 적용하지 않으면 비규격인 것으로 간주됩니다.  
  
 이 메시지는 기본적으로 경고입니다. 경고를 숨기거나 오류로 처리하는 방법에 대한 자세한 내용은 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)을 참조하세요.  
  
 **오류 ID:** BC40039  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- CLS 규격에 필요한 경우 밑줄로 시작 하는 해당 요소 중 루트 네임 스페이스 이름을 변경 합니다.  
  
- 네임 스페이스 이름을 그대로 유지 하는, 필요한 경우 다음 제거 합니다 <xref:System.CLSCompliantAttribute> 어셈블리에서로 표시 하거나 `<CLSCompliant(False)>`합니다.  
  
## <a name="see-also"></a>참고자료

- [Namespace 문](../../../visual-basic/language-reference/statements/namespace-statement.md)
- [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [/rootnamespace](../../../visual-basic/reference/command-line-compiler/rootnamespace.md)
- [프로젝트 디자이너, 응용 프로그램 페이지(Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)
- [선언 요소 이름](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)
- [Visual Basic 명명 규칙](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
