---
title: 데이터 집합 쿼리(LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: bb68d2e4-623d-4d60-85e3-965254f6fee7
ms.openlocfilehash: 79a9b320fbdbfecc3f7d531d992b1529873871a5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783042"
---
# <a name="querying-datasets-linq-to-dataset"></a>데이터 집합 쿼리(LINQ to DataSet)
<xref:System.Data.DataSet> 개체에 데이터가 채워지면 개체에 대한 쿼리를 시작할 수 있습니다. LINQ to DataSet 사용 하 여 쿼리를 작성 하 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 는 것 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]은 다른 사용 데이터 소스에 대해를 사용 하는 것과 비슷합니다 그러나 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 쿼리를 <xref:System.Data.DataSet> 개체에 사용할 경우 사용자 지정 형식의 열거형 대신 <xref:System.Data.DataRow> 개체의 열거형을 쿼리하게 됩니다. 즉, <xref:System.Data.DataRow> 쿼리에서는 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 클래스의 모든 멤버를 사용할 수 있으므로 다양한 기능의 복잡한 쿼리를 만들 수 있습니다.  
  
 의 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]다른 구현과 마찬가지로 쿼리 식 구문과 메서드 기반 쿼리 구문 이라는 두 가지 형식으로 LINQ to DataSet 쿼리를 만들 수 있습니다. 쿼리 식 구문 또는 메서드 기반 쿼리 구문을 사용하여 <xref:System.Data.DataSet>의 단일 테이블, <xref:System.Data.DataSet>의 여러 테이블 또는 형식화된 <xref:System.Data.DataSet>의 테이블에 대해 쿼리를 수행할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [단일 테이블 쿼리](single-table-queries-linq-to-dataset.md)  
 단일 테이블 쿼리를 수행하는 방법을 설명합니다.  
  
 [크로스 테이블 쿼리](cross-table-queries-linq-to-dataset.md)  
 크로스 테이블 쿼리를 수행하는 방법을 설명합니다.  
  
 [형식화된 데이터 집합 쿼리](querying-typed-datasets.md)  
 형식화된 <xref:System.Data.DataSet> 개체를 쿼리하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to DataSet 예제](linq-to-dataset-examples.md)
- [데이터를 데이터 세트에 로드](loading-data-into-a-dataset.md)
