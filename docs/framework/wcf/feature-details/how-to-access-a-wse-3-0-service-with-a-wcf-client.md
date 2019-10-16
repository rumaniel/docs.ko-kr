---
title: '방법: WSE 3.0 액세스 WCF 클라이언트를 사용 하 여 서비스'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
ms.openlocfilehash: e191bc6c75c8c04e2cdf32d80673c32499b5736d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64613113"
---
# <a name="how-to-access-a-wse-30-service-with-a-wcf-client"></a>방법: WSE 3.0 액세스 WCF 클라이언트를 사용 하 여 서비스
Windows Communication Foundation (WCF) 클라이언트는 WCF 클라이언트가 2004 년 8 월 버전의 Ws-addressing 사양 사용 하도록 구성 된 하는 경우 Microsoft.NET 서비스용 유선 수준으로 호환 Web Services Enhancements (WSE) 3.0 사용 하 여 합니다. 그러나 WSE 3.0 서비스 지원 하지 않습니다 메타 데이터 교환 (MEX) 프로토콜은 지금 사용 하는 경우는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) WCF 클라이언트 클래스를 만들려면 보안 설정이 적용 되지 않습니다는 생성 된 WCF 클라이언트입니다. 따라서 보안 설정을 지정 해야 합니다는 WSE 3.0 서비스에 WCF 클라이언트 생성 된 후 필요 합니다.  
  
 WSE 3.0 서비스의 요구 사항 및 WSE 3.0 서비스와 WCF 클라이언트 간의 상호 운용 가능한 요구 사항을 고려해 야 할 사용자 지정 바인딩을 사용 하 여 이러한 보안 설정을 적용할 수 있습니다. 이러한 상호 운용성 요구 사항에는 앞에서 말한 August 2004 WS-Addressing 사양 및 WSE 3.0의 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncrypt> 기본 메시지 보호를 사용하는 것이 포함됩니다. WCF의 기본 메시지 보호는 <xref:System.ServiceModel.Security.MessageProtectionOrder.SignBeforeEncryptAndEncryptSignature>합니다. 이 항목에서는 WSE 3.0 서비스와 상호 운용 하는 WCF 바인딩을 만드는 방법을 자세히 설명 합니다. WCF는이 바인딩을 통합 하는 샘플도 제공 합니다. 이 샘플에 대 한 자세한 내용은 참조 하세요. [ASMX 웹 서비스와의 상호 운용](../../../../docs/framework/wcf/samples/interoperating-with-asmx-web-services.md)합니다.  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a>WCF 클라이언트를 사용하여 WSE 3.0 웹 서비스에 액세스하려면  
  
1. 실행 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) WSE 3.0 웹 서비스에 대 한 WCF 클라이언트를 만듭니다.  
  
     WSE 3.0 웹 서비스의 경우 WCF 클라이언트 생성 됩니다. WSE 3.0이 MEX 프로토콜을 지원하지 않으므로 해당 도구를 사용하여 웹 서비스에 대한 보안 요구 사항을 검색할 수 없습니다. 애플리케이션 개발자는 해당 클라이언트에 대한 보안 설정을 추가해야 합니다.  
  
     WCF 클라이언트를 만드는 방법에 대 한 자세한 내용은 참조는 [방법: 클라이언트를 만드는](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)합니다.  
  
2. WSE 3.0 웹 서비스와 통신할 수 있는 바인딩을 나타내는 클래스를 만듭니다.  
  
     다음 클래스의 일부인 합니다 [WSE와의 상호 운용](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29) 샘플:  
  
    1. <xref:System.ServiceModel.Channels.Binding> 클래스에서 파생되는 클래스를 만듭니다.  
  
         다음 코드 예제에서는 `WseHttpBinding` 클래스로부터 파생되는 <xref:System.ServiceModel.Channels.Binding>이라는 클래스를 만듭니다.  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2. WSE 서비스에서 사용되는 WSE 턴키 어설션, 파생된 키가 필요한지 여부, 보안 세션이 사용되는지 여부, 서명 확인이 필요한지 여부 및 메시지 보호 설정을 지정하는 클래스에 속성을 추가합니다. WSE 3.0에서는 턴키 어설션이 클라이언트 또는 웹 서비스에 대 한 보안 요구 사항을 지정-WCF에서 바인딩의 인증 모드와 비슷합니다.  
  
         다음 코드 예제에서는 WSE 턴키 어설션, 파생된 키가 필요한지 여부, 보안 세션이 사용되는지 여부, 서명 확인이 필요한지 여부 및 메시지 보호 설정을 각각 지정하는 `SecurityAssertion`, `RequireDerivedKeys`, `EstablishSecurityContext` 및 `MessageProtectionOrder` 속성을 정의합니다.  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3. <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> 메서드를 재정의하여 바인딩 속성을 설정합니다.  
  
         다음 코드 예제에서는 `SecurityAssertion` 및 `MessageProtectionOrder` 속성의 값을 가져옴으로써 전송, 메시지 인코딩, 메시지 보호 설정을 지정합니다.  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3. 클라이언트 애플리케이션 코드에서 바인딩 속성을 설정하기 위해 코드를 추가합니다.  
  
     다음 코드 예제에서는 WSE 3.0에서 정의 된 대로 메시지 보호 및 인증이 WCF 클라이언트 사용 하도록 지정 `AnonymousForCertificate` 턴키 보안 어설션 합니다. 또한 보안 세션 및 파생된 키도 필요합니다.  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 WSE 3.0 턴키 보안 어설션의 속성에 해당하는 속성을 노출하는 사용자 지정 바인딩을 정의합니다. 명명 된 해당 사용자 지정 바인딩을 `WseHttpBinding`, WSSecurityAnonymous WSE 3.0 QuickStart 샘플과 통신 하는 WCF 클라이언트에 대 한 바인딩 속성을 지정 하려면 사용 됩니다.  

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.Binding>
- [WSE와의 상호 운용](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752257%28v=vs.90%29)
