---
title: LINQ to DataSet
ms.date: 03/30/2017
ms.assetid: 743e3755-3ecb-45a2-8d9b-9ed41f0dcf17
ms.openlocfilehash: 4995512336ee9eb6e33df011757ed533db57e76e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783793"
---
# <a name="linq-to-dataset"></a>LINQ to DataSet
LINQ to DataSet를 사용 하면 <xref:System.Data.DataSet> 개체에 캐시 된 데이터를 보다 쉽고 빠르게 쿼리할 수 있습니다. 특히 LINQ to DataSet는 개발자가 별도의 쿼리 언어를 사용 하는 대신 프로그래밍 언어 자체에서 쿼리를 작성할 수 있도록 하 여 쿼리를 단순화 합니다. 이러한 기능은 visual studio 개발자에 게 특히 유용 합니다 .이는 이제 visual Studio에서 제공 하는 컴파일 시간 구문 검사, 정적 입력 및 IntelliSense 지원을 해당 쿼리에 사용할 수 있습니다.  
  
 LINQ to DataSet를 사용 하 여 하나 이상의 데이터 원본에서 통합 된 데이터를 쿼리할 수도 있습니다. 이 기능은 논리적으로 집계된 데이터 쿼리, 웹 애플리케이션의 중간 계층 캐시 등과 같이 유연하게 데이터를 표현하고 처리해야 하는 여러 시나리오에 사용될 수 있습니다. 이러한 조작 방법은 일반적인 보고, 분석 및 비즈니스 인텔리전스 애플리케이션에 특히 필요합니다.  
  
 LINQ to DataSet 기능은 주로 <xref:System.Data.DataRowExtensions> 및 <xref:System.Data.DataTableExtensions> 클래스의 확장 메서드를 통해 노출 됩니다. LINQ to DataSet는 기존 ADO.NET 아키텍처를 기반으로 하며 응용 프로그램 코드에서 ADO.NET를 대체 하지 않습니다. 기존 ADO.NET 코드는 LINQ to DataSet 응용 프로그램에서 계속 작동 합니다. ADO.NET와 데이터 저장소에 대 한 LINQ to DataSet의 관계는 다음 다이어그램에 나와 있습니다.  
  
 ![ADO.NET 공급자를 기반으로 LINQ to DataSet 있음을 보여 주는 다이어그램](./media/linq-to-dataset/linq-dataset-ado-dotnet-provider.gif)  
  
## <a name="in-this-section"></a>섹션 내용  
 [시작](getting-started-linq-to-dataset.md)  
  
 [프로그래밍 가이드](programming-guide-linq-to-dataset.md)  
  
## <a name="reference"></a>참조  
 <xref:System.Data.DataTableExtensions>  
  
 <xref:System.Data.DataRowExtensions>  
  
 <xref:System.Data.DataRowComparer>  
  
## <a name="see-also"></a>참고자료

- [LINQ(Language-Integrated Query) - C#](../../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ(Language-Integrated Query) - Visual Basic](../../../visual-basic/programming-guide/concepts/linq/index.md)
- [LINQ 및 ADO.NET](linq-and-ado-net.md)
- [ADO.NET](index.md)
