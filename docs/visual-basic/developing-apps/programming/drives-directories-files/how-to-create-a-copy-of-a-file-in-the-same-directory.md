---
title: '방법: Visual Basic에서 동일한 디렉터리에 파일의 복사본 만들기'
ms.date: 07/20/2015
f1_keywords:
- File.Copy
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files [Visual Basic], copying
- CopyFile method [Visual Basic], copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: b2fdda86-e666-42c2-9706-9527e9fa68ff
ms.openlocfilehash: 747d985cbd9e2f2cc7f9b07f5723455a63a87b8f
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64629089"
---
# <a name="how-to-create-a-copy-of-a-file-in-the-same-directory-in-visual-basic"></a>방법: Visual Basic에서 동일한 디렉터리에 파일의 복사본 만들기
`My.Computer.FileSystem.CopyFile` 메서드를 사용하여 파일을 복사합니다. 매개 변수를 통해 기존 파일을 덮어쓰고, 파일 이름을 바꾸고, 작업의 진행률을 표시하고, 사용자가 작업을 취소할 수 있습니다.  
  
### <a name="to-create-a-copy-of-a-file-in-the-same-folder"></a>동일한 폴더에 파일의 복사본을 만들려면  
  
- 대상 파일과 위치를 제공하여 `CopyFile` 메서드를 사용합니다. 다음 예제에서는 `test2.txt`라는 `test.txt`의 복사본을 만듭니다.  
  
     [!code-vb[VbVbcnMyFileSystem#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#51)]  
  
### <a name="to-create-a-copy-of-a-file-in-the-same-folder-overwriting-existing-files"></a>동일한 폴더에 파일의 복사본을 만들고 기존 파일을 덮어쓰려면  
  
- 대상 파일과 위치를 제공하고 `overwrite`를 `True`로 설정하여 `CopyFile` 메서드를 사용합니다. 다음 예제에서는 `test2.txt`라는 `test.txt`의 복사본을 만들고 해당 이름의 기존 파일을 덮어씁니다.  
  
     [!code-vb[VbVbcnMyFileSystem#52](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#52)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서는 예외가 throw될 수 있습니다.  
  
- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)  
  
- 시스템이 절대 경로를 검색할 수 없는 경우(<xref:System.ArgumentException>)  
  
- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)  
  
- 소스 파일이 잘못되었거나 없는 경우(<xref:System.IO.FileNotFoundException>)  
  
- 조합된 경로가 기존 디렉터리를 가리키는 경우(<xref:System.IO.IOException>)  
  
- 대상 파일이 있고 `overwrite`가 `False`로 설정된 경우(<xref:System.IO.IOException>)  
  
- 사용자에게 파일에 액세스할 수 있는 권한이 없는 경우(<xref:System.IO.IOException>)  
  
- 대상 폴더에 있는 동일한 이름의 파일이 사용 중인 경우 (<xref:System.IO.IOException>)  
  
- 경로의 파일 이름이나 폴더 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)  
  
- `ShowUI`가 `True`로 설정되고, `onUserCancel`이 `ThrowException`으로 설정되고, 사용자가 작업을 취소한 경우(<xref:System.OperationCanceledException>)  
  
- `ShowUI`가 `True`로 설정되고, `onUserCancel`이 `ThrowException`으로 설정되고, 지정하지 않은 I/O 오류가 발생하는 경우(<xref:System.OperationCanceledException>)  
  
- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)  
  
- 사용자에게 필요한 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)  
  
- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>
- <xref:Microsoft.VisualBasic.FileIO.UICancelOption>
- [방법: 특정 패턴의 파일을 디렉터리로 복사](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-files-with-a-specific-pattern-to-a-directory.md)
- [방법: 다른 디렉터리에 파일의 복사본 만들기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-create-a-copy-of-a-file-in-a-different-directory.md)
- [방법: 디렉터리를 다른 디렉터리에 복사](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-copy-a-directory-to-another-directory.md)
- [방법: 파일 이름 바꾸기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-rename-a-file.md)
