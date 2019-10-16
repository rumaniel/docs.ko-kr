---
title: .NET Framework 파일 I/O 및 파일 시스템에 사용되는 클래스(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- file I/O classes
ms.assetid: 4a5ca924-eea8-4a95-a5f0-6ac10de276a3
ms.openlocfilehash: f9d898756b6b17ae69d1af7dd747c20a26d88417
ms.sourcegitcommit: 127343afce8422bfa944c8b0c4ecc8f79f653255
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67347996"
---
# <a name="classes-used-in-net-framework-file-io-and-the-file-system-visual-basic"></a>.NET Framework 파일 I/O 및 파일 시스템에 사용되는 클래스(Visual Basic)
다음 표에는 .NET Framework 파일 I/O에 공통적으로 사용되고 파일 I/O 클래스로 범주화되는 클래스, 스트림을 만드는 데 사용되는 클래스 및 스트림을 읽고 스트림에 쓰는 데 사용되는 클래스가 나와 있습니다.  
  
더 포괄적인 목록은 [클래스 라이브러리 개요](../../../../standard/class-library-overview.md)를 참조하세요.  
  
## <a name="basic-io-classes-for-files-drives-and-directories"></a>파일, 드라이브 및 디렉터리의 기본 I/O 클래스  
 다음 표에서는 파일 I/O에 사용되는 기본 클래스를 나열하고 설명합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|<xref:System.IO.Directory?displayProperty=nameWithType>|디렉터리와 하위 디렉터리를 통해 만들고, 이동하고, 열거하기 위한 정적 메서드를 제공합니다.|  
|<xref:System.IO.DirectoryInfo?displayProperty=nameWithType>|디렉터리와 하위 디렉터리를 통해 만들고, 이동하고, 열거하기 위한 인스턴스 메서드를 제공합니다.|  
|<xref:System.IO.DriveInfo?displayProperty=nameWithType>|드라이브를 통해 만들고, 이동하고, 열거하기 위한 인스턴스 메서드를 제공합니다.|  
|<xref:System.IO.File?displayProperty=nameWithType>|파일 만들기, 복사, 삭제, 이동 및 열기를 위한 정적 메서드를 제공하고 `FileStream`만들기를 지원합니다.|  
|<xref:System.IO.FileAccess?displayProperty=nameWithType>|파일에 대한 읽기, 쓰기 또는 읽기/쓰기 액세스 권한에 대한 상수를 정의합니다.|  
|<xref:System.IO.FileAttributes?displayProperty=nameWithType>|`Archive`, `Hidden` 및 `ReadOnly`와 같은 파일 및 디렉터리에 대한 특성을 제공합니다.|  
|<xref:System.IO.FileInfo?displayProperty=nameWithType>|파일 만들기, 복사, 삭제, 이동 및 열기를 위한 정적 메서드를 제공하고 `FileStream`만들기를 지원합니다.|  
|<xref:System.IO.FileMode?displayProperty=nameWithType>|파일을 여는 방식을 제어합니다. 이 매개 변수는 대부분의 `FileStream` 및 `IsolatedStorageFileStream`에 대한 생성자와 <xref:System.IO.File> 및 <xref:System.IO.FileInfo>의 `Open` 메서드에 대한 생성자에서 지정됩니다.|  
|<xref:System.IO.FileShare?displayProperty=nameWithType>|다른 파일 스트림이 같은 파일에 대해 가질 수 있는 액세스 형식을 제어하기 위한 상수를 정의합니다.|  
|<xref:System.IO.Path?displayProperty=nameWithType>|디렉터리 문자열을 처리하기 위한 메서드와 속성을 제공합니다.|  
|<xref:System.Security.Permissions.FileIOPermission?displayProperty=nameWithType>|<xref:System.Security.Permissions.FileIOPermissionAttribute.Read%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Write%2A>, <xref:System.Security.Permissions.FileIOPermissionAttribute.Append%2A> 및 <xref:System.Security.Permissions.FileIOPermissionAttribute.PathDiscovery%2A> 권한을 정의하여 파일 및 폴더 액세스를 제어합니다.|  
  
## <a name="classes-used-to-create-streams"></a>스트림을 만드는 데 사용되는 클래스  
 다음 표에서는 스트림을 만드는 데 사용되는 기본 클래스를 나열하고 설명합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|<xref:System.IO.BufferedStream?displayProperty=nameWithType>|다른 스트림에서 작업을 읽고 쓰기 위한 버퍼링 레이어를 추가합니다.|  
|<xref:System.IO.FileStream?displayProperty=nameWithType>|<xref:System.IO.FileStream.Seek%2A> 메서드를 통해 임의 파일 액세스를 지원합니다. <xref:System.IO.FileStream>은 기본적으로 파일을 동기적으로 열지만 비동기 작업도 지원합니다.|  
|<xref:System.IO.MemoryStream?displayProperty=nameWithType>|백업 저장소가 파일이 아니라 메모리인 스트림을 만듭니다.|  
|<xref:System.Net.Sockets.NetworkStream?displayProperty=nameWithType>|네트워크 액세스를 위한 데이터의 기본 스트림을 제공합니다.|  
|<xref:System.Security.Cryptography.CryptoStream?displayProperty=nameWithType>|데이터 스트림을 암호화 변환에 연결하는 스트림을 정의합니다.|  
  
## <a name="classes-used-to-read-from-and-write-to-streams"></a>스트림에서 읽고 스트림에 쓰는 데 사용되는 클래스  
 다음 표에는 스트림을 통해 파일에서 읽고 파일에 쓰는 데 사용되는 특정 클래스를 보여 줍니다.  
  
|**클래스**|**설명**|  
|---------------|---------------------|  
|<xref:System.IO.BinaryReader?displayProperty=nameWithType>|<xref:System.IO.FileStream>에서 인코딩된 문자열 및 기본 데이터 형식을 읽습니다.|  
|<xref:System.IO.BinaryWriter?displayProperty=nameWithType>|<xref:System.IO.FileStream>에 인코딩된 문자열 및 기본 데이터 형식을 씁니다.|  
|<xref:System.IO.StreamReader?displayProperty=nameWithType>|<xref:System.IO.FileStream>에서 문자를 읽고 <xref:System.IO.StreamReader.CurrentEncoding%2A>을 사용하여 문자와 바이트 간을 변환합니다. <xref:System.IO.StreamReader>에는 바이트 순서 표시 등의 <xref:System.IO.StreamReader.CurrentEncoding%2A> 관련 프리앰블 유무를 기준으로 하여 지정된 스트림의 올바른 <xref:System.IO.StreamReader.CurrentEncoding%2A> 확인을 시도하는 생성자가 있습니다.|  
|<xref:System.IO.StreamWriter?displayProperty=nameWithType>|`FileStream`에 문자를 쓰고 <xref:System.IO.StreamWriter.Encoding%2A>을 사용하여 문자와 바이트 간을 변환합니다.|  
|<xref:System.IO.StringReader?displayProperty=nameWithType>|`String`에서 문자를 읽습니다. 출력은 인코딩의 스트림 또는 `String` 중 하나일 수 있습니다.|  
|<xref:System.IO.StringWriter?displayProperty=nameWithType>|`String`에 문자를 씁니다. 출력은 인코딩의 스트림 또는 `String` 중 하나일 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목

- [스트림 작성](../../../../standard/io/composing-streams.md)
- [파일 및 스트림 I/O](../../../../standard/io/index.md)
- [Asynchronous File I/O](../../../../standard/io/asynchronous-file-i-o.md)
- [.NET Framework 파일 I/O 및 파일 시스템의 기본 사항(Visual Basic)](../../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)
