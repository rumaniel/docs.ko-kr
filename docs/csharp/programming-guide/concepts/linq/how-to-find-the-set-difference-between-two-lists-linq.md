---
title: '방법: 두 목록 간의 차집합 구하기(LINQ)(C#)'
ms.date: 07/20/2015
ms.assetid: 8e8945f0-4aba-439d-8d5d-c8d1eeef4e71
ms.openlocfilehash: decdbe45afd12581a53ed70ec843ee72f54f0409
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593345"
---
# <a name="how-to-find-the-set-difference-between-two-lists-linq-c"></a>방법: 두 목록 간의 차집합 구하기(LINQ)(C#)
이 예제에서는 LINQ를 사용하여 두 개의 문자열 목록을 비교하고 names1.txt에 있지만 names2.txt에는 없는 줄만 출력하는 방법을 보여 줍니다.  
  
### <a name="to-create-the-data-files"></a>데이터 파일을 만들려면  
  
1. [방법: 문자열 컬렉션 결합 및 비교(LINQ)(C#)](./how-to-combine-and-compare-string-collections-linq.md)에 표시된 대로 names1.txt 및 names2.txt를 솔루션 폴더에 복사합니다.  
  
## <a name="example"></a>예  
  
```csharp  
class CompareLists  
{          
    static void Main()  
    {  
        // Create the IEnumerable data sources.  
        string[] names1 = System.IO.File.ReadAllLines(@"../../../names1.txt");  
        string[] names2 = System.IO.File.ReadAllLines(@"../../../names2.txt");  
  
        // Create the query. Note that method syntax must be used here.  
        IEnumerable<string> differenceQuery =  
          names1.Except(names2);  
  
        // Execute the query.  
        Console.WriteLine("The following lines are in names1.txt but not names2.txt");  
        foreach (string s in differenceQuery)  
            Console.WriteLine(s);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
     The following lines are in names1.txt but not names2.txt  
    Potra, Cristina  
    Noriega, Fabricio  
    Aw, Kam Foo  
    Toyoshima, Tim  
    Guy, Wey Yuan  
    Garcia, Debra  
     */  
```  
  
 <xref:System.Linq.Enumerable.Except%2A>, <xref:System.Linq.Enumerable.Distinct%2A>, <xref:System.Linq.Enumerable.Union%2A>, <xref:System.Linq.Enumerable.Concat%2A> 등 C#에서 일부 유형의 쿼리 작업은 메서드 기반 구문으로만 표현할 수 있습니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 System.Linq 및 System.IO 네임스페이스에 대한 `using` 지시문을 통해 C# 콘솔 애플리케이션 프로젝트를 만듭니다.  
  
## <a name="see-also"></a>참고 항목

- [LINQ 및 문자열(C#)](./linq-and-strings.md)
