---
title: LINQ 쿼리에 대한 데이터 소스 활성화
ms.date: 07/20/2015
ms.assetid: d2ef04a5-31a6-45cb-af9a-a5ce7732662c
ms.openlocfilehash: f7511b051577d94bb3d422e87699efdcff4058e1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594600"
---
# <a name="enabling-a-data-source-for-linq-querying"></a>LINQ 쿼리에 대한 데이터 소스 활성화
다양한 방법으로 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]를 확장하여 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 패턴에서 원하는 데이터 소스를 쿼리할 수 있습니다. 데이터 소스의 예를 몇 가지 들자면 데이터 구조, 웹 서비스, 파일 시스템 또는 데이터베이스가 있습니다. 쿼리의 구문과 패턴은 변경되지 않으므로 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 패턴을 사용하면 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리가 활성화된 데이터 소스를 클라이언트가 쉽게 쿼리할 수 있습니다. 다음은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]를 다양한 데이터 소스로 확장할 수 있는 방법입니다.  
  
- 특정 형식에 이 형식의 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] to Objects 쿼리를 활성화하는 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스 구현  
  
- 형식을 확장하는 <xref:System.Linq.Enumerable.Where%2A> 및 <xref:System.Linq.Enumerable.Select%2A> 같은 표준 쿼리 연산자 메서드를 만들어 해당 형식의 사용자 지정 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 활성화  
  
- <xref:System.Linq.IQueryable%601> 인터페이스를 구현하는 데이터 소스에 대한 공급자 만들기. 이 인터페이스를 구현하는 공급자는 원격 실행과 같이 사용자 지정 방식으로 실행할 수 있는 식 트리의 형태로 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 받습니다.  
  
- 기존 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 기술을 이용하는 데이터 소스에 대한 공급자 만들기. 이러한 공급자를 사용하면 쿼리뿐만 아니라 사용자 정의 형식에 대한 삽입, 업데이트 및 삭제 작업과 매핑을 수행할 수 있습니다.  
  
 이 항목에서는 이러한 옵션에 대해 설명합니다.  
  
## <a name="how-to-enable-linq-querying-of-your-data-source"></a>데이터 소스의 LINQ 쿼리를 활성화하는 방법  
  
### <a name="in-memory-data"></a>메모리 내 데이터  
 메모리 내 데이터의 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 활성화하는 방법에는 두 가지가 있습니다. 데이터가 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 형식이라면 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] to Objects를 사용하여 데이터를 쿼리할 수 있습니다. 하지만 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 구현하여 형식의 열거형을 활성화하는 것이 바람직하지 않다면 해당 형식에서 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 표준 쿼리 연산자 메서드를 정의하거나 해당 형식을 확장하는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 표준 쿼리 연산자 메서드를 만들 수 있습니다. 표준 쿼리 연산자의 사용자 지정 구현에서는 지연된 실행을 사용하여 결과를 반환해야 합니다.  
  
### <a name="remote-data"></a>원격 데이터  
 원격 데이터 소스의 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 활성화하는 가장 좋은 방법은 <xref:System.Linq.IQueryable%601> 인터페이스를 구현하는 것입니다. 하지만 이 방식은 데이터 소스에서 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 같은 공급자를 확장하는 방식과 다릅니다. [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]과 같은 기존 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 기술을 Visual Studio 2008에서 사용할 수 있는 다른 데이터 소스 형식으로 확장하는 공급자 모델은 없습니다.
  
## <a name="iqueryable-linq-providers"></a>IQueryable LINQ 공급자  
 <xref:System.Linq.IQueryable%601>을 구현하는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자의 복잡성은 경우에 따라 크게 다릅니다. 이 단원에서는 이러한 복잡성의 차이에 대해 설명합니다.  
  
 덜 복잡한 `IQueryable` 공급자는 웹 서비스의 단일 메서드와 인터페이스할 수도 있습니다. 이러한 형식의 공급자는 쿼리에 처리할 특정 정보가 있다고 가정하므로 매우 한정적이며, 대개 단일 결과 형식을 노출하는 폐쇄형 형식 시스템을 갖고 있습니다. 대부분의 쿼리 실행은 로컬에서 수행됩니다. 예를 들어 표준 쿼리 연산자의 <xref:System.Linq.Enumerable> 구현을 사용하여 실행됩니다. 복잡성이 낮은 공급자는 식 트리에서 쿼리를 나타내는 하나의 메서드 호출 식만 검사하고 쿼리의 나머지 논리는 다른 곳에서 처리되도록 할 수 있습니다.  
  
 복잡성이 보통인 `IQueryable` 공급자는 부분적으로 표현되는 쿼리 언어가 있는 데이터 소스를 대상으로 할 수 있습니다. 공급자가 웹 서비스를 대상으로 하는 경우 둘 이상의 웹 서비스 메서드에 대한 인터페이스를 제공하고 쿼리가 노출하는 질문에 따라 호출할 메서드를 선택할 수 있습니다. 복잡성이 보통인 공급자는 복잡성이 낮은 공급자보다 풍부한 형식 시스템을 가질 수 있지만 여전히 고정된 형식 시스템을 유지합니다. 예를 들어 이 공급자는 이동 가능한 일대다 관계가 있는 형식을 노출할 수 있지만 사용자 정의 형식에 대한 매핑 기술을 제공하지 않습니다.  
  
 `IQueryable` 공급자와 같은 복잡한 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 공급자가 전체 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 SQL과 같이 표현이 가능한 쿼리 언어로 변환할 수 있습니다. 복잡한 공급자가 덜 복잡한 공급자보다 더욱 다양하고 방대한 질문을 쿼리로 처리할 수 있기 때문에 더 일반적이라 할 수 있습니다. 또한 개방형 형식 시스템을 가지므로 사용자 정의 형식을 매핑하는 확장 인프라를 포함해야 합니다. 복잡성이 높은 공급자를 개발하려면 상당한 노력이 필요합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq.IQueryable%601>
- <xref:System.Collections.Generic.IEnumerable%601>
- <xref:System.Linq.Enumerable>
- [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)
- [LINQ to Objects(C#)](./linq-to-objects.md)
