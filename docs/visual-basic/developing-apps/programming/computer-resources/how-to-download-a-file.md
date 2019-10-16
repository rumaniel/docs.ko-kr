---
title: '방법: Visual Basic에서 파일 다운로드'
ms.date: 07/20/2015
helpviewer_keywords:
- downloading Internet resources [Visual Basic], files
- downloading files [Visual Basic]
- remote computers [Visual Basic], downloading from
- files [Visual Basic], downloading
- files [Visual Basic], transferring
ms.assetid: ac479f81-c0e2-4b99-af73-217f446b73da
ms.openlocfilehash: 4dd45ef70dbe3b1949e6d787748bbb27bb88d52c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046610"
---
# <a name="how-to-download-a-file-in-visual-basic"></a>방법: Visual Basic에서 파일 다운로드

<xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A> 메서드를 사용하여 원격 파일을 다운로드한 다음 특정 위치에 저장할 수 있습니다. `ShowUI` 매개 변수가 `True`로 설정된 경우 다운로드 진행률을 표시하고 사용자가 작업을 취소할 수 있도록 하는 대화 상자가 표시됩니다. 기본적으로 동일한 이름의 기존 파일을 덮어쓰지 않습니다. 기존 파일을 덮어쓰려는 경우 `overwrite` 매개 변수를 `True`로 설정합니다.

다음 조건에서 예외가 발생합니다.

- 드라이브 이름이 잘못된 경우(<xref:System.ArgumentException>)

- 필요한 인증이 제공되지 않은 경우(<xref:System.UnauthorizedAccessException> 또는 <xref:System.Security.SecurityException>)

- 서버가 지정된 `connectionTimeout` 내에 응답하지 않는 경우(<xref:System.TimeoutException>)

- 웹 사이트에서 요청을 거부하는 경우(<xref:System.Net.WebException>)

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

> [!IMPORTANT]
> 파일 이름을 바탕으로 파일 내용을 판단하면 안 됩니다. 예를 들어 Form1.vb 파일이 Visual Basic 소스 파일이 아닐 수도 있습니다. 애플리케이션에서 데이터를 사용하기 전에 모든 입력을 확인해야 합니다. 파일의 내용이 예상한 내용과 다를 수 있으며 파일을 읽는 메서드가 실패할 수도 있습니다.

### <a name="to-download-a-file"></a>파일을 다운로드하려면

- 대상 파일의 위치를 문자열 또는 URI로 지정하고 파일을 저장할 위치를 지정하여 `DownloadFile` 메서드를 통해 파일을 다운로드합니다. 이 예제에서는 `http://www.cohowinery.com/downloads`에서 `WineList.txt` 파일을 다운로드하고 `C:\Documents and Settings\All Users\Documents`에 저장합니다.

  [!code-vb[VbResourceTasks#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#9)]

### <a name="to-download-a-file-specifying-a-time-out-interval"></a>시간 제한 간격을 지정하여 파일을 다운로드하려면

- 대상 파일의 위치를 문자열 또는 URI로 지정하고, 파일을 저장할 위치를 지정하고, 시간 제한 간격을 밀리초 단위로 지정(기본값은 1000)하여 `DownloadFile` 메서드를 통해 파일을 다운로드합니다. 이 예제에서는 시간 제한 간격을 500밀리초로 지정하여 `http://www.cohowinery.com/downloads`에서 `WineList.txt` 파일을 다운로드하고 `C:\Documents and Settings\All Users\Documents`에 저장합니다.

  [!code-vb[VbResourceTasks#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#10)]

### <a name="to-download-a-file-supplying-a-user-name-and-password"></a>사용자 이름 및 암호를 제공하여 파일을 다운로드하려면

- 대상 파일의 위치를 문자열 또는 URI로 지정하고 파일을 저장할 위치, 사용자 이름 및 암호를 지정하여 `DownLoadFile` 메서드를 통해 파일을 다운로드합니다. 이 예제에서는 사용자 이름 `anonymous` 및 빈 암호를 사용하여 `http://www.cohowinery.com/downloads`에서 `WineList.txt` 파일을 다운로드하고 `C:\Documents and Settings\All Users\Documents`에 저장합니다.

  [!code-vb[VbResourceTasks#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#11)]

  > [!IMPORTANT]
  > `DownLoadFile` 메서드에서 사용되는 FTP 프로토콜은 암호 등의 정보를 일반 텍스트로 보내므로 중요한 정보 전송에 사용하면 안 됩니다.

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.Devices.Network>
- <xref:Microsoft.VisualBasic.Devices.Network.DownloadFile%2A>
- [방법: 파일 업로드](../../../../visual-basic/developing-apps/programming/computer-resources/how-to-upload-a-file.md)
- [방법: 파일 경로의 구문 분석](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
