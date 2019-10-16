---
title: '방법: 텍스트 파일에서 읽기 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- StreamReader.ReadToEnd
helpviewer_keywords:
- text files, writing to
- reading text files
- reading data, text files
- text files, reading
ms.assetid: 92246c5b-e819-4eea-9370-1a9460e12de3
ms.openlocfilehash: 2b98f24da7f13ae752f248eb8f26c75c1d47a824
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923948"
---
# <a name="how-to-read-from-a-text-file-c-programming-guide"></a>방법: 텍스트 파일에서 읽기(C# 프로그래밍 가이드)
이 예제에서는 <xref:System.IO.File?displayProperty=nameWithType> 클래스의 정적 메서드 <xref:System.IO.File.ReadAllText%2A> 및 <xref:System.IO.File.ReadAllLines%2A>를 사용하여 텍스트 파일의 내용을 읽습니다.  
  
 <xref:System.IO.StreamReader>를 사용하는 예제는 [방법: 텍스트 파일을 한 번에 한 줄씩 읽기](./how-to-read-a-text-file-one-line-at-a-time.md)를 참조하세요.  
  
> [!NOTE]
> 이 예제에 사용되는 파일은 [방법: 텍스트 파일에 쓰기](./how-to-write-to-a-text-file.md) 항목에서 생성되었습니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csFilesandFolders#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#4)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 복사하고 C# 콘솔 애플리케이션에 붙여넣습니다.  
  
 [방법: 텍스트 파일에 쓰기](./how-to-write-to-a-text-file.md)의 텍스트 파일을 사용하지 않는 경우 `ReadAllText` 및 `ReadAllLines`에 대한 인수를 사용자 컴퓨터의 적절한 경로 및 파일 이름으로 바꿉니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 파일이 없거나 지정된 위치에 없는 경우. 경로와 파일 이름의 철자를 확인합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 파일 이름을 사용하여 파일 내용을 확인하지 마세요. 예를 들어 `myFile.cs` 파일이 C# 소스 파일이 아닐 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO?displayProperty=nameWithType>
- [C# 프로그래밍 가이드](../index.md)
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](./index.md)
