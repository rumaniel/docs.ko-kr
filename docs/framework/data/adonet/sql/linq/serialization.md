---
title: Serialization2
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a15ae411-8dc2-4ca3-84d2-01c9d5f1972a
ms.openlocfilehash: bf303f9a79fbcab85d33fcb3ebb132d1d3e2041d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781105"
---
# <a name="serialization"></a>Serialization
이 항목에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] serialization 기능에 대해 설명 합니다. 디자인 타임에 코드 생성 도중 serialization을 추가하는 방법과 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 클래스의 런타임 serialization 동작에 대한 정보가 제공됩니다.  
  
 다음 방법 중 하나로 디자인 타임에 serialization 코드를 추가할 수 있습니다.  
  
- 개체 관계형 디자이너에서 **Serialization 모드** 속성을 **단방향**으로 변경 합니다.  
  
- SQLMetal 명령줄에서 **/serialization** 옵션을 추가 합니다. 자세한 내용은 [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)를 참조하세요.  
  
## <a name="overview"></a>개요  
 에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 생성 된 코드는 기본적으로 지연 로드 기능을 제공 합니다. 지연된 로드를 사용하면 중간 계층에서 매우 편리하게 데이터를 필요한 때 투명하게 로드할 수 있습니다. 그러나 지연된 로드를 원하는지 여부에 상관없이 serializer가 지연된 로드를 트리거하기 때문에 이것은 serialization에서 문제가 됩니다. 실제로 개체가 serialize될 때 모든 지연 로드된 아웃바운드 참조 아래의 전이적 닫기가 serialize됩니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] serialization 기능은 주로 다음과 같은 두 개의 메커니즘을 통해 이 문제를 해결합니다.  
  
- 지연된 로드를 해제하기 위한 <xref:System.Data.Linq.DataContext> 모드(<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>). 자세한 내용은 <xref:System.Data.Linq.DataContext>을 참조하세요.  
  
- 생성된 엔터티에서 <xref:System.Runtime.Serialization.DataContractAttribute?displayProperty=nameWithType> 및 <xref:System.Runtime.Serialization.DataMemberAttribute?displayProperty=nameWithType> 특성을 생성하기 위한 코드 생성 스위치. serialization 아래의 지연 로드 클래스 동작을 비롯한 이 개념이 이 항목의 주제입니다.  
  
### <a name="definitions"></a>정의  
  
- *DataContract serializer*: .NET Framework 3.0 이상 버전의 WCF (Windows Communication Framework) 구성 요소에서 사용 하는 기본 serializer입니다.  
  
- *단방향 serialization*: 순환을 방지 하기 위해 단방향 연결 속성만 포함 하는 클래스의 serialize 된 버전입니다. 규칙에 따라 기본 및 외래 키 관계의 부모 쪽에 대한 속성이 serialization용으로 표시됩니다. 양방향 연결의 다른 쪽은 serialize되지 않습니다.  
  
     단방향 serialization은 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 지원되는 유일한 serialization 형식입니다.  
  
## <a name="code-example"></a>코드 예  
 다음 코드에서는 Northwind 샘플 데이터베이스의 일반 `Customer` 및 `Order` 클래스를 사용하고 이러한 클래스가 serialization 특성으로 데코레이팅되는 방법을 보여 줍니다.  
  
 [!code-csharp[DLinqSerialization#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#1)]
 [!code-vb[DLinqSerialization#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#1)]  
  
 [!code-csharp[DLinqSerialization#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#2)]
 [!code-vb[DLinqSerialization#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#2)]  
  
 [!code-csharp[DLinqSerialization#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#3)]
 [!code-vb[DLinqSerialization#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#3)]  
  
 다음 예제의 `Order` 클래스에서는 간단한 설명을 위해 `Customer` 클래스에 해당하는 역방향 연결 속성만 표시됩니다. 순환을 방지하기 위해 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성이 없습니다.  
  
 [!code-csharp[DLinqSerialization#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#4)]
 [!code-vb[DLinqSerialization#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#4)]  
  
 [!code-csharp[DLinqSerialization#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#5)]
 [!code-vb[DLinqSerialization#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#5)]  
  
### <a name="how-to-serialize-the-entities"></a>엔터티를 Serialize하는 방법  
 다음과 같이 앞 단원에 나온 코드의 엔터티를 serialize할 수 있습니다.  
  
 [!code-csharp[DLinqSerialization#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/Program.cs#6)]
 [!code-vb[DLinqSerialization#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/Module1.vb#6)]  
  
### <a name="self-recursive-relationships"></a>자체 재귀적 관계  
 자체 재귀적 관계는 동일한 패턴을 따릅니다. 외래 키에 해당하는 연결 속성에는 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성이 없지만 부모 속성에는 이 특성이 있습니다.  
  
 두 개의 자체 재귀 관계가 있는 다음 클래스를 살펴보세요. 직원. 관리자/보고서 및 직원. 전문가/Mentees.  
  
 [!code-csharp[DLinqSerialization#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSerialization/cs/northwind-ser.cs#7)]
 [!code-vb[DLinqSerialization#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSerialization/vb/northwind-ser.vb#7)]  
  
## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
- [SqlMetal.exe(코드 생성 도구)](../../../../tools/sqlmetal-exe-code-generation-tool.md)
- [방법: 엔터티를 직렬화 가능 하도록 만들기](how-to-make-entities-serializable.md)
