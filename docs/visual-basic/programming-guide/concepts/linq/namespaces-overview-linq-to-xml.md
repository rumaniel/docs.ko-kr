---
title: 네임스페이스 개요(LINQ to XML)
ms.date: 07/20/2015
ms.assetid: b8eb31fa-4b26-4acf-8050-6e705687f458
ms.openlocfilehash: bd83a423c8fd19506c5d23ea308bb56cced6ca93
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68710546"
---
# <a name="namespaces-overview-linq-to-xml"></a>네임스페이스 개요(LINQ to XML)

이 항목에서는 네임스페이스, <xref:System.Xml.Linq.XName> 클래스 및 <xref:System.Xml.Linq.XNamespace> 클래스에 대해 소개합니다.  
  
## <a name="xml-names"></a>XML 이름  

XML 이름으로 인해 XML 프로그래밍이 복잡해지는 경우가 많습니다. XML 이름은 XML 네임스페이스(또는 XML 네임스페이스 URI라고 함)와 로컬 이름으로 구성되어 있습니다. XML 네임스페이스는 .NET Framework 기반 프로그램의 네임스페이스와 유사합니다. XML 네임스페이스를 통해 요소와 특성의 이름을 고유하게 정규화할 수 있습니다. 이에 따라 XML 문서의 다양한 부분 간에 이름 충돌이 방지됩니다. XML 네임스페이스를 선언한 경우 해당 네임스페이스에서만 고유해야 하는 로컬 이름을 선택할 수 있습니다.  
  
 XML 이름의 또 다른 측면은 XML *네임스페이스 접두사*입니다. XML 접두사는 XML 이름이 복잡해지는 주된 원인입니다. 이러한 접두사를 통해 XML 네임스페이스의 바로 가기를 만들 수 있으며 이에 따라 XML 문서가 간결하고 이해하기 쉬워집니다. 그러나 XML 접두사는 의미를 갖기 위해 컨텍스트에 의존하므로 복잡성이 가중됩니다. 예를 들어, XML 접두사 `aw`를 XML 트리의 한 부분에 있는 한 XML 네임스페이스와 연결하고 XML 트리의 다른 부분에 있는 다른 XML 네임스페이스와 연결할 수 있습니다.  
  
Visual Basic 및 XML 리터럴과 함께 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하는 경우 네임스페이스의 문서로 작업할 때 네임스페이스 접두사를 사용해야 합니다.  
  
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 XML 이름을 나타내는 클래스는 <xref:System.Xml.Linq.XName>입니다. XML 이름은 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] API 전반에서 자주 나타나며, XML 이름이 필요할 때마다 <xref:System.Xml.Linq.XName> 매개 변수를 찾을 수 있습니다. 그러나 <xref:System.Xml.Linq.XName>으로 직접 작업하는 경우는 드뭅니다. <xref:System.Xml.Linq.XName>에는 문자열에서의 암시적 변환이 포함되어 있습니다.  
  
자세한 내용은 <xref:System.Xml.Linq.XNamespace> 및 <xref:System.Xml.Linq.XName>를 참조하세요.
