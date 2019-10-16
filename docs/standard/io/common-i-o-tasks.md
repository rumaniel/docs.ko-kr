---
title: 공통적인 I/O 작업
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- I/O, common tasks
ms.assetid: bf00c380-706a-4e38-b829-454a480629fc
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ac2b0eafa64b809d2b40ac6471806dc9ab3c8c53
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54609631"
---
# <a name="common-io-tasks"></a>공통적인 I/O 작업
<xref:System.IO> 네임스페이스에는 파일, 디렉터리 및 스트림에 대해 읽기, 쓰기 등의 다양한 작업을 수행할 수 있게 해 주는 여러 클래스가 있습니다. 자세한 내용은 [파일 및 스트림 I/O](../../../docs/standard/io/index.md)를 참조하세요.  
  
## <a name="common-file-tasks"></a>공통적인 파일 작업  
  
|수행 작업|참조 항목|  
|-------------------|--------------------------------------|  
|텍스트 파일 만들기|<xref:System.IO.File.CreateText%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.CreateText%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.File.Create%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.Create%2A?displayProperty=nameWithType> 메서드|  
|텍스트 파일에 쓰기|[방법: 파일에 텍스트 쓰기](../../../docs/standard/io/how-to-write-text-to-a-file.md)<br /><br /> [방법: 텍스트 파일 쓰기(C++/CLI)](/cpp/dotnet/how-to-write-a-text-file-cpp-cli)|  
|텍스트 파일에서 읽기|[방법: 파일에서 텍스트 읽기](../../../docs/standard/io/how-to-read-text-from-a-file.md)|  
|파일에 텍스트 추가|[방법: 로그 파일 열기 및 추가](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)<br /><br /> <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.AppendText%2A?displayProperty=nameWithType> 메서드|  
|파일 이름 바꾸기 또는 이동|<xref:System.IO.File.Move%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.MoveTo%2A?displayProperty=nameWithType> 메서드|  
|파일 삭제|<xref:System.IO.File.Delete%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.Delete%2A?displayProperty=nameWithType> 메서드|  
|파일 복사|<xref:System.IO.File.Copy%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.CopyTo%2A?displayProperty=nameWithType> 메서드|  
|파일 크기 가져오기|<xref:System.IO.FileInfo.Length%2A?displayProperty=nameWithType> 속성|  
|파일 특성 가져오기|<xref:System.IO.File.GetAttributes%2A?displayProperty=nameWithType> 메서드|  
|파일의 특성 설정|<xref:System.IO.File.SetAttributes%2A?displayProperty=nameWithType> 메서드|  
|파일이 있는지 확인|<xref:System.IO.File.Exists%2A?displayProperty=nameWithType> 메서드|  
|이진 파일에서 읽기|[방법: 새로 만든 데이터 파일 읽기 및 쓰기](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|이진 파일에 쓰기|[방법: 새로 만든 데이터 파일 읽기 및 쓰기](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|  
|파일 이름 확장명 검색|<xref:System.IO.Path.GetExtension%2A?displayProperty=nameWithType> 메서드|  
|파일의 정규화된 경로 검색|<xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> 메서드|  
|경로에서 파일 이름 및 확장명 검색|<xref:System.IO.Path.GetFileName%2A?displayProperty=nameWithType> 메서드|  
|파일의 확장명 변경|<xref:System.IO.Path.ChangeExtension%2A?displayProperty=nameWithType> 메서드|  
  
## <a name="common-directory-tasks"></a>공통적인 디렉터리 작업  
  
|수행 작업|참조 항목|  
|-------------------|--------------------------------------|  
|내 문서와 같은 특수 폴더에 있는 파일에 액세스|[방법: 파일에 텍스트 쓰기](../../../docs/standard/io/how-to-write-text-to-a-file.md)|  
|디렉터리 만들기|<xref:System.IO.Directory.CreateDirectory%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.FileInfo.Directory%2A?displayProperty=nameWithType> 속성|  
|하위 디렉터리 만들기|<xref:System.IO.DirectoryInfo.CreateSubdirectory%2A?displayProperty=nameWithType> 메서드|  
|디렉터리 이름 바꾸기 또는 이동|<xref:System.IO.Directory.Move%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.DirectoryInfo.MoveTo%2A?displayProperty=nameWithType> 메서드|  
|디렉터리 복사|[방법: 디렉터리 복사](../../../docs/standard/io/how-to-copy-directories.md)|  
|디렉터리 삭제|<xref:System.IO.Directory.Delete%2A?displayProperty=nameWithType> 메서드<br /><br /> <xref:System.IO.DirectoryInfo.Delete%2A?displayProperty=nameWithType> 메서드|  
|디렉터리에 있는 파일 및 하위 디렉터리 보기|[방법: 디렉터리 및 파일 열거](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)|  
|디렉터리 크기 찾기|<xref:System.IO.Directory?displayProperty=nameWithType> 클래스|  
|디렉터리가 있는지 확인|<xref:System.IO.Directory.Exists%2A?displayProperty=nameWithType> 메서드|  
  
## <a name="see-also"></a>참고 항목

- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
- [스트림 작성](../../../docs/standard/io/composing-streams.md)
- [Asynchronous File I/O](../../../docs/standard/io/asynchronous-file-i-o.md)
