---
title: '방법: 파일 또는 폴더 만들기 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- folders [C#]
- creating files [C#]
- files [C#]
- creating folders [C#]
ms.assetid: 4582ee2d-d72d-4687-bcb9-08d336c62c25
ms.openlocfilehash: c29d0638e2429119020fee5317d40a95b00e40ef
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590110"
---
# <a name="how-to-create-a-file-or-folder-c-programming-guide"></a>방법: 파일 또는 폴더 만들기(C# 프로그래밍 가이드)
프로그래밍 방식으로 컴퓨터에 폴더를 만들고, 하위 폴더를 만들고, 하위 폴더에 파일을 만들고, 파일에 데이터를 쓸 수 있습니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csFilesandFolders#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#10)]  
  
 폴더가 이미 있으면 <xref:System.IO.Directory.CreateDirectory%2A>는 아무 작업도 수행하지 않으며 예외가 throw되지 않습니다. 그러나 <xref:System.IO.File.Create%2A?displayProperty=nameWithType>는 기존 파일을 새 파일로 바꿉니다. 이 예제에서는 `if`-`else` 문을 사용하여 기존 파일이 바뀌지 않도록 합니다.  
  
 예제에서 다음을 변경하여 특정 이름의 파일이 이미 있는지 여부에 따라 다른 결과를 지정할 수 있습니다. 파일이 없는 경우 코드에서 파일을 만듭니다. 파일이 있는 경우 코드에서 해당 파일에 데이터를 추가합니다.  
  
- 임의가 아닌 파일 이름을 지정합니다.  
  
    ```csharp  
    // Comment out the following line.  
    //string fileName = System.IO.Path.GetRandomFileName();  
  
    // Replace that line with the following assignment.  
    string fileName = "MyNewFile.txt";  
    ```  
  
- 다음 코드를 사용하여 `if`-`else` 문을 `using` 문으로 바꿉니다.  
  
    ```csharp  
    using (System.IO.FileStream fs = new System.IO.FileStream(pathString, FileMode.Append))   
    {  
        for (byte i = 0; i < 100; i++)  
        {  
            fs.WriteByte(i);  
        }  
    }  
    ```  
  
 예제를 여러 번 실행하여 매번 파일에 데이터가 추가되는지 확인합니다.  
  
 시도할 수 있는 추가 `FileMode` 값은 <xref:System.IO.FileMode>를 참조하세요.  
  
 다음 조건에서 예외가 발생합니다.  
  
- 폴더 이름 형식이 잘못된 경우. 예를 들어 잘못된 문자를 포함하거나 공백만으로 이루어져 있습니다(<xref:System.ArgumentException> 클래스). <xref:System.IO.Path> 클래스를 사용하여 유효한 경로 이름을 만듭니다.  
  
- 만들 폴더의 부모 폴더가 읽기 전용입니다(<xref:System.IO.IOException> 클래스).  
  
- 폴더 이름이 `null`입니다(<xref:System.ArgumentNullException> 클래스).  
  
- 폴더 이름이 너무 깁니다(<xref:System.IO.PathTooLongException> 클래스).  
  
- 폴더 이름이 콜론(“:”)뿐입니다(<xref:System.IO.PathTooLongException> 클래스).  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 부분 신뢰 상황에서는 <xref:System.Security.SecurityException> 클래스의 인스턴스가 throw될 수 있습니다.  
  
 폴더를 만들 수 있는 권한이 없는 경우 이 예제에서는 <xref:System.UnauthorizedAccessException> 클래스의 인스턴스가 throw됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO?displayProperty=nameWithType>
- [C# 프로그래밍 가이드](../index.md)
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](./index.md)
