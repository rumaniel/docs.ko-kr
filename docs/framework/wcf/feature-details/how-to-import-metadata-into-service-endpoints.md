---
title: '방법: 서비스 엔드포인트로 메타데이터 가져오기'
ms.date: 03/30/2017
ms.assetid: b69dbe20-92a1-4911-89d8-ffbc3dad4663
ms.openlocfilehash: dce65c31134c211c134cbae2b9bd8296f74b1627
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930722"
---
# <a name="how-to-import-metadata-into-service-endpoints"></a>방법: 서비스 엔드포인트로 메타데이터 가져오기
이 항목에서는 서비스 끝점 컬렉션에 메타 데이터를 가져오고 [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)에 정의 된 서비스를 사용 하는 방법에 대해 설명 합니다. 이 항목에서는 서비스에서 메타데이터를 가져온 다음 서비스에 `Add` 메서드를 호출하는 클라이언트 애플리케이션을 만든 방법을 보여 줍니다.  
  
### <a name="to-import-metadata-into-service-endpoints"></a>서비스 엔드포인트로 메타데이터를 가져오려면  
  
1. <xref:System.ServiceModel.EndpointAddress> 개체를 선언하고 URI(Uniform Resource Identifier)를 사용하여 서비스의 MEX(메타데이터 교환) 주소에 대해 초기화합니다.  
  
     [!code-csharp[UE_ImportMetadata#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#0)]  
  
2. MEX 주소를 전달하여 <xref:System.ServiceModel.Description.MetadataExchangeClient>를 만들고 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>를 호출합니다. 그러면 서비스에서 메타데이터가 검색됩니다.  
  
     [!code-csharp[UE_ImportMetadata#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#1)]  
  
3. 이전에 검색한 메타데이터를 전달하여 <xref:System.ServiceModel.Description.WsdlImporter>를 만들고 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllContracts%2A>를 호출합니다. 그러면 <xref:System.ServiceModel.Description.ContractDescription> 개체 컬렉션이 생성됩니다. 필요에 따라 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllEndpoints%2A> 또는 <xref:System.ServiceModel.Description.WsdlImporter.ImportAllBindings%2A>를 호출할 수도 있습니다.  
  
     [!code-csharp[UE_ImportMetadata#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#2)]  
  
    > [!NOTE]
    > 메타데이터를 가져온 후에는 클라이언트 채널을 만들거나 메타데이터를 내보낼 수 없습니다. 이 시점에는 형식 정보를 사용할 수 없기 때문입니다. 실제로 서비스와 상호 작용하거나 메타데이터를 내보내려면 형식 정보가 필요합니다. 형식 정보를 생성하려면 4단계와 5단계에 표시된 코드를 생성해야 합니다. 또는 <xref:System.ServiceModel.Description.MetadataResolver> 도우미 클래스를 사용할 수도 있습니다. 자세한 내용은 [방법: MetadataResolver를 사용 하 여 동적으로](../../../../docs/framework/wcf/feature-details/how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)바인딩 메타 데이터를 가져옵니다.  
  
4. 각 계약에 대해 형식 정보를 생성합니다.  
  
     [!code-csharp[UE_ImportMetadata#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#3)]  
  
5. 이제 이 정보를 사용할 수 있습니다. 다음 샘플에서는 C# 소스 코드를 생성합니다.  
  
     [!code-csharp[UE_ImportMetadata#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/ue_importmetadata/cs/client.cs#4)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터](../../../../docs/framework/wcf/feature-details/metadata.md)
- [시작](../../../../docs/framework/wcf/samples/getting-started-sample.md)
