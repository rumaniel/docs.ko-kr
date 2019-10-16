---
title: 네임스페이스 개요(LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 16283322-8238-4918-ab11-802ac6748eb7
ms.openlocfilehash: d5f176a5561b77126ef23af996ab1e4bf51092ad
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68868832"
---
# <a name="namespaces-overview-linq-to-xml"></a>네임스페이스 개요(LINQ to XML)

이 문서에서는 네임스페이스, <xref:System.Xml.Linq.XName> 클래스 및 <xref:System.Xml.Linq.XNamespace> 클래스에 대해 소개합니다.

## <a name="xml-names"></a>XML 이름

XML 이름으로 인해 XML 프로그래밍이 복잡해지는 경우가 많습니다. XML 이름은 XML 네임스페이스(또는 XML 네임스페이스 URI라고 함)와 로컬 이름으로 구성되어 있습니다. XML 네임스페이스는 .NET Framework 기반 프로그램의 네임스페이스와 유사합니다. XML 네임스페이스를 통해 요소와 특성의 이름을 고유하게 정규화할 수 있습니다. 이에 따라 XML 문서의 다양한 부분 간에 이름 충돌이 방지됩니다. XML 네임스페이스를 선언한 경우 해당 네임스페이스에서만 고유해야 하는 로컬 이름을 선택할 수 있습니다.

XML 이름의 또 다른 측면은 XML *네임스페이스 접두사*입니다. XML 접두사는 XML 이름이 복잡해지는 주된 원인입니다. 이러한 접두사를 통해 XML 네임스페이스의 바로 가기를 만들 수 있으며 이에 따라 XML 문서가 간결하고 이해하기 쉬워집니다. 그러나 XML 접두사는 의미를 갖기 위해 컨텍스트에 의존하므로 복잡성이 가중됩니다. 예를 들어, XML 접두사 `aw`를 XML 트리의 한 부분에 있는 한 XML 네임스페이스와 연결하고 XML 트리의 다른 부분에 있는 다른 XML 네임스페이스와 연결할 수 있습니다.

C#과 함께 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]을 사용하는 경우의 이점 중 하나는 XML 접두사를 사용할 필요가 없다는 것입니다. [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 XML 문서를 로드하고 구문을 분석할 때 각 XML 접두사는 해당하는 XML 네임스페이스로 확인됩니다. 그 후 네임스페이스를 사용하는 문서로 작업할 때는 네임스페이스 접두사를 통해서가 아니라 거의 항상 네임스페이스 URI를 통해 네임스페이스에 액세스합니다. 개발자는 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 XML 이름으로 작업할 때 항상 정규화된 XML 이름(즉, XML 네임스페이스 및 로컬 이름)으로 작업합니다. 그러나 필요한 경우 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 네임스페이스 접두사로 작업하고 네임스페이스 접두사를 제어할 수 있습니다.

[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]에서 XML 이름을 나타내는 클래스는 <xref:System.Xml.Linq.XName>입니다. XML 이름은 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] API 전반에서 자주 나타나며, XML 이름이 필요할 때마다 <xref:System.Xml.Linq.XName> 매개 변수를 찾을 수 있습니다. 그러나 <xref:System.Xml.Linq.XName>으로 직접 작업하는 경우는 드뭅니다. <xref:System.Xml.Linq.XName>에는 문자열에서의 암시적 변환이 포함되어 있습니다.

자세한 내용은 <xref:System.Xml.Linq.XNamespace> 및 <xref:System.Xml.Linq.XName>를 참조하세요.
