---
title: '방법: Visual Basic에서 여러 형식의 텍스트 파일 읽기'
ms.date: 07/20/2015
helpviewer_keywords:
- TextFieldParser object, reading from a file
- TextFieldType enumeration
- My.Computer.FileSystem.WriteAllText method, parsing structured text files
- WriteAllText method [Visual Basic], parsing structured text files
- PeekChars method [Visual Basic], determining format of text
- reading text files [Visual Basic], multiple formats
- I/O [Visual Basic], reading text files
- text files [Visual Basic], reading
ms.assetid: 8d185eb2-79ca-42cd-95a7-d3ff44a5a0f8
ms.openlocfilehash: dc726f7648c1c0a564594331023f03d20569d766
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736815"
---
# <a name="how-to-read-from-fext-files-with-multiple-formats-in-visual-basic"></a>방법: Visual Basic에서 여러 형식의 텍스트 파일 읽기

<xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 개체는 로그와 같은 구조적 텍스트 파일을 쉽고 효율적으로 구문 분석하는 방법을 제공합니다. 파일을 구문 분석할 때 `PeekChars` 메서드를 사용하여 각 줄의 형식을 확인하면 여러 형식이 포함된 파일을 처리할 수 있습니다.
  
### <a name="to-parse-a-text-file-with-multiple-formats"></a>여러 형식이 포함된 텍스트 파일을 구문 분석하려면

1. *testfile.txt*라는 텍스트 파일을 프로젝트에 추가합니다. 텍스트 파일에 다음 콘텐츠를 추가합니다.

    ```text
    Err  1001 Cannot access resource.
    Err  2014 Resource not found.
    Acc  10/03/2009User1      Administrator.
    Err  0323 Warning: Invalid access attempt.
    Acc  10/03/2009User2      Standard user.
    Acc  10/04/2009User2      Standard user.
    ```

2. 필요한 형식 및 오류가 보고되었을 때 사용한 형식을 정의합니다. 각 배열의 마지막 항목이 -1이므로, 마지막 필드는 가변 너비로 가정됩니다. 이 오류는 배열의 마지막 항목이 0보다 작거나 같을 때 발생합니다.

     [!code-vb[VbFileIORead#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#4)]

3. 너비와 형식을 정의하는 새 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> 개체를 만듭니다.

     [!code-vb[VbFileIORead#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#5)]

4. 행을 반복하고 읽기 전에 형식을 테스트합니다.

     [!code-vb[VbFileIORead#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#6)]

5. 콘솔에 오류를 씁니다.

     [!code-vb[VbFileIORead#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#7)]

## <a name="example"></a>예

다음은 `testfile.txt` 파일에서 읽기를 수행하는 전체 예제입니다.

 [!code-vb[VbFileIORead#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#8)]

## <a name="robust-programming"></a>강력한 프로그래밍

다음 조건에서 예외가 발생합니다.  
  
- 지정한 형식을 사용하여 행을 구문 분석할 수 없는 경우(<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>). 예외 메시지에는 예외를 발생시키는 줄이 지정되어 있지만 <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> 속성은 해당 줄에 포함되어 있는 텍스트에 할당됩니다.
- 지정한 파일이 없는 경우(<xref:System.IO.FileNotFoundException>)
- 사용자에게 파일에 액세스할 수 있는 권한이 없는 부분 신뢰 상황인 경우 (<xref:System.Security.SecurityException>).
- 경로가 너무 긴 경우(<xref:System.IO.PathTooLongException>)
- 사용자에게 파일에 액세스할 수 있는 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.PeekChars%2A>
- <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.EndOfData%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TextFieldType%2A>
- [방법: 쉼표로 구분된 텍스트 파일에서 읽기](how-to-read-from-comma-delimited-text-files.md)
- [방법: 고정 너비 텍스트 파일에서 읽기](how-to-read-from-fixed-width-text-files.md)
- [TextFieldParser 개체를 사용하여 텍스트 파일 구문 분석](parsing-text-files-with-the-textfieldparser-object.md)
