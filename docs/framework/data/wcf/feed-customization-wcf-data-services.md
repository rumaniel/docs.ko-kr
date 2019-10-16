---
title: 피드 사용자 지정(WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, feeds
- WCF Data Services, Atom protocol
- Atom Publishing Protocol [WCF Data Services]
- WCF Data Services, customizing feeds
ms.assetid: 0d1a39bc-6462-4683-bd7d-e74e0fd28a85
ms.openlocfilehash: 17d54210d7abc16fe91fa94f39a8f85eac866088
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854191"
---
# <a name="feed-customization-wcf-data-services"></a>피드 사용자 지정(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 를 사용 하 여 데이터를 피드로 노출 합니다. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]는 데이터 피드에 대해 Atom 및 JavaScript Object Notation (JSON) 형식을 모두 지원 합니다. Atom 피드를 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 사용 하는 경우는 엔터티 및 관계와 같은 데이터를 HTTP 메시지의 본문에 포함할 수 있는 XML 형식으로 serialize 하는 표준 메서드를 제공 합니다. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]엔터티와 Atom 요소에 포함 된 데이터 간의 기본 엔터티 속성 매핑을 정의 합니다. 자세한 내용은 [OData: Atom 형식](https://go.microsoft.com/fwlink/?LinkID=185794)입니다.  
  
 데이터 서비스에서 반환된 속성 데이터를 표준 피드 형식이 아니라 사용자 지정 방식으로 serialize(직렬화)해야 하는 애플리케이션 시나리오가 있을 수도 있습니다. 를 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]사용 하면 엔터티의 속성이 사용 되지 않는 요소 및 항목의 특성이 나 피드의 항목의 사용자 지정 요소에 매핑될 수 있도록 데이터 피드의 serialization을 사용자 지정할 수 있습니다.  
  
> [!NOTE]
> 피드 사용자 지정은 Atom 피드에만 지원됩니다. 반환된 피드에 대해 JSON 형식이 요청되는 경우에는 사용자 지정 피드가 반환되지 않습니다.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 수동으로 데이터 모델의 엔터티 형식에 특성을 적용하여 Atom 페이로드에 대한 대체 엔터티 속성 매핑을 정의할 수 있습니다. 데이터 서비스의 데이터 소스 공급자가 이러한 특성의 적용 방법을 결정합니다.  
  
> [!IMPORTANT]
> 사용자 지정 피드를 정의하는 경우 사용자 지정 매핑이 정의되어 있는 모든 엔터티 속성이 프로젝션에 포함되도록 해야 합니다. 매핑된 엔터티 속성이 프로젝션에 포함되지 않는 경우 데이터가 손실될 수 있습니다. 자세한 내용은 [쿼리 프로젝션](query-projections-wcf-data-services.md)을 참조 하세요.  
  
## <a name="customizing-feeds-with-the-entity-framework-provider"></a>Entity Framework 공급자를 사용하여 피드 사용자 지정  
 Entity Framework 공급자와 함께 사용된 데이터 모델은 .edmx 파일에 XML로 표시됩니다. 이 경우 사용자 지정 피드를 정의하는 특성은 데이터 모델의 엔터티 형식과 속성을 나타내는 `EntityType` 및 `Property` 요소에 추가됩니다. 이러한 피드 사용자 지정 특성은 MC- [CSDL\]에서 \[정의 되지 않습니다. Entity Framework 공급자가 데이터 모델](https://go.microsoft.com/fwlink/?LinkId=159072)을 정의 하는 데 사용 하는 형식인 개념 스키마 정의 파일 형식입니다. 따라서 `m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"`에 정의된 특정 스키마 네임스페이스에 피드 사용자 지정 특성을 선언해야 합니다. 다음 XML 조각은 `Property`, `Products` 및 `ProductName` 속성을 정의하는 `ReorderLevel` 엔터티 형식의 `UnitsInStock` 요소에 적용되는 피드 사용자 지정 특성을 보여 줍니다.  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedAttributes](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/northwind.csdl#edmfeedattributes)]  
  
 이러한 특성은 `Products` 엔터티 집합에 대해 다음 사용자 지정 데이터 피드를 생성합니다. 사용자 지정 데이터 피드에서 `ProductName` 속성 값은 `author` 요소와 `ProductName` 속성 요소에 모두 표시되고, `UnitsInStock` 속성은 고유한 네임스페이스와 특성으로 `ReorderLevel` 속성을 사용하여 사용자 지정 요소에 표시됩니다.  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResultProduct](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/edmfeedresult.xml#edmfeedresultproduct)]  
  
 자세한 내용은 [방법: Entity Framework 공급자](how-to-customize-feeds-with-ef-provider-wcf-data-services.md)를 사용 하 여 피드를 사용자 지정 합니다.  
  
> [!NOTE]
> Entity Designer에서 데이터 모델 확장을 지원하지 않으므로 데이터 모델이 포함된 XML 파일을 수동으로 수정해야 합니다. 엔터티 데이터 모델 도구에 의해 생성 되는 .edmx 파일에 대 한 자세한 내용은 [.Edmx 파일 개요 (Entity Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))를 참조 하세요.  
  
### <a name="custom-feed-attributes"></a>사용자 지정 피드 특성  
 다음 표에서는 데이터 모델을 정의하는 CSDL(개념 스키마 정의 언어)에 추가할 수 있는 피드를 사용자 지정하는 XML 특성을 보여 줍니다. 이러한 특성은 리플렉션 공급자와 함께 사용되는 <xref:System.Data.Services.Common.EntityPropertyMappingAttribute>의 속성과 같습니다.  
  
|특성 이름|설명|  
|--------------------|-----------------|  
|`FC_ContentKind`|콘텐츠의 형식을 나타냅니다. 다음 키워드는 배포 콘텐츠 형식을 정의합니다.<br /><br /> `text:`속성 값은 피드에 텍스트로 표시 됩니다.<br /><br /> `html:`속성 값은 피드에 HTML로 표시 됩니다.<br /><br /> `xhtml:`속성 값은 피드의 XML 형식 HTML로 표시 됩니다.<br /><br /> 이러한 키워드는 리플렉션 공급자와 함께 사용되는 <xref:System.Data.Services.Common.SyndicationTextContentKind> 열거 값과 같습니다.<br /><br /> `FC_NsPrefix` 및 `FC_NsUri` 특성을 사용하는 경우 이 특성은 지원되지 않습니다.<br /><br /> `xhtml` 특성의 `FC_ContentKind` 값을 지정하는 경우 속성 값에 올바른 형식의 XML이 포함되도록 해야 합니다. 데이터 서비스는 변환을 수행하지 않고 값을 반환합니다. 반환된 XML의 모든 XML 요소 접두사에 매핑된 피드에 정의된 네임스페이스 URI 및 접두사가 있는지도 확인해야 합니다.|  
|`FC_KeepInContent`|참조된 속성 값이 피드의 콘텐츠 섹션과 매핑 대상 위치에 모두 포함되어야 함을 나타냅니다. 유효한 값은 `true` 및 `false`입니다. 결과 피드가 이전 버전의 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]와 호환 되도록 하려면 값을 `true` 지정 하 여 피드의 콘텐츠 섹션에 값이 포함 되어 있는지 확인 합니다.|  
|`FC_NsPrefix`|배포 이외의 매핑에서 XML 요소의 네임스페이스 접두사입니다. 이 특성은 `FC_NsUri` 특성과 함께 사용해야 하며, `FC_ContentKind` 특성과 함께 사용할 수는 없습니다.|  
|`FC_NsUri`|배포 이외의 매핑에서 XML 요소의 네임스페이스 URI입니다. 이 특성은 `FC_NsPrefix` 특성과 함께 사용해야 하며, `FC_ContentKind` 특성과 함께 사용할 수는 없습니다.|  
|`FC_SourcePath`|이 피드 매핑 규칙이 적용되는 엔터티의 속성 경로입니다. 이 특성은 `EntityType` 요소와 함께 사용하는 경우에만 지원됩니다.<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> 속성은 복합 형식을 직접 참조할 수 없습니다. 복합 형식의 경우 속성 이름이 백슬래시(`/`) 문자로 구분되는 경로 식을 사용해야 합니다. 예를 들어 정수 속성 `Person` `Age` 및 복합 속성이 있는 엔터티 형식에는 다음 값을 사용할 수 있습니다.<br /><br /> `Address`:<br /><br /> `Age`<br /><br /> `Address/Street`<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A> 속성은 공백이나 속성 이름에 사용할 수 없는 다른 문자가 포함된 값으로 설정할 수 없습니다.|  
|`FC_TargetPath`|속성을 매핑할 결과 피드의 대상 요소 이름입니다. 이 요소는 Atom 사양에 정의된 요소나 사용자 지정 요소일 수 있습니다.<br /><br /> 다음 키워드는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드의 특정 위치를 가리키는 미리 정의된 배포 대상 경로 값입니다.<br /><br /> `SyndicationAuthorEmail:``atom:author` 요소의 `atom:email` 자식 요소입니다.<br /><br /> `SyndicationAuthorName:``atom:author` 요소의 `atom:name` 자식 요소입니다.<br /><br /> `SyndicationAuthorUri:``atom:author` 요소의 `atom:uri` 자식 요소입니다.<br /><br /> `SyndicationContributorEmail:``atom:contributor` 요소의 `atom:email` 자식 요소입니다.<br /><br /> `SyndicationContributorName:``atom:contributor` 요소의 `atom:name` 자식 요소입니다.<br /><br /> `SyndicationContributorUri:``atom:contributor` 요소의 `atom:uri` 자식 요소입니다.<br /><br /> `SyndicationCustomProperty:`사용자 지정 속성 요소입니다. 사용자 지정 요소에 매핑되는 경우 대상은 중첩된 요소가 백슬래시(`/`)로 구분되고 특성이 앰퍼샌드(`@`)로 지정되는 경로 식이어야 합니다. 다음 예제에서 `UnitsInStock/@ReorderLevel` 문자열은 루트 항목 요소의 자식 요소 `ReorderLevel`에 대한 `UnitsInStock` 특성에 속성 값을 매핑합니다.<br /><br /> `<Property Name="ReorderLevel" Type="Int16"               m:FC_TargetPath="UnitsInStock/@ReorderLevel"               m:FC_NsPrefix="Northwind"               m:FC_NsUri="http://schemas.examples.microsoft.com/dataservices"               m:FC_KeepInContent="false"               />`<br /><br /> 대상이 사용자 지정 요소 이름인 경우 `FC_NsPrefix` 및 `FC_NsUri` 특성도 지정해야 합니다.<br /><br /> `SyndicationPublished:``atom:published` 요소입니다.<br /><br /> `SyndicationRights:``atom:rights` 요소입니다.<br /><br /> `SyndicationSummary:``atom:summary` 요소입니다.<br /><br /> `SyndicationTitle:``atom:title` 요소입니다.<br /><br /> `SyndicationUpdated:``atom:updated` 요소입니다.<br /><br /> 이러한 키워드는 리플렉션 공급자와 함께 사용되는 <xref:System.Data.Services.Common.SyndicationItemProperty> 열거 값과 같습니다.|  
  
> [!NOTE]
> 특성 이름과 값은 대/소문자를 구분합니다. `EntityType` 요소나 하나 이상의 `Property` 요소에 특성을 적용할 수 있지만 둘 다에 적용할 수는 없습니다.  
  
## <a name="customizing-feeds-with-the-reflection-provider"></a>리플렉션 공급자를 사용하여 피드 사용자 지정  
 리플렉션 공급자를 사용하여 구현된 데이터 모델의 피드를 사용자 지정하려면 데이터 모델의 엔터티 형식을 나타내는 클래스에 <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> 특성 인스턴스를 하나 이상 추가합니다. <xref:System.Data.Services.Common.EntityPropertyMappingAttribute> 클래스의 속성은 위 단원에 설명된 피드 사용자 지정 특성에 해당합니다. 다음은 두 속성에 모두 사용자 지정 피드 매핑을 정의하는 `Order` 형식의 선언 예제입니다.  
  
> [!NOTE]
> 이 예제의 [데이터 모델은 방법: 리플렉션 공급자](create-a-data-service-using-rp-wcf-data-services.md)를 사용 하 여 데이터 서비스를 만듭니다.  
  
 [!code-csharp[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_custom_feeds/cs/orderitems.svc.cs#customorderfeed)]
 [!code-vb[Astoria Custom Feeds#CustomOrderFeed](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_custom_feeds/vb/orderitems.svc.vb#customorderfeed)]  
  
 이러한 특성은 `Orders` 엔터티 집합에 대해 다음 사용자 지정 데이터 피드를 생성합니다. 이 사용자 지정 피드에서 속성 값 `OrderId` 은의 `author` `entry` `title` 요소에만 표시 되 고, 속성 값 `Customer` 은 요소와 `Customer` 속성 요소에 모두 표시 됩니다.  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/iqueryablefeedresult.xml#iqueryablefeedresult)]  
  
 자세한 내용은 [방법: 리플렉션 공급자](how-to-customize-feeds-with-the-reflection-provider-wcf-data-services.md)를 사용 하 여 피드를 사용자 지정 합니다.  
  
## <a name="customizing-feeds-with-a-custom-data-service-provider"></a>사용자 지정 데이터 서비스 공급자를 사용하여 피드 사용자 지정  
 사용자 지정 데이터 서비스 공급자를 사용하여 정의된 데이터 모델의 피드 사용자 지정은 데이터 모델의 엔터티 형식을 나타내는 <xref:System.Data.Services.Providers.ResourceType.AddEntityPropertyMappingAttribute%2A>의 <xref:System.Data.Services.Providers.ResourceType>를 호출하여 리소스 형식에 대해 정의됩니다. 자세한 내용은 [사용자 지정 데이터 서비스 공급자](custom-data-service-providers-wcf-data-services.md)를 참조 하세요.  
  
## <a name="consuming-custom-feeds"></a>사용자 지정 피드 사용  
 응용 프로그램에서 직접 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 피드를 사용 하는 경우 반환 된 피드의 사용자 지정 된 요소와 특성을 처리할 수 있어야 합니다. 데이터 서비스 공급자에 관계없이 데이터 모델에 사용자 지정 피드를 구현한 경우 `$metadata` 엔드포인트는 사용자 지정 피드 정보를 데이터 서비스에서 반환된 CSDL에 사용자 지정 피드 특성으로 반환합니다. **서비스 참조 추가** 대화 상자 또는 [datasvcutil.exe](wcf-data-service-client-utility-datasvcutil-exe.md) 도구를 사용 하 여 클라이언트 데이터 서비스 클래스를 생성 하는 경우 사용자 지정 된 피드 특성은 데이터 서비스에 대 한 요청 및 응답이 올바르게 처리 되도록 보장 하는 데 사용 됩니다.  
  
## <a name="feed-customization-considerations"></a>피드 사용자 지정 고려 사항  
 사용자 지정 피드 매핑을 정의할 때는 다음을 고려해야 합니다.  
  
- 클라이언트 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 는 공백만 포함 하는 경우 피드의 매핑된 요소를 비어 있는 것으로 처리 합니다. 이로 인해 공백만 포함 하는 매핑된 요소는 동일한 공백이 있는 클라이언트에서 구체화 되지 않습니다. 클라이언트에서이 공백을 유지 하려면 피드 매핑 특성에서 값 `KeepInContext` 을로 `true` 설정 해야 합니다.  
  
## <a name="versioning-requirements"></a>버전 관리 요구 사항  
 피드 사용자 지정에 대한 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜 버전 관리 요구 사항은 다음과 같습니다.  
  
- 피드를 사용자 지정하는 경우 클라이언트와 데이터 서비스가 모두 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 프로토콜 버전 2.0 이상을 지원해야 합니다.  
  
 자세한 내용은 [데이터 서비스 버전 관리](data-service-versioning-wcf-data-services.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [리플렉션 공급자](reflection-provider-wcf-data-services.md)
- [Entity Framework 공급자](entity-framework-provider-wcf-data-services.md)
