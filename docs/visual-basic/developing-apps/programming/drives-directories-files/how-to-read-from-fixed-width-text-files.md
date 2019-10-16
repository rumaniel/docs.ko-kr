---
title: '방법: Visual Basic에서 고정 너비 텍스트 파일 읽기'
ms.date: 07/20/2015
helpviewer_keywords:
- fixed-width text file
- reading text files [Visual Basic], fixed-width
- files [Visual Basic], parsing
- text files [Visual Basic], tasks
- text files [Visual Basic], reading
ms.assetid: 99be5692-967a-4e85-993e-cd18139a5a69
ms.openlocfilehash: 1df1c84e6eaf90b737b51e5512638e4a15de6866
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623446"
---
# <a name="how-to-read-from-fixed-width-text-files-in-visual-basic"></a>방법: Visual Basic에서 고정 너비 텍스트 파일 읽기
`TextFieldParser` 개체는 로그와 같은 구조적 텍스트 파일을 쉽고 효율적으로 구문 분석하는 방법을 제공합니다.  
  
 `TextFieldType` 속성은 구문 분석된 파일이 구분된 파일인지 또는 고정 너비 텍스트 필드가 있는 파일인지를 정의합니다. 고정 너비 텍스트 파일의 끝에 있는 필드는 가변 너비를 가질 수 있습니다. 끝에 있는 필드에 가변 너비를 지정하려면 0 이하의 너비로 정의합니다.  
  
### <a name="to-parse-a-fixed-width-text-file"></a>고정 너비 텍스트 파일을 구문 분석하려면  
  
1. 새 `TextFieldParser`를 만듭니다. 다음 코드는 `Reader`라는 `TextFieldParser`를 만들고 `test.log` 파일을 엽니다.  
  
     [!code-vb[VbFileIORead#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#9)]  
  
2. 너비와 형식을 정의하여 `TextFieldType` 속성을 `FixedWidth`로 정의합니다. 다음 코드는 텍스트 열을 정의합니다. 첫 번째 열은 너비가 5자이고, 두 번째 열은 10자, 세 번째 열은 11자, 네 번째 열은 가변 너비입니다.  
  
     [!code-vb[VbFileIORead#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#10)]  
  
3. 파일의 필드를 반복합니다. 손상된 줄이 있는 경우 오류를 보고하고 구문 분석을 계속합니다.  
  
     [!code-vb[VbFileIORead#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#11)]  
  
4. `End While` 및 `End Using`을 사용하여 `While` 및 `Using` 블록을 닫습니다.  
  
     [!code-vb[VbFileIORead#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#12)]  
  
## <a name="example"></a>예제  
 이 예제에서는 `test.log` 파일에서 읽습니다.  
  
 [!code-vb[VbFileIORead#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#13)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 지정한 형식을 사용하여 행을 구문 분석할 수 없는 경우(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>). 예외 메시지에는 예외를 발생시키는 줄이 지정되어 있지만 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> 속성은 해당 줄에 포함되어 있는 텍스트에 할당됩니다.  
  
- 지정한 파일이 없는 경우(<xref:System.IO.FileNotFoundException>)  
  
- 사용자에게 파일에 액세스할 수 있는 권한이 없는 부분 신뢰 상황인 경우 (<xref:System.Security.SecurityException>).  
  
- 경로가 너무 긴 경우(<xref:System.IO.PathTooLongException>)  
  
- 사용자에게 파일에 액세스할 수 있는 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=nameWithType>
- [방법: 쉼표로 구분된 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)
- [방법: 여러 형식의 텍스트 파일에서 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-text-files-with-multiple-formats.md)
- [TextFieldParser 개체를 사용하여 텍스트 파일 구문 분석](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)
- [연습: Visual Basic에서 파일과 디렉터리 조작](../../../../visual-basic/developing-apps/programming/drives-directories-files/walkthrough-manipulating-files-and-directories.md)
- [문제 해결: 텍스트 파일 읽기 및 쓰기](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
