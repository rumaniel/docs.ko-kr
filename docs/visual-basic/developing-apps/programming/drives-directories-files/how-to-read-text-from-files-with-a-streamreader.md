---
title: '방법: StreamReader(Visual Basic)를 사용하여 파일에서 텍스트 읽기'
ms.date: 07/20/2015
helpviewer_keywords:
- reading files [Visual Basic], text
- text, reading from files
- reading text from files [Visual Basic]
- files [Visual Basic], reading
ms.assetid: 384033c6-18f9-4d59-9610-36371226558f
ms.openlocfilehash: 5631b402743a7be19428d15f55fbaa78b5b90668
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623343"
---
# <a name="how-to-read-text-from-files-with-a-streamreader-visual-basic"></a>방법: StreamReader(Visual Basic)를 사용하여 파일에서 텍스트 읽기
`My.Computer.FileSystem` 개체는 <xref:System.IO.TextReader> 및 <xref:System.IO.TextWriter>를 여는 메서드를 제공합니다. `OpenTextFileWriter` 및 `OpenTextFileReader` 메서드는 **모두** 탭을 선택한 경우에만 IntelliSense에 표시되는 고급 메서드입니다.  
  
### <a name="to-read-a-line-from-a-file-with-a-text-reader"></a>텍스트 판독기를 사용하여 파일에서 줄을 읽으려면  
  
- 파일을 지정하여 `OpenTextFileReader` 메서드를 통해 <xref:System.IO.TextReader>를 엽니다. 이 예제에서는 `testfile.txt`라는 파일을 열고 파일에서 줄을 읽은 다음 메시지 상자에 줄을 표시합니다.  
  
     [!code-vb[VbFileIORead#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#1)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 읽은 파일은 텍스트 파일이어야 합니다.  
  
 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다.  
  
 애플리케이션에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다. 파일의 내용이 예상한 내용과 다를 수 있으며 파일을 읽는 메서드가 실패할 수도 있습니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 파일에서 읽으려면 어셈블리에 <xref:System.Security.Permissions.FileIOPermission> 클래스에서 부여한 권한 수준이 필요합니다. 부분 신뢰 컨텍스트에서 실행하는 경우 권한 부족으로 인해 코드에서 예외를 throw할 수 있습니다. 자세한 내용은 [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)을 참조하세요. 사용자에게 파일에 대한 액세스 권한도 필요합니다. 자세한 내용은 [ACL 기술 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:System.Windows.Forms.OpenFileDialog>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileWriter%2A>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.OpenTextFileReader%2A>
- [SaveFileDialog 구성 요소](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md)
- [파일 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
