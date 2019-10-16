---
title: 런타임에 동적으로 조건자 필터 지정(C#의 LINQ)
description: C#에서 LINQ를 사용하여 런타임에 동적으로 조건자 필터를 지정하는 방법을 알아봅니다.
ms.date: 12/01/2016
ms.assetid: 90238470-0767-497c-916c-52d0d16845e0
ms.openlocfilehash: 314be8f98b9ff014f14bef11a1f3581eff8574b4
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857738"
---
# <a name="dynamically-specify-predicate-filters-at-runtime"></a>런타임에 동적으로 조건자 필터 지정

경우에 따라 `where` 절의 소스 요소에 적용해야 하는 조건자 수를 런타임할 때까지 알 수 없습니다. 다음 예제와 같이 여러 조건자 필터를 동적으로 지정하는 한 가지 방법은 <xref:System.Linq.Enumerable.Contains%2A> 메서드를 사용하는 것입니다. 이 예제는 두 가지 방법으로 구성됩니다. 먼저 프로그램에서 제공되는 값을 필터링하여 프로젝트를 실행합니다. 그런 다음 런타임에 제공된 입력을 사용하여 프로젝트를 다시 실행합니다.

## <a name="to-filter-by-using-the-contains-method"></a>Contains 메서드를 사용하여 필터링하려면

1. 새 콘솔 애플리케이션을 열고 이름을 `PredicateFilters`로 지정합니다.

2. [개체의 컬렉션 쿼리](query-a-collection-of-objects.md)에서 `StudentClass` 클래스를 복사하여 `Program` 클래스 아래의 `PredicateFilters` 네임스페이스에 붙여 넣습니다. `StudentClass`는 `Student` 개체 목록을 제공합니다.

3. `StudentClass`에서 `Main` 메서드를 주석으로 처리합니다.

4. `Program` 클래스를 다음 코드로 바꿉니다.

     [!code-csharp[csProgGuideLINQ#26](~/samples/snippets/csharp/concepts/linq/how-to-dynamically-specify-predicate-filters-at-runtime_1.cs)]

5. `ids`의 선언 아래에서 `DynamicPredicates` 클래스의 `Main` 메서드에 다음 줄을 추가합니다.

     ```csharp
     QueryById(ids);
     ```

6. 프로젝트를 실행합니다.

7. 다음 출력이 콘솔 창에 표시됩니다.

     Garcia: 114

     O'Donnell: 112

     Omelchenko: 111

8. 다음 단계로 프로젝트를 다시 실행합니다. 이번에는 `ids` 배열 대신 런타임에 입력된 입력을 사용합니다. `Main` 메서드에서 `QueryByID(ids)`를 `QueryByID(args)`로 변경합니다.

9. 명령줄 인수 `122 117 120 115`를 사용하여 프로젝트를 실행합니다. 프로젝트가 실행되면 해당 값은 `Main` 메서드의 매개 변수인 `args`의 요소가 됩니다.

10. 다음 출력이 콘솔 창에 표시됩니다.

     Adams: 120

     Feng: 117

     Garcia: 115

     Tucker: 122

## <a name="to-filter-by-using-a-switch-statement"></a>switch 문을 사용하여 필터링하려면

1. `switch` 문을 사용하여 미리 결정된 대체 쿼리 중에서 선택할 수 있습니다. 다음 예제에서 `studentQuery`는 런타임에 지정되는 성적 수준 또는 학년에 따라 다른 `where` 절을 사용합니다.

2. 다음 메서드를 복사하여 `DynamicPredicates` 클래스에 붙여 넣습니다.

     [!code-csharp[csProgGuideLINQ#27](~/samples/snippets/csharp/concepts/linq//how-to-dynamically-specify-predicate-filters-at-runtime_2.cs)]

3. `Main` 메서드에서 `QueryByID` 호출을 `QueryByYear(args[0])` 호출로 바꿔 `args` 배열의 첫 번째 요소를 인수로 전송합니다.

4. 1에서 4 사이의 정수 값인 명령줄 인수를 사용하여 프로젝트를 실행합니다.

## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)](index.md)
- [where 절](../language-reference/keywords/where-clause.md)
