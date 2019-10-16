---
title: '방법: WCF Data Services (Entity Framework 공급자)를 사용 하 여 피드 사용자 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, customizing feeds
ms.assetid: fd16272e-36f2-415e-850e-8a81f2b17525
ms.openlocfilehash: 8f994065ea42d6fc522fa297cafa8c46a8164e67
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780157"
---
# <a name="how-to-customize-feeds-with-the-entity-framework-provider-wcf-data-services"></a>방법: WCF Data Services (Entity Framework 공급자)를 사용 하 여 피드 사용자 지정
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 엔터티의 속성이 AtomPub 프로토콜에 정의된 사용하지 않은 요소에 매핑될 수 있도록 데이터 서비스 응답의 Atom serialization을 사용자 지정할 수 있습니다. 이 항목에서는 Entity Framework 공급자를 사용하여 .edmx 파일에 정의된 데이터 모델의 엔터티 형식에 대한 매핑 특성을 정의하는 방법을 보여 줍니다. 자세한 내용은 [사용자 지정 피드](feed-customization-wcf-data-services.md)합니다.  
  
 이 항목에서는 데이터 모델이 포함되어 있고 도구에서 생성된 .edmx 파일을 수동으로 수정합니다. Entity Designer에서 데이터 모델 확장을 지원하지 않으므로 파일을 수동으로 수정해야 합니다. 엔터티 데이터 모델 도구에서 생성 하는 .edmx 파일에 대 한 자세한 내용은 [.Edmx 파일 개요 (Entity Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))를 참조 하세요. 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
### <a name="to-manually-modify-the-northwindedmx-file-to-add-feed-customization-attributes"></a>Northwind.edmx 파일을 수동으로 수정하여 피드 사용자 지정 특성을 추가하려면  
  
1. **솔루션 탐색기**에서 `Northwind.edmx` 파일을 마우스 오른쪽 단추로 클릭 한 다음 **연결 프로그램**을 클릭 합니다.  
  
2. **열기-Northwind .edmx** 대화 상자에서 **XML 편집기**를 선택한 다음 **확인**을 클릭 합니다.  
  
3. `ConceptualModels` 요소를 찾아 기존 `Customers` 엔터티 형식을 피드 사용자 지정 매핑 특성이 포함된 다음 요소로 바꿉니다.  
  
     [!code-xml[Astoria Custom Feeds#EdmFeedCustomers](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedcustomers)]  
  
4. 변경 내용을 저장하고 Northwind.edmx 파일을 닫습니다.  
  
5. 필드 Northwind .edmx 파일을 마우스 오른쪽 단추로 클릭 한 다음 **사용자 지정 도구 실행**을 클릭 합니다.  
  
     이렇게 하면 필요한 개체 계층 파일이 다시 생성됩니다.  
  
6. 프로젝트를 다시 컴파일합니다.  
  
## <a name="example"></a>예제  
 위 예제에서는 URI `http://myservice/Northwind.svc/Customers('ALFKI')`에 대해 다음 결과를 반환합니다.  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresult)]  
  
## <a name="see-also"></a>참고자료

- [Entity Framework 공급자](entity-framework-provider-wcf-data-services.md)
