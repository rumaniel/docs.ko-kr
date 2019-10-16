---
title: '방법: 사용자 지정 정책 어설션 내보내기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 99030386-43b0-4f7b-866d-17ea307f5cbd
ms.openlocfilehash: 992133ff9922e36b00683f4f48db88e1c2b91c1d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795673"
---
# <a name="how-to-export-custom-policy-assertions"></a>방법: 사용자 지정 정책 어설션 내보내기
정책 어설션은 서비스 엔드포인트의 기능 및 요구 사항에 대해 설명합니다. 서비스 애플리케이션은 서비스 메타데이터에서 사용자 지정 정책 어설션을 사용하여 엔드포인트, 바인딩 또는 계약 사용자 지정 정보에 대해 클라이언트 애플리케이션과 통신할 수 있습니다. WCF (Windows Communication Foundation)를 사용 하 여 통신 하는 기능 또는 요구 사항에 따라 끝점, 작업 또는 메시지 주제의 WSDL 바인딩에 연결 된 정책 식에서 어설션을 내보낼 수 있습니다.  
  
 사용자 지정 정책 어설션은 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> 인터페이스를 구현하고, 바인딩 요소를 서비스 엔드포인트의 바인딩에 직접 삽입하거나 바인딩 요소를 애플리케이션 구성 파일에 등록하여 내보냅니다. 정책 내보내기 구현을 통해 사용자 지정 정책 어설션을 <xref:System.Xml.XmlElement?displayProperty=nameWithType> 인스턴스로서 <xref:System.ServiceModel.Description.PolicyAssertionCollection?displayProperty=nameWithType> 메서드에 전달된 <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=nameWithType>의 해당 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A>에 추가해야 합니다.  
  
 또한 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 클래스의 <xref:System.ServiceModel.Description.WsdlExporter> 속성을 확인하고, 지정된 정책 버전에 따라 올바른 네임스페이스의 중첩된 정책 식 및 정책 프레임워크 특성을 내보내야 합니다.  
  
 사용자 지정 정책 어설션을 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType> 가져오려면 및 [방법: 사용자 지정 정책 어설션을](how-to-import-custom-policy-assertions.md)가져옵니다.  
  
### <a name="to-export-custom-policy-assertions"></a>사용자 지정 정책 어설션을 내보내려면  
  
1. <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=nameWithType>의 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> 인터페이스를 구현합니다. 다음 코드 예제에서는 바인딩 수준에서 사용자 지정 정책 어설션의 구현을 보여 줍니다.  
  
     [!code-csharp[CustomPolicySample#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyexporter.cs#14)]
     [!code-vb[CustomPolicySample#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyexporter.vb#14)]  
  
2. 바인딩 요소를 엔드포인트 바인딩에 프로그래밍 방식으로 삽입하거나 애플리케이션 구성 파일을 사용하여 삽입합니다. 다음 절차를 참조하십시오.  
  
### <a name="to-insert-a-binding-element-using-an-application-configuration-file"></a>애플리케이션 구성 파일을 사용하여 바인딩 요소를 삽입하려면  
  
1. 사용자 지정 정책 어설션 바인딩 요소에 대한 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=nameWithType>를 구현합니다.  
  
2. Bindingelementextensions > 요소를 사용 하 여 [ \<](../../configure-apps/file-schema/wcf/bindingelementextensions.md) 구성 파일에 바인딩 요소 확장을 추가 합니다.  
  
3. <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>을 사용하여 사용자 지정 바인딩을 만듭니다.  
  
### <a name="to-insert-a-binding-element-programmatically"></a>바인딩 요소를 프로그래밍 방식으로 삽입하려면  
  
1. 새 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>를 만들어 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=nameWithType>에 추가합니다.  
  
2. 1단계의 사용자 지정 바인딩을 새 엔드포인트에 추가하고, <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> 메서드를 호출하여 해당 새 서비스 엔드포인트를 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>에 추가합니다.  
  
3. <xref:System.ServiceModel.ServiceHost>을 엽니다. 다음 코드 예제에서는 사용자 지정 바인딩을 만들고 프로그래밍 방식으로 바인딩 요소를 삽입하는 방법에 대해 보여 줍니다.  
  
     [!code-csharp[s_imperative#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_imperative/cs/service.cs#1)]
     [!code-vb[s_imperative#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_imperative/vb/service.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Description.IPolicyImportExtension>
- <xref:System.ServiceModel.Description.IPolicyExportExtension>
- [방법: 사용자 지정 정책 어설션 가져오기](how-to-import-custom-policy-assertions.md)
