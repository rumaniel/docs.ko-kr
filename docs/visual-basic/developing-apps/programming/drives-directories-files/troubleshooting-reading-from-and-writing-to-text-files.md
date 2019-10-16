---
title: '문제 해결: 텍스트 파일 읽기 및 쓰기(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting file I/O
- writing text to files [Visual Basic], troubleshooting
- troubleshooting Visual Basic, text files
- I/O [Visual Basic], troubleshooting text files
- writing to files [Visual Basic], troubleshooting
- reading text files [Visual Basic], troubleshooting
ms.assetid: a8e9b44d-facb-4718-8c0f-466537171182
ms.openlocfilehash: 90a04d9de2ac77c28a92d99e1fe118a1f8ecf448
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58831789"
---
# <a name="troubleshooting-reading-from-and-writing-to-text-files-visual-basic"></a>문제 해결: 텍스트 파일 읽기 및 쓰기(Visual Basic)
이 항목에서는 텍스트 파일로 작업할 때 발생하는 일반적인 문제를 설명하고 각 문제에 대한 접근 방법을 제안합니다.  
  
## <a name="common-problems"></a>일반적인 문제  
 텍스트 파일로 작업할 때 발생하는 가장 일반적인 문제에는 보안 예외, 파일 인코딩, 잘못된 경로 등이 있습니다.  
  
### <a name="security-exceptions"></a>보안 예외  
 보안 오류가 발생하면 <xref:System.Security.SecurityException>이 throw됩니다. 이 예외는 사용자에게 필요한 사용 권한이 없어서 발생하는 경우가 많으며, 격리된 스토리지의 파일로 작업하거나 사용 권한을 추가하면 해결할 수 있습니다.  
  
### <a name="file-encodings"></a>파일 인코딩  
 문자 인코딩이라고도 하는 파일 인코딩은 텍스트 처리 시 문자를 나타내는 방법을 지정합니다. 텍스트 파일의 예기치 않은 문자는 잘못된 인코딩에서 발생할 수 있습니다. 처리할 수 있거나 없는 언어 문자를 기준으로 대부분의 파일에서 특정 인코딩이 다른 인코딩보다 선호될 수 있지만, 일반적으로 유니코드가 선호됩니다. 자세한 내용은 [파일 인코딩](../../../../visual-basic/developing-apps/programming/drives-directories-files/file-encodings.md) 및 <xref:System.Text.Encoding>을 참조하세요.  
  
### <a name="incorrect-paths"></a>잘못된 경로  
 파일 경로, 특히 상대 경로를 구문 분석할 때 잘못된 데이터를 제공하기 쉽습니다. 올바른 경로를 제공하면 많은 문제를 해결할 수 있습니다. 자세한 내용은 [방법: 파일 경로의 구문 분석](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem>
- [파일 읽기](../../../../visual-basic/developing-apps/programming/drives-directories-files/reading-from-files.md)
- [파일에 쓰기](../../../../visual-basic/developing-apps/programming/drives-directories-files/writing-to-files.md)
- [TextFieldParser 개체를 사용하여 텍스트 파일 구문 분석](../../../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)
