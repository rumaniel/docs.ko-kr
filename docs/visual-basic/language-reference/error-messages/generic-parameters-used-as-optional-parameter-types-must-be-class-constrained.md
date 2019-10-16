---
title: 선택적 매개 변수 형식으로 사용된 제네릭 매개 변수에는 클래스 제약 조건이 있어야 합니다.
ms.date: 07/20/2015
f1_keywords:
- vbc32124
- bc32124
helpviewer_keywords:
- BC32124
ms.assetid: 55aa8b2a-9ce3-4620-a710-2f9b0feb6143
ms.openlocfilehash: 11cf4f8d9457ebff385a601786dc97334f274324
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662067"
---
# <a name="generic-parameters-used-as-optional-parameter-types-must-be-class-constrained"></a>선택적 매개 변수 형식으로 사용된 제네릭 매개 변수에는 클래스 제약 조건이 있어야 합니다.
프로시저는 참조 형식에 구속 되지 않은 형식 매개 변수를 사용 하는 선택적 매개 변수를 사용 하 여 선언 됩니다.  
  
 항상 각 선택적 매개 변수에 기본값을 제공 해야 합니다. 선택적 값 이어야 합니다 매개 변수는 참조 형식의 경우 `Nothing`은 참조 형식에 대 한 올바른 값이 있습니다. 그러나 매개 변수 값 형식의 경우 해당 형식을 Visual Basic에서 미리 정의 된 기본 데이터 형식 이어야 합니다. 사용자 정의 구조체와 같은 복합 값 형식에 유효한 기본값이 없는 때문입니다.  
  
 선택적 매개 변수의 형식 매개 변수를 사용 하는 경우에 유효한 기본값이 사용 하 여 값 형식의 방지 하려면 참조 형식의 임을 보장 해야 합니다. 즉, 형식 매개 변수를 사용 하 여 제한 해야 합니다는 `Class` 키워드 또는 특정 클래스의 이름입니다.  
  
 **오류 ID:** BC32124  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 형식 매개 변수는 참조 형식에 적용할 제한 또는 선택적 매개 변수를 사용 하지 마세요.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 제네릭 형식](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)
- [형식 목록](../../../visual-basic/language-reference/statements/type-list.md)
- [Class 문](../../../visual-basic/language-reference/statements/class-statement.md)
- [선택적 매개 변수](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)
- [구조체](../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [Nothing](../../../visual-basic/language-reference/nothing.md)
