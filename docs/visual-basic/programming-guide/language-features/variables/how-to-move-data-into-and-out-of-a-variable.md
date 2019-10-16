---
title: '방법: 변수 외부/외부로 데이터 이동 (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], retrieving values
- variables [Visual Basic], storing data
ms.assetid: 93744f46-bf78-4fa0-9640-1de01bc38d9a
ms.openlocfilehash: df55f122c4ea029a383196f8d9684295ac8926aa
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631115"
---
# <a name="how-to-move-data-into-and-out-of-a-variable-visual-basic"></a>방법: 변수 외부/외부로 데이터 이동 (Visual Basic)

변수 이름을 대입문의 왼쪽에 배치 하 여 변수에 값을 저장 합니다.

## <a name="putting-data-in-a-variable"></a>변수에 데이터 배치

#### <a name="to-store-a-value-in-a-variable"></a>변수에 값을 저장 하려면

- 대입문의 왼쪽에 변수 이름을 사용 합니다.

    다음 예에서는 변수의 `alpha`값을 설정 합니다.

    ```vb
    alpha = (beta * 6.27) / (gamma + 2.1)
    ```

    대입문의 오른쪽에 생성 된 값은 변수에 저장 됩니다.

## <a name="getting-data-from-a-variable"></a>변수에서 데이터 가져오기

식에 변수 이름을 포함 하 여 변수의 값을 검색 합니다.

#### <a name="to-retrieve-a-value-from-a-variable"></a>변수에서 값을 검색 하려면

- 식에서 변수 이름을 사용 합니다. 상수 값을 정의 하는 식을 제외 하 고 상수 또는 리터럴을 사용할 수 있는 모든 위치에서 변수를 사용할 수 있습니다.

  \-또는-

- 대입문에서 등호 (`=`) 뒤에 변수 이름을 사용 합니다.

  다음 예에서는 변수의 `startValue` 값을 읽은 다음 식의 변수 `counter` 값을 사용 합니다.

  ```vb
  counter = startValue
  cellValue = (counter + 5) ^ 2
  ```

  변수 값은 상수와 마찬가지로 식에도 관여 하 고 대입문의 왼쪽에 있는 변수나 속성에 저장 됩니다.

## <a name="see-also"></a>참고자료

- [변수](../../../../visual-basic/programming-guide/language-features/variables/index.md)
- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
