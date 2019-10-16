---
title: '방법: Visual Basic에서 파일 경로 구문 분석'
ms.date: 07/20/2015
helpviewer_keywords:
- file names [Visual Basic], parsing [Visual Basic]
- parsing, file paths [Visual Basic]
ms.assetid: c1bd99c9-8160-456a-b5ab-60a49139b923
ms.openlocfilehash: 6961f481126d34b18c5a11d83c4c6c37c2c81c71
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64629160"
---
# <a name="how-to-parse-file-paths-in-visual-basic"></a>방법: Visual Basic에서 파일 경로 구문 분석
<xref:Microsoft.VisualBasic.FileIO.FileSystem> 개체는 파일 경로를 구문 분석할 때 유용한 메서드 여러 개를 제공합니다.  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CombinePath%2A> 메서드는 두 개의 경로를 가져와서 적절한 형식으로 조합된 경로를 반환합니다.  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetParentPath%2A> 메서드는 제공된 경로의 상위에 대한 절대 경로를 반환합니다.  
  
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A> 메서드는 <xref:System.IO.FileInfo> 개체를 반환합니다. 이 개체를 쿼리하여 파일의 이름 및 경로 등과 같은 속성을 확인할 수 있습니다.  
  
 파일 이름 확장명에 근거하여 파일 내용을 판단하지 않는 것이 좋습니다. 예를 들어 Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다.  
  
### <a name="to-determine-a-files-name-and-path"></a>파일의 이름 및 경로를 확인하려면  
  
- <xref:System.IO.FileInfo.DirectoryName%2A> 개체의 <xref:System.IO.FileInfo.Name%2A> 및 <xref:System.IO.FileInfo> 속성을 사용하여 파일의 이름과 경로를 확인합니다. 이 예제에서는 이름과 경로를 확인하고 이를 표시합니다.  
  
     [!code-vb[VbVbcnMyFileSystem#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#54)]  
  
### <a name="to-combine-a-files-name-and-directory-to-create-the-full-path"></a>파일의 이름과 디렉터리를 결합하여 전체 경로를 만들려면  
  
- 디렉터리와 이름을 제공하여 `CombinePath` 메서드를 사용합니다. 이 예제에서는 이전 예제에서 만들어진 문자열 `folderPath` 와 `fileName` 을 가져와서 이를 결합한 다음 결과를 표시합니다.  
  
     [!code-vb[VbVbcnMyFileSystem#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#55)]  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CombinePath%2A>
- <xref:System.IO.FileInfo>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetFileInfo%2A>
- [방법: 디렉터리에 있는 파일의 컬렉션 가져오기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)
