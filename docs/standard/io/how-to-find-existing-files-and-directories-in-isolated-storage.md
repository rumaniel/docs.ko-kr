---
title: '방법: 격리된 스토리지의 기존 파일 및 디렉터리 찾기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- stores, finding files and directories
- locating files in isolated storage file
- directories [.NET Framework], isolated storage
- isolated storage, finding files and directories
- data storage using isolated storage, finding files and directories
- files [.NET Framework], isolated storage
- data stores, finding files and directories
- locating directories in isolated storage file
- storing data using isolated storage, finding files and directories
ms.assetid: eb28458a-6161-4e7a-9ada-30ef93761b5c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 277f7d562d5e345556a9047f6e4bf2b60eaef462
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54646713"
---
# <a name="how-to-find-existing-files-and-directories-in-isolated-storage"></a>방법: 격리된 스토리지의 기존 파일 및 디렉터리 찾기

격리된 스토리지에서 디렉터리를 검색하려면 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A?displayProperty=nameWithType> 메서드를 사용합니다. 이 메서드는 검색 패턴을 나타내는 문자열을 사용합니다. 검색 패턴에서 단일 문자(?) 및 여러 문자(\*) 와일드카드 문자를 모두 사용할 수 있지만, 와일드카드 문자는 이름의 마지막 부분에 표시되어야 합니다. 예를 들어, `directory1/*ect*`는 올바른 검색 문자열이지만 `*ect*/directory2`는 잘못된 검색 문자열입니다.  
  
 파일을 검색하려면 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A?displayProperty=nameWithType> 메서드를 사용합니다. <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A>에 적용되는 검색 문자열의 와일드카드 문자 제한 사항이 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>에도 똑같이 적용됩니다.  
  
 이러한 메서드는 둘 다 재귀적입니다. <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 클래스는 저장소의 모든 디렉터리 또는 파일을 열거하는 메서드를 제공하지 않습니다. 그러나 다음 코드 예제에서 재귀 메서드를 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 분리된 저장소에서 파일 및 디렉터리를 만드는 방법을 보여줍니다. 먼저 사용자, 도메인 및 어셈블리별로 격리된 저장소를 검색하여 `isoStore` 변수에 대입합니다. <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A> 메서드는 몇 개의 디렉터리를 설정하는 데 사용되고 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream.%23ctor%28System.String%2CSystem.IO.FileMode%2CSystem.IO.IsolatedStorage.IsolatedStorageFile%29> 생성자는 이러한 디렉터리에 몇 개의 파일을 만듭니다. 그런 다음 코드는 `GetAllDirectories` 메서드의 결과를 반복합니다. 이 메서드는 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A>를 사용하여 현재 디렉터리에서 모든 디렉터리 이름을 찾습니다. 이러한 이름이 배열로 저장된 다음 `GetAllDirectories`는 찾은 각 디렉터리를 전달하기 위해 자신을 호출합니다. 결과적으로, 모든 디렉터리 이름은 배열에 반환됩니다. 다음으로 코드는 `GetAllFiles` 메서드를 호출합니다. 이 메서드는 `GetAllDirectories`를 호출하여 모든 디렉터리의 이름을 확인한 다음 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> 메서드를 사용하여 각 디렉터리를 검사하여 파일을 확인합니다. 결과는 표시를 위해 배열로 반환됩니다.  
  
 [!code-cpp[Conceptual.IsolatedStorage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source8.cpp#9)]
 [!code-csharp[Conceptual.IsolatedStorage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source8.cs#9)]
 [!code-vb[Conceptual.IsolatedStorage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source8.vb#9)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- [격리된 스토리지](../../../docs/standard/io/isolated-storage.md)
