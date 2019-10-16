---
title: LINQ 쿼리 작업의 형식 관계(C#)
ms.date: 07/20/2015
helpviewer_keywords:
- inferring type information [LINQ in C#]
- data sources [LINQ in C#], type relationships
- queries [LINQ in C#], type relationships
- relationships [LINQ in C#]
- type relationships [LINQ in C#]
- variable relationships [LINQ in C#]
- type information inferred [LINQ in C#]
- data transformations [LINQ in C#]
- LINQ [C#], type relationships
ms.assetid: 99118938-d47c-4d7e-bb22-2657a9f95268
ms.openlocfilehash: 42519a74be1bd6934bc7a3304d154321697d128c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591015"
---
# <a name="type-relationships-in-linq-query-operations-c"></a>LINQ 쿼리 작업의 형식 관계(C#)
쿼리를 효과적으로 작성하려면 전체 쿼리 작업의 변수 형식이 모두 어떻게 서로 관련되는지를 이해해야 합니다. 이러한 관계를 이해하면 설명서의 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 샘플 및 코드 예제를 더 쉽게 이해할 수 있습니다. 또한 `var`을 사용하여 변수를 암시적으로 형식화하는 경우 백그라운드에서 발생하는 상황을 이해할 수 있습니다.  
  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 작업은 데이터 소스, 쿼리 자체 및 쿼리 실행에서 강력하게 형식화됩니다. 쿼리의 변수 형식은 데이터 소스의 요소 형식 및 `foreach` 문의 반복 변수 형식과 호환되어야 합니다. 이 강력한 형식화는 사용자가 발견하기 전에 수정될 수 있도록 컴파일 시간에 형식 오류가 catch되도록 합니다.  
  
 이러한 형식 관계를 보여 주기 위해 뒤에 나오는 대부분의 예제에서는 모든 변수에 명시적 형식화를 사용합니다. 마지막 예제에서는 [var](../../../language-reference/keywords/var.md)을 통해 암시적 형식화를 사용하는 경우에도 어떻게 동일한 원칙이 적용되는지를 보여 줍니다.  
  
## <a name="queries-that-do-not-transform-the-source-data"></a>소스 데이터를 변환하지 않는 쿼리  
 다음 그림에서는 데이터 변환을 수행하지 않는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] to Objects 쿼리 작업을 보여 줍니다. 소스에는 문자열 시퀀스가 포함되어 있고, 쿼리 출력도 문자열 시퀀스입니다.  
  
 ![LINQ 쿼리에서 데이터 형식의 관계를 보여 주는 다이어그램](./media/type-relationships-in-linq-query-operations/linq-query-data-type-relation.png)  
  
1. 데이터 소스의 형식 인수에 따라 범위 변수의 형식이 결정됩니다.  
  
2. 선택된 개체의 형식에 따라 쿼리 변수의 형식이 결정됩니다. 여기서 `name`은 문자열입니다. 따라서 쿼리 변수는 `IEnumerable<string>`입니다.  
  
3. 쿼리 변수는 `foreach` 문에서 반복됩니다. 쿼리 변수가 문자열 시퀀스이기 때문에 반복 변수도 문자열입니다.  
  
## <a name="queries-that-transform-the-source-data"></a>소스 데이터를 변환하는 쿼리  
 다음 그림에서는 간단한 데이터 변환을 수행하는 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 쿼리 작업을 보여 줍니다. 쿼리는 `Customer` 개체 시퀀스를 입력으로 사용하고 결과에서 `Name` 속성만 선택합니다. `Name`이 문자열이기 때문에 쿼리에서 출력으로 문자열 시퀀스를 생성합니다.  
  
 ![데이터 형식을 변환하는 쿼리를 보여 주는 다이어그램](./media/type-relationships-in-linq-query-operations/linq-query-transform-data-type.png)  
  
1. 데이터 소스의 형식 인수에 따라 범위 변수의 형식이 결정됩니다.  
  
2. `select` 문은 전체 `Customer` 개체가 아니라 `Name` 속성을 반환합니다. `Name`이 문자열이므로 `custNameQuery`의 형식 인수는 `Customer`가 아니라 `string`입니다.  
  
3. `custNameQuery`가 문자열 시퀀스이므로 `foreach` 루프의 반복 변수도 `string`이어야 합니다.  
  
 다음 그림에서는 약간 더 복잡한 변환을 보여 줍니다. `select` 문은 원래 `Customer` 개체의 두 멤버만 캡처하는 무명 형식을 반환합니다.  
  
 ![데이터 형식을 변환하는 더 복잡한 쿼리를 보여 주는 다이어그램](./media/type-relationships-in-linq-query-operations/linq-complex-query-transform-data-type.png)  
  
1. 데이터 소스의 형식 인수는 항상 쿼리의 범위 변수 형식입니다.  
  
2. `select` 문이 무명 형식을 생성하기 때문에 `var`을 사용하여 쿼리 변수를 암시적으로 형식화해야 합니다.  
  
3. 쿼리 변수의 형식이 암시적이기 때문에 `foreach` 루프의 반복 변수도 암시적이어야 합니다.  
  
## <a name="letting-the-compiler-infer-type-information"></a>컴파일러에서 형식 정보를 유추하도록 허용  
 쿼리 작업의 형식 관계를 이해해야 하지만 컴파일러가 모든 작업을 대신 수행하도록 하는 옵션도 있습니다. [var](../../../language-reference/keywords/var.md) 키워드를 쿼리 작업의 모든 지역 변수에 사용할 수 있습니다. 다음 그림은 앞에서 설명한 예제 번호 2와 유사합니다. 그러나 컴파일러는 쿼리 작업의 각 변수에 대해 강력한 형식을 제공합니다.  
  
 ![암시적 형식의 형식 흐름을 보여 주는 다이어그램](./media/type-relationships-in-linq-query-operations/linq-type-flow-implicit-typing.png)  
  
 `var`에 대한 자세한 내용은 [암시적 형식 지역 변수](../../classes-and-structs/implicitly-typed-local-variables.md)를 참조하세요.  
