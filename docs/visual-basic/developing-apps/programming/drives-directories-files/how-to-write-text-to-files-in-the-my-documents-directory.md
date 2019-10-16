---
title: '방법: Visual Basic에서 내 문서 디렉터리의 파일에 텍스트 쓰기'
ms.date: 07/20/2015
helpviewer_keywords:
- files [Visual Basic], writing to
- text, writing to files
- examples [Visual Basic], text files
- writing to files [Visual Basic], in My Documents
ms.assetid: 1c726124-781d-4976-9baa-ed46814ff3fe
ms.openlocfilehash: 4f9eb4c9e0eb92712b5ea1a4feef24f2bb95d70b
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59335461"
---
# <a name="how-to-write-text-to-files-in-the-my-documents-directory-in-visual-basic"></a>방법: Visual Basic에서 내 문서 디렉터리의 파일에 텍스트 쓰기
`My.Computer.FileSystem.SpecialDirectories` 개체를 사용하면 **MyDocuments** 디렉터리 등의 특수 디렉터리에 액세스할 수 있습니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-write-new-text-files-in-the-my-documents-directory"></a>내 문서 디렉터리에 새 텍스트 파일을 쓰려면  
  
1. `My.Computer.FileSystem.SpecialDirectories.MyDocuments` 속성을 사용하여 경로를 제공합니다.  
  
     [!code-vb[VbFileIOWrite#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#1)]  
  
2. `WriteAllText` 메서드를 사용하여 지정한 파일에 텍스트를 씁니다.  
  
     [!code-vb[VbVbcnMyFileSystem#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#14)]  
  
## <a name="example"></a>예제  
 [!code-vb[VbFileIOWrite#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOWrite/VB/Class1.vb#2)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 `test.txt`를 쓰려는 파일 이름으로 바꿉니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 이 코드는 파일에 텍스트를 쓸 때 발생할 수 있는 모든 예외를 다시 throw합니다. 유효한 파일 이름에 대한 사용자 선택 항목을 제한하는 [OpenFileDialog](../../../../framework/winforms/controls/openfiledialog-component-windows-forms.md) 및 [SaveFileDialog](../../../../framework/winforms/controls/savefiledialog-component-windows-forms.md) 구성 요소와 같은 Windows Forms 컨트롤을 사용하여 예외 발생 가능성을 줄일 수 있습니다. 그러나 이러한 컨트롤을 사용해도 예외가 완전히 방지되지는 않습니다. 사용자가 파일을 선택한 시간과 코드가 실행되는 시간 사이에 파일 시스템이 변경될 수 있습니다. 따라서 파일 작업 시에는 거의 항상 예외 처리가 필요합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 부분 신뢰 컨텍스트에서 실행하는 경우 권한 부족으로 인해 코드에서 예외를 throw할 수 있습니다. 자세한 내용은 [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)을 참조하세요.  
  
 이 예제에서는 새 파일을 만듭니다. 애플리케이션에서 파일을 만들어야 하는 경우 해당 애플리케이션에 폴더에 대한 만들기 권한이 있어야 합니다. 권한은 액세스 제어 목록을 사용하여 설정됩니다. 파일이 이미 있는 경우에는 애플리케이션에 더 낮은 권한인 쓰기 권한만 있으면 됩니다. 가능한 경우 배포하는 동안 파일을 만들고, 폴더에 대한 만들기 권한 대신 단일 파일에 대한 읽기 권한만 부여하는 것이 더 안전합니다. 또한 루트 폴더나 **Program Files** 폴더보다 사용자 폴더에 데이터를 쓰는 것이 더 안전합니다. 자세한 내용은 [ACL 기술 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229742(v=vs.100))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.Path.Combine%2A?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>
