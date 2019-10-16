---
title: '연습: 관계 간 쿼리(Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: a7da43e3-769f-4e07-bcd6-552b8bde66f4
ms.openlocfilehash: 3164656bb183e7773b098cab79d8fe5e0dc5de34
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792152"
---
# <a name="walkthrough-querying-across-relationships-visual-basic"></a>연습: 관계 간 쿼리(Visual Basic)
이 연습에서는 *연결* 을 사용 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 하 여 데이터베이스에서 외래 키 관계를 나타내는 방법을 보여 줍니다.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 이 연습은 Visual Basic 개발 설정을 사용하여 작성했습니다.  
  
## <a name="prerequisites"></a>전제 조건  
 연습을 완료 [해야 합니다. 간단한 개체 모델 및 쿼리 (Visual Basic)](walkthrough-simple-object-model-and-query-visual-basic.md). 이 연습은 c:\linqtest에 있는 northwnd.mdf 파일을 비롯하여 해당 연습의 단순 개체 모델 및 쿼리를 기반으로 합니다.  
  
## <a name="overview"></a>개요  
 이 연습은 다음과 같은 세 가지 주요 작업으로 구성됩니다.  
  
- Northwind 샘플 데이터베이스의 Orders 테이블을 나타내는 엔터티 클래스 추가  
  
- `Customer` 및 `Customer` 클래스 간의 관계를 향상시키기 위해 `Order` 클래스에 주석 추가  
  
- `Order` 클래스를 사용하여 `Customer` 정보를 가져오는 과정을 테스트하는 쿼리 만들기 및 실행  
  
## <a name="mapping-relationships-across-tables"></a>테이블 간 관계 매핑  
 `Customer` 클래스 정의 후에 `Order`가 외래 키로 `Orders.Customer`에 관련된다는 것을 나타내는 다음 코드가 포함된 `Customers.CustomerID` 엔터티 클래스 정의를 만듭니다.  
  
#### <a name="to-add-the-order-entity-class"></a>Order 엔터티 클래스를 추가하려면  
  
- `Customer` 클래스 뒤에 다음 코드를 입력하거나 붙여넣습니다.  
  
     [!code-vb[DLinqWalk2VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#1)]  
  
## <a name="annotating-the-customer-class"></a>Customer 클래스에 주석 지정  
 이 단계에서는 `Customer` 클래스에 대한 관계를 나타내기 위해 `Order` 클래스에 주석을 지정합니다. 어느 방향으로든 관계를 정의하여 링크를 충분히 만들 수 있으므로 이 추가 작업이 반드시 필요한 것은 아닙니다. 그러나 이 주석을 추가하면 어느 방향으로나 개체를 쉽게 탐색할 수 있습니다.  
  
#### <a name="to-annotate-the-customer-class"></a>Customer 클래스에 주석을 달려면  
  
- `Customer` 클래스에 다음 코드를 입력하거나 붙여넣습니다.  
  
     [!code-vb[DLinqWalk2VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#2)]  
  
## <a name="creating-and-running-a-query-across-the-customer-order-relationship"></a>Customer 및 Order 관계에서 쿼리 만들기 및 실행  
 이제 `Order` 개체에서 `Customer` 개체를 직접 액세스하거나 그 반대 방향으로 액세스할 수 있습니다. 고객과 주문 간에 명시적 *조인이* 필요 하지 않습니다.  
  
#### <a name="to-access-order-objects-by-using-customer-objects"></a>Customer 개체를 사용하여 Order 개체에 액세스하려면  
  
1. 다음 코드를 `Sub Main` 메서드에 입력하거나 붙여넣어 이 메서드를 수정합니다.  
  
     [!code-vb[DLinqWalk2VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#3)]  
  
2. F5 키를 눌러 애플리케이션을 디버깅합니다.  
  
     두 이름이 메시지 상자에 표시되며 콘솔 창에는 생성된 SQL 코드가 표시됩니다.  
  
3. 메시지 상자를 닫아 디버깅을 중지합니다.  
  
## <a name="creating-a-strongly-typed-view-of-your-database"></a>강력한 형식의 데이터베이스 뷰 만들기  
 강력한 형식의 데이터베이스 뷰로 작업을 시작하는 것이 훨씬 더 쉽습니다. <xref:System.Data.Linq.DataContext> 개체를 강력한 형식으로 설정하면 <xref:System.Data.Linq.DataContext.GetTable%2A> 호출이 필요하지 않습니다. 강력한 형식의 <xref:System.Data.Linq.DataContext> 개체를 사용할 경우 모든 쿼리에서 강력한 형식의 테이블을 사용할 수 있습니다.  
  
 다음 단계에서는 `Customers`를 데이터베이스의 Customers 테이블에 매핑되는 강력한 형식의 테이블로 만듭니다.  
  
#### <a name="to-strongly-type-the-datacontext-object"></a>DataContext 개체를 강력한 형식으로 설정하려면  
  
1. `Customer` 클래스 선언 위에 다음 코드를 추가합니다.  
  
     [!code-vb[DLinqWalk2VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#4)]  
  
2. 다음과 같이 강력한 형식의 `Sub Main`를 사용하도록 <xref:System.Data.Linq.DataContext>을 수정합니다.  
  
     [!code-vb[DLinqWalk2VB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk2VB/vb/Module1.vb#5)]  
  
3. F5 키를 눌러 애플리케이션을 디버깅합니다.  
  
     콘솔 창 출력은 다음과 같습니다.  
  
     `ID=WHITC`  
  
4. 콘솔 창에서 Enter 키를 눌러 애플리케이션을 닫습니다.  
  
5. 이 응용 프로그램을 저장 하려면 **파일** 메뉴에서 **모두 저장** 을 클릭 합니다.  
  
## <a name="next-steps"></a>다음 단계  
 다음 연습 ([연습: 데이터 조작 (Visual Basic)](walkthrough-manipulating-data-visual-basic.md)은 데이터를 조작 하는 방법을 보여 줍니다. 다음 연습에서는 이미 완료한 이 시리즈의 연습 두 개를 저장할 필요가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [연습으로 학습](learning-by-walkthroughs.md)
