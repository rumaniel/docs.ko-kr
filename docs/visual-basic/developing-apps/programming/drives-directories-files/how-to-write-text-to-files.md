---
title: '방법: Visual Basic에서 파일에 텍스트 쓰기'
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], writing to
- text, writing to files
- writing to files [Visual Basic]
- examples [Visual Basic], text files
ms.assetid: 304956eb-530d-4df7-b48f-9b4d1f2581a0
ms.openlocfilehash: 7f9702469afbe9fdaa9bf727f5f70459ce884d6e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623261"
---
# <a name="how-to-write-text-to-files-in-visual-basic"></a>방법: Visual Basic에서 파일에 텍스트 쓰기
<xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A> 메서드를 사용하여 파일에 텍스트를 쓸 수 있습니다. 지정한 파일이 없으면 새로 만들어집니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-write-text-to-a-file"></a>파일에 텍스트를 쓰려면  
  
- 파일과 쓸 텍스트를 지정하여 `WriteAllText` 메서드를 통해 파일에 텍스트를 씁니다. 이 예제에서는 `test.txt`라는 파일에 `"This is new text."` 줄을 쓰고 파일에 있는 기존 텍스트에 텍스트를 추가합니다.  
  
     [!code-vb[VbFileIOWrite#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#3)]  
  
#### <a name="to-write-a-series-of-strings-to-a-file"></a>일련의 문자열을 파일에 쓰려면  
  
- 문자열 컬렉션을 반복합니다. 대상 파일 및 추가할 문자열을 지정하고 `append`를 `True`로 설정하여 `WriteAllText` 메서드를 통해 파일에 텍스트를 씁니다.  
  
     이 예제에서는 `Documents and Settings` 디렉터리에 있는 파일 이름을 `FileList.txt`에 쓰고, 가독성을 높이기 위해 각 이름 사이에 캐리지 리턴을 삽입합니다.  
  
     [!code-vb[VbFileIOWrite#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#4)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)  
  
- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)  
  
- `File`이 존재하지 않는 경로를 가리키는 경우(<xref:System.IO.FileNotFoundException> 또는 <xref:System.IO.DirectoryNotFoundException>)  
  
- 다른 프로세스에서 파일을 사용 중이거나 I/O 오류가 발생한 경우(<xref:System.IO.IOException>)  
  
- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)  
  
- 경로의 파일 이름이나 디렉터리 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)  
  
- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)  
  
- 디스크가 꽉 찼고 `WriteAllText`에 대한 호출에 실패한 경우(<xref:System.IO.IOException>)  
  
 부분 신뢰 컨텍스트에서 실행하는 경우 권한 부족으로 인해 코드에서 예외를 throw할 수 있습니다. 자세한 내용은 [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- [방법: 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files.md)
