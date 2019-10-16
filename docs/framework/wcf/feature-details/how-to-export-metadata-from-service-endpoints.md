---
title: '방법: 서비스 엔드포인트에서 메타데이터 내보내기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b6c4dfd0-f270-43ec-961a-e16eb6af2f2c
ms.openlocfilehash: 6bf2eb3d295f9cbf6a7e13a612d5846ceaa75ab4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778302"
---
# <a name="how-to-export-metadata-from-service-endpoints"></a>방법: 서비스 엔드포인트에서 메타데이터 내보내기
이 항목에서는 서비스 엔드포인트로부터 메타데이터를 내보내는 방법에 대해 설명합니다.  
  
### <a name="to-export-metadata-from-service-endpoints"></a>서비스 엔드포인트에서 메타데이터를 내보내려면  
  
1. 새 Visual Studio Console App Project를 만듭니다. 다음 단계에 표시된 코드를 생성된 Program.cs 파일의 main() 메서드에 추가합니다.  
  
2. <xref:System.ServiceModel.Description.WsdlExporter>를 만듭니다.  
  
     [!code-csharp[S_UEWsdlExporter#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#1)]
     [!code-vb[S_UEWsdlExporter#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#1)]  
  
3. <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 속성을 <xref:System.ServiceModel.Description.PolicyVersion> 열거형의 값 중 하나로 설정합니다. 샘플에서는 값을 WS-Policy 1.5에 해당되는 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>로 설정합니다.  
  
     [!code-csharp[S_UEWsdlExporter#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#2)]
     [!code-vb[S_UEWsdlExporter#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#2)]  
  
4. <xref:System.ServiceModel.Description.ServiceEndpoint> 개체의 배열을 만듭니다.  
  
     [!code-csharp[S_UEWsdlExporter#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#3)]
     [!code-vb[S_UEWsdlExporter#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#3)]  
  
5. 각 서비스 엔드포인트의 메타데이터를 내보냅니다.  
  
     [!code-csharp[S_UEWsdlExporter#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#4)]
     [!code-vb[S_UEWsdlExporter#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#4)]  
  
6. 내보내기 프로세스 중에 오류가 발생하지 않았는지 확인하고 메타데이터를 검색합니다.  
  
     [!code-csharp[S_UEWsdlExporter#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#5)]
     [!code-vb[S_UEWsdlExporter#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#5)]  
  
7. 이제 <xref:System.ServiceModel.Description.MetadataSet.WriteTo%28System.Xml.XmlWriter%29> 메서드를 호출하여 파일에 쓰는 등의 방식으로 메타데이터를 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음은 이 예제에 해당되는 전체 코드 목록입니다.  
  
 [!code-csharp[S_UEWsdlExporter#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_uewsdlexporter/cs/program.cs#0)]
 [!code-vb[S_UEWsdlExporter#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_uewsdlexporter/vb/program.vb#0)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 Program.cs를 컴파일할 때에는 System.ServiceModel.dll을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [메타데이터 아키텍처 개요](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)
- [메타데이터 사용](../../../../docs/framework/wcf/feature-details/using-metadata.md)
- [끝점: 주소, 바인딩 및 계약](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
