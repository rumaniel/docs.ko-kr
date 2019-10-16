---
title: '방법: Visual Basic에서 파일 업로드'
ms.date: 07/20/2015
helpviewer_keywords:
- networks, uploading files
- files [Visual Basic], uploading
- uploading files [Visual Basic]
- UploadFile method [Visual Basic]
- My.Computer.Network.UploadFile method
ms.assetid: a8b37924-c523-4fd3-b5ca-cb0074df29cd
ms.openlocfilehash: b2c313078e3438c84068b6cc54d787b567a768b8
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64662705"
---
# <a name="how-to-upload-a-file-in-visual-basic"></a>방법: Visual Basic에서 파일 업로드
<xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A> 메서드는 파일을 업로드하고 원격 위치에 저장하는 데 사용될 수 있습니다. `ShowUI` 매개 변수를 `True`로 설정하면 업로드 진행률을 표시하고 사용자가 작업을 취소할 수 있도록 하는 대화 상자가 표시됩니다.  
  
### <a name="to-upload-a-file"></a>파일을 업로드하려면  
  
- 소스 파일 위치와 대상 디렉터리 위치를 문자열 또는 URI(Uniform Resource Identifier)로 지정하여 `UploadFile` 메서드를 통해 파일을 업로드합니다. 이 예제에서는 `Order.txt` 파일을 `http://www.cohowinery.com/uploads.aspx`에 업로드합니다.  
  
     [!code-vb[VbResourceTasks#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#6)]  
  
### <a name="to-upload-a-file-and-show-the-progress-of-the-operation"></a>파일을 업로드하고 작업 진행률을 표시하려면  
  
- 소스 파일 위치와 대상 디렉터리 위치를 문자열 또는 URI로 지정하여 `UploadFile` 메서드를 통해 파일을 업로드합니다. 이 예제에서는 사용자 이름 또는 암호를 제공하지 않고 `Order.txt` 파일을 `http://www.cohowinery.com/uploads.aspx`에 업로드하며, 업로드 진행률을 표시하고, 시간 제한 간격으로 500밀리초가 지정됩니다.  
  
     [!code-vb[VbResourceTasks#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#7)]  
  
### <a name="to-upload-a-file-supplying-a-user-name-and-password"></a>사용자 이름 및 암호를 제공하여 파일을 업로드하려면  
  
- 소스 파일 위치와 대상 디렉터리 위치를 문자열 또는 URI로 지정하고 사용자 이름 및 암호를 지정하여 `UploadFile` 메서드를 통해 파일을 업로드합니다. 이 예제에서는 사용자 이름 `anonymous` 및 빈 암호를 제공하여 `Order.txt` 파일을 `http://www.cohowinery.com/uploads.aspx`에 업로드합니다.  
  
     [!code-vb[VbResourceTasks#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#8)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서는 예외가 throw될 수 있습니다.  
  
- 로컬 파일 경로가 잘못된 경우(<xref:System.ArgumentException>)  
  
- 인증에 실패한 경우(<xref:System.Security.SecurityException>)  
  
- 연결 시간이 초과된 경우(<xref:System.TimeoutException>)  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Devices.Network?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Devices.Network.UploadFile%2A>
- [방법: 파일 다운로드](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-download-a-file.md)
- [방법: 파일 경로의 구문 분석](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
