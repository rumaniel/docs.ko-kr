---
title: '방법: 격리된 스토리지의 파일 및 디렉터리 만들기'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- directories [.NET Framework], isolated storage
- files [.NET Framework], isolated storage
- isolated storage, creating files and directories
- data stores, creating files and directories
- data storage using isolated storage, creating files and directories
- stores, creating files and directories
- storing data using isolated storage, creating files and directories
ms.assetid: 2ca4d2a4-809b-4f00-bc08-bf4a64d3a5c3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 92f4b686a5a2bdc74ff3f0f68de4c6b2048da5a1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54709015"
---
# <a name="how-to-create-files-and-directories-in-isolated-storage"></a>방법: 격리된 스토리지의 파일 및 디렉터리 만들기
격리된 저장소를 가져온 다음에는 데이터를 저장할 디렉터리와 파일을 만들 수 있습니다. 저장소 내에서 파일 및 디렉터리 이름은 가상 파일 시스템의 루트와 관련하여 지정됩니다.  
  
 디렉터리를 만들려면 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=nameWithType> 인스턴스 메서드를 사용하십시오. 존재하지 않는 디렉터리의 하위 디렉터리를 지정하면 두 디렉터리가 모두 만들어지고 이미 존재하는 디렉터리를 지정하면 메서드가 디렉터리를 만들지 않은 채 반환되고 예외가 throw되지 않습니다. 그러나 잘못된 문자를 포함하는 디렉터리 이름을 지정하면 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 예외가 throw됩니다.  
  
 파일을 만들려면 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 Windows 운영 체제에서 격리된 스토리지 파일 및 디렉터리 이름은 대/소문자를 구분하지 않습니다. 즉, `ThisFile.txt`라는 파일을 만든 다음 `THISFILE.TXT`라는 다른 파일을 만들면 한 파일만 만들어집니다. 파일 이름은 표시를 위해 원래 대소문자를 유지합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 분리된 저장소에서 파일 및 디렉터리를 만드는 방법을 보여줍니다.  
  
 [!code-csharp[Conceptual.IsolatedStorage#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source.cs#1)]
 [!code-vb[Conceptual.IsolatedStorage#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source.vb#1)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>
- [격리된 스토리지](../../../docs/standard/io/isolated-storage.md)
