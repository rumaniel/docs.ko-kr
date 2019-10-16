---
title: 루프 범위와 단계 변수는 같은 형식으로 변환할 수 없으므로 '<variablename>' 형식을 확대 변환할 수 없습니다.
ms.date: 07/20/2015
f1_keywords:
- bc30982
- vbc30982
helpviewer_keywords:
- BC30982
ms.assetid: 741e85d9-a747-42ad-a1e1-a3f1928aaff5
ms.openlocfilehash: c3086f79fb71693810bc8f14e8c0f493aa1e6515
ms.sourcegitcommit: 463f3f050cecc0b6403e67f19a61f870fb8e7b7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68512716"
---
# <a name="type-of-variablename-cannot-be-inferred-because-the-loop-bounds-and-the-step-variable-do-not-widen-to-the-same-type"></a>루프 범위와\<단계 변수는 같은 형식으로 확장 되지 않으므로 ' variablename > ' 형식을 유추할 수 없습니다.

다음 조건이 true 이기 `For...Next` 때문에 컴파일러가 루프 제어 변수의 데이터 형식을 유추할 수 없는 루프를 작성 했습니다.

- `As` 절을 사용하여 루프 제어 변수의 데이터 형식을 지정하지 않았습니다.

- 루프 범위와 단계 변수에 두 개 이상의 데이터 형식이 포함되어 있습니다.

- 데이터 형식 간에 표준 변환이 없습니다.

 따라서 컴파일러가 루프 제어 변수의 데이터 형식을 유추할 수 없습니다.

 다음 예제에서 단계 변수는 문자이 고 루프 범위는 두 정수입니다. 문자와 정수 사이에는 표준 변환이 없기 때문에이 오류가 보고 됩니다.

```vb
Dim stepVar = "1"c
Dim m = 0
Dim n = 20

' Not valid.
' For i = 1 To 10 Step stepVar
    ' Loop processing
' Next
```

**오류 ID:** BC30982

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

- 필요에 따라 루프 범위와 단계 변수의 형식을 변경 하 여 그 중 하나 이상이 다른 형식으로 확장 될 수 있도록 합니다. 앞의 예제에서는의 `stepVar` 형식을로 `Integer`변경 합니다.

  ```vb
  Dim stepVar = 1
  ```

  또는

  ```vb
  Dim stepVar As Integer = 1
  ```

- 명시적 변환 함수를 사용 하 여 루프 범위와 단계 변수를 적절 한 형식으로 변환 합니다. 앞의 예제에서 `Val` 함수를에 `stepVar`적용 합니다.

  ```vb
  For i = 1 To 10 Step Val(stepVar)
      ' Loop processing
  Next
  ```

## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [암시적 변환과 명시적 변환](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [지역 형식 유추](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Infer 문](../../../visual-basic/language-reference/statements/option-infer-statement.md)
- [형식 변환 함수](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [확대 변환과 축소 변환](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
