---
title: '방법: 문자열에서 단어가 나오는 횟수 세기(LINQ)(C#)'
ms.date: 07/20/2015
ms.assetid: f8e6f546-7c14-4aa1-8a75-e8d09f3b8ccd
ms.openlocfilehash: 12118c6322df0cfb93cb3d4a4dbbc02d68a0c776
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69593910"
---
# <a name="how-to-count-occurrences-of-a-word-in-a-string-linq-c"></a>방법: 문자열에서 단어가 나오는 횟수 세기(LINQ)(C#)
이 예제에서는 LINQ 쿼리를 사용하여 문자열에서 지정된 단어의 발생 수를 계산하는 방법을 보여 줍니다. 계산을 수행하려면 먼저 <xref:System.String.Split%2A> 메서드를 호출하여 단어 배열을 만듭니다. <xref:System.String.Split%2A> 메서드를 사용하는 경우 성능이 저하됩니다. 문자열의 유일한 작업이 단어 개수 계산인 경우 <xref:System.Text.RegularExpressions.Regex.Matches%2A> 또는 <xref:System.String.IndexOf%2A> 메서드를 대신 사용하는 것이 좋습니다. 그러나 성능이 중요한 문제가 아니거나 다른 유형의 쿼리를 수행하기 위해 이미 문장을 분할한 경우 LINQ를 사용하여 단어 또는 구도 계산하는 것이 좋습니다.  
  
## <a name="example"></a>예  
  
```csharp  
class CountWords  
{  
    static void Main()  
    {  
        string text = @"Historically, the world of data and the world of objects" +  
          @" have not been well integrated. Programmers work in C# or Visual Basic" +  
          @" and also in SQL or XQuery. On the one side are concepts such as classes," +  
          @" objects, fields, inheritance, and .NET Framework APIs. On the other side" +  
          @" are tables, columns, rows, nodes, and separate languages for dealing with" +  
          @" them. Data types often require translation between the two worlds; there are" +  
          @" different standard functions. Because the object world has no notion of query, a" +  
          @" query can only be represented as a string without compile-time type checking or" +  
          @" IntelliSense support in the IDE. Transferring data from SQL tables or XML trees to" +  
          @" objects in memory is often tedious and error-prone.";  
  
        string searchTerm = "data";  
  
        //Convert the string into an array of words  
        string[] source = text.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);  
  
        // Create the query.  Use ToLowerInvariant to match "data" and "Data"   
        var matchQuery = from word in source  
                         where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()  
                         select word;  
  
        // Count the matches, which executes the query.  
        int wordCount = matchQuery.Count();  
        Console.WriteLine("{0} occurrences(s) of the search term \"{1}\" were found.", wordCount, searchTerm);  
  
        // Keep console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
}  
/* Output:  
   3 occurrences(s) of the search term "data" were found.  
*/  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 System.Linq 및 System.IO 네임스페이스에 대한 `using` 지시문을 통해 C# 콘솔 애플리케이션 프로젝트를 만듭니다.  
  
## <a name="see-also"></a>참고 항목

- [LINQ 및 문자열(C#)](./linq-and-strings.md)
