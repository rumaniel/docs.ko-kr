---
title: F#을 사용하여 Azure File 스토리지 시작
description: Azure File Storage를 사용하여 클라우드에 파일 데이터를 저장하고 Azure 가상 머신(VM) 또는 Windows를 실행하는 온-프레미스 애플리케이션에서 클라우드 파일 공유를 탑재합니다.
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: a0e3cab56ba0f3db27335822616b4976a5d9de62
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630500"
---
# <a name="get-started-with-azure-file-storage-using-f"></a>F #을 사용 하 여 Azure File storage 시작\#

Azure File storage는 표준 [SMB (서버 메시지 블록) 프로토콜](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)을 사용 하 여 클라우드에서 파일 공유를 제공 하는 서비스입니다. SMB 2.1 및 SMB 3.0이 모두 지원 됩니다. Azure File Storage를 사용하여 파일 공유에 의존하는 레거시 애플리케이션을 비경제적인 다시 쓰기 작업 없이 빠르게 Azure로 마이그레이션할 수 있습니다. Azure 가상 머신 또는 클라우드 서비스 또는 온-프레미스 클라이언트에서 실행 되는 응용 프로그램은 데스크톱 응용 프로그램이 일반적인 SMB 공유를 탑재 하는 것 처럼 클라우드에 파일 공유를 탑재할 수 있습니다. File Storage 공유를 동시에 탑재하고 액세스할 수 있는 애플리케이션 구성 요소 수에는 제한이 없습니다.

파일 저장소에 대 한 개념적 개요는 [파일 저장소에 대 한 .net 가이드](/azure/storage/storage-dotnet-how-to-use-files)를 참조 하세요.

## <a name="prerequisites"></a>필수 구성 요소

이 가이드를 사용 하려면 먼저 [Azure storage 계정을 만들어야](/azure/storage/storage-create-storage-account)합니다.
이 계정에 대 한 저장소 액세스 키도 필요 합니다.

## <a name="create-an-f-script-and-start-f-interactive"></a>F# 스크립트 만들기 및 대화형 시작 F#

이 문서의 샘플은 F# 응용 프로그램 또는 F# 스크립트에서 사용할 수 있습니다. F# 스크립트를 만들려면 `.fsx` F# 개발 환경에서 `files.fsx`확장명을 사용 하 여 파일을 만듭니다.

그런 다음 [Paket](https://fsprojects.github.io/Paket/) 또는 `WindowsAzure.Storage` [NuGet](https://www.nuget.org/) 과 같은 [패키지 관리자](package-management.md) 를 사용 하 여 `#r` 패키지를 설치 하 `WindowsAzure.Storage.dll` 고 지시어를 사용 하 여 스크립트에 참조 합니다.

### <a name="add-namespace-declarations"></a>네임 스페이스 선언 추가

파일의 맨 `open` 위에 다음 문을 추가 합니다. `files.fsx`

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>연결 문자열 가져오기

이 자습서에 대 한 Azure Storage 연결 문자열이 필요 합니다. 연결 문자열에 대 한 자세한 내용은 [저장소 연결 문자열 구성](/azure/storage/storage-configure-connection-string)을 참조 하세요.

자습서의 경우 다음과 같이 스크립트에 연결 문자열을 입력 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L11-L11)]

그러나 실제 프로젝트에는이 방법이 **권장 되지 않습니다** . 스토리지 계정 키는 스토리지 계정의 루트 암호와 비슷합니다. 항상 스토리지 계정 키를 보호해야 합니다. 다른 사용자에 게 배포 하거나 하드 코딩 하거나 다른 사용자가 액세스할 수 있는 일반 텍스트 파일로 저장 하지 않도록 합니다. 손상 된 것으로 생각 되는 경우 Azure Portal을 사용 하 여 키를 다시 생성할 수 있습니다.

실제 응용 프로그램의 경우 저장소 연결 문자열을 유지 하는 가장 좋은 방법은 구성 파일에 있습니다. 구성 파일에서 연결 문자열을 가져오려면 다음을 수행할 수 있습니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L13-L15)]

Azure Configuration Manager 사용은 선택 사항입니다. .NET Framework의 `ConfigurationManager` 형식과 같은 API를 사용할 수도 있습니다.

### <a name="parse-the-connection-string"></a>연결 문자열 구문 분석

연결 문자열을 구문 분석 하려면 다음을 사용 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L21-L22)]

그러면이 반환 `CloudStorageAccount`됩니다.

### <a name="create-the-file-service-client"></a>파일 서비스 클라이언트 만들기

`CloudFileClient` 형식을 사용 하면 파일 저장소에 저장 된 파일을 프로그래밍 방식으로 사용할 수 있습니다. 서비스 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L28-L28)]

이제 데이터를 읽고 파일 저장소에 데이터를 쓰는 코드를 작성할 준비가 되었습니다.

## <a name="create-a-file-share"></a>파일 공유 만들기

이 예제에서는 파일 공유를 만드는 방법을 보여 줍니다 (아직 없는 경우).

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L34-L35)]

## <a name="create-a-root-directory-and-a-subdirectory"></a>루트 디렉터리 및 하위 디렉터리 만들기

여기서 루트 디렉터리를 가져오고 루트의 하위 디렉터리를 가져옵니다. 이미 존재 하지 않는 경우 둘 다 만듭니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L41-L43)]

## <a name="upload-text-as-a-file"></a>파일로 텍스트 업로드

이 예제에서는 텍스트를 파일로 업로드 하는 방법을 보여 줍니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L49-L50)]

### <a name="download-a-file-to-a-local-copy-of-the-file"></a>파일의 로컬 복사본에 파일 다운로드

여기서는 방금 만든 파일을 다운로드 하 여 콘텐츠를 로컬 파일에 추가 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L56-L56)]

### <a name="set-the-maximum-size-for-a-file-share"></a>파일 공유의 최대 크기를 설정 합니다.

아래 예제에서는 공유의 현재 사용량을 확인 하는 방법과 공유에 대 한 할당량을 설정 하는 방법을 보여 줍니다. `FetchAttributes`공유의 `Properties` `SetProperties` 를 채우고 로컬 변경 내용을 Azure File storage에 전파 하려면를 호출 해야 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L62-L72)]

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>파일 또는 파일 공유에 대 한 공유 액세스 서명 생성

파일 공유 또는 개별 파일에 대 한 SAS (공유 액세스 서명)를 생성할 수 있습니다. 또한 공유 액세스 서명을 관리 하는 파일 공유에 대 한 공유 액세스 정책을 만들 수 있습니다. 공유 액세스 정책을 만드는 것은 SAS가 손상 되어야 하는 경우 SAS를 해지 하는 수단을 제공 하기 때문에 권장 됩니다.

여기에서 공유에 대 한 공유 액세스 정책을 만든 다음 해당 정책을 사용 하 여 공유의 파일에 대 한 SAS 제약 조건을 제공 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L78-L94)]

공유 액세스 서명을 만들고 사용 하는 방법에 대 한 자세한 내용은 [sas (공유 액세스 서명) 사용](/azure/storage/storage-dotnet-shared-access-signature-part-1) 및 [Blob 저장소를 사용 하 여 sas 만들기 및 사용](/azure/storage/storage-dotnet-shared-access-signature-part-2)을 참조 하세요.

### <a name="copy-files"></a>파일 복사

파일을 다른 파일이 나 blob 또는 파일에 blob으로 복사할 수 있습니다. Blob을 파일에 복사 하거나 파일을 blob에 복사 하는 경우 동일한 저장소 계정 내에서 복사 하는 경우에도 SAS (공유 액세스 서명)를 사용 하 여 원본 개체를 인증 *해야* 합니다.

### <a name="copy-a-file-to-another-file"></a>다른 파일에 파일 복사

여기서는 동일한 공유의 다른 파일에 파일을 복사 합니다. 이 복사 작업은 동일한 스토리지 계정의 파일 간에 복사를 수행하므로 공유 키 인증을 사용하여 복사를 수행할 수 있습니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L100-L101)]

### <a name="copy-a-file-to-a-blob"></a>Blob에 파일 복사

여기에서는 파일을 만들고 동일한 저장소 계정 내의 blob에 복사 합니다. 원본 파일에 대 한 SAS를 만듭니다 .이는 서비스에서 복사 작업을 수행 하는 동안 소스 파일에 대 한 액세스를 인증 하는 데 사용 합니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L107-L120)]

동일한 방식으로 blob을 파일에 복사할 수 있습니다. 원본 개체가 blob 인 경우 복사 작업 중에 해당 blob에 대 한 액세스를 인증 하는 SAS를 만듭니다.

## <a name="troubleshooting-file-storage-using-metrics"></a>메트릭을 사용 하 여 파일 저장소 문제 해결

Azure 스토리지 분석는 파일 저장소에 대 한 메트릭을 지원 합니다. 메트릭 데이터를 사용 하 여 요청을 추적 하 고 문제를 진단할 수 있습니다.

[Azure Portal](https://portal.azure.com)에서 파일 저장소에 대 한 메트릭을 사용 하도록 설정 하거나, 다음과 F# 같이이 작업을 수행할 수 있습니다.

[!code-fsharp[FileStorage](~/samples/snippets/fsharp/azure/file-storage.fsx#L126-L140)]

## <a name="next-steps"></a>다음 단계

Azure File storage에 대 한 자세한 내용은 다음 링크를 참조 하세요.

### <a name="conceptual-articles-and-videos"></a>개념 문서 및 비디오

- [Azure Files 저장소: Windows 및 Linux 용 원활한 클라우드 SMB 파일 시스템](https://azure.microsoft.com/resources/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
- [Linux에서 Azure File Storage를 사용 하는 방법](/azure/storage/storage-how-to-use-files-linux)

### <a name="tooling-support-for-file-storage"></a>파일 저장소에 대 한 도구 지원

- [Azure Storage에서 Azure PowerShell 사용](/azure/storage/storage-powershell-guide-full)
- [Microsoft Azure Storage와 함께 AzCopy를 사용 하는 방법](/azure/storage/storage-use-azcopy)
- [Azure Storage에서 Azure CLI 사용](/azure/storage/storage-azure-cli#create-and-manage-file-shares)

### <a name="reference"></a>참조

- [.NET 용 저장소 클라이언트 라이브러리 참조](https://msdn.microsoft.com/library/azure/mt347887.aspx)
- [파일 서비스 REST API 참조](/rest/api/storageservices/fileservices/File-Service-REST-API)

### <a name="blog-posts"></a>블로그 게시물

- [Azure File storage는 이제 일반 공급 됩니다.](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
- [Azure File Storage 내](https://azure.microsoft.com/blog/inside-azure-file-storage/) 
- [Microsoft Azure 파일 서비스 소개](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/12/introducing-microsoft-azure-file-service/)
- [Microsoft Azure 파일에 대 한 연결 유지](https://blogs.msdn.microsoft.com/windowsazurestorage/2014/05/26/persisting-connections-to-microsoft-azure-files/)
