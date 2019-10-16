---
title: '방법: 텍스트 파일을 한 번에 한 줄씩 읽기(Visual C#)'
ms.date: 07/20/2015
helpviewer_keywords:
- ReadLine method [C#]
- reading text files, line by line
- text files [C#]
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
ms.openlocfilehash: 75274d93ee29feb5f79dfc29c24109f25fd98a5c
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589956"
---
# <a name="how-to-read-a-text-file-one-line-at-a-time-visual-c"></a>방법: 텍스트 파일을 한 번에 한 줄씩 읽기(Visual C#)
이 예제에서는 `StreamReader` 클래스의 `ReadLine` 메서드를 사용하여 텍스트 파일 내용을 한 번에 한 줄씩 문자열로 읽어옵니다. 각 텍스트 줄은 `line` 문자열에 저장되고 화면에 표시됩니다.  
  
## <a name="example"></a>예  
  
```csharp
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =   
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine(line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 복사하고 콘솔 애플리케이션의 `Main` 메서드에 붙여넣습니다.  
  
 `"c:\test.txt"`를 실제 파일 이름으로 바꿉니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 파일이 없을 수 있는 경우  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 `myFile.cs` 파일이 C# 소스 파일이 아닐 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO?displayProperty=nameWithType>
- [C# 프로그래밍 가이드](../index.md)
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](./index.md)
