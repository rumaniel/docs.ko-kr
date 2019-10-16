---
title: '방법: 데이터베이스 값을 유지하여 충돌 해결'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b475cf72-9e64-4f6e-99c1-af7737bc85ef
ms.openlocfilehash: e42f48a188741c3ddff44f6444fa351192c8175f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793343"
---
# <a name="how-to-resolve-conflicts-by-retaining-database-values"></a>방법: 데이터베이스 값을 유지하여 충돌 해결
변경 내용을 다시 전송하기 전에 예상 데이터베이스 값과 실제 데이터베이스 값의 차이를 조정하려면 <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues>를 사용하여 데이터베이스에서 찾은 값을 유지합니다. 그런 다음 개체 모델의 현재 값을 덮어씁니다. 자세한 내용은 [낙관적 동시성: 개요](optimistic-concurrency-overview.md).  
  
> [!NOTE]
> 모든 경우에 데이터베이스에서 업데이트된 데이터를 검색하여 클라이언트의 레코드를 먼저 새로 고칩니다. 이렇게 하면 다음 업데이트 시도는 동일한 동시성 검사에서 실패하지 않습니다.  
  
## <a name="example"></a>예제  
 이 시나리오에서는 User1이 변경 내용을 제출하려는 경우 User2가 그 동안에 Assistant 열과 Department 열을 변경했기 때문에 <xref:System.Data.Linq.ChangeConflictException> 예외가 throw됩니다. 다음 표에서는 상황을 보여 줍니다.  
  
||관리자가|Assistant|Department|  
|------|-------------|---------------|----------------|  
|User1과 User2가 쿼리했을 때 원래 데이터베이스 상태|Alfreds|Maria|Sales|  
|User1이 변경 내용 전송 준비|Alfred||마케팅|  
|User2가 이미 변경 내용 전송||Mary|서비스|  
  
 User1이 최신 데이터베이스 값으로 개체 모델의 현재 값을 덮어써서 이 충돌을 해결하려고 합니다.  
  
 User1이 <xref:System.Data.Linq.RefreshMode.OverwriteCurrentValues>를 사용하여 충돌을 해결하는 경우 데이터베이스의 결과는 다음 표와 같습니다.  
  
||관리자가|Assistant|Department|  
|------|-------------|---------------|----------------|  
|충돌 해결 후 변경된 상태|Alfreds<br /><br /> (원래 값)|Mary<br /><br /> (User2가 전송한 값)|서비스<br /><br /> (User2가 전송한 값)|  
  
 다음 예제 코드에서는 개체 모델의 현재 값을 데이터베이스 값으로 덮어쓰는 방법을 보여 줍니다. 각 멤버 충돌에 대한 검사 또는 사용자 지정 처리는 발생하지 않습니다.  
  
 [!code-csharp[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [방법: 변경 내용 충돌 관리](how-to-manage-change-conflicts.md)
