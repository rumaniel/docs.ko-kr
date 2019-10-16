---
title: Object 변수 또는 With 블록 변수가 설정되지 않았습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID91
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
ms.openlocfilehash: 07c215d373e4ac1cbadf82a48b8cb3d90efdbdb4
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70040553"
---
# <a name="object-variable-or-with-block-variable-not-set"></a>Object 변수 또는 With 블록 변수가 설정되지 않았습니다.
잘못 된 개체 변수를 참조 하 고 있습니다.   여러 가지 원인에 의해 이런 오류가 발생할 수 있습니다.

- 형식을 지정 하지 않고 변수가 선언 되었습니다. 형식을 지정 하지 않고 변수를 선언 하는 경우 기본값은 형식 `Object`입니다.

    예를 들어를 사용 하 여 `Dim x` 선언 된 변수는 `Object;` 형식 `Dim x As String` `String`입니다.

    > [!TIP]
    > `Option Strict` 문은 `Object` 형식을 반환 하는 암시적 형식 지정을 허용 하지 않습니다. 형식을 생략 하면 컴파일 타임 오류가 발생 합니다. [Option Strict 문](../../../visual-basic/language-reference/statements/option-strict-statement.md)을 참조 하십시오.

- 로 `Nothing`설정 된 개체를 참조 하려고 합니다.

- 올바르게 선언 되지 않은 배열 변수의 요소에 액세스 하려고 합니다.

    예를 들어로 `products() As String` 선언 된 배열은 배열의 `products(3) = "Widget"`요소를 참조 하려고 할 때 오류를 트리거합니다. 배열에는 요소가 없고 개체로 처리 됩니다.

- 블록이 초기화 되기 전에 `With...End With` 블록 내의 코드에 액세스 하려고 합니다.   문 `With...End With` 진입점을 `With` 실행 하 여 블록을 초기화 해야 합니다.

> [!NOTE]
> 이전 버전의 Visual Basic 또는 VBA에서이 오류는 대신 `Set` 키워드 (`x = "name"` 대신 `Set x = "name"`)를 사용 하지 않고 변수에 값을 할당 하 여 트리거됩니다. Visual Basic .net에서는 더 이상 키워드를사용할수없습니다.`Set`

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

1. 파일 `Option Strict` 의 `On` 시작 부분에 다음 코드를 추가 하 여를로 설정 합니다.

    ```vb
    Option Strict On
    ```

    프로젝트를 실행 하면 형식 없이 지정 된 변수에 대 한 **오류 목록** 컴파일러 오류가 표시 됩니다.

2. 을 사용 `Option Strict`하지 않으려는 경우 코드에서 형식 없이 지정 된 변수 (`Dim x` 대신 `Dim x As String`)를 검색 하 고 원하는 형식을 선언에 추가 합니다.

3. 로 `Nothing`설정 된 개체 변수를 참조 하지 않는지 확인 합니다.  코드에서 키워드 `Nothing`를 검색 하 고 개체를 참조 한 후에 야로 `Nothing` 설정 되도록 코드를 수정 합니다.

4. 액세스 하기 전에 배열 변수가 치수화 되었는지 확인 합니다. 처음에 배열을 만들 때 차원을 할당 하거나 (`Dim x(5) As String` `Dim x() As String`대신 `ReDim` ) 키워드를 사용 하 여 배열 크기를 설정 하 고 처음 액세스할 수 있습니다.

5. 문 진입점을 `With` `With` 실행 하 여 블록이 초기화 되었는지 확인 합니다.

## <a name="see-also"></a>참고자료

- [개체 변수 선언](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [ReDim 문](../../../visual-basic/language-reference/statements/redim-statement.md)
- [With...End With 문](../../../visual-basic/language-reference/statements/with-end-with-statement.md)
