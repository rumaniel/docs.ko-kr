---
title: '낙관적 동시성: 개요'
ms.date: 03/30/2017
ms.assetid: c2e38512-d0c8-4807-b30a-cb7e30338694
ms.openlocfilehash: fa7d423c0abc07e0d97f7d0d4d557aa11d675ee4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792932"
---
# <a name="optimistic-concurrency-overview"></a>낙관적 동시성: 개요
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 낙관적 동시성 제어를 지원합니다. 다음 표에서는 설명서에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 낙관적 동시성에 적용 되는 용어에 대해 설명 합니다.  
  
|용어|설명|  
|-----------|-----------------|  
|동시성|둘 이상의 사용자가 동일한 데이터베이스 행을 동시에 업데이트하려는 상황입니다.|  
|동시성 충돌(concurrency conflict)|둘 이상의 사용자가 한 행의 하나 이상의 열에 충돌하는 값을 동시에 전송하려는 상황입니다.|  
|동시성 제어|동시성 충돌을 해결하는 데 사용되는 기술입니다.|  
|낙관적 동시성 제어|변경 내용이 전송되도록 허용하기 전에 다른 트랜잭션에서 행의 값을 변경했는지 조사하는 기술입니다.<br /><br /> *비관적 동시성 제어*와 달리 동시성 충돌을 방지 하기 위해 레코드를 잠급니다.<br /><br /> *낙관적* 제어는 한 트랜잭션이 다른 트랜잭션으로 간섭 하는 가능성을 고려 하지 않기 때문에 가능 합니다.|  
|충돌 해결|데이터베이스를 다시 쿼리한 다음 차이를 조정하여 충돌하는 항목을 새로 고치는 프로세스입니다.<br /><br /> 개체를 새로 고칠 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 변경 추적기는 다음 데이터를 보유합니다.<br /><br /> -원래 데이터베이스에서 가져온 값으로 업데이트 확인에 사용 됩니다.<br />-후속 쿼리의 새 데이터베이스 값입니다.<br /><br /> 그런 다음 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 개체가 충돌하는지 여부(즉, 해당 멤버 값 중 하나 이상이 변경되었는지 여부)를 확인합니다. 개체가 충돌할 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 해당 멤버 중에서 충돌하는 멤버를 확인합니다.<br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]이 검색한 모든 멤버 충돌은 충돌 목록에 추가됩니다.|  
  
 개체 모델에서 *낙관적 동시성 충돌* 은 다음 두 조건에 모두 해당 하는 경우에 발생 합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]  
  
- 클라이언트가 변경 내용을 데이터베이스로 전송하려고 합니다.  
  
- 하나 이상의 업데이트 확인 값이 클라이언트가 마지막으로 읽은 후에 데이터베이스에서 업데이트되었습니다.  
  
 이 충돌을 해결하는 과정에는 충돌하는 개체의 멤버를 검색한 다음 수행할 작업을 결정하는 작업이 포함됩니다.  
  
> [!NOTE]
> <xref:System.Data.Linq.Mapping.UpdateCheck.Always> 또는 <xref:System.Data.Linq.Mapping.UpdateCheck.WhenChanged>로 매핑된 멤버만 낙관적 동시성 검사에 참여합니다. <xref:System.Data.Linq.Mapping.UpdateCheck.Never>로 표시된 멤버에는 검사가 수행되지 않습니다. 자세한 내용은 <xref:System.Data.Linq.Mapping.UpdateCheck>을 참조하세요.  
  
## <a name="example"></a>예제  
 예를 들어, 다음 시나리오에서 User1은 데이터베이스에서 행을 쿼리하여 업데이트 준비를 시작합니다. User1은 Alfreds, Maria 및 Sales 값을 가진 행을 받습니다.  
  
 User1은 Manager 열의 값을 Alfred로 변경하고 Department 열의 값을 Marketing으로 변경하려고 합니다. User1이 이러한 변경 내용을 전송하기 전에 User2가 데이터베이스에 변경 내용을 전송했습니다. 따라서 이제 Assistant 열의 값은 Mary로 변경되고 Department 열의 값은 Service로 변경되었습니다.  
  
 이제 User1이 변경 내용을 전송하려고 하면 전송이 실패하고 <xref:System.Data.Linq.ChangeConflictException> 예외가 throw됩니다. Assistant 열과 Department 열에 대한 데이터베이스 값이 예상했던 것과 다르기 때문에 이 결과가 발생합니다. Assistant 및 Department 열을 나타내는 멤버가 충돌합니다. 다음 표에서는 이 상황을 요약하여 보여 줍니다.  
  
||관리자가|Assistant|Department|  
|------|-------------|---------------|----------------|  
|원래 상태|Alfreds|Maria|Sales|  
|User1|Alfred||마케팅|  
|User2||Mary|서비스|  
  
 여러 다른 방법으로 이와 같은 충돌을 해결할 수 있습니다. 자세한 내용은 [방법: 변경 충돌](how-to-manage-change-conflicts.md)을 관리 합니다.  
  
## <a name="conflict-detection-and-resolution-checklist"></a>충돌 감지 및 해결 검사 목록  
 모든 상세 수준에서 충돌을 감지하고 해결할 수 있습니다. 한편으로는 추가 고려 사항 없이 세 가지 방법(<xref:System.Data.Linq.RefreshMode> 참조) 중 하나로 모든 충돌을 해결할 수도 있고 다른 한편으로는 충돌하는 모든 멤버에서 각 충돌 유형에 대한 특정 작업을 지정할 수도 있습니다.  
  
- 개체 모델에서 <xref:System.Data.Linq.Mapping.UpdateCheck> 옵션을 지정하거나 수정합니다.  
  
     자세한 내용은 [방법: 동시성 충돌](how-to-specify-which-members-are-tested-for-concurrency-conflicts.md)에 대해 테스트할 멤버를 지정 합니다.  
  
- <xref:System.Data.Linq.DataContext.SubmitChanges%2A>에 대한 호출의 try/catch 블록에서 예외를 throw하려는 지점을 지정합니다.  
  
     자세한 내용은 [방법: 동시성 예외가 Throw](how-to-specify-when-concurrency-exceptions-are-thrown.md)되는 시기를 지정 합니다.  
  
- 검색하려는 충돌 정보의 양을 결정하고 이에 따라 try/catch 블록에 코드를 포함시킵니다.  
  
     자세한 내용은 [방법: 엔터티 충돌 정보](how-to-retrieve-entity-conflict-information.md) 검색 및 [방법: 멤버 충돌 정보](how-to-retrieve-member-conflict-information.md)를 검색 합니다.  
  
- 검색 하는 `try` 다양 한 충돌을 해결 하는 방법을 `catch` 코드에 / 포함 합니다.  
  
     자세한 내용은 [방법: 데이터베이스 값](how-to-resolve-conflicts-by-retaining-database-values.md)을 보존 하 여 충돌 [해결, 방법: 데이터베이스 값](how-to-resolve-conflicts-by-overwriting-database-values.md)을 덮어써서 충돌을 해결 하 [고 다음을 수행 합니다. 데이터베이스 값](how-to-resolve-conflicts-by-merging-with-database-values.md)과 병합 하 여 충돌을 해결 합니다.  
  
## <a name="linq-to-sql-types-that-support-conflict-discovery-and-resolution"></a>충돌 검색 및 해결을 지원하는 LINQ to SQL 형식  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 낙관적 동시성의 충돌 해결을 지원하기 위한 클래스와 기능은 다음과 같습니다.  
  
- <xref:System.Data.Linq.ObjectChangeConflict?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.MemberChangeConflict?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.ChangeConflictCollection?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.ChangeConflictException?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.ChangeConflicts%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.DataContext.Refresh%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.Mapping.UpdateCheck?displayProperty=nameWithType>  
  
- <xref:System.Data.Linq.RefreshMode?displayProperty=nameWithType>  
  
## <a name="see-also"></a>참고자료

- [방법: 변경 내용 충돌 관리](how-to-manage-change-conflicts.md)
