---
title: '방법: 데이터베이스에 변경 내용 전송'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: c279d4ed32aed4788ee5866a24572663a1e2f580
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793114"
---
# <a name="how-to-submit-changes-to-the-database"></a>방법: 데이터베이스에 변경 내용 전송
개체의 변경 내용 수에 관계없이 메모리 내의 복제본에만 변경 내용이 적용됩니다. 데이터베이스의 실제 데이터는 변경하지 않습니다. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>의 <xref:System.Data.Linq.DataContext>를 명시적으로 호출한 후에 변경 내용이 서버에 전송됩니다.  
  
 이러한 호출을 수행할 때 <xref:System.Data.Linq.DataContext>는 변경 내용을 해당 SQL 명령으로 변환하려고 합니다. 사용자 고유의 사용자 지정 논리를 사용 하 여 이러한 작업을 재정의할 수 있지만 전송 순서는 <xref:System.Data.Linq.DataContext> *변경 프로세서*라는의 서비스에 의해 오케스트레이션 됩니다. 작업이 진행되는 순서는 다음과 같습니다.  
  
1. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 호출하는 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 알려진 개체 집합을 사용하여 새 인스턴스와의 연결 여부를 확인합니다. 새 인스턴스와 연결되어 있는 경우 새 인스턴스는 추적된 개체 집합에 추가됩니다.  
  
2. 보류 중인 변경 내용이 있는 모든 개체는 이들 간의 종속성을 기반으로 개체 시퀀스로 정렬됩니다. 다른 개체에 종속된 변경 내용을 가진 개체는 해당 종속 개체 뒤에 정렬됩니다.  
  
3. 실제 변경 내용이 전송되기 직전 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 트랜잭션을 시작하여 일련의 개별 명령을 캡슐화합니다.  
  
4. 개체에 대한 변경 내용은 하나씩 SQL 명령으로 변환되어 서버로 전송됩니다.  
  
 이때 데이터베이스에서 오류가 발견되면 전송 프로세스가 중지되고 예외가 발생합니다. 데이터베이스의 모든 변경 내용이 어떠한 전송도 발생하지 않은 것처럼 롤백됩니다. <xref:System.Data.Linq.DataContext>에는 여전히 모든 변경 내용에 대한 전체 기록이 있습니다. 따라서 문제를 해결하고 다음 코드 예제에서처럼 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 다시 호출할 수 있습니다.  
  
## <a name="example"></a>예제  
 전송 주위의 트랜잭션이 성공적으로 완료되는 경우 <xref:System.Data.Linq.DataContext>는 변경 추적 정보를 무시하여 개체의 변경 내용을 적용합니다.  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [방법: 충돌 하는 전송 검색 및 해결](how-to-detect-and-resolve-conflicting-submissions.md)
- [방법: 변경 내용 충돌 관리](how-to-manage-change-conflicts.md)
- [샘플 데이터베이스 다운로드](downloading-sample-databases.md)
- [데이터 변경 및 변경 내용 전송](making-and-submitting-data-changes.md)
