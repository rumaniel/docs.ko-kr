---
title: '방법: Visual Basic에서 파일 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- text files [Visual Basic], creating
- files [Visual Basic], creating
ms.assetid: 0253bb6d-5519-4a50-b882-b93ef5cca0d9
ms.openlocfilehash: f24fdd6ce1fea7540c33e4a2fdfc06885825f76a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64628989"
---
# <a name="how-to-create-a-file-in-visual-basic"></a>방법: Visual Basic에서 파일 만들기
이 예제에서는 <xref:System.IO.File> 클래스의 <xref:System.IO.File.Create%2A> 메서드를 사용하여 지정된 경로에 빈 텍스트 파일을 만듭니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbFileIOMisc#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIOMisc/VB/class2.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 파일에 쓰려면 `file` 변수를 사용합니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 파일이 이미 있으면 대체됩니다.  
  
 다음 조건에서 예외가 발생합니다.  
  
- 경로 이름 형식이 잘못되었습니다. 예를 들어 잘못된 문자를 포함하거나 공백만으로 이루어져 있습니다(<xref:System.ArgumentException>).  
  
- 경로가 읽기 전용인 경우(<xref:System.IO.IOException>)  
  
- 경로 이름이 `Nothing`인 경우(<xref:System.ArgumentNullException>)  
  
- 경로 이름이 너무 긴 경우(<xref:System.IO.PathTooLongException>)  
  
- 경로가 잘못된 경우(<xref:System.IO.DirectoryNotFoundException>)  
  
- 경로가 콜론 ":"뿐인 경우(<xref:System.NotSupportedException>)  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 부분 신뢰 환경에서는 <xref:System.Security.SecurityException>이 throw될 수 있습니다.  
  
 <xref:System.IO.File.Create%2A> 메서드를 호출하려면 <xref:System.Security.Permissions.FileIOPermission>이 필요합니다.  
  
 사용자에게 파일을 만들 수 있는 권한이 없으면 <xref:System.UnauthorizedAccessException>이 throw됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO>
- <xref:System.IO.File.Create%2A>
- [부분적으로 신뢰할 수 있는 코드에서 라이브러리 사용](../../../../framework/misc/using-libraries-from-partially-trusted-code.md)
- [코드 액세스 보안 기본 사항](../../../../framework/misc/code-access-security-basics.md)
