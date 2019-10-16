---
title: '방법: MetadataExchangeClient를 사용하여 메타데이터 검색'
ms.date: 03/30/2017
ms.assetid: 0754e9dc-13c5-45c2-81b5-f3da466e5a87
ms.openlocfilehash: c9558e1943c3886a61c3b19801e22d57732e459a
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968761"
---
# <a name="how-to-use-metadataexchangeclient-to-retrieve-metadata"></a>방법: MetadataExchangeClient를 사용하여 메타데이터 검색
WS-MetadataExchange(MEX) 프로토콜을 사용하여 메타데이터를 다운로드하려면 <xref:System.ServiceModel.Description.MetadataExchangeClient> 클래스를 사용합니다. 검색된 메타데이터 파일은 <xref:System.ServiceModel.Description.MetadataSet> 개체로 반환됩니다. 반환된 <xref:System.ServiceModel.Description.MetadataSet> 개체에는 <xref:System.ServiceModel.Description.MetadataSection> 개체의 컬렉션이 들어 있으며, 각 개체에는 특정 메타데이터 언어와 식별자가 포함되어 있습니다. 반환된 메타데이터는 파일로 작성할 수 있으며, 반환된 메타데이터에 WSDL(웹 서비스 기술 언어) 문서가 있는 경우에는 <xref:System.ServiceModel.Description.WsdlImporter>를 사용하여 메타데이터를 가져올 수 있습니다.  
  
 주소를 사용하는 <xref:System.ServiceModel.Description.MetadataExchangeClient> 생성자는 주소의 URI(Uniform Resource Identifier) 체계와 일치하는 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 정적 클래스의 바인딩을 사용합니다. 또는 사용할 바인딩을 명시적으로 지정할 수 있도록 하는 <xref:System.ServiceModel.Description.MetadataExchangeClient> 생성자를 사용할 수 있습니다. 지정된 바인딩을 사용하여 모든 메타데이터 참조를 확인할 수 있습니다.  
  
 WCF (다른 Windows Communication Foundation) 클라이언트와 마찬가지로 형식에서는 <xref:System.ServiceModel.Description.MetadataExchangeClient> 끝점 구성 이름을 사용 하 여 클라이언트 끝점 구성을 로드 하기 위한 생성자를 제공 합니다. 지정된 엔드포인트 구성은 <xref:System.ServiceModel.Description.IMetadataExchange> 계약을 지정해야 합니다. 엔드포인트 구성에 있는 주소는 로드되지 않으므로, 주소를 사용하는 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 오버로드 중 하나를 사용해야 합니다. <xref:System.ServiceModel.EndpointAddress> 인스턴스를 사용하여 메타데이터 주소를 지정하면, <xref:System.ServiceModel.Description.MetadataExchangeClient>에서는 해당 주소가 MEX 끝점을 가리키는 것으로 간주합니다. 메타데이터 주소를 URL로 지정하는 경우에는 사용할 <xref:System.ServiceModel.Description.MetadataExchangeClientMode>도 MEX 또는 HTTP GET 중에서 지정해야 합니다.  
  
> [!IMPORTANT]
> 기본적으로 <xref:System.ServiceModel.Description.MetadataExchangeClient>는 WSDL 및 XML 스키마에서 가져오거나 포함하는 모든 참조를 확인합니다. <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 속성을 `false`로 설정하면 이 기능을 사용하지 않도록 할 수 있습니다. 그리고 <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> 속성을 사용하여 확인할 최대 참조 수를 제어할 수 있습니다. 또한 이 속성은 검색되는 메타데이터 양을 제어하기 위해 바인딩의 `MaxReceivedMessageSize` 속성과 함께 사용할 수도 있습니다.  
  
### <a name="to-use-metadataexchangeclient-to-obtain-metadata"></a>MetadataExchangeClient를 사용하여 메타데이터를 가져오려면  
  
1. 바인딩, 엔드포인트 구성 이름 또는 메타데이터의 주소를 명시적으로 지정하여 새로운 <xref:System.ServiceModel.Description.MetadataExchangeClient> 개체를 만듭니다.  
  
2. 필요에 따라 <xref:System.ServiceModel.Description.MetadataExchangeClient>를 구성합니다. 예를 들어 메타데이터 요청 시 사용할 자격 증명을 지정하고, 확인할 메타데이터 참조 방법을 제어하며, 시간 제한을 초과하기 전에 메타데이터 요청 <xref:System.ServiceModel.Description.MetadataExchangeClient.OperationTimeout%2A> 속성을 설정할 수 있습니다.  
  
3. <xref:System.ServiceModel.Description.MetadataSet> 메서드 중 하나를 호출하여, 검색된 메타데이터가 들어 있는 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 개체를 구합니다. <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A> 생성 시 주소를 명시적으로 지정한 경우에는 인수를 사용하지 않는 <xref:System.ServiceModel.Description.MetadataExchangeClient> 오버로드만 사용할 수 있음에 유의하십시오.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.ServiceModel.Description.MetadataExchangeClient>를 사용하여 메타데이터 파일을 다운로드하고 열거하는 방법을 보여 줍니다.  

 [!code-csharp[MetadataResolver#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/metadataresolver/cs/client.cs#3)]  

## <a name="compiling-the-code"></a>코드 컴파일  
 이 코드 예제를 컴파일하려면 System.ServiceModel.dll 어셈블리를 참조하여 <xref:System.ServiceModel.Description> 네임스페이스를 가져와야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.MetadataResolver>
- <xref:System.ServiceModel.Description.MetadataExchangeClient>
- <xref:System.ServiceModel.Description.WsdlImporter>
