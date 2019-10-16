---
title: 제네릭 형식(제네릭) 개요
description: 제네릭이 실제 데이터 형식에 커밋하지 않고 형식이 안전한 데이터 구조를 정의할 수 있게 해주는 코드 템플릿으로 사용되는 방법을 알아봅니다.
author: kuhlenh
ms.author: wiwagn
ms.date: 10/09/2018
ms.openlocfilehash: 3c1181f5be717f328ae906c6009fc8a34b904c89
ms.sourcegitcommit: 7156c0b9e4ce4ce5ecf48ce3d925403b638b680c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58465427"
---
# <a name="generic-types-overview"></a>제네릭 형식 개요

개발자는 암시적이든 명시적이든 .NET에서 항상 제네릭을 사용합니다. .NET에서 LINQ를 사용할 때 <xref:System.Collections.Generic.IEnumerable%601>로 작업하고 있다는 것을 알아차리셨나요? 또는 Entity Framework를 사용하여 데이터베이스에 통신하기 위한 "제네릭 리포지토리"의 온라인 샘플을 본 적이 있다면 대부분의 메서드가 IQueryable\<T>를 반환하는 것을 보셨나요? 이러한 예제에서 **T**가 무엇이고 왜 사용되는지 궁금하게 여겼을 수도 있습니다.

.NET Framework 2.0에서 처음 소개된 **제네릭**은 기본적으로 개발자가 실제 데이터 형식에 커밋하지 않고 [형식이 안전한](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hbzz1a9a(v=vs.100)) 데이터 구조를 정의할 수 있게 해주는 “코드 템플릿”입니다. 예를 들어 <xref:System.Collections.Generic.List%601>는 `List<int>`, `List<string>` 또는 `List<Person>`과 같은 모든 형식으로 선언하고 사용할 수 있는 [제네릭 컬렉션](xref:System.Collections.Generic)입니다.

제네릭이 유용한 이유를 이해하려면 제네릭을 추가하기 전과 이후의 특정 클래스인 <xref:System.Collections.ArrayList>를 살펴보아야 합니다. .NET Framework 1.0에서 `ArrayList` 요소는 <xref:System.Object> 형식이었습니다. 이는 추가된 모든 요소가 자동으로 `Object`로 변환되었음을 의미합니다. 목록에서 요소를 읽을 때 동일한 작업이 수행됩니다. [boxing 및 unboxing](../csharp/programming-guide/types/boxing-and-unboxing.md)이라고 하는 이 프로세스는 성능에 영향을 줍니다. 그러나 이보다 더 중요한 사항은 컴파일 시간에 목록에 있는 데이터 형식을 확인할 방법이 없다는 것입니다. 이 때문에 손상되기 쉬운 일부 코드가 발생합니다. 제네릭은 목록의 각 인스턴스에 포함될 데이터 형식을 정의하여 이 문제를 해결합니다. 예를 들어 `List<int>`에는 정수만 추가하고 `List<Person>`에는 사용자만 추가하면 됩니다.

또한 제네릭은 런타임에 사용할 수 있습니다. 즉, 런타임에서 사용 중 데이터 구조의 형식을 알고 메모리에 보다 효율적으로 저장할 수 있습니다.

다음 예제에는 런타임에 데이터 구조 형식을 알고 있을 경우의 효율성을 보여 주는 작은 프로그램이 있습니다.

```csharp
  using System;
  using System.Collections;
  using System.Collections.Generic;
  using System.Diagnostics;

  namespace GenericsExample {
    class Program {
      static void Main(string[] args) {
        //generic list
        List<int> ListGeneric = new List<int> { 5, 9, 1, 4 };
        //non-generic list
        ArrayList ListNonGeneric = new ArrayList { 5, 9, 1, 4 };
        // timer for generic list sort
        Stopwatch s = Stopwatch.StartNew();
        ListGeneric.Sort();
        s.Stop();
        Console.WriteLine($"Generic Sort: {ListGeneric}  \n Time taken: {s.Elapsed.TotalMilliseconds}ms");

        //timer for non-generic list sort
        Stopwatch s2 = Stopwatch.StartNew();
        ListNonGeneric.Sort();
        s2.Stop();
        Console.WriteLine($"Non-Generic Sort: {ListNonGeneric}  \n Time taken: {s2.Elapsed.TotalMilliseconds}ms");
        Console.ReadLine();
      }
    }
  }
```

이 프로그램은 다음과 비슷한 출력을 생성합니다.

```console
Generic Sort: System.Collections.Generic.List`1[System.Int32]
 Time taken: 0.0034ms
Non-Generic Sort: System.Collections.ArrayList
 Time taken: 0.2592ms
```

여기서 알 수 있는 첫 번째 사항은 제네릭 목록의 정렬 속도가 제네릭이 아닌 목록보다 훨씬 빠르다는 것입니다. 제네릭 목록의 형식은 고유 형식([System.Int32])인 반면 제네릭이 아닌 목록의 형식은 일반 형식이라는 것도 발견했을 수 있습니다. 제네릭 `List<int>`는 <xref:System.Int32> 형식임을 런타임에서 알고 있기 때문에 메모리의 기본 정수 배열에 목록 요소를 저장할 수 있는 반면, 제네릭이 아닌 `ArrayList`는 각 목록 요소를 개체로 캐스트해야 합니다. 이 예제에 나와 있는 대로 추가 캐스트는 시간이 걸리며 목록 정렬 속도가 느려집니다.

런타임에서 제네릭 형식을 알고 있을 경우의 추가적인 이점은 향상된 디버깅 환경입니다. C#에서 제네릭을 디버그하는 경우 데이터 구조의 각 요소가 어떤 형식인지 알고 있습니다. 제네릭이 없었다면 각 요소의 형식을 알 수 없었을 것입니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드 - 제네릭](../../docs/csharp/programming-guide/generics/index.md)
