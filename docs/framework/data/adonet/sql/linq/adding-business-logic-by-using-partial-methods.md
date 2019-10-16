---
title: Partial 메서드를 사용하여 비즈니스 논리 추가
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
ms.openlocfilehash: 251d7a05971ff7940f85ec9d555d26f2e57067c3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248131"
---
# <a name="adding-business-logic-by-using-partial-methods"></a>Partial 메서드를 사용하여 비즈니스 논리 추가
*부분 메서드*를 사용 하 C# 여 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 프로젝트에서 Visual Basic 및 생성 된 코드를 사용자 지정할 수 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 생성한 코드에는 부분 메서드의 일부로 시그니처를 정의합니다. 메서드를 구현하려면 사용자 고유의 부분 메서드를 추가합니다. 사용자 고유의 구현을 추가하지 않으면 컴파일러에서는 부분 메서드 시그니처를 취소하고 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]의 기본 메서드를 호출합니다.  
  
> [!NOTE]
> Visual Studio를 사용 하는 경우 개체 관계형 디자이너를 사용 하 여 엔터티 클래스에 유효성 검사 및 기타 사용자 지정 항목을 추가할 수 있습니다.  
  
 예를 들어 Northwind 샘플 데이터베이스의 `Customer` 클래스에 대한 기본 매핑에는 다음 부분 메서드가 포함됩니다.  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 다음과 같은 코드를 사용자 고유의 부분 `Customer` 클래스에 추가하여 사용자 고유의 메서드를 구현할 수 있습니다.  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 이러한 접근 방식은 일반적으로 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 `Insert`, `Update` 및 `Delete`에 대한 기본 메서드를 재정의하고 개체 수명 주기 이벤트 동안 속성의 유효성을 검사하는 데 사용됩니다.  
  
 자세한 내용은 [부분 메서드](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md) (Visual Basic) 또는 [부분 (메서드) (C# 참조)](../../../../../csharp/language-reference/keywords/partial-method.md) (C#)을 참조 하세요.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 다음 예제에서는 SQLMetal와 같은 코드 생성 도구에서 정의한 `ExampleClass`를 먼저 보여 준 다음 두 개의 메서드 중 하나만 구현하는 방법을 보여 줍니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 `Shipper`와 `Order` 엔터티 간의 관계를 사용합니다. 메서드 중 부분 메서드는 `InsertShipper`와 `DeleteShipper`입니다. 이러한 메서드는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 매핑을 통해 제공된 기본 부분 메서드를 재정의합니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>참고자료

- [데이터 변경 및 변경 내용 전송](making-and-submitting-data-changes.md)
- [삽입, 업데이트 및 삭제 작업 사용자 지정](customizing-insert-update-and-delete-operations.md)
