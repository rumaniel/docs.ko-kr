---
title: 파일 및 스트림 I/O - .NET
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- IO namespace
- files, I/O
- System.IO namespace
- I/O [.NET Framework]
- streams, I/O
- data streams, I/O
ms.assetid: 4f4a33a9-66b7-4cd7-a285-4ad3e4276cd2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d3b3dcc3b96e12f89508f4d2708c5ab083516dba
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025506"
---
# <a name="file-and-stream-io"></a>파일 및 스트림 I/O

파일 및 스트림 I/O(입/출력)는 스토리지 매체로 데이터를 전송하거나 스토리지 매체로부터 데이터를 전송 받습니다. .NET Framework에서 `System.IO` 네임스페이스는 데이터 스트림과 파일에서 읽기 및 쓰기를 동기적 및 비동기적으로 사용하는 형식을 포함합니다. 이러한 네임스페이스는 파일의 압축 및 압축 풀기 기능을 수행하는 형식 및 파이프 및 직렬 포트를 통한 통신을 가능하도록 하는 형식을 포함합니다.

파일은 정돈되고 이름이 지정된 컬렉션의 바이트이며, 이 컬렉션에는 영구 스토리지가 있습니다. 사용자가 파일을 사용할 때, 디렉터리 경로, 디스크 스토리지 및 파일과 디렉터리 이름을 다룹니다. 반대로, 스트림은 여러 가지 스토리지 매체 중 하나인 백업 저장소(예를 들어, 디스크 또는 메모리)에서 읽고 쓸 수 있는 바이트 시퀀스입니다. 디스크 외에 여러 백업 저장소가 존재하듯이, 파이프 스트림 외에 여러 종류의 스트림, 예를 들어 네트워크, 메모리, 파일 스트림도 존재합니다.

## <a name="files-and-directories"></a>파일 및 디렉터리

사용자는 이 형식들을 <xref:System.IO?displayProperty=nameWithType> 네임스페이스에서 파일 및 디렉터리와 상호 작용하기 위해 사용할 수 있습니다. 예를 들어, 파일 및 디렉터리에 대한 속성을 가져오고 설정할 수 있고, 검색 조건에 따라 파일 및 디렉터리의 컬렉션을 검색할 수 있습니다.

.NET Core 1.1 및 .NET Framework 4.6.2 이상에서 지원되는 DOS 디바이스 구문을 비롯한 Windows 시스템에 대한 경로 명명 규칙 및 파일 경로를 표현하는 방법은 [Windows 시스템의 파일 경로 형식](file-path-formats.md)을 참조하세요.

다음은 몇 가지 흔히 사용되는 파일 및 디렉터리 클래스입니다.

- <xref:System.IO.File> - 파일 만들기, 복사, 삭제, 이동 및 열기를 위한 정적 메서드를 제공하고 <xref:System.IO.FileStream> 개체 만들기를 지원합니다.

- <xref:System.IO.FileInfo> - 파일 만들기, 복사, 삭제, 이동 및 열기를 위한 인스턴스 메서드를 제공하고 <xref:System.IO.FileStream> 개체 만들기를 지원합니다.

- <xref:System.IO.Directory> - 디렉터리와 하위 디렉터리를 통해 만들고, 이동하고, 열거하기 위한 정적 메서드를 제공합니다.

- <xref:System.IO.DirectoryInfo> - 디렉터리와 하위 디렉터리를 통해 만들고, 이동하고, 열거하기 위한 인스턴스 메서드를 제공합니다.

- <xref:System.IO.Path> - 플랫폼 간에 호환되는 방식으로 디렉터리 문자열을 처리하기 위한 메서드와 속성을 제공합니다.

파일 시스템 메서드를 호출할 때 항상 강력한 예외 처리를 제공해야 합니다. 자세한 내용은 [I/O 오류 처리](handling-io-errors.md)를 참조하세요.

Visual Basic 사용자는 이러한 클래스를 사용하는 것 외에도, 파일 I/O에 대한 <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=nameWithType> 클래스에서 제공하는 메서드와 속성을 사용할 수 있습니다.

[방법: 디렉터리 복사](how-to-copy-directories.md), [방법: 디렉터리 목록 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5cf8zcfh(v=vs.100)) 및 [방법: 디렉터리 및 파일 열거](how-to-enumerate-directories-and-files.md)를 참조하세요.

## <a name="streams"></a>스트림

추상 기본 클래스 <xref:System.IO.Stream>은 바이트 읽기 및 쓰기를 지원합니다. 스트림을 나타내는 모든 클래스는 <xref:System.IO.Stream> 클래스로부터 상속됩니다. <xref:System.IO.Stream> 클래스와 이 클래스에서 파생되는 클래스는 데이터 소스와 리포지토리의 일반 뷰를 제공하고, 이때 프로그래머는 운영 체제 및 내부 디바이스의 세부 사항에서 격리됩니다.

스트림에는 다음의 세 가지 기본 작업이 포함됩니다.

- 읽기 - 스트림의 데이터를 바이트 배열과 같은 데이터 구조로 전송합니다.

- 쓰기 - 데이터 소스에서 스트림으로 데이터를 전송합니다.

- 검색 - 스트림 내에서 현재 위치를 쿼리하고 수정합니다.

내부 데이터 소스 또는 리포지토리에 따라 스트림에서 이러한 기능 중 일부만 지원할 수도 있습니다. 예를 들어, <xref:System.IO.Pipes.PipeStream> 클래스는 검색을 지원하지 않습니다. <xref:System.IO.Stream.CanRead%2A>, <xref:System.IO.Stream.CanWrite%2A>, <xref:System.IO.Stream.CanSeek%2A> 스트림 속성은 스트림이 지원하는 작업을 지정합니다.

다음은 몇 가지 자주 사용되는 스트림 클래스입니다.

- <xref:System.IO.FileStream> – 파일을 읽고 쓰는 데 사용됩니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> – 격리된 스토리지의 파일을 읽고 파일에 기록하는 데 사용됩니다.

- <xref:System.IO.MemoryStream> – 메모리를 백업 저장소로 읽고 여기에 기록하는 데 사용됩니다.

- <xref:System.IO.BufferedStream> – 읽기 및 쓰기 작업의 성능을 향상시키는 데 사용됩니다.

- <xref:System.Net.Sockets.NetworkStream> – 네트워크 소켓을 통한 읽기 및 쓰기를 지원합니다.

- <xref:System.IO.Pipes.PipeStream> – 익명 및 명명된 파이프를 통한 읽기와 쓰기를 지원합니다.

- <xref:System.Security.Cryptography.CryptoStream> – 데이터 스트림을 암호화 변형에 연결하는 데 사용됩니다.

스트림의 비동기화 작업에 대한 예제는 [비동기 파일 I/O](asynchronous-file-i-o.md)를 참조하세요.

## <a name="readers-and-writers"></a>판독기 및 작성기

또한 <xref:System.IO?displayProperty=nameWithType> 네임스페이스는 스트림으로부터 인코딩된 문자를 읽고 이를 스트림에 쓰기 위한 형식을 제공합니다. 일반적으로 스트림은 바이트 입력 및 출력용으로 디자인됩니다. 판독기 및 작성기 형식은 스트림 작업을 완료할 수 있도록 인코딩된 문자와 바이트의 변환을 처리합니다. 각 판독기 및 작성기 클래스는 스트림과 연결되어 있고, 이것은 클래스의 `BaseStream` 속성을 통해 검색될 수 있습니다.

일부 자주 사용되는 판독기 및 작성기 클래스는 다음과 같습니다.

- <xref:System.IO.BinaryReader> 및 <xref:System.IO.BinaryWriter> – 기본 데이터 형식을 바이너리 값으로 읽고 쓰는 데 사용됩니다.

- <xref:System.IO.StreamReader> 및 <xref:System.IO.StreamWriter> – 인코딩 값을 사용하여 바이트에서 문자, 문자에서 바이트로 변환함으로써 문자를 읽고 쓰는 데 사용됩니다.

- <xref:System.IO.StringReader> 및 <xref:System.IO.StringWriter> – 문자열에서 문자를, 문자에서 문자열을 읽고 쓰는 데 사용됩니다.

- <xref:System.IO.TextReader> 및 <xref:System.IO.TextWriter> – 이진 데이터가 아닌 문자 및 문자열을 읽고 쓰는 다른 판독기와 작성기에 대한 추상 기본 클래스로 사용됩니다.

[방법: 파일에서 텍스트 읽기](how-to-read-text-from-a-file.md), [방법: 파일에 텍스트 쓰기](how-to-write-text-to-a-file.md), [방법: 문자열에서 문자 읽기](how-to-read-characters-from-a-string.md) 및 [방법: 문자열에 문자 쓰기](how-to-write-characters-to-a-string.md)를 참조하세요.

## <a name="asynchronous-io-operations"></a>비동기 I/O 작업

많은 양의 데이터를 읽거나 쓸 때 리소스가 많이 사용될 수 있습니다. 이러한 작업은 애플리케이션 사용자에게 응답을 유지해야 하는 경우 비동기적으로 수행해야 합니다. 동기 I/O 작업에서 UI 스레드는 리소스 집약적인 작업이 완료될 때까지 차단됩니다.  [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램을 개발할 때 비동기 I/O 작업을 사용하여 응용 프로그램이 작동을 멈춘 것처럼 보이지 않게 해줍니다.

비동기 멤버의 이름에는 `Async`가 포함됩니다(예: <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> 및 <xref:System.IO.Stream.WriteAsync%2A> 메서드). 이러한 메서드는 `async` 및 `await` 키워드와 함께 사용합니다.

자세한 내용은 [비동기 파일 I/O](asynchronous-file-i-o.md)를 참조하세요.

## <a name="compression"></a>압축

압축은 스토리지에 맞춰 파일 크기를 줄이는 프로세스를 가리킵니다. 압축 해제는 압축된 파일의 내용을 사용 가능한 형식으로 추출하는 프로세스입니다. <xref:System.IO.Compression?displayProperty=nameWithType> 네임스페이스는 파일 및 스트림을 압축하고 압축을 푸는 형식을 포함합니다.

다음 클래스는 파일과 스트림을 압축하고 압축 해제할 때 자주 사용됩니다.

- <xref:System.IO.Compression.ZipArchive> – zip 보관 파일에 항목을 만들고 이를 검색하는 데 사용됩니다.

- <xref:System.IO.Compression.ZipArchiveEntry> – 압축된 파일을 표시할 때 사용됩니다.

- <xref:System.IO.Compression.ZipFile> – 압축된 패키지를 만들고 추출하고 여는 데 사용됩니다.

- <xref:System.IO.Compression.ZipFileExtensions> – 압축된 패키지에 항목을 만들고 추출하는 데 사용됩니다.

- <xref:System.IO.Compression.DeflateStream> – Deflate 알고리즘을 사용하여 스트림을 압축 및 압축 해제하는 데 사용됩니다.

- <xref:System.IO.Compression.GZipStream> – gzip 데이터 형식의 스트림을 압축 및 압축 해제하는 데 사용됩니다.

[방법: 파일 압축 및 추출](how-to-compress-and-extract-files.md)을 참조하세요.

## <a name="isolated-storage"></a>격리된 스토리지

격리된 스토리지는 코드와 저장된 데이터를 연결하는 표준화된 방법을 정의하여 격리와 안전을 제공하는 데이터 스토리지 메커니즘입니다. 스토리지는 사용자, 어셈블리 및 도메인(옵션)에 의해 격리된 가상 파일 시스템을 제공합니다. 격리된 스토리지는 애플리케이션에 사용자 파일을 액세스할 수 있는 권한이 없는 경우 특히 유용합니다. 컴퓨터의 보안 정책에 의해 제어되는 방식으로 애플리케이션에 대한 설정이나 파일을 저장할 수 있습니다.

격리된 스토리지는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]앱에 사용할 수 없습니다. 대신 <xref:Windows.Storage?displayProperty=nameWithType>네임스페이스의 애플리케이션 데이터 클래스를 사용합니다. 자세한 내용은 [애플리케이션 데이터](https://docs.microsoft.com/previous-versions/windows/apps/hh464917%28v=win.10%29)를 참조하세요.

다음의 클래스는 격리된 스토리지를 구현할 때 자주 사용됩니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorage> – 격리된 스토리지 구현을 위한 기본 클래스를 제공합니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile> – 파일 및 디렉터리를 포함하는 격리된 스토리지 영역을 제공합니다.

- <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> - 격리된 스토리지 내에서 파일을 노출시킵니다.

[격리된 스토리지](isolated-storage.md)를 참조하세요.

## <a name="io-operations-in-windows-store-apps"></a>Windows 스토어 앱에서 I/O 작업

[!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에는 스트림에서 읽고 스트림에 쓰기 위한 다양한 형식이 포함됩니다. 하지만, 이 세트에 모든 .NET Framework I/O 형식이 포함되는 것은 아닙니다.

다음은 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 I/O 작업을 사용할 때 알아야 할 몇 가지 중요한 차이점입니다.

- 특히 파일 작업에 관련된 형식(예: <xref:System.IO.File>, <xref:System.IO.FileInfo>, <xref:System.IO.Directory> 및 <xref:System.IO.DirectoryInfo>)은 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]에 포함되지 않습니다. 대신 <xref:Windows.Storage.StorageFile> 및 <xref:Windows.Storage.StorageFolder> 등 Windows 런타임의 <xref:Windows.Storage?displayProperty=nameWithType> 네임스페이스에 있는 유형을 사용합니다.

- 격리된 스토리지는 사용할 수 없습니다. 대신에 [애플리케이션 데이터](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10))를 사용합니다.

- 비동기 메서드(예: <xref:System.IO.Stream.ReadAsync%2A> 및 <xref:System.IO.Stream.WriteAsync%2A>)를 사용하여 UI 스레드를 차단하지 못하게 합니다.

- 경로 기반 압축 형식 <xref:System.IO.Compression.ZipFile> 및 <xref:System.IO.Compression.ZipFileExtensions>는 사용할 수 없습니다. 대신 <xref:Windows.Storage.Compression?displayProperty=nameWithType> 네임스페이스에 있는 유형을 사용합니다.

필요하다면 .NET Framework 스트림과 Windows 런타임 스트림 간에 변환할 수 있습니다. 자세한 내용은 [방법: .NET Framework 스트림과 Windows 런타임 스트림 간 변환](how-to-convert-between-dotnet-streams-and-winrt-streams.md) 또는 <xref:System.IO.WindowsRuntimeStreamExtensions>을 참조하세요.

[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱에서 I/O 작업에 대한 자세한 내용은 [빠른 시작: 파일 읽기 및 쓰기](https://docs.microsoft.com/previous-versions/windows/apps/hh758325(v=win.10))를 참조하세요.

## <a name="io-and-security"></a>I/O 및 보안

<xref:System.IO?displayProperty=nameWithType> 네임스페이스에서 클래스를 사용할 때, 파일 및 디렉터리에 대한 액세스를 제어하기 위해 액세스 제어 목록(ACL)과 같은 운영 체제 보안 요구 사항을 따라야 합니다. <xref:System.Security.Permissions.FileIOPermission> 요구 사항에 이 요구 사항이 추가됩니다. ACL은 프로그래밍 방식으로 관리할 수 있습니다. 자세한 내용은 [방법: 액세스 제어 목록 항목 추가 또는 제거](how-to-add-or-remove-access-control-list-entries.md)를 참조하세요.

기본 보안 정책은 인터넷 또는 인트라넷 애플리케이션에서 사용자의 컴퓨터에 있는 파일의 액세스를 방지합니다. 따라서 실제 파일의 경로를 인터넷이나 인트라넷을 통해 다운로드되는 코드를 작성할 때 필요한 I/O 클래스를 사용하지 마세요. 대신에 기존의 .NET Framework 애플리케이션의 경우 [격리된 스토리지](isolated-storage.md)를 사용하거나 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 애플리케이션의 경우 [애플리케이션 데이터](https://docs.microsoft.com/previous-versions/windows/apps/hh464917(v=win.10))를 사용합니다.

스트림이 생성될 때만 보안 검사가 수행됩니다. 따라서 스트림을 열지 말고, 이것을 신뢰할 수 없는 코드 또는 애플리케이션 도메인으로 전달합니다.

## <a name="related-topics"></a>관련 항목

- [공통 I/O 작업](common-i-o-tasks.md)\
파일, 디렉터리 및 스트림과 관련된 I/O 작업 목록과 각 작업에 대한 예제 및 관련 내용에 대한 링크를 제공합니다.

- [비동기 파일 I/O](asynchronous-file-i-o.md)\
비동기 I/O의 기본 연산 및 성능상의 이점에 대해 설명합니다.

- [격리된 스토리지](isolated-storage.md)\
코드와 저장된 데이터를 연결하는 표준화된 방법을 정의하여 격리와 안전을 제공하는 데이터 스토리지 메커니즘에 대해 설명합니다.

- [파이프](pipe-operations.md)\
.NET Framework에서 익명 사용자와 명명된 파이프 작업에 대해 설명합니다.

- [메모리 매핑된 파일](memory-mapped-files.md)\
가상 메모리의 디스크에 있는 파일의 내용을 포함하는 메모리 매핑된 파일에 대해 설명합니다. 메모리 매핑된 파일을 사용하면 매우 큰 파일을 편집하고 프로세스 간 통신을 위한 공유 메모리를 만들 수 있습니다.
