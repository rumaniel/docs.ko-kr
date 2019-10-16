---
title: '방법: Visual Basic에서 파일 이름 바꾸기'
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], renaming files
- files [Visual Basic], renaming
ms.assetid: 0ea7e0c8-2cb2-4bf5-a00d-7b6e3c08a3bc
ms.openlocfilehash: 2bc3e19968362993528c166ca6ec7a7fbbec1993
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623256"
---
# <a name="how-to-rename-a-file-in-visual-basic"></a>방법: Visual Basic에서 파일 이름 바꾸기
`My.Computer.FileSystem` 개체의 `RenameFile` 메서드를 사용하면 현재 위치, 파일 이름 및 새 파일 이름을 제공하여 파일 이름을 바꿀 수 있습니다. 이 메서드를 사용하여 파일을 이동할 수는 없습니다. 파일을 이동하고 파일 이름을 바꾸려면 `MoveFile` 메서드를 사용합니다.  
  
### <a name="to-rename-a-file"></a>파일 이름을 바꾸려면  
  
- `My.Computer.FileSystem.RenameFile` 메서드를 사용하여 파일 이름을 바꿉니다. 이 예제에서는 `Test.txt` 파일의 이름을 `SecondTest.txt`로 바꿉니다.  
  
     [!code-vb[VbVbcnMyFileSystem#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#9)]  
  
 이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 코드 조각은 **파일 시스템 - 드라이브, 폴더, 파일 처리**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)  
  
- `newName`에 경로 정보가 포함된 경우(<xref:System.ArgumentException>)  
  
- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)  
  
- `newName` 이 `Nothing` 이거나 빈 문자열인 경우(<xref:System.ArgumentNullException>)  
  
- 소스 파일이 잘못되었거나 없는 경우(<xref:System.IO.FileNotFoundException>)  
  
- `newName`에 지정된 이름의 기존 파일 또는 디렉터리가 있는 경우(<xref:System.IO.IOException>)  
  
- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)  
  
- 경로의 파일 이름이나 디렉터리 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)  
  
- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)  
  
- 사용자에게 필요한 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.RenameFile%2A>
- [방법: 파일 이동](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-move-a-file.md)
- [파일/디렉터리 만들기, 삭제 및 이동](../../../../visual-basic/developing-apps/programming/drives-directories-files/creating-deleting-and-moving-files-and-directories.md)
- [방법: 동일한 디렉터리에 파일의 복사본 만들기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-the-same-directory.md)
- [방법: 다른 디렉터리에 파일의 복사본 만들기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)
