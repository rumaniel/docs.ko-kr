---
title: '방법: 파일 압축 및 추출'
ms.date: 01/14/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O [.NET Framework], compression
- compression
- compress files
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9a4ea4c32f5b73b283a5982f16e55a4d078171c1
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55255005"
---
# <a name="how-to-compress-and-extract-files"></a>방법: 파일 압축 및 추출

<xref:System.IO.Compression> 네임스페이스는 파일 및 스트림을 압축하고 압축을 푸는 다음 형식을 포함합니다. 또한 이러한 형식을 사용하여 압축된 파일의 내용을 읽고 수정할 수 있습니다.

- <xref:System.IO.Compression.ZipFile>
- <xref:System.IO.Compression.ZipArchive>
- <xref:System.IO.Compression.ZipArchiveEntry>
- <xref:System.IO.Compression.DeflateStream>
- <xref:System.IO.Compression.GZipStream>

다음 예제에서는 압축된 파일로 수행할 수 있는 일부 작업을 보여줍니다.

## <a name="example-1-create-and-extract-a-zip-file"></a>예제 1: .zip 파일 만들기 및 추출

다음 예제에서는 <xref:System.IO.Compression.ZipFile> 클래스를 사용하여 압축된 *.zip* 파일을 만들고 추출하는 방법을 보여줍니다. 이 예제는 폴더의 콘텐츠를 새로운 *.zip* 파일로 압축한 다음, zip을 새 폴더에 추출합니다. 

샘플을 실행하려면 프로그램 폴더에 *start* 폴더를 만들어서 zip 파일로 채웁니다. 

"'ZipFile' 이름이 현재 컨텍스트에 없습니다."라는 빌드 오류가 발생하면 `System.IO.Compression.FileSystem` 어셈블리에 대한 참조를 프로젝트에 추가합니다.

[!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]

## <a name="example-2-extract-specific-file-extensions"></a>예제 2: 특정 파일 확장명 추출

다음 예제는 기존 *.zip* 파일의 콘텐츠를 반복하고 확장명이 *.txt*인 파일을 추출합니다. <xref:System.IO.Compression.ZipArchive> 클래스를 사용하여 zip에 액세스하고 <xref:System.IO.Compression.ZipArchiveEntry> 클래스를 사용하여 개별 항목을 검사합니다. <xref:System.IO.Compression.ZipArchiveEntry> 개체의 <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A> 확장 메서드는 <xref:System.IO.Compression.ZipFileExtensions?displayProperty=nameWithType> 클래스에서 사용할 수 있습니다. 

샘플을 실행하려면 *result.zip*이라는 *.zip* 파일을 프로그램 폴더에 둡니다. 메시지가 표시되면 추출할 폴더 이름을 입력합니다. 

"'ZipFile' 이름이 현재 컨텍스트에 없습니다."라는 빌드 오류가 발생하면 `System.IO.Compression.FileSystem` 어셈블리에 대한 참조를 프로젝트에 추가합니다.

"'ZipArchive' 형식이 참조되지 않은 어셈블리에 정의되었습니다."라는 오류가 발생하면 `System.IO.Compression` 어셈블리에 대한 참조를 프로젝트에 추가합니다. 

> [!IMPORTANT]
> 파일 압축을 풀 때는 압축을 풀 디렉터리에서 이스케이프할 수 있는 악성 파일 경로를 찾아야 합니다. 이를 경로 통과 공격이라고 합니다. 다음 예제는 악성 파일 경로를 확인하는 방법과 안전하게 압축을 푸는 방법을 보여줍니다.

[!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]

## <a name="example-3-add-a-file-to-an-existing-zip"></a>예제 3: 기존 zip에 파일 추가

다음 예제는 <xref:System.IO.Compression.ZipArchive> 클래스를 사용하여 기존 *.zip* 파일에 액세스하고 파일을 추가합니다. 새 파일은 기존 .zip 파일에 추가할 때 압축됩니다.

[!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
[!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]

## <a name="example-4-compress-and-decompress-gz-files"></a>예제 4: .gz 파일 압축 및 압축 풀기

<xref:System.IO.Compression.GZipStream> 및 <xref:System.IO.Compression.DeflateStream> 클래스를 사용하여 데이터를 압축하거나 압축을 풀 수도 있습니다. 동일한 압축 알고리즘을 사용합니다. *.gz* 파일에 기록된 <xref:System.IO.Compression.GZipStream> 개체의 압축은 많은 일반적인 도구를 사용하여 풀 수 있습니다. 다음 예제에서는 <xref:System.IO.Compression.GZipStream> 클래스를 사용하여 파일의 디렉터리를 압축하고 압축을 푸는 방법을 보여 줍니다.

[!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
[!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.IO.Compression.ZipArchive>  
- <xref:System.IO.Compression.ZipFile>  
- <xref:System.IO.Compression.ZipArchiveEntry>  
- <xref:System.IO.Compression.DeflateStream>  
- <xref:System.IO.Compression.GZipStream>  
- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
