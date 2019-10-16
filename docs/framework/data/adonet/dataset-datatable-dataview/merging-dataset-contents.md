---
title: 데이터 세트 콘텐츠 병합
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e9309a-3ebb-4a9c-9d78-21c4e2bafc5b
ms.openlocfilehash: abc9183666602a7ef369e690e3ae499f8c7b8b11
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784404"
---
# <a name="merging-dataset-contents"></a>데이터 세트 콘텐츠 병합

<xref:System.Data.DataSet.Merge%2A> 메서드를 사용하여 <xref:System.Data.DataSet>, <xref:System.Data.DataTable> 또는 <xref:System.Data.DataRow> 배열의 내용을 기존 `DataSet`으로 병합할 수 있습니다. 새 데이터가 기존 `DataSet`으로 병합되는 방법은 몇 가지 요소 및 옵션에 따라 달라집니다.

## <a name="primary-keys"></a>기본 키

병합을 통해 새 데이터와 스키마를 받는 테이블에 기본 키가 있는 경우 들어오는 데이터의 새 행은 들어오는 데이터의 행과 동일한 <xref:System.Data.DataRowVersion.Original> 기본 키 값을 가진 기존 행이 있는지 비교됩니다. 들어오는 스키마의 열이 기존 스키마의 열과 일치하면 기존 행의 데이터가 수정됩니다. 기존 스키마와 일치하지 않는 열은 <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> 매개 변수에 따라 무시되거나 추가됩니다. 기존 행과 일치하지 않는 기본 키 값을 가진 새 행은 기존 테이블에 추가됩니다.

들어오는 행 또는 기존 행의 상태가 <xref:System.Data.DataRowState.Added>이면 <xref:System.Data.DataRowVersion.Current> 행 버전이 없으므로 해당 기본 키 값은 `Added` 행의 `Original` 기본 키 값을 사용하여 비교됩니다.

들어오는 테이블과 기존 테이블에 이름은 같지만 데이터 형식이 다른 열이 있으면 예외가 throw되고 <xref:System.Data.DataSet.MergeFailed>의 `DataSet` 이벤트가 발생합니다. 들어오는 테이블과 기존 테이블에 모두 키가 정의되어 있지만 각 열의 기본 키가 서로 다르면 예외가 throw되고 `MergeFailed`의 `DataSet` 이벤트가 발생합니다.

병합을 통해 새 데이터를 받는 테이블에 기본 키가 없으면 들어오는 데이터의 새 행이 테이블의 기존 행과 일치할 수는 없고, 대신 기존 테이블에 추가됩니다.

## <a name="table-names-and-namespaces"></a>테이블 이름 및 네임스페이스

<xref:System.Data.DataTable> 개체에는 선택적으로 <xref:System.Data.DataTable.Namespace%2A> 속성 값을 할당할 수 있습니다. <xref:System.Data.DataTable.Namespace%2A> 값이 할당된 경우 <xref:System.Data.DataSet>에는 <xref:System.Data.DataTable> 값이 같은 여러 <xref:System.Data.DataTable.TableName%2A> 개체가 있을 수 있습니다. 병합 작업 도중 <xref:System.Data.DataTable.TableName%2A> 및 <xref:System.Data.DataTable.Namespace%2A>를 사용하여 병합의 대상을 식별합니다. <xref:System.Data.DataTable.Namespace%2A>가 할당되지 않은 경우에는 <xref:System.Data.DataTable.TableName%2A>만 사용하여 병합의 대상을 식별합니다.

> [!NOTE]
> 이는 .NET Framework의 버전 2.0에서 변경된 동작입니다. 버전 1.1에서는 네임스페이스가 지원되었지만 병합 작업 도중 무시되었습니다. 이러한 이유로 <xref:System.Data.DataSet> 속성 값을 사용하는 <xref:System.Data.DataTable.Namespace%2A>은 실행 중인 .NET Framework의 버전에 따라 다르게 동작합니다. 예를 들어 `DataSets` 속성 값은 같지만 `DataTables` 속성 값이 다른 <xref:System.Data.DataTable.TableName%2A>가 있는 두 개의 <xref:System.Data.DataTable.Namespace%2A>가 있다고 가정합니다. .NET Framework의 버전 1.1에서는 두 <xref:System.Data.DataTable.Namespace%2A> 개체를 병합할 때 서로 다른 <xref:System.Data.DataSet> 이름은 무시됩니다. 하지만 버전 2.0부터는 병합할 경우 두 개의 새로운 `DataTables`가 대상 <xref:System.Data.DataSet>에 생성됩니다. 원래의 `DataTables`는 병합의 영향을 받지 않습니다.

## <a name="preservechanges"></a>PreserveChanges

`DataSet`, `DataTable` 또는 `DataRow` 배열을 `Merge` 메서드로 전달할 때는 기존 `DataSet`의 변경 내용을 유지할 것인지 여부와 들어오는 데이터에서 발견되는 새 스키마 요소를 처리하는 방법을 지정하는 선택적 매개 변수를 포함할 수 있습니다. 들어오는 데이터 다음에 나오는 이러한 매개 변수 중 첫 번째는 부울 플래그인 <xref:System.Data.LoadOption.PreserveChanges>이며, 이 플래그는 기존 `DataSet`의 변경 내용을 유지할지 여부를 지정합니다. `PreserveChanges` 플래그가 `true`로 설정되어 있으면 들어오는 값은 기존 행의 `Current` 행 버전에 있는 기존 값을 덮어쓰지 않습니다. `PreserveChanges` 플래그가 `false`로 설정되어 있으면 들어오는 값은 기존 행의 `Current` 행 버전에 있는 기존 값을 덮어씁니다. `PreserveChanges` 플래그를 지정하지 않으면 `false`가 기본값으로 설정됩니다. 행 버전에 대 한 자세한 내용은 참조 하세요. [행 상태 및 행 버전](row-states-and-row-versions.md)합니다.

`PreserveChanges`가 `true`이면 기존 행의 데이터는 기존 행의 <xref:System.Data.DataRowVersion.Current> 행 버전에 유지되지만 기존 행의 <xref:System.Data.DataRowVersion.Original> 행 버전에 있는 데이터는 들어오는 행의 `Original` 행 버전에 있는 데이터로 덮어쓰여집니다. 기존 행의 <xref:System.Data.DataRow.RowState%2A>는 <xref:System.Data.DataRowState.Modified>로 설정됩니다. 다음과 같은 예외가 있습니다.

- 기존 행의 `RowState`가 `Deleted`인 경우 이 `RowState`는 `Deleted`로 유지되며 `Modified`로 설정되지 않습니다. 이 경우, 들어오는 행의 데이터는 기존 행의 `Original` 행 버전에 계속 저장되어 기존 행의 `Original` 행 버전을 덮어씁니다. 단, 들어오는 행의 `RowState`가 `Added`인 경우는 예외입니다.

- 들어오는 행의 `RowState`가 `Added`이면 들어오는 행에 `Original` 행 버전이 없으므로 기존 행의 `Original` 행 버전 데이터가 들어오는 행의 데이터로 덮어쓰여지지 않습니다.

`PreserveChanges`가 `false`이면 기존 행의 `Current` 및 `Original` 행 버전이 들어오는 행의 데이터로 덮어쓰여지며 기존 행의 `RowState`는 들어오는 행의 `RowState`로 설정됩니다. 다음과 같은 예외가 있습니다.

- 들어오는 행의 `RowState`가 `Unchanged`이고 기존 행의 `RowState`가 `Modified`, `Deleted` 또는 `Added`이면 기존 행의 `RowState`가 `Modified`로 설정됩니다.

- 들어오는 행의 `RowState`가 `Added`이고 기존 행의 `RowState`가 `Unchanged`, `Modified` 또는 `Deleted`이면 기존 행의 `RowState`가 `Modified`로 설정됩니다. 또한, 들어오는 행에 `Original` 행 버전이 없으므로 기존 행의 `Original` 행 버전 데이터는 들어오는 행의 데이터로 덮어쓰여지지 않습니다.

## <a name="missingschemaaction"></a>MissingSchemaAction

<xref:System.Data.MissingSchemaAction> 메서드의 선택적 `Merge` 매개 변수를 사용하면 기존 `Merge`에 포함되어 있지 않은 들어오는 데이터의 스키마 요소를 `DataSet`에서 어떻게 처리할지 지정할 수 있습니다.

다음 표에서는 `MissingSchemaAction`의 옵션을 설명합니다.

|MissingSchemaAction 옵션|설명|
|--------------------------------|-----------------|
|<xref:System.Data.MissingSchemaAction.Add>|`DataSet`에 새 스키마 정보를 추가한 다음 새 열을 들어오는 값으로 채웁니다. 이 값이 기본값입니다.|
|<xref:System.Data.MissingSchemaAction.AddWithKey>|`DataSet`에 새 스키마와 기본 키 정보를 추가한 다음 새 열을 들어오는 값으로 채웁니다.|
|<xref:System.Data.MissingSchemaAction.Error>|일치하지 않는 스키마 정보가 발견되면 예외가 throw됩니다.|
|<xref:System.Data.MissingSchemaAction.Ignore>|새 스키마 정보를 무시합니다.|

## <a name="constraints"></a>제약 조건

`Merge` 메서드를 사용하면 새 데이터가 기존 `DataSet`에 모두 추가되기 전까지 제약 조건이 검사되지 않습니다. 데이터가 추가되고 나면 `DataSet`의 현재 값에 제약 조건이 적용됩니다. 제약 조건 위반으로 인해 throw되는 모든 예외를 처리하도록 코드를 작성해야 합니다.

`DataSet`의 기존 행이 기본 키 값이 1인 `Unchanged` 행인 경우를 살펴보세요. `Modified` 기본 키 값이 2이고 `Original` 기본 키 값이 1인 `Current` 들어오는 행에 대해 병합 작업을 수행할 경우 `Original` 기본 키 값이 다르기 때문에 기존 행과 들어오는 행은 일치하지 않는 것으로 간주됩니다. 그러나 병합을 완료하고 제약 조건을 검사하면 `Current` 기본 키 값이 기본 키 열의 UNIQUE 제약 조건을 위반하므로 예외가 throw됩니다.

> [!NOTE]
> ID 열과 같은 자동 증분 열이 있는 데이터베이스 테이블에 행이 삽입되는 경우에는 삽입을 통해 반환되는 ID 열 값이 `DataSet`의 값과 일치하지 않을 수 있으므로 반환되는 행이 병합되는 대신 추가됩니다. 자세한 내용은 [id 또는 일련 번호 값 검색](../retrieving-identity-or-autonumber-values.md)을 참조 하세요.

다음 코드 예제에서는 두 개의 `DataSet` 들어오는 `DataSet` 개체의 결합 된 스키마 `DataSet` 를 사용 하 여 스키마가 서로 다른 두 개의 개체를 하나로 병합 합니다.

[!code-csharp[DataWorks DataSet.Merge#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.Merge#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/VB/source.vb#1)]

다음 코드 예제에서는 업데이트 사항이 있는 기존 `DataSet`을 사용하여 해당 업데이트를 `DataAdapter`로 전달하여 데이터 소스에서 처리되도록 합니다. 그러면 결과가 원래 `DataSet`에 병합됩니다. 오류를 발생시킨 변경 내용이 거부된 후에는 병합된 변경 내용이 `AcceptChanges`를 사용하여 커밋됩니다.

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#1)]

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#2)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#2)]

## <a name="see-also"></a>참고자료

- [DataSet, DataTable 및 DataView](index.md)
- [행 상태 및 행 버전](row-states-and-row-versions.md)
- [DataAdapter 및 DataReader](../dataadapters-and-datareaders.md)
- [ADO.NET에서 데이터 검색 및 수정](../retrieving-and-modifying-data.md)
- [ID 또는 일련 번호 값 검색](../retrieving-identity-or-autonumber-values.md)
- [ADO.NET 개요](../ado-net-overview.md)
