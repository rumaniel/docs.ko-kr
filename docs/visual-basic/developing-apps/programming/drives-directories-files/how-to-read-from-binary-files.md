---
title: '방법: Visual Basic의 이진 파일에서 읽기'
ms.date: 07/20/2015
helpviewer_keywords:
- binary files [Visual Basic], reading from
- I/O [Visual Basic], reading from binary files
- ReadAllBytes method [Visual Basic], reading from binary files
- My.Computer.FileSystem object, reading from binary files
ms.assetid: d2b1269e-24b6-42e0-9414-ae708db282d8
ms.openlocfilehash: 72e9361193a5b099841d989e842ff36662cf690d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623716"
---
# <a name="how-to-read-from-binary-files-in-visual-basic"></a>방법: Visual Basic의 이진 파일에서 읽기
`My.Computer.FileSystem` 개체는 이진 파일을 읽기 위한 `ReadAllBytes` 메서드를 제공합니다.  
  
### <a name="to-read-from-a-binary-file"></a>이진 파일을 읽으려면  
  
- 파일 내용을 바이트 배열로 반환하는 `ReadAllBytes` 메서드를 사용합니다. 이 예제에서는 `C:/Documents and Settings/selfportrait.jpg` 파일에서 읽습니다.  
  
     [!code-vb[VbVbcnMyFileSystem#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#78)]  
  
- 큰 이진 파일의 경우 <xref:System.IO.FileStream> 개체의 <xref:System.IO.FileStream.Read%2A> 메서드를 사용하여 파일에서 한 번에 지정된 양만큼만 읽을 수 있습니다. 그런 다음 각 읽기 작업에 대해 메모리에 로드되는 파일 크기를 제한할 수 있습니다. 다음 코드 예제에서는 파일을 복사하고, 호출자가 읽기 작업당 메모리로 읽어오는 파일 크기를 지정할 수 있도록 합니다.  
  
     [!code-vb[VbVbcnMyFileSystem#91](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#91)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서는 예외가 throw될 수 있습니다.  
  
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

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllBytes%2A>
- [파일 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
- [방법: 여러 형식의 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)
- [데이터를 클립보드에 저장하고 클립보드에서 읽기](../../../../visual-basic/developing-apps/programming/computer-resources/storing-data-to-and-reading-from-the-clipboard.md)
