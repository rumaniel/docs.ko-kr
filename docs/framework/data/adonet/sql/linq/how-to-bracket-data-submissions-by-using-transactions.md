---
title: '방법: 트랜잭션을 사용하여 대괄호로 묶은 데이터 전송'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 94044a31-de90-479b-935a-8159b4ae5c5a
ms.openlocfilehash: 6a4c5ba7c4938b48fe489e43ff4a3ff806bd8916
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793811"
---
# <a name="how-to-bracket-data-submissions-by-using-transactions"></a>방법: 트랜잭션을 사용하여 대괄호로 묶은 데이터 전송
<xref:System.Transactions.TransactionScope>를 사용하여 데이터베이스에 대한 전송을 표시합니다. 자세한 내용은 [트랜잭션 지원](transaction-support.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 코드에서는 데이터베이스 전송을 <xref:System.Transactions.TransactionScope>로 묶습니다.  
  
 [!code-csharp[DLinqSubmittingChanges#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#3)]
 [!code-vb[DLinqSubmittingChanges#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [샘플 데이터베이스 다운로드](downloading-sample-databases.md)
- [데이터 변경 및 변경 내용 전송](making-and-submitting-data-changes.md)
- [트랜잭션 지원](transaction-support.md)
