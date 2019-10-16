---
title: '방법: 개체 변수를 선언 하 고 개체를에 할당 Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], declaring
- declaring object variables [Visual Basic]
ms.assetid: 2fa77dde-1fb2-439a-80d4-3e9787649fad
ms.openlocfilehash: 71949d50b01d7f252a988e86ca259261086d3b3b
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630878"
---
# <a name="how-to-declare-an-object-variable-and-assign-an-object-to-it-in-visual-basic"></a>방법: 개체 변수를 선언 하 고 개체를에 할당 Visual Basic

[Dim 문에](../../../../visual-basic/language-reference/statements/dim-statement.md)를 지정 `As Object` 하 여 [개체 데이터 형식의](../../../../visual-basic/language-reference/data-types/object-data-type.md) 변수를 선언 합니다. 개체를 대입문 또는 initialization 절에서 등호 (`=`) 뒤에 배치 하 여 개체를 이러한 변수에 할당 합니다.

## <a name="example"></a>예제

다음 예에서는 `Object` 변수를 선언 하 고 여기에 현재 인스턴스를 할당 합니다.

```vb
Dim thisObject As Object
thisObject = "This is an Object"
```

변수를 선언의 일부로 초기화 하 여 선언과 할당을 결합할 수 있습니다. 다음 예제는 앞의 예제와 동일 합니다.

```vb
Dim thisObject As Object= "This is an Object"
```

## <a name="compiling-the-code"></a>코드 컴파일

이 예제에는 다음 사항이 필요합니다.

- <xref:System> 네임스페이스에 대한 참조

- `Dim` 문을 넣을 클래스, 구조체 또는 모듈입니다.

- 대입문을 배치 하는 프로시저입니다.

## <a name="see-also"></a>참고자료

- [변수 선언](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [개체 변수](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [개체 변수 선언](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
- [Object 데이터 형식](../../../../visual-basic/language-reference/data-types/object-data-type.md)
- [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Strict 문](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
