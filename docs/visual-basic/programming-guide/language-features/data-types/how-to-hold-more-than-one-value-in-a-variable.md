---
title: '방법: 변수에 값을 두 개 이상 저장 합니다 (Visual Basic).'
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic], composite data types
- composite types [Visual Basic]
- composite data types [Visual Basic]
- data types [Visual Basic], composite
- arrays [Visual Basic], composite data types
- structures [Visual Basic], composite data types
- arrays [Visual Basic], compilation errors
- types [Visual Basic], composite
ms.assetid: 5fe0e558-aac2-4a40-b7f2-7cfea7336917
ms.openlocfilehash: 8d07a34a98303f9d220dba0a3c955120b421340e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71054191"
---
# <a name="how-to-hold-more-than-one-value-in-a-variable-visual-basic"></a>방법: 변수에 값을 두 개 이상 저장 합니다 (Visual Basic).

*복합 데이터 형식*으로 선언 하는 경우 변수에 두 개 이상의 값이 포함 됩니다.

[복합 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md) 에는 구조체, 배열 및 클래스가 포함 됩니다. 복합 데이터 형식의 변수는 기본 데이터 형식과 기타 복합 형식의 조합을 포함할 수 있습니다. 구조체와 클래스는 데이터 뿐만 아니라 코드도 포함할 수 있습니다.

## <a name="to-hold-more-than-one-value-in-a-variable"></a>변수에 두 개 이상의 값을 저장 하려면

1. 변수에 사용 하려는 복합 데이터 형식을 결정 합니다.

2. 복합 데이터 형식이 아직 정의 되지 않은 경우 변수에서 사용할 수 있도록 정의 합니다.

    - Structure [문을](../../../../visual-basic/language-reference/statements/structure-statement.md)사용 하 여 구조체를 정의 합니다.

    - [Dim 문으로](../../../../visual-basic/language-reference/statements/dim-statement.md)배열을 정의 합니다.

    - [클래스 문으로](../../../../visual-basic/language-reference/statements/class-statement.md)클래스를 정의 합니다.

3. `Dim` 문을 사용 하 여 변수를 선언 합니다.

4. 변수 이름 뒤에 `As` 절을 추가 합니다.

5. `As` 키워드 뒤에 적절 한 복합 데이터 형식의 이름을 추가 합니다.

## <a name="see-also"></a>참고자료

- [데이터 형식](../../../../visual-basic/language-reference/data-types/index.md)
- [형식 문자](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
- [복합 데이터 형식](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)
- [구조체](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)
- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [개체 및 클래스](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
