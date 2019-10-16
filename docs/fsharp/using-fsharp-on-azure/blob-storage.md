---
title: F#을 사용하여 Azure Blob 스토리지 시작
description: Azure Blob storage를 사용 하 여 클라우드에 구조화 되지 않은 데이터를 저장 합니다.
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: c765f38cba7642e813a5966d3b7754c5ce45abbd
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70107118"
---
# <a name="get-started-with-azure-blob-storage-using-f"></a>F #을 사용 하 여 Azure Blob storage 시작\#

Azure Blob Storage는 클라우드에서 구조화되지 않은 데이터를 개체/Blob으로 저장하는 서비스입니다. Blob Storage는 문서, 미디어 파일, 애플리케이션 설치 관리자 등과 같은 모든 유형의 텍스트 또는 이진 데이터를 저장할 수 있습니다. Blob 스토리지를 개체 스토리지라고도 합니다.

이 문서에서는 Blob storage를 사용 하 여 일반적인 작업을 수행 하는 방법을 보여 줍니다. 샘플은 .NET 용 Azure Storage F# 클라이언트 라이브러리를 사용 하 여 작성 되었습니다. 여기에서 설명 하는 태스크에는 blob을 업로드, 나열, 다운로드 및 삭제 하는 방법이 포함 됩니다.

Blob 저장소에 대 한 개념적 개요는 [blob 저장소에 대 한 .net 가이드](/azure/storage/storage-dotnet-how-to-use-blobs)를 참조 하세요.

## <a name="prerequisites"></a>전제 조건

이 가이드를 사용 하려면 먼저 [Azure storage 계정을 만들어야](/azure/storage/storage-create-storage-account)합니다. 이 계정에 대 한 저장소 액세스 키도 필요 합니다.

## <a name="create-an-f-script-and-start-f-interactive"></a>F# 스크립트 만들기 및 대화형 시작 F#

이 문서의 샘플은 F# 응용 프로그램 또는 F# 스크립트에서 사용할 수 있습니다. F# 스크립트를 만들려면 `.fsx` F# 개발 환경에서 `blobs.fsx`확장명을 사용 하 여 파일을 만듭니다.

그런 다음 [Paket](https://fsprojects.github.io/Paket/) 또는 `WindowsAzure.Storage` [NuGet](https://www.nuget.org/) 과 같은 [패키지 관리자](package-management.md) 를 사용 하 여 지시문을 `Microsoft.WindowsAzure.ConfigurationManager` `#r` 사용 하 여 `WindowsAzure.Storage.dll` 및 `Microsoft.WindowsAzure.Configuration.dll` 패키지를 설치 하 고 스크립트에 및를 참조 합니다.

### <a name="add-namespace-declarations"></a>네임 스페이스 선언 추가

파일의 맨 `open` 위에 다음 문을 추가 합니다. `blobs.fsx`

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>연결 문자열 가져오기

이 자습서에서는 Azure Storage 연결 문자열이 필요 합니다. 연결 문자열에 대 한 자세한 내용은 [저장소 연결 문자열 구성](/azure/storage/storage-configure-connection-string)을 참조 하세요.

자습서의 경우 다음과 같이 스크립트에 연결 문자열을 입력 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L11-L11)]

그러나 실제 프로젝트에는이 방법이 **권장 되지 않습니다** . 저장소 계정 키는 저장소 계정의 루트 암호와 비슷합니다. 항상 저장소 계정 키를 보호 해야 합니다. 다른 사용자에 게 배포 하거나 하드 코딩 하거나 다른 사용자가 액세스할 수 있는 일반 텍스트 파일로 저장 하지 않도록 합니다. 손상 된 것으로 생각 되는 경우 Azure Portal을 사용 하 여 키를 다시 생성할 수 있습니다.

실제 응용 프로그램의 경우 저장소 연결 문자열을 유지 하는 가장 좋은 방법은 구성 파일에 있습니다. 구성 파일에서 연결 문자열을 가져오려면 다음을 수행할 수 있습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L13-L15)]

Azure Configuration Manager 사용은 선택 사항입니다. .NET Framework의 `ConfigurationManager` 형식과 같은 API를 사용할 수도 있습니다.

### <a name="parse-the-connection-string"></a>연결 문자열 구문 분석

연결 문자열을 구문 분석 하려면 다음을 사용 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L21-L22)]

그러면이 반환 `CloudStorageAccount`됩니다.

### <a name="create-some-local-dummy-data"></a>로컬 더미 데이터 만들기

시작 하기 전에 스크립트의 디렉터리에 더미 로컬 데이터를 만듭니다. 나중에이 데이터를 업로드 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L28-L30)]

### <a name="create-the-blob-service-client"></a>Blob service 클라이언트 만들기

형식을 `CloudBlobClient` 사용 하 여 blob 저장소에 저장 된 컨테이너 및 blob을 검색할 수 있습니다. 서비스 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L36-L36)]

이제 데이터를 읽고 Blob 저장소에 데이터를 쓰는 코드를 작성할 준비가 되었습니다.

## <a name="create-a-container"></a>컨테이너 만들기

이 예제에서는 컨테이너가 아직 없는 경우 만드는 방법을 보여 줍니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L42-L46)]

기본적으로 새 컨테이너는 전용입니다. 즉,이 컨테이너에서 blob을 다운로드 하려면 저장소 액세스 키를 지정 해야 합니다. 컨테이너 내의 파일을 모든 사용자가 사용할 수 있게 하려는 경우 다음 코드를 사용 하 여 컨테이너를 공용으로 설정할 수 있습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L48-L49)]

인터넷 상의 누구 든 지 공용 컨테이너의 blob을 볼 수 있지만 적절 한 계정 액세스 키 또는 공유 액세스 서명이 있는 경우에만 수정 하거나 삭제할 수 있습니다.

## <a name="upload-a-blob-into-a-container"></a>컨테이너에 blob 업로드

Azure Blob Storage는 블록 blob 및 페이지 blob을 지원 합니다. 대부분의 경우 블록 blob은 사용 하기에 권장 되는 형식입니다.

블록 blob에 파일을 업로드 하려면 컨테이너 참조를 가져온 다음이 참조를 사용 하 여 블록 blob 참조를 가져옵니다. Blob 참조가 있으면 메서드를 `UploadFromFile` 호출 하 여 데이터 스트림을 업로드할 수 있습니다. 이 작업은 blob이 없는 경우 새로 만들고, blob이 있는 경우 덮어씁니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L55-L59)]

## <a name="list-the-blobs-in-a-container"></a>컨테이너의 blob 나열

컨테이너의 blob을 나열 하려면 먼저 컨테이너 참조를 가져옵니다. 그런 다음 컨테이너의 `ListBlobs` 메서드를 사용 하 여 컨테이너 내의 blob 및/또는 디렉터리를 검색할 수 있습니다. 반환 `IListBlobItem`된에 대 한 다양 한 속성 및 메서드 집합에 액세스 하려면이 `CloudBlockBlob`를, `CloudPageBlob`또는 `CloudBlobDirectory` 개체로 캐스팅 해야 합니다. 형식을 알 수 없는 경우 형식 검사를 사용 하 여 캐스팅할 형식을 결정할 수 있습니다. 다음 코드에서는 `mydata` 컨테이너에 있는 각 항목의 URI를 검색 하 고 출력 하는 방법을 보여 줍니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L67-L80)]

이름에 경로 정보를 사용 하 여 blob의 이름을 지정할 수도 있습니다. 이렇게 하면 기존 파일 시스템과 같이 구성 하 고 트래버스할 수 있는 가상 디렉터리 구조를 만듭니다. 디렉터리 구조는 가상 전용입니다. Blob 저장소에서 사용할 수 있는 리소스는 컨테이너 및 blob 뿐입니다. 그러나 저장소 클라이언트 라이브러리는 가상 디렉터리를 `CloudBlobDirectory` 참조 하는 개체를 제공 하 고 이러한 방식으로 구성 된 blob을 사용 하 여 작업 하는 프로세스를 간소화 합니다.

예를 들어 라는 `photos`컨테이너에 있는 다음 블록 blob 집합을 고려 합니다.

*photo1.jpg*\
*2015/architecture/description.txt*\
*2015/architecture/photo3.jpg*\
*2015/architecture/photo4.jpg*\
*2016/architecture/photo5.jpg*\
*2016/architecture/photo6.jpg*\
*2016/architecture/description.txt*\
*2016/photo7.jpg*\

위의 샘플과 같이 `ListBlobs` 컨테이너에서를 호출 하면 계층적 목록이 반환 됩니다. 컨테이너의 디렉터리와 `CloudBlobDirectory` blob `CloudBlockBlob` 을 각각 나타내는 및 개체가 둘 다 포함 된 경우 결과 출력은 다음과 유사 하 게 표시 됩니다.

```console
Directory: https://<accountname>.blob.core.windows.net/photos/2015/
Directory: https://<accountname>.blob.core.windows.net/photos/2016/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

필요에 따라 `UseFlatBlobListing` `ListBlobs` 메서드의 매개 변수를로 `true`설정할 수 있습니다. 이 경우 컨테이너의 모든 blob이 `CloudBlockBlob` 개체로 반환 됩니다. 플랫 목록을 반환 `ListBlobs` 하기 위해에 대 한 호출은 다음과 같습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L82-L89)]

컨테이너의 현재 내용에 따라 결과는 다음과 같습니다.

```console
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2015/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2016/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2016/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Blob 다운로드

Blob을 다운로드 하려면 먼저 blob 참조를 검색 한 다음 메서드를 `DownloadToStream` 호출 합니다. 다음 예제에서는 `DownloadToStream` 메서드를 사용 하 여 blob 콘텐츠를 스트림 개체로 전송 합니다. 그러면이 개체를 로컬 파일에 유지할 수 있습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L95-L101)]

메서드를 `DownloadToStream` 사용 하 여 blob 콘텐츠를 텍스트 문자열로 다운로드할 수도 있습니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L103-L106)]

## <a name="delete-blobs"></a>Blob 삭제

Blob을 삭제 하려면 먼저 blob 참조를 가져온 다음 메서드를 `Delete` 호출 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L112-L116)]

## <a name="list-blobs-in-pages-asynchronously"></a>비동기적으로 페이지의 blob 나열

많은 수의 blob을 나열 하거나 한 목록 작업에서 반환 하는 결과 수를 제어 하려는 경우 결과 페이지에 blob을 나열할 수 있습니다. 이 예제에서는 많은 결과 집합을 반환 하기 위해 대기 하는 동안 실행이 차단 되지 않도록 페이지의 결과를 비동기적으로 반환 하는 방법을 보여 줍니다.

이 예제에서는 플랫 blob 목록을 보여 주지만 `useFlatBlobListing` `ListBlobsSegmentedAsync` 메서드의 매개 변수를로 `false`설정 하 여 계층적 목록을 수행할 수도 있습니다.

이 샘플에서는 `async` 블록을 사용 하 여 비동기 메서드를 정의 합니다. 키워드 ``let!`` 는 나열 작업이 완료 될 때까지 샘플 메서드의 실행을 일시 중단 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L122-L160)]

이제 다음과 같이이 비동기 루틴을 사용할 수 있습니다. 먼저이 자습서의 앞부분에서 만든 로컬 파일을 사용 하 여 더미 데이터를 업로드 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L162-L166)]

이제 루틴을 호출 합니다. 를 사용 `Async.RunSynchronously` 하 여 비동기 작업을 강제로 실행 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L168-L168)]

## <a name="writing-to-an-append-blob"></a>추가 blob에 쓰기

추가 blob은 로깅과 같은 추가 작업에 최적화 되어 있습니다. 블록 blob과 마찬가지로 추가 blob은 블록으로 구성 되지만 추가 blob에 새 블록을 추가 하는 경우 항상 blob의 끝에 추가 됩니다. 추가 blob에서 기존 블록을 업데이트 하거나 삭제할 수 없습니다. 추가 blob에 대 한 블록 Id는 블록 blob에 대 한 블록 Id로 노출 되지 않습니다.

추가 blob의 각 블록은 최대 4mb까지 다양 한 크기를 가질 수 있으며, 추가 blob은 최대 5만 블록을 포함할 수 있습니다. 따라서 추가 blob의 최대 크기는 195 GB (4mb X 5만 블록) 보다 약간 더 됩니다.

다음 예에서는 새 추가 blob을 만들고 일부 데이터를 추가 하 여 간단한 로깅 작업을 시뮬레이션 합니다.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L174-L203)]

3 가지 유형의 blob 간의 차이점에 대 한 자세한 내용은 [블록 blob, 페이지 blob 및 추가 Blob 이해](https://msdn.microsoft.com/library/azure/ee691964.aspx) 를 참조 하세요.

## <a name="concurrent-access"></a>동시 액세스

여러 클라이언트나 여러 프로세스 인스턴스에서 blob에 대 한 동시 액세스를 지원 하려면 **etag** 또는 **임대**를 사용할 수 있습니다.

- **Etag** -blob 또는 컨테이너가 다른 프로세스에 의해 수정 되었는지 감지 하는 방법을 제공 합니다.

- **임대** -일정 시간 동안 blob에 대 한 배타적, 갱신 가능, 쓰기 또는 삭제 권한을 얻는 방법을 제공 합니다.

자세한 내용은 [Microsoft Azure Storage에서 동시성 관리](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)를 참조 하세요.

## <a name="naming-containers"></a>컨테이너 이름 지정

Azure storage의 모든 blob은 컨테이너에 있어야 합니다. 컨테이너는 blob 이름의 일부를 형성 합니다. 예를 들어 `mydata` 는 다음 샘플 blob uri에 있는 컨테이너의 이름입니다.

- https://storagesample.blob.core.windows.net/mydata/blob1.txt
- https://storagesample.blob.core.windows.net/mydata/photos/myphoto.jpg

컨테이너 이름은 다음과 같은 명명 규칙을 준수 하는 유효한 DNS 이름 이어야 합니다.

1. 컨테이너 이름은 문자 또는 숫자로 시작 해야 하며 문자, 숫자 및 대시 (-) 문자만 포함할 수 있습니다.
1. 모든 대시 (-) 문자는 바로 앞과 뒤에 문자 또는 숫자가와 야 합니다. 컨테이너 이름에는 연속 대시를 사용할 수 없습니다.
1. 컨테이너 이름의 모든 문자는 소문자 여야 합니다.
1. 컨테이너 이름은 3 자에서 63 자 사이 여야 합니다.

컨테이너의 이름은 항상 소문자 여야 합니다. 컨테이너 이름에 대문자를 포함 하거나 컨테이너 명명 규칙을 위반 하는 경우 400 오류 (잘못 된 요청)가 나타날 수 있습니다.

## <a name="managing-security-for-blobs"></a>Blob에 대 한 보안 관리

기본적으로 Azure Storage는 계정 액세스 키를 소유 하는 계정 소유자에 대 한 액세스를 제한 하 여 데이터 보안을 유지 합니다. 저장소 계정에서 blob 데이터를 공유 해야 하는 경우 계정 액세스 키의 보안을 손상 시 키 지 않고이를 수행 하는 것이 중요 합니다. 또한 blob 데이터를 암호화 하 여 네트워크를 통해 안전 하 게 전송 하 고 Azure Storage 수 있습니다.

### <a name="controlling-access-to-blob-data"></a>Blob 데이터에 대 한 액세스 제어

기본적으로 저장소 계정의 blob 데이터는 저장소 계정 소유자만 액세스할 수 있습니다. Blob 저장소에 대 한 요청을 인증 하려면 기본적으로 계정 액세스 키가 필요 합니다. 그러나 특정 blob 데이터를 다른 사용자가 사용할 수 있도록 설정할 수 있습니다.

### <a name="encrypting-blob-data"></a>Blob 데이터 암호화

Azure Storage은 클라이언트와 서버 모두에서 blob 데이터를 암호화 하는 것을 지원 합니다.

## <a name="next-steps"></a>다음 단계

이제 Blob storage의 기본 사항을 배웠으므로 다음 링크를 따라 자세히 알아보세요.

### <a name="tools"></a>도구

- [F# AzureStorageTypeProvider](https://fsprojects.github.io/AzureStorageTypeProvider/)\
Blob F# , 테이블 및 큐 Azure Storage 자산을 탐색 하 고이에 대 한 CRUD 작업을 쉽게 적용 하는 데 사용할 수 있는 형식 공급자입니다.

- [FSharp.Azure.Storage](https://github.com/fsprojects/FSharp.Azure.Storage)\
Microsoft Azure F# Table Storage 서비스를 사용 하는 API

- [Microsoft Azure Storage 탐색기 (MASE)](/azure/vs-azure-tools-storage-manage-with-storage-explorer)\
Windows, OS X 및 Linux에서 Azure Storage 데이터로 시각적으로 작업할 수 있도록 해 주는 Microsoft의 독립 실행형 무료 앱입니다.

### <a name="blob-storage-reference"></a>Blob storage 참조

- [.NET 용 Azure Storage Api](/dotnet/api/overview/azure/storage)
- [Azure Storage Services REST API 참조](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)

### <a name="related-guides"></a>관련 가이드

- [에서 Azure Blob Storage 시작C#](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/)
- [Windows에서 AzCopy 명령줄 유틸리티를 사용 하 여 데이터 전송](/azure/storage/common/storage-use-azcopy)
- [Linux에서 AzCopy 명령줄 유틸리티를 사용 하 여 데이터 전송](/azure/storage/common/storage-use-azcopy-linux)
- [Azure Storage 연결 문자열 구성](/azure/storage/common/storage-configure-connection-string)
- [Azure Storage 팀 블로그](https://blogs.msdn.microsoft.com/windowsazurestorage/)
- [빠른 시작: .NET을 사용 하 여 개체 저장소에 blob 만들기](/azure/storage/blobs/storage-quickstart-blobs-dotnet)
