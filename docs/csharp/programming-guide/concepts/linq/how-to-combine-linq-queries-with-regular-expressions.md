---
title: '방법: LINQ 쿼리와 정규식 결합(C#)'
ms.date: 07/20/2015
ms.assetid: 6b003b65-20a4-4ca2-929e-2ee3f215aecc
ms.openlocfilehash: c535620f2dee1ec9cd1b6ee994fbf860629601ba
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033313"
---
# <a name="how-to-combine-linq-queries-with-regular-expressions-c"></a>방법: LINQ 쿼리와 정규식 결합(C#)
이 예제에서는 <xref:System.Text.RegularExpressions.Regex> 클래스를 사용하여 더 복잡한 텍스트 문자열 일치를 찾는 정규식을 작성하는 방법을 보여 줍니다. LINQ 쿼리를 사용하면 손쉽게 정규식을 통해 검색하려는 파일을 정확히 필터링하고 결과를 구성할 수 있습니다.  
  
## <a name="example"></a>예  
  
```csharp  
class QueryWithRegEx  
{  
    public static void Main()  
    {  
        // Modify this path as necessary so that it accesses your version of Visual Studio.  
        string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio 14.0\";  
        // One of the following paths may be more appropriate on your computer.  
        //string startFolder = @"C:\Program Files (x86)\Microsoft Visual Studio\2017\";  
  
        // Take a snapshot of the file system.  
        IEnumerable<System.IO.FileInfo> fileList = GetFiles(startFolder);  
  
        // Create the regular expression to find all things "Visual".  
        System.Text.RegularExpressions.Regex searchTerm =  
            new System.Text.RegularExpressions.Regex(@"Visual (Basic|C#|C\+\+|Studio)");  
  
        // Search the contents of each .htm file.  
        // Remove the where clause to find even more matchedValues!  
        // This query produces a list of files where a match  
        // was found, and a list of the matchedValues in that file.  
        // Note: Explicit typing of "Match" in select clause.  
        // This is required because MatchCollection is not a   
        // generic IEnumerable collection.  
        var queryMatchingFiles =  
            from file in fileList  
            where file.Extension == ".htm"  
            let fileText = System.IO.File.ReadAllText(file.FullName)  
            let matches = searchTerm.Matches(fileText)  
            where matches.Count > 0  
            select new  
            {  
                name = file.FullName,  
                matchedValues = from System.Text.RegularExpressions.Match match in matches  
                                select match.Value  
            };  
  
        // Execute the query.  
        Console.WriteLine("The term \"{0}\" was found in:", searchTerm.ToString());  
  
        foreach (var v in queryMatchingFiles)  
        {  
            // Trim the path a bit, then write   
            // the file name in which a match was found.  
            string s = v.name.Substring(startFolder.Length - 1);  
            Console.WriteLine(s);  
  
            // For this file, write out all the matching strings  
            foreach (var v2 in v.matchedValues)  
            {  
                Console.WriteLine("  " + v2);  
            }  
        }  
  
        // Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit");  
        Console.ReadKey();  
    }  
  
    // This method assumes that the application has discovery   
    // permissions for all folders under the specified path.  
    static IEnumerable<System.IO.FileInfo> GetFiles(string path)  
    {  
        if (!System.IO.Directory.Exists(path))  
            throw new System.IO.DirectoryNotFoundException();  
  
        string[] fileNames = null;  
        List<System.IO.FileInfo> files = new List<System.IO.FileInfo>();  
  
        fileNames = System.IO.Directory.GetFiles(path, "*.*", System.IO.SearchOption.AllDirectories);  
        foreach (string name in fileNames)  
        {  
            files.Add(new System.IO.FileInfo(name));  
        }  
        return files;  
    }  
}  
```  
  
 `RegEx` 검색에서 반환되는 <xref:System.Text.RegularExpressions.MatchCollection> 개체를 쿼리할 수도 있습니다. 이 예제에서는 각 일치 항목의 값만 결과로 생성됩니다. 그러나 LINQ를 사용하여 해당 컬렉션에 대한 모든 종류의 필터링, 정렬 및 그룹화를 수행할 수도 있습니다. <xref:System.Text.RegularExpressions.MatchCollection>은 제네릭이 아닌 <xref:System.Collections.IEnumerable> 컬렉션이므로 쿼리에 범위 변수의 형식을 명시적으로 기술해야 합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 System.Core.dll에 대한 참조와 System.Linq 및 System.IO 네임스페이스에 대한 `using` 지시문을 사용하여 .NET Framework 버전 3.5 이상을 대상으로 하는 프로젝트를 만듭니다.  
  
## <a name="see-also"></a>참고 항목

- [LINQ 및 문자열(C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-strings.md)  
- [LINQ 및 파일 디렉터리(C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)
