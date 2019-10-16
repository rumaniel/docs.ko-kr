---
title: 중간 구체화(C#)
ms.date: 07/20/2015
ms.assetid: 7922d38f-5044-41cf-8e17-7173d6553a5e
ms.openlocfilehash: af1eb7df7da02d8e72fc102cda4ee5f329dc7974
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253156"
---
# <a name="intermediate-materialization-c"></a>중간 구체화(C#)
주의하지 않으면 특정한 경우에 쿼리에서 컬렉션을 미리 구체화하여 애플리케이션의 메모리와 성능 프로필을 크게 변경할 수 있습니다. 일부 표준 쿼리 연산자는 단일 요소를 생성하기 전에 소스 컬렉션을 구체화합니다. 예를 들어, <xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType>는 먼저 전체 소스 컬렉션을 반복한 다음 모든 항목을 정렬하고 마지막으로 첫 번째 항목을 생성합니다. 즉, 정렬된 컬렉션의 첫 번째 항목을 가져오는 것은 비용이 많이 들며 그 다음에 나오는 각 항목에는 비용이 많이 들지 않습니다. 이는 적절한 동작입니다. 해당 쿼리 연산자가 다른 방식으로 작업하는 것은 불가능할 것입니다.  
  
## <a name="example"></a>예  
 이 예제에서는 이전 예제를 변경합니다. `AppendString` 메서드는 소스를 반복하기 전에 <xref:System.Linq.Enumerable.ToList%2A>을 호출합니다. 이로 인해 구체화가 수행됩니다.  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        // the following statement materializes the source collection in a List<T>  
        // before iterating through it  
        foreach (string str in source.ToList())  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 이 예제는 다음과 같은 출력을 생성합니다.  
  
```output  
ToUpper: source >abc<  
ToUpper: source >def<  
ToUpper: source >ghi<  
AppendString: source >ABC<  
Main: str >ABC!!!<  
  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
 이 예제에서 <xref:System.Linq.Enumerable.ToList%2A>을 호출하면 `AppendString`이 첫 번째 항목을 생성하기 전에 전체 소스를 열거하는 것을 확인할 수 있습니다. 소스가 큰 배열인 경우에는 애플리케이션의 메모리 프로필이 크게 변경됩니다.  
  
 표준 쿼리 연산자도 연결할 수 있습니다. 이 자습서의 최종 항목에서 이에 대해 설명합니다.  
  
- [여러 표준 쿼리 연산자 연결(C#)](./chaining-standard-query-operators-together.md)  
  
## <a name="see-also"></a>참고 항목

- [자습서: 여러 쿼리 연결(C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
