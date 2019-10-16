---
title: '방법: Visual Basic에서 텍스트 파일에서 읽기'
ms.date: 07/20/2015
helpviewer_keywords:
- extended characters [Visual Basic], reading
- reading text files [Visual Basic]
- reading data, text files
- examples [Visual Basic], reading text files
- text files [Visual Basic], reading
ms.assetid: 735fe9d7-0f7a-4185-ba02-f35e580ec4b8
ms.openlocfilehash: 26e6d8f9cc64f0f1238afaaf6aaf85d69f6c32ce
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039425"
---
# <a name="how-to-read-from-text-files-in-visual-basic"></a>방법: Visual Basic에서 텍스트 파일에서 읽기

<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.ReadAllText%2A> 개체의 `My.Computer.FileSystem` 메서드를 사용하면 텍스트 파일을 읽을 수 있습니다. 파일 내용에 ASCII 또는 UTF-8 등의 인코딩이 사용된 경우 파일 인코딩을 지정할 수 있습니다.

확장 문자가 사용된 파일을 읽을 때는 파일 인코딩을 지정해야 합니다.

> [!NOTE]
> 파일의 텍스트를 한 번에 한 줄씩 읽으려면 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.OpenTextFileReader%2A> 개체의 `My.Computer.FileSystem` 메서드를 사용합니다. `OpenTextFileReader` 메서드는 <xref:System.IO.StreamReader> 개체를 반환합니다. <xref:System.IO.StreamReader.ReadLine%2A> 개체의 `StreamReader` 메서드를 사용하여 파일을 한 번에 한 줄씩 읽을 수 있습니다. <xref:System.IO.StreamReader.EndOfStream%2A> 개체의 `StreamReader` 메서드를 사용하여 파일의 끝인지 여부를 테스트할 수 있습니다.

## <a name="to-read-from-a-text-file"></a>텍스트 파일을 읽으려면

`ReadAllText` 개체의 `My.Computer.FileSystem` 메서드에 경로를 지정하여 텍스트 파일의 내용을 문자열로 읽어옵니다. 다음 예제에서는 test.txt의 내용을 문자열로 읽어온 다음 그 내용을 메시지 상자에 표시합니다.

[!code-vb[VbFileIORead#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#2)]

### <a name="to-read-from-a-text-file-that-is-encoded"></a>인코딩된 텍스트 파일을 읽으려면

`ReadAllText` 개체의 `My.Computer.FileSystem` 메서드에 경로와 파일 인코딩 형식을 지정하여 텍스트 파일의 내용을 문자열로 읽어옵니다. 다음 예제에서는 UTF32 파일인 test.txt의 내용을 문자열로 읽어온 다음 그 내용을 메시지 상자에 표시합니다.

[!code-vb[VbFileIORead#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#3)]

## <a name="robust-programming"></a>강력한 프로그래밍

다음 조건에서 예외가 발생합니다.

- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)

- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)

- 파일이 없는 경우(<xref:System.IO.FileNotFoundException>)

- 다른 프로세스에서 파일을 사용 중이거나 I/O 오류가 발생한 경우(<xref:System.IO.IOException>)

- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)

- 경로의 파일 이름이나 디렉터리 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)

- 문자열을 버퍼에 쓰기 위한 메모리가 부족한 경우(<xref:System.OutOfMemoryException>)

- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)

파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다.

애플리케이션에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다. 파일의 내용이 예상한 내용과 다를 수 있으며 파일을 읽는 메서드가 실패할 수도 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>
- [파일 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
- [방법: 쉼표로 구분된 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)
- [방법: 고정 너비 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)
- [방법: 여러 형식의 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)
- [문제 해결: 텍스트 파일 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
- [연습: Visual Basic에서 파일과 디렉터리 조작](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)
- [파일 인코딩](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md)
