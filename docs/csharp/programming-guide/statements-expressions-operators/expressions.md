---
title: 식 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 05/11/2017
helpviewer_keywords:
- expressions [C#]
- C# language, expressions
ms.assetid: c7d8feb0-0e58-4f94-8bf6-4d070550a832
ms.openlocfilehash: 1a0e94f40a9dc861b32e6a1c12935faadda9921b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69921803"
---
# <a name="expressions-c-programming-guide"></a>식(C# 프로그래밍 가이드)

‘식’은 단일 값, 개체, 메서드 또는 네임스페이스로 평가될 수 있는 하나 이상의 피연산자 및 0개 이상의 [연산자](../../language-reference/operators/index.md) 시퀀스입니다.  식은 리터럴 값, 메서드 호출, 연산자 및 피연산자, *단순 이름* 등으로 구성될 수 있습니다. 단순한 이름이란 변수, 형식 멤버, 메서드 매개 변수, 네임스페이스 또는 형식의 이름일 수 있습니다.  
  
 식은 다른 식을 매개 변수로 사용하는 연산자 또는 다른 메서드 호출을 매개 변수로 가지는 메서드 호출을 사용할 수 있으므로 간단한 식부터 복잡한 식까지 다양할 수 있습니다. 다음은 식의 두 가지 예입니다.  
  
```csharp  
((x < 10) && ( x > 5)) || ((x > 20) && (x < 25));

System.Convert.ToInt32("35");  
```  
  
## <a name="expression-values"></a>식 값

 식이 사용되는 대부분의 컨텍스트(예: 문 또는 메서드 매개 변수)에서 식은 특정 값으로 평가되어야 합니다. x와 y가 정수이면 `x + y` 식은 숫자 값으로 평가됩니다. `new MyClass()` 식은 `MyClass` 클래스의 새 인스턴스에 대한 참조로 평가됩니다. `myClass.ToString()` 식은 메서드의 반환 형식인 문자열로 평가됩니다. 그러나 네임스페이스 이름은 식으로 분류되지만 값으로 평가되지 않으므로 식의 최종 결과가 될 수 없습니다. 네임스페이스 이름을 메서드 매개 변수에 전달할 수 없거나, 새 식에 사용하거나 변수에 할당할 수 없습니다. 더 큰 식의 하위 식으로만 사용할 수 있습니다. 형식(<xref:System.Type?displayProperty=nameWithType> 개체와 다름), 메서드 그룹 이름(특정 메서드와 다름), 이벤트 [add](../../language-reference/keywords/add.md) 및 [remove](../../language-reference/keywords/remove.md) 접근자의 경우도 마찬가지입니다.  
  
 모든 값에는 연결된 형식이 있습니다. 예를 들어 x와 y가 둘 다 `int` 형식의 변수이면 `x + y` 식의 값도 `int`로 형식화됩니다. 다른 형식의 변수에 값이 할당된 경우 또는 x와 y가 서로 다른 형식인 경우 형식 변환 규칙이 적용됩니다. 이러한 변환이 작동하는 방식에 대한 자세한 내용은 [캐스팅 및 형식 변환](../types/casting-and-type-conversions.md)을 참조하세요.  
  
## <a name="overflows"></a>오버플로

 값이 값 형식의 최대값보다 클 경우 숫자 식에서 오버플로가 발생할 수 있습니다. 자세한 내용은 [Checked 및 Unchecked](../../language-reference/keywords/checked-and-unchecked.md) 및 [명시적 숫자 변환 표](../../language-reference/keywords/explicit-numeric-conversions-table.md)를 참조하세요.  
  
## <a name="operator-precedence-and-associativity"></a>연산자 우선 순위 및 결합성

 식이 평가되는 방식은 결합성 및 연산자 우선 순위 규칙에 의해 제어됩니다. 자세한 내용은 [연산자](../../language-reference/operators/index.md)를 참조하세요.  
  
 할당 식 및 메서드 호출을 제외한 대부분의 식은 문에 포함되어야 합니다. 자세한 내용은 [문](./statements.md)을 참조하세요.  
  
## <a name="literals-and-simple-names"></a>리터럴 및 단순 이름

 가장 간단한 두 가지 형식의 식은 리터럴과 단순 이름입니다. 리터럴은 이름이 없는 상수 값입니다. 예를 들어 다음 코드 예제에서 `5` 및 `"Hello World"`는 둘 다 리터럴 값입니다.  
  
 [!code-csharp[csProgGuideStatements#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#2)]  
  
 리터럴에 대한 자세한 내용은 [형식](../../language-reference/keywords/types.md)을 참조하세요.  
  
 앞의 예제에서 `i` 및 `s`는 둘 다 지역 변수를 식별하는 단순 이름입니다. 이러한 변수가 식에 사용되는 경우 변수 이름은 현재 메모리의 변수 위치에 저장된 값으로 평가됩니다. 이는 다음 예제에서 확인할 수 있습니다.  
  
 [!code-csharp[csProgGuideStatements#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#3)]

## <a name="invocation-expressions"></a>호출 식

 다음 코드 예제에서 `DoWork` 호출은 호출 식입니다.  
  
```csharp
DoWork();  
```  
  
 메서드 호출 시 이름(앞의 예제 참조) 또는 다른 식의 결과와 뒤에 나오는 괄호 및 메서드 매개 변수인 메서드 이름이 필요합니다. 자세한 내용은 [메서드](../classes-and-structs/methods.md)를 참조하세요. 대리자 호출은 괄호 안에 대리자 이름 및 메서드 매개 변수를 사용합니다. 자세한 내용은 [대리자](../delegates/index.md)를 참조하세요. 메서드가 값을 반환하는 경우 메서드 호출 및 대리자 호출은 메서드의 반환 값으로 평가됩니다. void를 반환하는 메서드를 식에 값 대신 사용할 수 없습니다.  

## <a name="query-expressions"></a>쿼리 식

 쿼리 식에는 일반적인 식과 동일한 규칙이 적용됩니다. 자세한 내용은 [LINQ](../../linq/index.md)를 참조하세요.  
  
## <a name="lambda-expressions"></a>람다 식

 람다 식은 이름이 없지만 입력 매개 변수와 여러 개의 문을 사용할 수 있는 "인라인 메서드"를 나타냅니다. 메서드에 인수를 전달하기 위해 LINQ에서 광범위하게 사용됩니다. 람다 식은 사용되는 컨텍스트에 따라 대리자 또는 식 트리로 컴파일됩니다. 자세한 내용은 [람다 식](lambda-expressions.md)을 참조하세요.  
  
## <a name="expression-trees"></a>식 트리

식 트리를 사용하면 식을 데이터 구조로 나타낼 수 있습니다. 쿼리 식을 SQL 데이터베이스 등의 다른 일부 컨텍스트에서 의미 있는 코드로 변환하기 위해 LINQ 공급자에서 광범위하게 사용됩니다. 자세한 내용은 [식 트리(C#)](../concepts/expression-trees/index.md)를 참조하세요.
  
## <a name="expression-body-definitions"></a>식 본문 정의

C#에서는 메서드, 생성자, 종료자, 속성 및 인덱서에 대한 간단한 식 본문 정의를 제공할 수 있도록 하는 *식 본문 멤버*를 지원합니다. 자세한 내용은 [식 본문 멤버](expression-bodied-members.md)를 참조하세요.

## <a name="remarks"></a>설명

 식에서 변수, 개체 속성 또는 개체 인덱서 액세스를 식별할 때마다 해당 항목의 값이 식의 값으로 사용됩니다. 식이 궁극적으로 필수 형식으로 평가되기만 하면 C#에서 값 또는 개체가 필요한 어디에든 식을 배치할 수 있습니다.  

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [식](~/_csharplang/spec/expressions.md) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [연산자](../../language-reference/operators/index.md)
- [메서드](../classes-and-structs/methods.md)
- [대리자](../delegates/index.md)
- [유형](../types/index.md)
- [LINQ](../../linq/index.md)
