---
title: '방법: 파일 및 폴더 복사, 삭제 및 이동 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- I/O [C#]
ms.assetid: 62e52cd7-9597-4e4a-acf9-1315f5cdbf05
ms.openlocfilehash: dd32798062dbfc9a10acd27ce51d8d5dd3b164f6
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590094"
---
# <a name="how-to-copy-delete-and-move-files-and-folders-c-programming-guide"></a>방법: 파일 및 폴더 복사, 삭제 및 이동(C# 프로그래밍 가이드)
다음 예제에서는 <xref:System.IO?displayProperty=nameWithType> 네임스페이스의 <xref:System.IO.File?displayProperty=nameWithType>, <xref:System.IO.Directory?displayProperty=nameWithType>, <xref:System.IO.FileInfo?displayProperty=nameWithType>, <xref:System.IO.DirectoryInfo?displayProperty=nameWithType> 클래스를 사용하여 파일과 폴더를 동기 방식으로 복사, 이동 및 삭제하는 방법을 보여 줍니다. 이러한 예제는 진행률 표시줄이나 다른 사용자 인터페이스를 제공하지 않습니다. 표준 진행률 대화 상자를 제공하려면 [방법: 파일 작업에 대한 진행률 대화 상자 제공](how-to-provide-a-progress-dialog-box-for-file-operations.md)을 참조하세요.  
  
 <xref:System.IO.FileSystemWatcher?displayProperty=nameWithType>를 사용하여 여러 파일에 대해 작업할 때 진행률을 계산할 수 있는 이벤트를 제공할 수 있습니다. 또 다른 방법은 플랫폼 호출을 사용하여 Windows Shell에서 적절한 파일 관련 메서드를 호출하는 것입니다. 이러한 파일 작업을 비동기적으로 수행하는 방법에 대한 자세한 내용은 [비동기 파일 I/O](../../../standard/io/asynchronous-file-i-o.md)를 참조하세요.  
  
## <a name="example"></a>예  
 다음 예제에서는 파일 및 디렉터리를 복사하는 방법을 보여 줍니다.  
  
 [!code-csharp[csFilesandFolders#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#7)]  
  
## <a name="example"></a>예  
 다음 예제에서는 파일 및 디렉터리를 이동하는 방법을 보여 줍니다.  
  
 [!code-csharp[csFilesandFolders#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#8)]  
  
## <a name="example"></a>예  
 다음 예제에서는 파일 및 디렉터리를 삭제하는 방법을 보여 줍니다.  
  
 [!code-csharp[csFilesandFolders#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#9)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO?displayProperty=nameWithType>
- [C# 프로그래밍 가이드](../index.md)
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](index.md)
- [방법: 파일 작업에 대한 진행률 대화 상자 제공](how-to-provide-a-progress-dialog-box-for-file-operations.md)
- [파일 및 스트림 I/O](../../../standard/io/index.md)
- [공통적인 I/O 작업](../../../standard/io/common-i-o-tasks.md)
