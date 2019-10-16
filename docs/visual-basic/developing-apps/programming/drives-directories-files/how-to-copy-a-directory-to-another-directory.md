---
title: '방법: Visual Basic에서 디렉터리를 다른 디렉터리에 복사'
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [Visual Basic], copying directories
- I/O [Visual Basic], copying folders
- folders [Visual Basic], copying
- directories [Visual Basic], copying
ms.assetid: 2a370bd7-10ba-4219-afc4-4519d031eb6c
ms.openlocfilehash: d8f32da0f4b701d745cd5f70feb7cc461a09842f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039463"
---
# <a name="how-to-copy-a-directory-to-another-directory-in-visual-basic"></a>방법: Visual Basic에서 디렉터리를 다른 디렉터리에 복사

<xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A> 메서드를 사용하여 디렉터리를 다른 디렉터리에 복사합니다. 이 메서드는 디렉터리 자체뿐만 아니라 디렉터리 내용을 복사합니다. 대상 디렉터리가 없는 경우 새로 만듭니다. 같은 이름의 디렉터리가 대상 위치에 있고 `overwrite`가 `False`로 설정된 경우 두 디렉터리의 내용이 병합됩니다. 작업 중에 디렉터리의 새 이름을 지정할 수 있습니다.

디렉터리 내의 파일을 복사하는 경우 `overwrite`가 `False`로 설정된 동안 병합 중에 있는 파일 등의 특정 파일에서 발생하는 예외가 throw될 수 있습니다. 이러한 예외가 throw되면 `Data` 속성이 파일 또는 디렉터리 경로가 키이고 특정 예외 메시지가 해당 값에 포함된 항목을 저장하는 단일 예외에 통합됩니다.

## <a name="to-copy-a-directory-to-another-directory"></a>디렉터리를 다른 디렉터리에 복사하려면

- 소스 및 대상 디렉터리 이름을 지정하여 `CopyDirectory` 메서드를 사용합니다. 다음 예제에서는 `TestDirectory1`이라는 디렉터리를 `TestDirectory2`에 복사하고 기존 파일을 덮어씁니다.

    [!code-vb[VbVbcnMyFileSystem#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#16)]

    이 코드 예제는 IntelliSense 코드 조각으로 사용할 수도 있습니다. 코드 조각 선택에서 **파일 시스템 - 드라이브, 폴더, 파일 처리**에 있습니다. 자세한 내용은 [코드 조각](/visualstudio/ide/code-snippets)을 참조하세요.

## <a name="robust-programming"></a>강력한 프로그래밍

다음 조건에서 예외가 발생합니다.

- 디렉터리에 대해 지정된 새 이름이 콜론(:) 또는 슬래시(\ 또는 /)를 포함하는 경우(<xref:System.ArgumentException>)

- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)

- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)

- `destinationDirectoryName`이 `Nothing` 또는 빈 문자열인 경우(<xref:System.ArgumentNullException>)

- 소스 디렉터리가 없는 경우(<xref:System.IO.DirectoryNotFoundException>)

- 소스 디렉터리가 루트 디렉터리인 경우(<xref:System.IO.IOException>)

- 조합된 경로가 기존 파일을 가리키는 경우(<xref:System.IO.IOException>)

- 소스 경로 및 대상 경로가 동일한 경우(<xref:System.IO.IOException>)

- `ShowUI`가 `UIOption.AllDialogs`로 설정되었으며 사용자가 작업을 취소하거나 디렉터리에 있는 하나 이상의 파일을 복사할 수 없는 경우(<xref:System.OperationCanceledException>)

- 작업이 순환 방식인 경우(<xref:System.InvalidOperationException>)

- 경로에 콜론(:)이 포함된 경우(<xref:System.NotSupportedException>)

- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)

- 경로의 파일 이름이나 폴더 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)

- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)

- 대상 파일이 있지만 액세스할 수 없는 경우(<xref:System.UnauthorizedAccessException>)

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyDirectory%2A>
- [방법: 특정 패턴의 하위 디렉터리 찾기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)
- [방법: 디렉터리에 있는 파일의 컬렉션 가져오기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)
