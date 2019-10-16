---
title: 프로젝트 수준의 Imports '<qualifiedelementname>'에 지정된 네임스페이스 또는 형식에 public 멤버가 없거나 해당 네임스페이스 또는 형식을 찾을 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc40057
- bc40057
helpviewer_keywords:
- BC40057
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
ms.openlocfilehash: 105fa8da838938d13022c210c1f65cdafd251003
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61918309"
---
# <a name="namespace-or-type-specified-in-the-project-level-imports-qualifiedelementname-doesnt-contain-any-public-member-or-cannot-be-found"></a>프로젝트 수준의 Imports'에 지정 된 Namespace 또는 형식을\<qualifiedelementname >' public 멤버가 없거나 찾을 수 없습니다
프로젝트 수준의 Imports'에 지정 된 Namespace 또는 형식을\<qualifiedelementname >' public 멤버가 없거나 찾을 수 없습니다. 네임 스페이스 또는 형식 정의 되어 있고 하나 이상의 public 멤버를 포함 하는지 확인 합니다. 별칭 이름에는 다른 별칭 포함 되어 있지 않은지 확인 하십시오.  
  
 프로젝트 가져오기 속성을 포함 하는 요소를 찾을 수 없습니다를 정의 하지 않습니다 지정 `Public` 멤버입니다.  
  
 A *요소가 포함 된* 네임 스페이스, 클래스, 구조체, 모듈, 인터페이스 또는 열거형 일 수 있습니다. 요소를 포함 하는 변수, 프로시저 또는 다른 요소를 포함 하는 등의 멤버를 포함합니다.  
  
 가져오기의 목적은 이러한를 한정할 필요 없이 네임 스페이스 또는 형식 멤버에 액세스 하기 위해 코드를 허용 하도록 합니다. 프로젝트 네임 스페이스 또는 형식에 대 한 참조를 추가 해야 할 수 있습니다. 자세한 내용은 "를 포함 하는 요소 가져오기"를 참조 하세요 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)합니다.  
  
 컴파일러는 포함 하는 지정 된 요소를 찾을 수 없으면 사용 하는 참조를 확인할 수 없습니다. 요소를 찾습니다 있지만 요소는 노출 하지 않는 경우 `Public` 멤버 다음 참조가 없는 성공할 수 있습니다. 두 경우 모두에서 요소를 가져오는 의미가 없습니다.  
  
 사용할 합니다 **프로젝트 디자이너** 가져올 요소를 지정 합니다. 사용 합니다 **가져온 네임 스페이스** 섹션을 **참조** 페이지. 가져올 수 있습니다는 **프로젝트 디자이너** 두 번 클릭 합니다 **My Project** 에서 아이콘 **솔루션 탐색기**.  
  
 **오류 ID:** BC40057  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 열기는 **프로젝트 디자이너** 으로 전환 합니다 **참조** 페이지입니다.  
  
2. 에 **가져온 네임 스페이스** 섹션을 포함 하는 요소를 프로젝트에서 액세스할 수 있는지 확인 합니다.  
  
3. 포함 하는 요소가 하나 이상 노출 확인 `Public` 멤버입니다.  
  
## <a name="see-also"></a>참고자료

- [프로젝트 디자이너, 참조 페이지(Visual Basic)](/visualstudio/ide/reference/references-page-project-designer-visual-basic)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
- [공용](../../../visual-basic/language-reference/modifiers/public.md)
- [Visual Basic의 네임 스페이스](../../../visual-basic/programming-guide/program-structure/namespaces.md)
- [선언된 요소 참조](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
