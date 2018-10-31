---
title: Expression Trees
description: .NET Core의 식 트리에 대해 알아본 다음 이를 사용하여 검사, 수정 및 실행할 수 있는 구조로 코드를 나타내는 방법을 알아봅니다.
ms.date: 06/20/2016
ms.assetid: aceb4719-0d5a-4b19-b01f-b51063bcc54f
ms.openlocfilehash: 56509f1eb0f2bdca8a8f3a51df958d42e95af6f4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50190738"
---
# <a name="expression-trees"></a>Expression Trees

LINQ를 사용했다면 `Func` 형식이 API 집합의 일부인 풍부한 라이브러리 경험이 있는 것입니다. LINQ에 익숙하지 않은 경우 [LINQ 자습서](linq/index.md) 및 [람다 식](lambda-expressions.md)에 대한 자습서를 먼저 읽어보는 것이 좋습니다. *식 트리*에서는 함수인 인수를 사용하는 보다 풍부한 조작을 제공합니다.

LINQ 쿼리를 만들 때 일반적으로 람다 식을 사용하여 함수 인수를 작성합니다. 일반적인 LINQ 쿼리에서 이러한 함수 인수는 컴파일러가 만드는 대리자로 변환됩니다. 

보다 풍부한 조작을 원하는 경우 *식 트리*를 사용해야 합니다.
식 트리는 검사, 수정 또는 실행할 수 있는 구조로 코드를 나타냅니다. 이러한 도구는 런타임에 코드를 조작할 수 있는 강력한 기능을 제공합니다. 실행 중인 알고리즘을 검사하고 새 기능을 삽입하는 코드를 작성할 수 있습니다. 보다 고급 시나리오에서는 실행 중인 알고리즘을 수정하고 C# 식을 다른 형태로 변환하여 다른 환경에서 실행할 수도 있습니다.

식 트리를 사용하는 코드를 이미 작성했을 수 있습니다. Entity Framework의 LINQ API는 LINQ 쿼리 식 패턴에 대한 인수로 식 트리를 허용합니다.
따라서 [Entity Framework](/ef/)는 C#에서 작성된 쿼리를 데이터베이스 엔진에서 실행되는 SQL로 변환할 수 있습니다. 또 다른 예로 널리 사용되는 .NET 모의 프레임워크인 [Moq](https://github.com/Moq/moq)가 있습니다.

이 자습서의 나머지 섹션에서는 식 트리의 정의를 살펴보고, 식 트리를 지원하는 프레임워크 클래스를 검사하며, 식 트리로 작업하는 방법을 보여 줍니다. 식 트리를 읽는 방법, 식 트리를 만드는 방법, 수정된 식 트리를 만드는 방법, 식 트리로 표시되는 코드를 실행하는 방법 등을 알아봅니다. 자습서를 읽고 나면 이러한 구조를 사용하여 풍부한 적응 알고리즘을 만들 수 있습니다.

1. [식 트리 설명](expression-trees-explained.md)

    *식 트리*의 구조와 개념을 이해합니다.
    
2. [식 트리를 지원하는 프레임워크 형식](expression-classes.md)
    
    식 트리를 정의하고 조작하는 구조 및 클래스에 대해 알아봅니다.
    
3. [식 실행](expression-trees-execution.md)

    람다 식으로 표시되는 식 트리를 대리자로 변환하고 결과 대리자를 실행하는 방법을 알아봅니다.

4. [식 해석](expression-trees-interpreting.md)

    *식 트리*를 트래버스하고 검사하여 식 트리가 나타내는 코드를 이해하는 방법을 알아봅니다.

5. [식 작성](expression-trees-building.md)

    식 트리에 대한 노드를 생성하고 식 트리를 작성하는 방법을 알아봅니다.

6. [식 변환](expression-trees-translating.md)

    식 트리의 수정된 복사본을 작성하거나 식 트리를 다른 형식으로 변환하는 방법을 알아봅니다.

7. [요약](expression-trees-summary.md)

    식 트리에 대한 정보를 검토합니다.
    
