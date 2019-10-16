---
ms.openlocfilehash: 33ad1c044001e0a8d09708cc7a1f06e05cb307de
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804574"
---
### <a name="different-exception-handling-for-objectcontextcreatedatabase-and-dbproviderservicescreatedatabase-methods"></a>ObjectContext.CreateDatabase 및 DbProviderServices.CreateDatabase 메서드를 처리하는 다른 예외

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 데이터베이스 만들기에 실패하면 <code>CreateDatabase</code> 메서드는 빈 데이터베이스를 삭제하려고 합니다. 해당 작업에 성공하면 원래의 <xref:System.Data.SqlClient.SqlException?displayProperty=name>이 전파됩니다(항상 .NET Framework 4.0에서 throw된 <xref:System.InvalidOperationException?displayProperty=name> 대신).|
|제안 해결 방법|<xref:System.Data.Objects.ObjectContext.CreateDatabase> 또는 <xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)>를 실행하는 동안 <xref:System.InvalidOperationException?displayProperty=name>을 catch하는 경우, 이제 SQLExceptions도 catch됩니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Data.Objects.ObjectContext.CreateDatabase?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbProviderServices.CreateDatabase(System.Data.Common.DbConnection,System.Nullable{System.Int32},System.Data.Metadata.Edm.StoreItemCollection)?displayProperty=nameWithType></li></ul>|
