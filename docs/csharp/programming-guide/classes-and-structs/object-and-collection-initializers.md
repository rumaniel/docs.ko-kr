---
title: 개체 및 컬렉션 이니셜라이저 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 12/19/2018
helpviewer_keywords:
- object initializers [C#]
- collection initializers [C#]
ms.assetid: c58f3db5-d7d4-4651-bd2d-5a3a97357f61
ms.openlocfilehash: f6977fa6c5a8909d6108a5ccfc140b89a4fdd5a4
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596568"
---
# <a name="object-and-collection-initializers-c-programming-guide"></a>개체 및 컬렉션 이니셜라이저(C# 프로그래밍 가이드)

C#을 사용하면 개체 또는 컬렉션을 인스턴스화하고 단일 명령문에서 멤버 할당을 수행할 수 있습니다.

## <a name="object-initializers"></a>개체 이니셜라이저

개체 이니셜라이저를 사용하면 명시적으로 생성자를 호출한 다음 할당문 줄을 추가하지 않고도 생성 시 개체의 모든 액세스 가능한 필드나 속성에 값을 할당할 수 있습니다. 개체 이니셜라이저 구문을 사용하면 생성자의 인수를 지정하거나 인수(및 괄호 구문)를 생략할 수 있습니다.  다음 예제에서는 명명된 형식인 `Cat`로 개체 이니셜라이저를 사용하는 방법과 매개 변수가 없는 생성자를 호출하는 방법을 보여 줍니다. `Cat` 클래스의 자동 구현된 속성 사용을 확인합니다. 자세한 내용은 [자동으로 구현된 속성](auto-implemented-properties.md)을 참조하세요.  
  
[!code-csharp[ObjectInitializer1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#CatDeclaration)]  
[!code-csharp[ObjectInitializer1a](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ObjectPropertyInitialization)]  
 
개체 이니셜라이저 구문을 사용하여 인스턴스를 만들 수 있으며, 만들고 나면 새로 만든 개체와 할당된 해당 속성이 할당의 변수에 할당됩니다.

C# 6부터 객체 이니셜라이저는 필드 및 속성을 할당하는 것 외에 인덱서를 설정할 수도 있습니다. 기본적인 `Matrix` 클래스를 예로 들어 보겠습니다.

[!code-csharp[ObjectInitializer2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#MatrixDeclaration)]  

다음 코드를 사용하여 matrix라는 ID를 초기화할 수 있습니다.

[!code-csharp[ObjectInitializer2a](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#MatrixInitialization)]  

액세스 가능한 setter가 포함된 액세스 가능한 인덱서는 인수의 개수나 형식에 관계없이 객체 이니셜라이저에서 식 중 하나로 사용할 수 있습니다. 인덱스 인수는 할당의 왼쪽에 있으며, 값은 식의 오른쪽에 있습니다.  예를 들어 `IndexersExample`에 적절한 인덱서가 있는 경우 이 모든 것이 유효합니다.

```csharp
var thing = new IndexersExample {
    name = "object one",
    [1] = '1',
    [2] = '4',
    [3] = '9',
    Size = Math.PI,
    ['C',4] = "Middle C"
}
```

이전 코드를 컴파일하려면 `IndexersExample` 형식에 다음 멤버가 있어야 합니다.

```csharp
public string name;
public double Size { set { ... }; }
public char this[int i] { set { ... }; }
public string this[char c, int i] {  set { ... }; }
```

## <a name="object-initializers-with-anonymous-types"></a>익명 형식의 개체 이니셜라이저

개체 이니셜라이저는 모든 컨텍스트에서 사용할 수 있지만 특히 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식에 유용합니다. 쿼리 식은 [무명 형식](./anonymous-types.md)을 자주 사용합니다. 이 형식은 다음 선언에 표시된 바와 같이 개체 이니셜라이저를 사용하는 경우에만 초기화될 수 있습니다.  

```csharp
var pet = new { Age = 10, Name = "Fluffy" };  
```

무명 형식을 사용하면 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식의 `select` 절에서 원래 시퀀스의 개체를 값과 모양이 원본과 다를 수 있는 개체로 변환할 수 있습니다. 이 기능은 각 개체의 일부 정보만 시퀀스에 저장하려는 경우에 유용합니다. 다음 예제에서 제품 개체(`p`)는 많은 필드와 메서드를 포함하며, 제품 이름과 단위 가격이 들어 있는 개체 시퀀스만 만들려 한다고 가정합니다.  
  
[!code-csharp[ObjectInitializer3](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#AnonymousUse)]  

이 쿼리를 실행하면 다음 예제와 같이 `productInfos` 문에서 액세스할 수 있는 개체 시퀀스가 `foreach` 변수에 포함됩니다.  

```csharp
foreach(var p in productInfos){...}  
```

새 익명 형식의 각 개체에는 원래 개체의 속성이나 필드와 동일한 이름을 받는 두 개의 public 속성이 있습니다. 익명 형식을 만들 때 필드 이름을 바꿀 수도 있습니다. 다음 예제에서는 `UnitPrice` 필드의 이름을 `Price`로 바꿉니다.  

```csharp
select new {p.ProductName, Price = p.UnitPrice};  
```

## <a name="collection-initializers"></a>컬렉션 이니셜라이저

컬렉션 이니셜라이저를 사용하면 <xref:System.Collections.IEnumerable>을 구현하고 적절한 시그니처가 있는 `Add`를 인스턴스 메서드 또는 확장 메서드로 포함하는 컬렉션 형식을 초기화할 때 하나 이상의 요소 이니셜라이저를 지정할 수 있습니다. 요소 이니셜라이저는 단순한 값, 식 또는 개체 이니셜라이저일 수 있습니다. 컬렉션 이니셜라이저를 사용하면 호출을 여러 번 지정할 필요가 없습니다. 컴파일러가 호출을 자동으로 추가합니다.  
  
다음 예제에서는 두 개의 단순한 컬렉션 이니셜라이저를 보여줍니다.  

```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };  
```

다음 컬렉션 이니셜라이저는 개체 이니셜라이저를 사용하여 앞의 예제에서 정의된 `Cat` 클래스의 개체를 초기화합니다. 개별 개체 이니셜라이저는 괄호로 묶이고 쉼표로 구분됩니다.  
  
[!code-csharp[ListInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ListInitializer)]  
  
컬렉션의 `Add` 메서드에서 허용하는 경우 [null](../../language-reference/keywords/null.md)을 컬렉션 이니셜라이저의 요소로 지정할 수 있습니다.  
  
[!code-csharp[ListInitializerNull](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#ListInitialerWithNull)]  
  
 컬렉션이 읽기/쓰기 인덱싱을 지원하는 경우 인덱싱된 요소를 지정할 수 있습니다.
  
[!code-csharp[DictionaryInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#DictionaryIndexerInitializer)]  

이전 샘플에서는 <xref:System.Collections.Generic.Dictionary%602.Item(%600)>을 호출하여 값을 설정하는 코드를 생성합니다. C# 6부터 다음 구문을 사용하여 사전 및 다른 연관 컨테이너를 초기화할 수 있습니다. 괄호와 할당이 있는 인덱서 구문 대신 여러 값이 있는 개체를 사용합니다.

[!code-csharp[DictionaryAddInitializer](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#DictionaryAddInitializer)]  

이 이니셜라이저 예제에서는 <xref:System.Collections.Generic.Dictionary%602.Add(%600,%601)>를 호출하여 사전에 세 가지 항목을 추가합니다. 연관 컬렉션을 초기화하는 이러한 두 가지 방법은 컴파일러가 생성하는 메서드 호출 때문에 약간 다르게 작동합니다. 두 가지 방법 모두 `Dictionary` 클래스와 함께 작동합니다. 다른 형식은 공용 API에 따라 어느 한 쪽만 지원할 수 있습니다.

## <a name="examples"></a>예제

다음 예제에서는 개체 및 컬렉션 이니셜라이저의 개념을 결합합니다.

[!code-csharp[InitializerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullExample)]  

다음 예제에서는 <xref:System.Collections.IEnumerable>을 구현하고 여러 매개 변수가 있는 `Add` 메서드를 포함하는 개체를 보여줍니다. 이는 `Add` 메서드의 시그니처에 해당하는 목록의 항목당 여러 요소가 있는 컬렉션 이니셜라이저를 사용합니다.

[!code-csharp[InitializerListExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullListExample)]  

다음 예제에 표시된 것처럼 `Add` 메서드는 `params` 키워드를 사용하여 가변적인 인수 개수를 사용할 수 있습니다. 이 예제에서는 인덱스를 사용하여 컬렉션을 초기화하기 위한 인덱서의 사용자 지정 구현도 보여줍니다.

[!code-csharp[InitializerListExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/BasicObjectInitializers.cs#FullDictionaryInitializer)]  

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [LINQ 쿼리 식](../linq-query-expressions/index.md)
- [익명 형식](anonymous-types.md)
