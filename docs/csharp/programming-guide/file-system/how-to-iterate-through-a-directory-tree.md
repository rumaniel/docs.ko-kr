---
title: '방법: 디렉터리 트리 반복 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- iterating through folders [C#]
- file iteration [C#]
ms.assetid: c4be4a75-6b1b-46a7-9d38-bab353091ed7
ms.openlocfilehash: ec48b9ff5a9ebe352bf0361b9e52ee0fb48576a8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923975"
---
# <a name="how-to-iterate-through-a-directory-tree-c-programming-guide"></a>방법: 디렉터리 트리 반복(C# 프로그래밍 가이드)
"디렉터리 트리 반복" 구는 지정된 루트 폴더 아래의 임의 깊이까지 중첩된 각 하위 디렉터리에 있는 각 파일에 대한 액세스를 의미합니다. 반드시 각 파일을 열 필요는 없습니다. 단순히 파일 또는 하위 디렉터리의 이름을 `string`으로 검색하거나, <xref:System.IO.FileInfo?displayProperty=nameWithType> 또는 <xref:System.IO.DirectoryInfo?displayProperty=nameWithType> 개체의 형태로 추가 정보를 검색할 수 있습니다.  
  
> [!NOTE]
> Windows에서 "디렉터리" 및 "폴더" 용어는 같은 의미로 사용됩니다. 대부분의 설명서와 사용자 인터페이스 텍스트는 "폴더"라는 용어를 사용하지만 .NET Framework 클래스 라이브러리는 "디렉터리"라는 용어를 사용합니다.  
  
 지정된 루트 아래의 모든 디렉터리에 대해 확실히 액세스 권한이 있는 가장 간단한 경우에는 `System.IO.SearchOption.AllDirectories` 플래그를 사용할 수 있습니다. 이 플래그는 지정된 패턴과 일치하는 모든 중첩된 하위 디렉터리를 반환합니다. 다음 예제에서는 이 플래그를 사용하는 방법을 보여 줍니다.  
  
```csharp  
root.GetDirectories("*.*", System.IO.SearchOption.AllDirectories);  
```  
  
 이 방식의 취약성은 지정된 루트 아래의 하위 디렉터리 중 하나에서 <xref:System.IO.DirectoryNotFoundException> 또는 <xref:System.UnauthorizedAccessException>이 발생할 경우 전체 메서드가 실패하고 디렉터리가 반환되지 않습니다. <xref:System.IO.DirectoryInfo.GetFiles%2A> 메서드를 사용하는 경우도 마찬가지입니다. 특정 하위 폴더에서 이러한 예외를 처리해야 하는 경우 다음 예제와 같이 디렉터리 트리를 수동으로 탐색해야 합니다.  
  
 디렉터리 트리를 수동으로 탐색하는 경우 하위 디렉터리를 먼저 처리하거나(*전위 순회*), 파일을 먼저 처리(*후위 순회*)할 수 있습니다. 전위 순회를 수행하는 경우 해당 폴더 자체에 바로 있는 파일을 반복하기 전에 현재 폴더 아래의 전체 트리를 탐색합니다. 이 문서의 뒷부분에 나오는 예제에서는 후위 순회를 수행하지만 전위 순회를 수행하도록 쉽게 수정할 수 있습니다.  
  
 또 다른 옵션은 재귀 또는 스택 기반 탐색을 사용하는지 여부입니다. 이 문서의 뒷부분에 나오는 예제에서는 두 가지 방식을 모두 보여 줍니다.  
  
 파일 및 폴더에 대해 다양한 작업을 수행해야 하는 경우 단일 대리자를 통해 호출할 수 있는 별도 함수로 작업을 리팩터링하여 이러한 예제를 모듈화할 수 있습니다.  
  
> [!NOTE]
> NTFS 파일 시스템에는 *재분석 지점*이 *연결 지점*, *기호 링크* 및 *하드 링크* 형태로 포함될 수 있습니다. <xref:System.IO.DirectoryInfo.GetFiles%2A>, <xref:System.IO.DirectoryInfo.GetDirectories%2A> 등의 .NET Framework 메서드는 재분석 지점 아래의 하위 디렉터리를 반환하지 않습니다. 이 동작은 두 재분석 지점이 서로를 가리키는 경우 무한 루프로 전환되는 위험으로부터 보호합니다. 일반적으로 재분석 지점을 다룰 때는 파일이 실수로 수정되거나 삭제되지 않도록 특별히 주의해야 합니다. 재분석 지점을 정밀하게 제어해야 하는 경우 플랫폼 호출 또는 네이티브 코드를 사용하여 적절한 Win32 파일 시스템 메서드를 직접 호출합니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 재귀를 사용하여 디렉터리 트리를 탐색하는 방법을 보여 줍니다. 재귀 방식은 세련된 방식이긴 하지만 디렉터리 트리가 크고 깊이 중첩된 경우 스택 오버플로 예외가 발생할 가능성이 있습니다.  
  
 처리되는 특정 예외와 각 파일 또는 폴더에서 수행되는 특정 작업은 예로만 제공됩니다. 특정 요구 사항에 맞게 이 코드를 수정해야 합니다. 자세한 내용은 코드 주석을 참조하세요.  
  
 [!code-csharp[csFilesandFolders#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#1)]  
  
## <a name="example"></a>예  
 다음 예제에서는 재귀를 사용하지 않고 디렉터리 트리의 파일 및 폴더를 반복하는 방법을 보여 줍니다. 이 기술은 LIFO(후입선출) 스택인 제네릭 <xref:System.Collections.Generic.Stack%601> 컬렉션 형식을 사용합니다.  
  
 처리되는 특정 예외와 각 파일 또는 폴더에서 수행되는 특정 작업은 예로만 제공됩니다. 특정 요구 사항에 맞게 이 코드를 수정해야 합니다. 자세한 내용은 코드 주석을 참조하세요.  
  
 [!code-csharp[csFilesandFolders#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csFilesAndFolders/CS/FileIteration.cs#2)]  
  
 일반적으로 모든 폴더를 테스트하여 애플리케이션에 폴더를 열 수 있는 권한이 있는지 확인하려면 너무 많은 시간이 걸립니다. 따라서 코드 예제에서는 해당 작업 부분을 `try/catch` 블록으로 묶습니다. 폴더에 대한 액세스가 거부될 경우 사용 권한을 높인 후 다시 액세스를 시도하도록 `catch` 블록을 수정할 수 있습니다. 일반적으로 애플리케이션을 알 수 없는 상태로 유지하지 않고 처리할 수 있는 예외만 catch합니다.  
  
 디렉터리 트리의 내용을 메모리 내 또는 디스크에 저장해야 하는 경우 최상의 옵션은 각 파일의 <xref:System.IO.FileSystemInfo.FullName%2A> 속성(`string` 형식)만 저장하는 것입니다. 그런 다음 이 문자열을 사용하여 필요에 따라 <xref:System.IO.FileInfo> 또는 <xref:System.IO.DirectoryInfo> 개체를 새로 만들거나, 추가 처리가 필요한 파일을 열 수 있습니다.  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 강력한 파일 반복 코드는 파일 시스템의 여러 복잡성을 고려해야 합니다. Windows 파일 시스템에 대한 자세한 내용은 [NTFS 개요](/windows-server/storage/file-server/ntfs-overview)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO>
- [LINQ 및 파일 디렉터리](../concepts/linq/linq-and-file-directories.md)
- [파일 시스템 및 레지스트리(C# 프로그래밍 가이드)](./index.md)
