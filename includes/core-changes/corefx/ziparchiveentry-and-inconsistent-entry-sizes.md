---
ms.openlocfilehash: 9520f8c6b6671917f5694bc602293a00e2dab82d
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216938"
---
### <a name="ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes"></a>ZipArchiveEntry가 더 이상 일치하지 않는 항목 크기의 아카이브를 처리하지 않음

Zip 보관 파일은 중앙 디렉터리 및 로컬 헤더에 압축 크기와 압축되지 않은 크기를 모두 나열합니다.  항목 데이터 자체도 크기를 표시합니다.  .NET Core 2.2 버전 이하에서는 이러한 값에 대해 일관성을 검사하지 않았습니다. .NET Core 3.0부터는 검사됩니다.

#### <a name="change-description"></a>변경 내용 설명

.Net Core 2.2 버전 이하에서는 로컬 헤더가 zip 파일의 중앙 헤더와 일치하지 않는 경우에도 <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType>이 성공합니다. 데이터는 압축된 스트림의 끝에 도달할 때까지 압축이 풀립니다. 이는 해당 길이가 중앙 디렉터리/로컬 헤더에 나열된 압축되지 않은 파일 크기를 초과하는 경우에도 마찬가지입니다.

.Net Core 3.0부터 <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType> 메서드는 로컬 헤더 및 중앙 헤더에서 항목의 압축된 크기와 압축되지 않은 크기가 일치하는지 확인합니다.  보관 파일의 로컬 헤더 및/또는 데이터 설명자가 zip 파일의 중앙 디렉터리와 일치하지 않는 크기를 나열하는 경우 메서드가 <xref:System.IO.InvalidDataException>을 throw합니다. 항목을 읽을 때 압축 해제된 데이터가 헤더에 나열된 압축되지 않은 파일 크기로 잘립니다.

이러한 변경은 <xref:System.IO.Compression.ZipArchiveEntry>가 해당 데이터의 크기를 정확하게 표시하고 해당 양의 데이터만 읽도록 하기 위함입니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

이러한 문제가 발생하는 zip 보관 파일을 다시 패키지합니다.

#### <a name="category"></a>범주

CoreFx

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.IO.Compression.ZipArchiveEntry.Open?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A?displayProperty=nameWithType>
- <xref:System.IO.Compression.ZipFile.ExtractToDirectory%2A?displayProperty=nameWithType>

<!--

### Affected APIs

`M:System.IO.Compression.ZipArchiveEntry.Open`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToDirectory%2A`
`Overload:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A`
`Overload:System.IO.Compression.ZipFile.ExtractToDirectory%2A`

-->
