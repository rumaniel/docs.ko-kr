---
title: F#을 사용하여 Azure Table 스토리지 시작
description: Azure Table storage 또는 Azure Cosmos DB를 사용 하 여 클라우드에 구조화 된 데이터를 저장 합니다.
author: sylvanc
ms.date: 03/26/2018
ms.openlocfilehash: 509435d47231040362586fa263fbecb1125f862b
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182607"
---
# <a name="get-started-with-azure-table-storage-and-the-azure-cosmos-db-table-api-using-f"></a>F를 사용 하 여 Azure Table storage 및 Azure Cosmos DB Table API 시작\#

Azure Table storage는 클라우드에 구조화 된 NoSQL 데이터를 저장 하는 서비스입니다. Table storage는 스키마 없는 디자인을 사용 하는 키/특성 저장소입니다. 테이블 저장소는 스키마가 다르기 때문에 응용 프로그램의 요구 사항이 진화 함에 따라 데이터를 쉽게 적용할 수 있습니다. 모든 종류의 응용 프로그램에 대해 빠르고 비용 효율적으로 데이터에 액세스할 수 있습니다. 테이블 저장소는 일반적으로 유사한 데이터 볼륨에 대 한 기존 SQL 보다 비용이 훨씬 낮습니다.

테이블 저장소를 사용 하 여 웹 응용 프로그램에 대 한 사용자 데이터, 주소록, 장치 정보 및 서비스에 필요한 다른 유형의 메타 데이터와 같은 유연한 데이터 집합을 저장할 수 있습니다. 테이블에 엔터티를 개수에 관계 없이 저장할 수 있으며 저장소 계정에는 저장소 계정의 최대 용량 한도까지 원하는 수의 테이블이 포함 될 수 있습니다.

Azure Cosmos DB는 Azure Table storage 용으로 작성 되었으며 다음과 같은 프리미엄 기능이 필요한 응용 프로그램에 대 한 Table API를 제공 합니다.

- 턴키 전역 배포.
- 전 세계 전용 처리량.
- 99 번째 백분위 수에서 1 자리 밀리초 대기 시간입니다.
- 보장 된 고가용성.
- 자동 보조 인덱싱.

Azure Table storage 용으로 작성 된 응용 프로그램은 코드를 변경 하지 않고 Table API를 사용 하 여 Azure Cosmos DB으로 마이그레이션하고 프리미엄 기능을 활용할 수 있습니다. Table API에는 .NET, Java, Python 및 node.js에 사용할 수 있는 클라이언트 Sdk가 있습니다.

자세한 내용은 [Azure Cosmos DB Table API 소개](https://docs.microsoft.com/azure/cosmos-db/table-introduction)를 참조 하세요.

## <a name="about-this-tutorial"></a>이 자습서 정보

이 자습서에서는 테이블 만들기 및 F# 삭제, 테이블 데이터 삽입, 업데이트, 삭제 및 쿼리를 비롯 하 여 Azure table storage 또는 Azure Cosmos DB Table API를 사용 하 여 몇 가지 일반적인 작업을 수행 하는 코드를 작성 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>전제 조건

이 가이드를 사용 하려면 먼저 [Azure storage 계정](/azure/storage/storage-create-storage-account) 또는 [Azure Cosmos DB 계정을](https://azure.microsoft.com/try/cosmosdb/)만들어야 합니다.

## <a name="create-an-f-script-and-start-f-interactive"></a>F# 스크립트 만들기 및 대화형 시작 F#

이 문서의 샘플은 F# 응용 프로그램 또는 F# 스크립트에서 사용할 수 있습니다. F# 스크립트를 만들려면 `.fsx` F# 개발 환경에서 `tables.fsx`확장명을 사용 하 여 파일을 만듭니다.

그런 다음 [Paket](https://fsprojects.github.io/Paket/) 또는 `WindowsAzure.Storage` [NuGet](https://www.nuget.org/) 과 같은 [패키지 관리자](package-management.md) 를 사용 하 여 `#r` 패키지를 설치 하 `WindowsAzure.Storage.dll` 고 지시어를 사용 하 여 스크립트에 참조 합니다. Microsoft Azure 네임 스페이스 `Microsoft.WindowsAzure.ConfigurationManager` 를 얻기 위해 다시이 작업을 수행 합니다.

### <a name="add-namespace-declarations"></a>네임 스페이스 선언 추가

파일의 맨 `open` 위에 다음 문을 추가 합니다. `tables.fsx`

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L1-L5)]

### <a name="get-your-azure-storage-connection-string"></a>Azure Storage 연결 문자열 가져오기

Azure Storage Table service에 연결 하는 경우이 자습서에 대 한 연결 문자열이 필요 합니다. Azure Portal에서 연결 문자열을 복사할 수 있습니다. 연결 문자열에 대 한 자세한 내용은 [저장소 연결 문자열 구성](/azure/storage/storage-configure-connection-string)을 참조 하세요.

### <a name="get-your-azure-cosmos-db-connection-string"></a>Azure Cosmos DB 연결 문자열 가져오기

Azure Cosmos DB에 연결 하는 경우이 자습서에 대 한 연결 문자열이 필요 합니다. Azure Portal에서 연결 문자열을 복사할 수 있습니다. Azure Portal의 Cosmos DB 계정에서 **설정** > **연결 문자열**로 이동 하 고 **복사** 단추를 클릭 하 여 기본 연결 문자열을 복사 합니다. 

자습서의 경우 다음 예제와 같이 스크립트에 연결 문자열을 입력 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L11-L11)]

그러나 실제 프로젝트에는이 방법이 **권장 되지 않습니다** . 저장소 계정 키는 저장소 계정의 루트 암호와 비슷합니다. 항상 저장소 계정 키를 보호 해야 합니다. 다른 사용자에 게 배포 하거나 하드 코딩 하거나 다른 사용자가 액세스할 수 있는 일반 텍스트 파일로 저장 하지 않도록 합니다. 손상 된 것으로 생각 되는 경우 Azure Portal을 사용 하 여 키를 다시 생성할 수 있습니다.

실제 응용 프로그램의 경우 저장소 연결 문자열을 유지 하는 가장 좋은 방법은 구성 파일에 있습니다. 구성 파일에서 연결 문자열을 가져오려면 다음을 수행할 수 있습니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L13-L15)]

Azure Configuration Manager 사용은 선택 사항입니다. .NET Framework의 `ConfigurationManager` 형식과 같은 API를 사용할 수도 있습니다.

### <a name="parse-the-connection-string"></a>연결 문자열 구문 분석

연결 문자열을 구문 분석 하려면 다음을 사용 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L21-L22)]

그러면이 반환 `CloudStorageAccount`됩니다.

### <a name="create-the-table-service-client"></a>Table service 클라이언트 만들기

클래스 `CloudTableClient` 를 사용 하면 테이블 저장소에서 테이블과 엔터티를 검색할 수 있습니다. 서비스 클라이언트를 만드는 한 가지 방법은 다음과 같습니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L28-L29)]

이제 데이터를 읽고 테이블 저장소에 데이터를 기록 하는 코드를 작성할 준비가 되었습니다.

### <a name="create-a-table"></a>테이블 생성하기

이 예에서는 테이블이 아직 없는 경우 테이블을 만드는 방법을 보여 줍니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L35-L39)]

### <a name="add-an-entity-to-a-table"></a>테이블에 엔터티 추가

엔터티에는에서 `TableEntity`상속 되는 형식이 있어야 합니다. 원하는 방식으로 `TableEntity` 확장할 수 있지만 형식에 매개 변수가 없는 생성자가 *있어야 합니다* . `get` 및`set` 를 모두 포함 하는 속성만 Azure 테이블에 저장 됩니다.

엔터티의 파티션 및 행 키는 테이블에서 엔터티를 고유 하 게 식별 합니다. 동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 사용 하는 것 보다 더 빨리 쿼리할 수 있지만 다양 한 파티션 키를 사용 하면 병렬 작업의 확장성을 높일 수 있습니다.

다음은를 파티션 키 `Customer` `lastName` 로 사용 하 고 `firstName` 을 행 키로 사용 하는의 예입니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L45-L52)]

이제 테이블 `Customer` 에를 추가 합니다. 이렇게 하려면 테이블에서 실행 되 `TableOperation` 는를 만듭니다. 이 경우 `Insert` 작업을 만듭니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L54-L55)]

### <a name="insert-a-batch-of-entities"></a>엔터티 일괄 처리 삽입

단일 쓰기 작업을 사용 하 여 엔터티 일괄 처리를 테이블에 삽입할 수 있습니다. 일괄 처리 작업을 통해 작업을 단일 실행으로 결합할 수 있지만 몇 가지 제한 사항이 있습니다.

- 동일한 일괄 작업에서 업데이트, 삭제 및 삽입을 수행할 수 있습니다.
- 일괄 처리 작업에는 최대 100 개의 엔터티가 포함 될 수 있습니다.
- 일괄 처리 작업의 모든 엔터티에는 동일한 파티션 키가 있어야 합니다.
- 일괄 처리 작업에서 쿼리를 수행할 수 있지만 일괄 처리에서 유일한 작업 이어야 합니다.

다음은 두 개의 삽입을 일괄 처리 작업으로 결합 하는 코드입니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L62-L71)]

### <a name="retrieve-all-entities-in-a-partition"></a>파티션의 모든 엔터티 검색

테이블에서 파티션의 모든 엔터티를 쿼리하려면 `TableQuery` 개체를 사용 합니다. 여기서 "Smith"가 파티션 키인 엔터티를 필터링 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L77-L82)]

이제 결과를 인쇄 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L84-L85)]

### <a name="retrieve-a-range-of-entities-in-a-partition"></a>파티션의 엔터티 범위 검색

파티션의 모든 엔터티를 쿼리하지 않으려면 파티션 키 필터를 행 키 필터와 결합 하 여 범위를 지정할 수 있습니다. 여기서는 두 개의 필터를 사용 하 여 행 키 (이름)가 알파벳의 "M" 보다 이전 문자로 시작 하는 "Smith" 파티션의 모든 엔터티를 가져옵니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L91-L100)]

이제 결과를 인쇄 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L102-L103)]

### <a name="retrieve-a-single-entity"></a>단일 엔터티 검색

단일 특정 엔터티를 검색 하는 쿼리를 작성할 수 있습니다. 여기서는를 `TableOperation` 사용 하 여 고객 "이혜준 씨 Smith"를 지정 합니다. 컬렉션 대신를 `Customer`반환 합니다. 쿼리에서 파티션 키와 행 키를 모두 지정 하는 것은 Table service에서 단일 엔터티를 검색 하는 가장 빠른 방법입니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L109-L111)]

이제 결과를 인쇄 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L113-L115)]

### <a name="replace-an-entity"></a>엔터티 바꾸기

엔터티를 업데이트 하려면 Table service에서 엔터티를 검색 하 고 엔터티 개체를 수정한 다음 작업을 `Replace` 사용 하 여 변경 내용을 Table service에 다시 저장 합니다. 이렇게 하면 서버의 엔터티가 검색 된 후 변경 되어 작업이 실패 하는 경우를 제외 하 고 서버에서 엔터티가 완전히 바뀝니다. 이 오류는 응용 프로그램에서 실수로 다른 원본의 변경 내용을 덮어쓰는 것을 방지 하기 위한 것입니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L121-L128)]

### <a name="insert-or-replace-an-entity"></a>엔터티 삽입 또는 바꾸기

경우에 따라 엔터티가 테이블에 있는지 여부를 알 수 없습니다. 이 경우 저장 된 현재 값이 더 이상 필요 하지 않습니다. 를 사용 `InsertOrReplace` 하 여 엔터티를 만들거나, 상태에 관계 없이 엔터티를 대체할 수 있습니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L134-L141)]

### <a name="query-a-subset-of-entity-properties"></a>엔터티 속성의 하위 집합 쿼리

테이블 쿼리는 엔터티의 일부 속성만 검색할 수 있습니다. 프로젝션 이라고 하는이 기술은 특히 규모가 많은 엔터티의 경우 쿼리 성능을 향상 시킬 수 있습니다. 여기서는 및 `DynamicTableEntity` `EntityResolver`를 사용 하 여 전자 메일 주소만 반환 합니다. 로컬 저장소 에뮬레이터에서는 프로젝션이 지원 되지 않으므로이 코드는 Table service의 계정을 사용 하는 경우에만 실행 됩니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L147-L158)]

### <a name="retrieve-entities-in-pages-asynchronously"></a>페이지에서 엔터티를 비동기적으로 검색

다 수의 엔터티를 읽고 모두 반환 될 때까지 기다리지 않고 검색할 때 처리 하려면 분할 된 쿼리를 사용할 수 있습니다. 여기서는 대량 결과 집합이 반환 될 때까지 대기 하는 동안 실행이 차단 되지 않도록 비동기 워크플로를 사용 하 여 페이지에서 결과를 반환 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L163-L178)]

이제이 계산을 동기적으로 실행 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L180-L180)]

### <a name="delete-an-entity"></a>엔터티 삭제

엔터티를 검색 한 후 삭제할 수 있습니다. 엔터티를 업데이트 하는 것 처럼 엔터티가 검색 된 후 변경 된 경우에는이 작업이 실패 합니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L186-L187)]

### <a name="delete-a-table"></a>테이블 삭제

저장소 계정에서 테이블을 삭제할 수 있습니다. 삭제 된 테이블은 삭제 후 일정 시간 동안 다시 만들 수 없습니다.

[!code-fsharp[TableStorage](~/samples/snippets/fsharp/azure/table-storage.fsx#L193-L193)]

## <a name="next-steps"></a>다음 단계

이제 테이블 저장소의 기본 사항을 배웠으므로 다음 링크를 따라 좀 더 복잡 한 저장소 작업 및 Azure Cosmos DB Table API에 대해 알아보세요.

- [Azure Cosmos DB Table API 소개](https://docs.microsoft.com/azure/cosmos-db/table-introduction)
- [.NET 용 저장소 클라이언트 라이브러리 참조](https://docs.microsoft.com/dotnet/api/overview/azure/storage)
- [Azure Storage 형식 공급자](https://fsprojects.github.io/AzureStorageTypeProvider/)
- [Azure Storage 팀 블로그](https://blogs.msdn.microsoft.com/windowsazurestorage/)
- [연결 문자열 구성](https://docs.microsoft.com/azure/storage/common/storage-configure-connection-string)
- [.NET에서 Azure Table Storage 시작](https://azure.microsoft.com/resources/samples/storage-table-dotnet-getting-started/)
