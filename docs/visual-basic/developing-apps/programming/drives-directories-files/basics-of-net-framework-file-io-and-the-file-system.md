---
title: .NET Framework 파일 I/O 및 파일 시스템의 기본 사항(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- file access, file I/O in Visual Basic
- file attributes, determining
- streams, fundamental operations
- file permissions
- streams
- streams, definition
ms.assetid: 49d837c0-cf28-416f-8606-4d83d7b479ef
ms.openlocfilehash: 3ff305a6b22918681561ed7262a7377dbdf7aadc
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65591521"
---
# <a name="basics-of-net-framework-file-io-and-the-file-system-visual-basic"></a>.NET Framework 파일 I/O 및 파일 시스템의 기본 사항(Visual Basic)

<xref:System.IO> 네임스페이스의 클래스는 드라이브, 파일 및 디렉터리 작업에 사용됩니다.

<xref:System.IO> 네임스페이스는 <xref:System.IO.File> 및 <xref:System.IO.Directory> 클래스를 포함하며, 이러한 클래스는 파일 및 디렉터리를 조작하는 .NET Framework 기능을 제공합니다. 이러한 개체의 메서드는 정적 멤버 또는 공유 멤버이므로, 먼저 클래스의 인스턴스를 만들지 않고 직접 사용할 수 있습니다. `My` 기능의 사용자에게 익숙한 <xref:System.IO.FileInfo> 및 <xref:System.IO.DirectoryInfo> 클래스가 이러한 클래스와 연관되어 있습니다. 이러한 클래스를 사용하려면 이름을 정규화하거나, 영향받는 코드의 시작 부분에 `Imports` 문을 포함하여 적절한 네임스페이스를 가져와야 합니다. 자세한 내용은 [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)을 참조하세요.

> [!NOTE]
> 이 섹션의 다른 항목은 드라이브, 파일 및 디렉터리 작업에 `My.Computer.FileSystem` 클래스 대신 `System.IO` 개체를 사용합니다. `My.Computer.FileSystem` 개체의 주요 용도는 Visual Basic 프로그램에서 사용하는 것입니다. `System.IO` 클래스는 Visual Basic을 포함하여 .NET Framework를 지원하는 모든 언어에서 사용할 수 있습니다.

## <a name="definition-of-a-stream"></a>스트림 정의

.NET Framework는 스트림을 사용하여 파일의 읽기와 쓰기를 지원합니다. 스트림은 연속 데이터의 1차원 집합이라고 생각할 수 있습니다. 여기에는 시작과 끝이 있고 커서가 스트림에서 현재 위치를 나타냅니다.

![FileStream의 현재 위치를 보여 주는 커서](./media/basics-of-net-framework-file-io-and-the-file-system/filestream-cursor-position.gif)

## <a name="stream-operations"></a>스트림 작업

스트림에 포함된 데이터는 메모리, 파일 또는 TCP/IP 소켓에서 온 것일 수 있습니다. 스트림에는 적용 가능한 기본 작업이 있습니다.

- **읽기**. 스트림에서 읽을 수 있고, 스트림에서 데이터 구조(예: 문자열 또는 바이트 배열)로 데이터를 전송할 수 있습니다.

- **쓰기**. 스트림에 쓸 수 있고, 데이터 소스에서 스트림으로 데이터를 전송할 수 있습니다.

- **검색**. 쿼리할 수 있으며 스트림에서 현재 위치를 수정할 수 있습니다.

자세한 내용은 [Composing Streams](../../../../standard/io/composing-streams.md)을 참조하세요.

## <a name="types-of-streams"></a>스트림의 형식

.NET Framework에서 스트림은 <xref:System.IO.Stream> 클래스로 표시되며, 이는 다른 모든 스트림에 대한 추상 클래스를 형성합니다. <xref:System.IO.Stream> 클래스의 인스턴스를 직접 만들 수는 없지만, 이 인스턴스가 구현하는 클래스 중 하나를 사용해야 합니다.

많은 유형의 스트림이 있지만, 파일 I/O(입출력) 작업을 위해 가장 중요한 형식은 <xref:System.IO.FileStream> 클래스(파일 읽기 및 쓰기 방법 제공) 및 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 클래스(격리된 스토리지에 파일과 디렉터리를 만드는 방법 제공)입니다. 파일 I/O 작업 시 사용할 수 있는 기타 스트림은 다음과 같습니다.

- <xref:System.IO.BufferedStream>

- <xref:System.Security.Cryptography.CryptoStream>

- <xref:System.IO.MemoryStream>

- <xref:System.Net.Sockets.NetworkStream>.

다음 표에서는 스트림을 사용하여 일반적으로 수행되는 작업을 보여 줍니다.

|대상|참조|
|---|---|
|데이터 파일 읽기 및 쓰기|[방법: 새로 만든 데이터 파일 읽기 및 쓰기](../../../../standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)|
|파일에서 텍스트 읽기|[방법: 파일에서 텍스트 읽기](../../../../standard/io/how-to-read-text-from-a-file.md)|
|파일에 텍스트 쓰기|[방법: 파일에 텍스트 쓰기](../../../../standard/io/how-to-write-text-to-a-file.md)|
|문자열에서 문자 읽기|[방법: 문자열에서 문자 읽기](../../../../standard/io/how-to-read-characters-from-a-string.md)|
|문자열에 문자 쓰기|[방법: 문자열에 문자 쓰기](../../../../standard/io/how-to-write-characters-to-a-string.md)|
|데이터 암호화|[데이터 암호화](../../../../standard/security/encrypting-data.md)|
|데이터 암호 해독|[데이터 해독](../../../../standard/security/decrypting-data.md)|

## <a name="file-access-and-attributes"></a>파일 액세스 및 특성

<xref:System.IO.FileStream> 클래스의 생성자가 사용하는 플래그가 포함된 <xref:System.IO.FileAccess>, <xref:System.IO.FileMode> 및 <xref:System.IO.FileShare> 열거형을 사용하여 파일을 만들고 열고 공유하는 방법을 제어할 수 있습니다. 예를 들어 새 <xref:System.IO.FileStream>을 열거나 만들 때 <xref:System.IO.FileMode> 열거형을 사용하면 추가하기 위해 파일을 열지 여부, 지정된 파일이 없을 경우 새 파일을 만들지 여부, 파일을 덮어쓸지 여부 등을 지정할 수 있습니다.

<xref:System.IO.FileAttributes> 열거형을 사용하면 파일에 관한 정보를 수집할 수 있습니다. <xref:System.IO.FileAttributes> 열거형은 압축, 암호화, 숨김, 읽기 전용, 보관, 디렉터리, 시스템 파일 또는 임시 파일과 같은 파일의 저장된 특성을 반환합니다.

다음 표에서는 파일 액세스 및 파일 특성과 관련된 작업을 보여 줍니다.

|대상|참조|
|---|---|
|로그 파일 열기 및 텍스트 추가|[방법: 로그 파일 열기 및 추가](../../../../standard/io/how-to-open-and-append-to-a-log-file.md)|
|파일의 특성 확인|<xref:System.IO.FileAttributes>|

## <a name="file-permissions"></a>파일 사용 권한

파일 및 디렉터리에 대한 액세스 제어는 <xref:System.Security.Permissions.FileIOPermission> 클래스로 수행할 수 있습니다. 이는 기본적으로 ASPNET(ASP.NET 및 .NET Framework 설치 과정에서 생성됨)이라는 이름의 특수한 로컬 사용자 계정 컨텍스트 내에서 실행되는 Web Forms로 작업하는 개발자에게 특히 중요할 수 있습니다. 그러한 애플리케이션 요청이 리소스에 액세스할 경우 ASPNET 사용자 계정은 제한된 권한을 갖게 되며, 따라서 웹 애플리케이션에서 파일에 쓰기 등의 작업을 수행하지 못할 수 있습니다. 자세한 내용은 <xref:System.Security.Permissions.FileIOPermission>을 참조하세요.

## <a name="isolated-file-storage"></a>격리된 파일 스토리지

격리된 스토리지는 사용자 또는 코드에 권한이 부족한 상태에서 파일로 작업할 때 발생하는 문제를 해결하기 위한 시도입니다. 격리된 스토리지는 하나 이상의 스토리지를 유지할 수 있는 데이터 구획을 각 사용자에게 할당합니다. 사용자 및 어셈블리를 기준으로 저장소를 서로 격리할 수 있습니다. 저장소를 만든 사용자 및 어셈블리만이 저장소에 액세스할 수 있습니다. 저장소는 완전한 가상 파일 시스템 역할을 합니다. 한 저장소 내에서 디렉터리와 파일을 만들고 조작할 수 있습니다.

다음 표에서는 격리된 파일 스토리지와 일반적으로 관련된 작업을 보여 줍니다.

|대상|참조|
|---|---|
|격리된 저장소 만들기|[방법: 격리된 스토리지의 저장소 가져오기](../../../../standard/io/how-to-obtain-stores-for-isolated-storage.md)|
|격리된 저장소 열거|[방법: 격리된 스토리지의 저장소 열거](../../../../standard/io/how-to-enumerate-stores-for-isolated-storage.md)|
|격리된 저장소 삭제|[방법: 격리된 스토리지에서 저장소 삭제](../../../../standard/io/how-to-delete-stores-in-isolated-storage.md)|
|격리된 스토리지에서 파일 또는 디렉터리 만들기|[방법: 격리된 스토리지의 파일 및 디렉터리 만들기](../../../../standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|
|격리된 스토리지에서 파일 찾기|[방법: 격리된 스토리지의 기존 파일 및 디렉터리 찾기](../../../../standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|
|격리된 스토리지에서 파일 읽기 또는 쓰기|[방법: 격리된 스토리지의 파일 읽기 및 쓰기](../../../../standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|
|격리된 스토리지에서 파일 또는 디렉터리 삭제|[방법: 격리된 스토리지의 파일 및 디렉터리 삭제](../../../../standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|

## <a name="file-events"></a>파일 이벤트

<xref:System.IO.FileSystemWatcher> 구성 요소를 사용하면 네트워크 액세스 권한이 있는 컴퓨터나 시스템의 파일 및 디렉터리에서 변경 내용을 관찰할 수 있습니다. 예를 들어 파일이 수정되는 경우 변경이 발생했다는 경고를 사용자에게 보낼 수 있습니다. 변경이 일어나는 경우 하나 이상의 이벤트가 발생하고, 버퍼에 저장되고, 처리를 위해 <xref:System.IO.FileSystemWatcher> 구성 요소로 전달됩니다.

## <a name="see-also"></a>참고 항목

- [스트림 작성](../../../../standard/io/composing-streams.md)
- [파일 및 스트림 I/O](../../../../standard/io/index.md)
- [Asynchronous File I/O](../../../../standard/io/asynchronous-file-i-o.md)
- [.NET Framework 파일 I/O 및 파일 시스템에 사용되는 클래스(Visual Basic)](../../../../visual-basic/developing-apps/programming/drives-directories-files/classes-used-in-net-framework-file-io-and-the-file-system.md)
