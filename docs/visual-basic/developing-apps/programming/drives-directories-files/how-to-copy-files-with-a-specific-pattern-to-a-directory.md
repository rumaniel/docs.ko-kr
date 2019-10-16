---
title: '방법: Visual Basic에서 특정 패턴의 파일을 디렉터리에 복사'
ms.date: 07/20/2015
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files [Visual Basic], copying
- CopyFile method [Visual Basic], copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: f205d2ad-bbe5-4d55-8a40-acda21aa82dd
ms.openlocfilehash: 15bec7c9604b243c586b393d71007b02917d3a6e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64628930"
---
# <a name="how-to-copy-files-with-a-specific-pattern-to-a-directory-in-visual-basic"></a>방법: Visual Basic에서 특정 패턴의 파일을 디렉터리에 복사
<xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> 메서드는 파일의 경로 이름을 나타내는 읽기 전용 문자열 컬렉션을 반환합니다. `wildCards` 매개 변수를 사용하여 특정 패턴을 지정할 수 있습니다.  
  
 일치하는 파일이 없으면 빈 컬렉션이 반환됩니다.  
  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A> 메서드를 사용하여 파일을 디렉터리로 복사할 수 있습니다.  
  
### <a name="to-copy-files-with-a-specific-pattern-to-a-directory"></a>특정 패턴의 파일을 디렉터리로 복사하려면  
  
1. `GetFiles` 메서드를 사용하여 파일 목록을 반환합니다. 이 예제에서는 지정된 디렉터리에 있는 .rtf 파일을 모두 반환합니다.  
  
     [!code-vb[VbFileIOMisc#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#36)]  
  
2. `CopyFile` 메서드를 사용하여 파일을 복사합니다. 이 예제에서는 `testdirectory`라는 디렉터리로 파일을 복사합니다.  
  
     [!code-vb[VbVbcnMyFileSystem#88](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#88)]  
  
3. `For` 문으로 `Next` 문을 닫습니다.  
  
     [!code-vb[VbVbcnMyFileSystem#89](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#89)]  
  
## <a name="example"></a>예제  
 위 코드 조각의 완전한 형식인 다음 예제에서는 지정된 디렉터리의 모든 .rtf 파일을 `testdirectory`라는 이름의 디렉터리로 복사합니다.  
  
 [!code-vb[VbFileIOMisc#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/Class1.vb#37)]  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 다음 조건에서 예외가 발생합니다.  
  
- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)  
  
- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)  
  
- 디렉터리가 없는 경우(<xref:System.IO.DirectoryNotFoundException>)  
  
- 디렉터리가 기존 파일을 가리키는 경우(<xref:System.IO.IOException>)  
  
- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)  
  
- 경로의 파일 이름이나 디렉터리 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)  
  
- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>) 사용자에게 필요한 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>
- <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>
- [방법: 특정 패턴의 하위 디렉터리 찾기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)
- [문제 해결: 텍스트 파일 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
- [방법: 디렉터리에 있는 파일의 컬렉션 가져오기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)
