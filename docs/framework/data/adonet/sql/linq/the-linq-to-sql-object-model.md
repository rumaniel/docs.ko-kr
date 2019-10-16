---
title: LINQ to SQL 개체 모델
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81dd0c37-e2a4-4694-83b0-f2e49e693810
ms.openlocfilehash: b73904e2347c501b21b2c5933d0b43c7abafeb7c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792319"
---
# <a name="the-linq-to-sql-object-model"></a>LINQ to SQL 개체 모델
에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]개발자의 프로그래밍 언어로 표현 된 개체 모델은 관계형 데이터베이스의 데이터 모델에 매핑됩니다. 그런 다음 개체 모델에 따라 데이터 작업이 수행됩니다.  
  
 이 시나리오에서는 데이터베이스에 대해 `INSERT`와 같은 데이터베이스 명령을 실행하지 않습니다. 대신 개체 모델 내에서 값을 변경하고 메서드를 실행합니다. 데이터베이스를 쿼리하거나 데이터베이스에 변경 내용을 보내려는 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 사용자의 요청을 올바른 SQL 명령으로 변환하고 이러한 명령을 데이터베이스에 보냅니다.  
  
 ![Linq 개체 모델을 보여 주는 스크린샷](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 개체 모델의 가장 기본적인 요소와 관계형 데이터 모델의 요소 간의 관계가 다음 표에 요약되어 있습니다.  
  
|LINQ to SQL 개체 모델|관계형 데이터 모델|  
|------------------------------|---------------------------|  
|엔터티 클래스|Table|  
|클래스 멤버|Column|  
|연결|외래 키 관계|  
|메서드|저장 프로시저 또는 함수|  
  
> [!NOTE]
> 지금부터는 관계형 데이터 모델과 규칙에 대해 어느 정도 지식이 있다고 가정하고 설명합니다.  
  
## <a name="linq-to-sql-entity-classes-and-database-tables"></a>LINQ to SQL 엔터티 클래스 및 데이터베이스 테이블  
 에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]데이터베이스 테이블은 *엔터티 클래스로*표현 됩니다. 엔터티 클래스는 클래스를 데이터베이스 테이블과 연결하는 특수한 정보를 사용하여 클래스에 주석을 단다는 점을 제외하고 사용자가 만들 수 있는 다른 클래스와 같습니다. 다음 예제와 같이 사용자 지정 특성(<xref:System.Data.Linq.Mapping.TableAttribute>)을 클래스 선언에 추가하여 이 주석을 만듭니다.  
  
### <a name="example"></a>예제  
 [!code-csharp[DLinqObjectModel#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#1)]
 [!code-vb[DLinqObjectModel#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#1)]  
  
 테이블로 선언된 클래스의 인스턴스(즉, 엔터티 클래스)만 데이터베이스에 저장할 수 있습니다.  
  
 자세한 내용은 [특성 기반 매핑의](attribute-based-mapping.md)테이블 특성 섹션을 참조 하세요.  
  
## <a name="linq-to-sql-class-members-and-database-columns"></a>LINQ to SQL 클래스 멤버 및 데이터베이스 열  
 클래스를 테이블과 연결하는 것 외에도 데이터베이스 열을 나타내는 필드나 속성을 지정합니다. 이 작업을 위해 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음 예제와 같이 <xref:System.Data.Linq.Mapping.ColumnAttribute> 특성을 정의합니다.  
  
### <a name="example"></a>예제  
 [!code-csharp[DLinqObjectModel#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#2)]
 [!code-vb[DLinqObjectModel#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#2)]  
  
 열에 매핑된 필드와 속성만 데이터베이스에서 유지되거나 검색됩니다. 열로 선언되지 않은 필드와 속성은 애플리케이션 논리의 임시 부분으로 간주됩니다.  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute> 특성에는 열을 나타내는 이러한 멤버를 사용자 지정(예: 기본 키 열을 나타내도록 멤버 지정)하는 데 사용할 수 있는 다양한 속성이 있습니다. 자세한 내용은 [특성 기반 매핑의](attribute-based-mapping.md)열 특성 섹션을 참조 하세요.  
  
## <a name="linq-to-sql-associations-and-database-foreign-key-relationships"></a>LINQ to SQL 연결 및 데이터베이스 외래 키 관계  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 <xref:System.Data.Linq.Mapping.AssociationAttribute> 특성을 적용하여 외래 키와 기본 키 사이의 관계와 같은 데이터베이스 연결을 나타냅니다. 다음 코드 세그먼트에서 `Order` 클래스는 `Customer` 특성이 있는 <xref:System.Data.Linq.Mapping.AssociationAttribute> 속성을 포함합니다. 이 속성과 해당 특성은 `Order` 클래스에 `Customer` 클래스와의 관계를 제공합니다.  
  
 다음 코드 예제에서는 `Customer` 클래스의 `Order` 속성을 보여 줍니다.  
  
### <a name="example"></a>예제  
 [!code-csharp[DLinqObjectModel#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#3)]
 [!code-vb[DLinqObjectModel#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#3)]  
  
 자세한 내용은 [특성 기반 매핑의](attribute-based-mapping.md)Association 특성 섹션을 참조 하세요.  
  
## <a name="linq-to-sql-methods-and-database-stored-procedures"></a>LINQ to SQL 메서드 및 데이터베이스 저장 프로시저  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 저장 프로시저와 사용자 정의 함수를 지원합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 이러한 데이터베이스 정의 추상화를 클라이언트 개체에 매핑하면 클라이언트 코드에서 강력한 형식으로 해당 개체에 액세스할 수 있습니다. 메서드 시그니처는 데이터베이스에 정의된 프로시저 및 함수의 시그니처와 매우 유사합니다. IntelliSense를 사용하여 이러한 메서드를 검색할 수 있습니다.  
  
 매핑된 프로시저에 대한 호출에서 반환되는 결과 집합은 강력한 형식의 컬렉션입니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 <xref:System.Data.Linq.Mapping.FunctionAttribute> 및 <xref:System.Data.Linq.Mapping.ParameterAttribute> 특성을 사용하여 저장 프로시저와 함수를 메서드에 매핑합니다. 저장 프로시저를 나타내는 메서드와 사용자 정의 함수를 나타내는 메서드는 <xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A> 속성에 의해 구별됩니다. 이 속성이 `false`(기본값)로 설정된 경우 메서드는 저장 프로시저를 나타내고 `true`로 설정된 경우 메서드는 데이터베이스 함수를 나타냅니다.  
  
> [!NOTE]
> Visual Studio를 사용 하는 경우 개체 관계형 디자이너를 사용 하 여 저장 프로시저 및 사용자 정의 함수에 매핑된 메서드를 만들 수 있습니다.  
  
### <a name="example"></a>예제  
 [!code-csharp[DLinqObjectModel#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#4)]
 [!code-vb[DLinqObjectModel#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#4)]  
  
 자세한 내용은 [특성 기반 매핑](attribute-based-mapping.md) 및 [저장 프로시저](stored-procedures.md)의 함수 특성, 저장 프로시저 특성 및 매개 변수 특성 섹션을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [특성 기반 매핑](attribute-based-mapping.md)
- [배경 정보](background-information.md)
