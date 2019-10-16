---
title: 배열 범위는 형식 지정자에 사용할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- vbc30638
- bc30638
helpviewer_keywords:
- BC30638
ms.assetid: 93b654f4-70fa-4a48-baed-ffae42075550
ms.openlocfilehash: 951f710160ae1023671773c21c73946f5ae94c2b
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512758"
---
# <a name="array-bounds-cannot-appear-in-type-specifiers"></a>배열 범위는 형식 지정자에 사용할 수 없습니다.

배열 크기는 데이터 형식 지정자의 일부로 선언할 수 없습니다.

**오류 ID:** BC30638

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

- 다음 예제와 같이 배열 크기를 형식 뒤에 배치 하는 대신 변수 이름 바로 뒤에 배열 크기를 지정 합니다.

  ```vb
  Dim Array(8) As Integer
  ```

- 다음 예제에 표시 된 것과 같이 배열을 정의 하 고 원하는 수의 요소를 사용 하 여 초기화 합니다.

  ```vb
  Dim Array2() As Integer = New Integer(8) {}
  ```

## <a name="see-also"></a>참고자료

- [배열(C++)](../../../visual-basic/programming-guide/language-features/arrays/index.md)
