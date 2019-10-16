---
title: '방법: Visual Basic에서 특정 패턴의 하위 디렉터리 찾기'
ms.date: 07/20/2015
helpviewer_keywords:
- pattern matching
- folders, finding
ms.assetid: c9265fd1-7483-4150-8b7f-ff642caa939d
ms.openlocfilehash: 96ae5c5c44263a47343058012d8b8aa064d9cd92
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71039445"
---
# <a name="how-to-find-subdirectories-with-a-specific-pattern-in-visual-basic"></a>방법: Visual Basic에서 특정 패턴의 하위 디렉터리 찾기

<xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A> 메서드는 디렉터리에 있는 하위 디렉터리의 경로 이름을 나타내는 읽기 전용 문자열 컬렉션을 반환합니다. `wildCards` 매개 변수를 사용하여 특정 패턴을 지정할 수 있습니다. 하위 디렉터리의 내용을 검색에 포함하려면 `searchType` 매개 변수를 `SearchOption.SearchAllSubDirectories`로 설정합니다.

지정한 패턴과 일치하는 디렉터리가 없으면 빈 컬렉션이 반환됩니다.

## <a name="to-find-subdirectories-with-a-specific-pattern"></a>특정 패턴의 하위 디렉터리를 찾으려면

검색하려는 디렉터리의 이름 및 경로를 제공하여 `GetDirectories` 메서드를 사용합니다. 다음 예제에서는 디렉터리 구조에서 이름에 "Logs" 단어가 포함된 모든 디렉터리를 반환하고 `ListBox1`에 추가합니다.

[!code-vb[VbVbcnFileAccess#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnFileAccess/VB/Class1.vb#1)]

## <a name="robust-programming"></a>강력한 프로그래밍

다음 조건에서 예외가 발생합니다.

- 길이가 0인 문자열이거나, 공백만 포함하거나, 잘못된 문자를 포함하거나, 경로가 디바이스 경로인 경우(\\\\.\\로 시작됨)와 같은 여러 가지 이유 중 하나로 경로가 올바르지 않은 경우(<xref:System.ArgumentException>)

- 경로가 `Nothing`이기 때문에 올바르지 않은 경우(<xref:System.ArgumentNullException>)

- 지정된 와일드카드 문자 중 하나 이상이 `Nothing` 또는 빈 문자열이거나 공백으로만 구성된 경우(<xref:System.ArgumentNullException>)

- `directory`가 없는 경우(<xref:System.IO.DirectoryNotFoundException>)

- `directory`가 기존 파일을 가리키는 경우(<xref:System.IO.IOException>)

- 경로가 시스템 정의 최대 길이를 초과하는 경우(<xref:System.IO.PathTooLongException>)

- 경로의 파일 이름이나 폴더 이름에 콜론(:)이 있거나 이름의 형식이 잘못된 경우(<xref:System.NotSupportedException>)

- 경로를 보는 데 필요한 권한이 사용자에게 없는 경우(<xref:System.Security.SecurityException>)

- 사용자에게 필요한 권한이 없는 경우(<xref:System.UnauthorizedAccessException>)

## <a name="see-also"></a>참고 항목

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.GetDirectories%2A>
- [방법: 특정 패턴의 파일 찾기](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-files-with-a-specific-pattern.md)
