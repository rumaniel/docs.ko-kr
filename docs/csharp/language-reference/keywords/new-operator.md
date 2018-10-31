---
title: new 연산자(C# 참조)
ms.date: 03/15/2018
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: 362217b247bd2ab7a2eec2f86cbaaf1a0652a3ad
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48839607"
---
# <a name="new-operator-c-reference"></a>new 연산자(C# 참조)

개체를 만들고 생성자를 호출하는 데 사용됩니다. 예:

```csharp
Class1 obj  = new Class1();
```

무명 형식의 인스턴스를 만드는 데에도 사용됩니다.

```csharp
var query = from cust in customers
            select new { Name = cust.Name, Address = cust.PrimaryAddress };
```

또한 `new` 연산자는 값 형식에 대한 기본 생성자를 호출하는 데 사용됩니다. 예:

```csharp
int i = new int();
```

앞의 문에서 `i`는 `int` 형식의 기본값인 `0`으로 초기화됩니다. 이 문은 다음과 동일한 효과가 있습니다.

```csharp
int i = 0;
```

기본값의 전체 목록은 [기본값 표](default-values-table.md)를 참조하세요.

모든 값 형식에 암시적으로 공용 기본 생성자가 있기 때문에 [struct](struct.md)에 대한 기본 생성자를 선언하면 오류가 발생합니다. 구조체 형식에서 매개 변수가 있는 생성자를 선언하여 해당 초기 값을 설정할 수 있지만, 이 작업은 기본값이 아닌 값이 필요한 경우에만 요구됩니다.

구조체와 같은 값 유형 객체와 클래스와 같은 참조 유형 객체는 모두 자동으로 삭제되지만, 값 유형 객체는 포함된 컨텍스트가 제거될 때 삭제되는 반면에 참조 유형 객체는 마지막 참조가 삭제된 후 지정되지 않은 시간에 가비지 수집기에 의해 제거됩니다. 파일 핸들이나 네트워크 연결과 같은 리소스를 포함하는 유형의 경우에는 결정적 정리를 사용하여 포함된 리소스가 가능한 빨리 릴리스되도록 하는 것이 좋습니다. 자세한 내용은 [using 문](using-statement.md)을 참조하세요.

`new` 연산자를 오버로드할 수 없습니다.

`new` 연산자가 메모리 할당에 실패할 경우 <xref:System.OutOfMemoryException> 예외를 throw합니다.

## <a name="example"></a>예

다음 예제에서는 `new` 연산자를 사용하여 `struct` 개체 및 클래스 개체가 생성 및 초기화된 다음 값이 할당됩니다. 기본값과 할당된 값이 표시됩니다.

[!code-csharp[csrefKeywordsOperator#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#7)]

예제에서는 문자열의 기본값이 `null`이므로 표시되지 않습니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../language-reference/index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [연산자 키워드](operator-keywords.md)
- [new](new.md)
- [익명 형식](../../programming-guide/classes-and-structs/anonymous-types.md)