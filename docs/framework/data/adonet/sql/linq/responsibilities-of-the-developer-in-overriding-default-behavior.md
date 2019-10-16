---
title: 기본 동작 재정의에서 개발자의 책임
ms.date: 03/30/2017
ms.assetid: c6909ddd-e053-46a8-980c-0e12a9797be1
ms.openlocfilehash: 4bfb108e81f64ea368c6bcc846553eb1af5c23b1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792733"
---
# <a name="responsibilities-of-the-developer-in-overriding-default-behavior"></a>기본 동작 재정의에서 개발자의 책임
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 다음 요구 사항을 적용 하지 않습니다. 그러나 이러한 요구 사항이 충족 되지 않는 경우 동작은 정의 되지 않습니다.  
  
- 재정의 메서드에서는 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 또는 <xref:System.Data.Linq.Table%601.Attach%2A>를 호출해서는 안 됩니다. 이러한 메서드를 호출하면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 예외를 throw합니다.  
  
- 재정의 메서드는 트랜잭션을 시작, 커밋 또는 중지하는 데 사용할 수 없습니다. <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 작업은 트랜잭션에서 수행됩니다. 내부 중첩 트랜잭션이 외부 트랜잭션을 방해할 수 있습니다. 로드 재정의 메서드는 <xref:System.Transactions.Transaction>에서 작업이 수행되지 않는 것을 확인한 후에만 트랜잭션을 시작할 수 있습니다.  
  
- 재정의 메서드는 적용 가능한 낙관적 동시성 매핑을 따릅니다. 낙관적 동시성 충돌이 발생하면 재정의 메서드에서는 <xref:System.Data.Linq.ChangeConflictException>을 throw하며 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]<xref:System.Data.Linq.DataContext.SubmitChanges%2A> 에서<xref:System.Data.Linq.DataContext.SubmitChanges%2A>제공 하는 옵션을 올바르게 처리할 수 있도록이 예외를 catch 합니다.  
  
- 만들기(`Insert`) 및 `Update` 재정의 메서드에서는 작업이 완료되면 데이터베이스에서 생성된 열의 값을 해당 개체 멤버로 다시 보내야 합니다.  
  
     예를 들어가 `Order.OrderID` id 열 (*autoincrement* 기본 키)에 매핑되는 경우 재정의 메서드는 `InsertOrder()` `Order.OrderID` 데이터베이스에서 생성 된 id를 검색 하 고 멤버를 해당 id로 설정 해야 합니다. 마찬가지로 타임스탬프 멤버를 데이터베이스에서 생성된 타임스탬프 값으로 업데이트하여 업데이트된 개체가 일치되도록 해야 합니다. 데이터베이스에서 생성된 값을 전파하는 데 실패하면 <xref:System.Data.Linq.DataContext>에서 추적한 개체와 데이터베이스 간에 불일치가 발생할 수 있습니다.  
  
- 올바른 동적 API를 호출하는 것은 사용자의 책임입니다. 예를 들어 업데이트 재정의 메서드에서는 <xref:System.Data.Linq.DataContext.ExecuteDynamicUpdate%2A>만 호출할 수 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 호출된 동적 메서드가 적용 가능한 작업과 일치하는지 여부를 감지하거나 확인하지 않습니다. 업데이트할 개체에 대해 <xref:System.Data.Linq.DataContext.ExecuteDynamicDelete%2A>와 같은 적용 불가능한 메서드를 호출하면 결과가 정의되지 않습니다.  
  
- 마지막으로 재정의 메서드는 지정된 작업을 수행해야 합니다. 즉시 로드, 지연된 로드 및 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]와 같은 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 작업의 의미가 구현되려면 재정의 메서드에서 해당 서비스를 제공해야 합니다. 예를 들어 데이터베이스의 내용을 확인하지 않고 빈 컬렉션만 반환하는 로드 재정의는 데이터 불일치를 발생시킬 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- [삽입, 업데이트 및 삭제 작업 사용자 지정](customizing-insert-update-and-delete-operations.md)
