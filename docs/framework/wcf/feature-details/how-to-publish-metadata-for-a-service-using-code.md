---
title: '방법: 코드를 사용하여 서비스에 대한 메타데이터 게시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 51407e6d-4d87-42d5-be7c-9887b8652006
ms.openlocfilehash: 1faed5717c65c4973c3f1965df649df6f2e24722
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045896"
---
# <a name="how-to-publish-metadata-for-a-service-using-code"></a>방법: 코드를 사용하여 서비스에 대한 메타데이터 게시
이 항목은 WCF (Windows Communication Foundation) 서비스에 대 한 메타 데이터 게시를 설명 하는 두 가지 방법 항목 중 하나입니다. 서비스에서 메타데이터를 게시하는 방법을 지정하는 두 가지 방법은 구성 파일을 사용하는 방법과 코드를 사용하는 방법입니다. 이 항목에서는 코드를 사용하여 서비스에 대해 메타데이터를 게시하는 방법에 대해 설명합니다.  
  
> [!CAUTION]
> 이 항목에서는 보호되지 않은 방식으로 메타데이터를 게시하는 방법을 보여 줍니다. 즉, 모든 클라이언트가 서비스에서 메타데이터를 검색할 수 있습니다. 서비스에서 보호되는 방식으로 메타데이터를 게시해야 하는 경우에는 [사용자 지정 보안 메타 데이터 끝점](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)을 참조 하세요.  
  
 구성 파일 [에 메타 데이터를 게시 하는 방법에 대 한 자세한 내용은 방법: 구성 파일](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)을 사용 하 여 서비스에 대 한 메타 데이터를 게시 합니다. 메타데이터를 게시하면 클라이언트에서 WS-Transfer GET 요청을 사용하는 메타데이터 또는 `?wsdl` 쿼리 문자열을 사용하는 HTTP/GET 요청을 검색할 수 있습니다. 코드가 작동 중인지 확인하려면 기본 WCF 서비스를 만들어야 합니다. 다음 코드로 된 기본 자체 호스팅 서비스가 제공됩니다.  
  
 [!code-csharp[htPublishMetadataCode#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#0)]
 [!code-vb[htPublishMetadataCode#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#0)]  
  
### <a name="to-publish-metadata-in-code"></a>코드에서 메타데이터를 게시하려면  
  
1. 콘솔 애플리케이션의 main 메서드 내에서 서비스 형식 및 기본 주소를 전달하여 <xref:System.ServiceModel.ServiceHost> 개체를 인스턴스화합니다.  
  
     [!code-csharp[htPublishMetadataCode#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#1)]
     [!code-vb[htPublishMetadataCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#1)]  
  
2. 1단계의 코드 바로 아래에 try 블록을 만듭니다. 이렇게 하면 서비스가 실행되는 동안 throw된 예외가 catch됩니다.  
  
     [!code-csharp[htPublishMetadataCode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#2)]
     [!code-vb[htPublishMetadataCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#2)]  
  
     [!code-csharp[htPublishMetadataCode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#3)]
     [!code-vb[htPublishMetadataCode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#3)]  
  
3. 서비스 호스트에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>가 포함되어 있는지 여부를 확인합니다. 포함되지 않은 경우에는 새 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 인스턴스를 만듭니다.  
  
     [!code-csharp[htPublishMetadataCode#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#4)]
     [!code-vb[htPublishMetadataCode#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#4)]  
  
4. <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 속성을 `true.`로 설정합니다.  
  
     [!code-csharp[htPublishMetadataCode#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#5)]
     [!code-vb[htPublishMetadataCode#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#5)]  
  
5. <xref:System.ServiceModel.Description.ServiceMetadataBehavior>에 <xref:System.ServiceModel.Description.MetadataExporter> 속성이 포함됩니다. <xref:System.ServiceModel.Description.MetadataExporter>에 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 속성이 포함됩니다. <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 속성 값을 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>로 설정합니다. <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 속성을 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>로 설정할 수도 있습니다. 메타 데이터 내보내기 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> 로 설정 하면 "ws-policy 1.5을 준수 하는 메타 데이터를 사용 하 여 정책 정보를 생성 합니다. <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>로 설정된 경우, 메타데이터 내보내기는 WS-Policy 1.2를 준수하는 정책 정보를 생성합니다.  
  
     [!code-csharp[htPublishMetadataCode#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#6)]
     [!code-vb[htPublishMetadataCode#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#6)]  
  
6. 서비스 호스트의 동작 컬렉션에 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 인스턴스를 추가합니다.  
  
     [!code-csharp[htPublishMetadataCode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#7)]
     [!code-vb[htPublishMetadataCode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#7)]  
  
7. 서비스 호스트에 메타데이터 교환 엔드포인트를 추가합니다.  
  
     [!code-csharp[htPublishMetadataCode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#8)]
     [!code-vb[htPublishMetadataCode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#8)]  
  
8. 서비스 호스트에 애플리케이션 엔드포인트를 추가합니다.  
  
     [!code-csharp[htPublishMetadataCode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#9)]
     [!code-vb[htPublishMetadataCode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#9)]  
  
    > [!NOTE]
    > 서비스에 엔드포인트를 추가하지 않으면 런타임에서 기본 엔드포인트를 자동으로 추가합니다. 이 예제에서는 서비스의 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>가 `true`로 설정되어 있으므로 서비스의 메타데이터 게시 기능을 사용할 수 있습니다. 기본 끝점에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../../docs/framework/wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.  
  
9. 서비스 호스트를 열고 들어오는 호출을 기다립니다. 사용자가 Enter 키를 누르면 서비스 호스트가 닫힙니다.  
  
     [!code-csharp[htPublishMetadataCode#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#10)]
     [!code-vb[htPublishMetadataCode#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#10)]  
  
10. 콘솔 애플리케이션을 빌드하고 실행합니다.  
  
11. Internet Explorer를 사용 하 여 서비스의 기본 주소 (http://localhost:8001/MetadataSample 이 예제에서는)로 이동 하 여 메타 데이터 게시가 설정 되었는지 확인 합니다. 웹 페이지의 맨 위에 "간단한 서비스"라는 메시지가 표시되고 바로 아래에 "서비스를 만들었습니다."라는 메시지가 표시됩니다. 그렇지 않으면 결과 페이지의 맨 위에 메시지가 표시 됩니다. "이 서비스에 대 한 메타 데이터 게시는 현재 사용할 수 없습니다."  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 코드에서 서비스에 대 한 메타 데이터를 게시 하는 기본 WCF 서비스를 구현 하는 방법을 보여 줍니다.  
  
 [!code-csharp[htPublishMetadataCode#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#11)]
 [!code-vb[htPublishMetadataCode#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#11)]  
  
## <a name="see-also"></a>참고자료

- [방법: 관리 되는 응용 프로그램에서 WCF 서비스 호스팅](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)
- [자체 호스팅](../../../../docs/framework/wcf/samples/self-host.md)
- [메타데이터 아키텍처 개요](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
- [메타데이터 사용](../../../../docs/framework/wcf/feature-details/using-metadata.md)
- [방법: 구성 파일을 사용 하 여 서비스에 대 한 메타 데이터 게시](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)
