---
title: '방법: 리플렉션을 사용하여 어셈블리의 메타데이터 쿼리(LINQ)(C#)'
ms.date: 07/20/2015
ms.assetid: c4cdce49-b1c8-4420-b12a-9ff7e6671368
ms.openlocfilehash: fb0fb118eaabbd9d66c5c4a445b0393a69dd2355
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69592917"
---
# <a name="how-to-query-an-assemblys-metadata-with-reflection-linq-c"></a>방법: 리플렉션을 사용하여 어셈블리의 메타데이터 쿼리(LINQ)(C#)

.NET Framework 클래스 라이브러리 리플렉션 API는 .NET 어셈블리에서 메타데이터를 검사하고 해당 어셈블리에 없는 형식, 형식 멤버, 매개 변수 등의 컬렉션을 만드는 데 사용할 수 있습니다. 이러한 컬렉션은 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 지원하므로 LINQ를 사용하여 쿼리할 수 있습니다.  
  
다음 예제에서는 리플렉션과 함께 LINQ를 사용하여 지정된 검색 조건과 일치하는 메서드에 대한 특정 메타데이터를 검색하는 방법을 보여 줍니다. 이 경우 쿼리는 배열과 같은 열거 가능한 형식을 반환하는 모든 메서드의 이름을 어셈블리에서 검색합니다.  
  
## <a name="example"></a>예  
  
```csharp  
using System;
using System.Linq;
using System.Reflection;  

class ReflectionHowTO  
{  
    static void Main()  
    {  
        Assembly assembly = Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089");  
        var pubTypesQuery = from type in assembly.GetTypes()  
                    where type.IsPublic  
                        from method in type.GetMethods()  
                        where method.ReturnType.IsArray == true 
                            || ( method.ReturnType.GetInterface(  
                                typeof(System.Collections.Generic.IEnumerable<>).FullName ) != null  
                            && method.ReturnType.FullName != "System.String" )  
                        group method.ToString() by type.ToString();  

        foreach (var groupOfMethods in pubTypesQuery)  
        {  
            Console.WriteLine("Type: {0}", groupOfMethods.Key);  
            foreach (var method in groupOfMethods)  
            {  
                Console.WriteLine("  {0}", method);  
            }  
        }  

        Console.WriteLine("Press any key to exit... ");  
        Console.ReadKey();  
    }  
}
```  

이 예제에서는 <xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=nameWithType> 메서드를 사용하여 지정된 어셈블리의 형식 배열을 반환합니다. public 형식만 반환되도록 [where](../../../language-reference/keywords/where-clause.md) 필터가 적용됩니다. 각 public 형식에 대해 <xref:System.Type.GetMethods%2A?displayProperty=nameWithType> 호출에서 반환된 <xref:System.Reflection.MethodInfo> 배열을 사용하여 하위 쿼리가 생성됩니다. 이러한 결과는 해당 반환 형식이 배열이거나 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 형식인 메서드만 반환하도록 필터링됩니다. 마지막으로, 이러한 결과는 형식 이름을 키로 사용하여 그룹화됩니다.  
  
## <a name="see-also"></a>참고 항목

- [LINQ to Objects(C#)](./linq-to-objects.md)
