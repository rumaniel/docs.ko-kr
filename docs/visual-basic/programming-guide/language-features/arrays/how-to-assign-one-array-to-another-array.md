---
title: '방법: 한 배열을 다른 배열 (Visual Basic) 할당'
ms.date: 07/20/2015
helpviewer_keywords:
- covariance, arrays
- arrays [Visual Basic], assigning
- arrays [Visual Basic], covariance
ms.assetid: 1ae89ea5-f292-4282-bcfc-e9b06b37fbd5
ms.openlocfilehash: a39888f19e5033a5c6622313fb7451d6463b2f7c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64858877"
---
# <a name="how-to-assign-one-array-to-another-array-visual-basic"></a>방법: 한 배열을 다른 배열 (Visual Basic) 할당

배열 개체 이기 때문에 다른 개체 형식 처럼 대입 문에서 사용할 수 있습니다. 배열 변수 배열 요소 및 차수 및 길이 정보를 구성 하는 데이터 포인터를 보유 하 고 할당만이 포인터를 복사 합니다.

### <a name="to-assign-one-array-to-another-array"></a>한 배열을 다른 배열에 할당 하려면

1. 두 배열의 동일한 차수 (차원 수)과 호환 되는 요소 데이터 형식을 확인 합니다.

2. 소스 배열에서 대상 배열에 할당할 표준 대입문을 사용 합니다. 괄호를 사용 하 여 배열 이름 중 하나를 수행 하지 마세요.

    ```vb
    Dim formArray() As System.Windows.Forms.Form
    Dim controlArray() As System.Windows.Forms.Control
    controlArray = formArray
    ```

다른 배열에 할당 하는 경우 다음 규칙이 적용 됩니다.

- **같은 순위가 결정 됩니다.** 대상 배열의 차수 (차원 수)는 원본 배열의과 같아야 합니다.

  두 배열의 순위 값이 같으면 제공 차원 필요가 없습니다 같아야 합니다. 지정 된 차원의 요소 수가 할당 하는 동안 변경할 수 있습니다.

- **요소 형식입니다.** 두 배열 중 하나 있어야 *참조 형식* 요소 또는 두 배열 있어야 *값 형식* 요소입니다. 자세한 내용은 [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)을 참조하세요.

  - 두 배열의 값 형식 요소의 경우 요소 데이터 형식을 정확 하 게 동일 해야 합니다. 유일한 예외는 배열을 할당할 수 있는 `Enum` 요소를 사용 하는 기본 형식의 배열 `Enum`합니다.

  - 두 배열은 참조 형식 요소에 있으면 원본 요소 형식이 대상 요소 형식에서 파생 되어야 합니다. 이 경우 두 배열의 경우 해당 요소와 동일한 상속 관계 이 이라고 *배열 공변성 (covariance)* 합니다.

컴파일러 오류 위의 규칙 위반 하면 예를 들어 데이터 형식이 호환 되지 않는 경우 또는 순위 같지 보고 합니다. 오류 처리를 할당 하기 전에 배열 호환 되는지 확인 하기 위해 코드에 추가할 수 있습니다. 사용할 수도 있습니다는 [TryCast 연산자](../../../../visual-basic/language-reference/operators/trycast-operator.md) 키워드 예외가 throw 되지 않게 하려는 경우.

## <a name="see-also"></a>참고자료

- [배열](../../../../visual-basic/programming-guide/language-features/arrays/index.md)
- [배열 문제 해결](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)
- [Enum 문](../../../../visual-basic/language-reference/statements/enum-statement.md)
- [배열 규칙](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)
