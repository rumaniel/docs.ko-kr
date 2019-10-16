---
title: '방법: X.509 인증서를 사용하여 서비스 보안'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
ms.openlocfilehash: 69db887bf8e7b51c4450c04bd1a08d3d952e84f7
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643567"
---
# <a name="how-to-secure-a-service-with-an-x509-certificate"></a>방법: X.509 인증서를 사용하여 서비스 보안
X.509 인증서를 사용 하 여 서비스를 보안은 대부분의 바인딩은 Windows Communication Foundation (WCF)에서 사용 하는 기본 기술입니다. 이 항목에서는 X.509 인증서와 함께 자체 호스팅된 서비스를 구성하는 단계에 대해 설명합니다.  
  
 필수 구성 요소는 서버를 인증하는 데 사용할 수 있는 유효한 인증서입니다. 인증서는 신뢰할 수 있는 인증 기관에 의해 서버에 발급되어야 합니다. 인증서가 유효하지 않은 경우, 서비스를 사용하려고 시도하는 클라이언트에서 해당 서비스를 신뢰할 수 없으며, 결과적으로 연결이 되지 않습니다. 인증서를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [Working with Certificates](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)합니다.  
  
### <a name="to-configure-a-service-with-a-certificate-using-code"></a>코드를 사용하여 인증서와 함께 서비스를 구성하려면  
  
1. 서비스 계약과 구현된 서비스를 만듭니다. 자세한 내용은 [서비스 디자인 및 구현](../../../../docs/framework/wcf/designing-and-implementing-services.md)합니다.  
  
2. 다음 코드에서처럼 <xref:System.ServiceModel.WSHttpBinding> 클래스의 인스턴스를 만들고, 보안 모드를 <xref:System.ServiceModel.SecurityMode.Message>로 설정합니다.  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3. 다음 코드에서처럼 계약 형식과 구현된 계약 각각에 대해 두 개의 <xref:System.Type> 변수를 만듭니다.  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4. 서비스의 기본 주소에 대해 <xref:System.Uri> 클래스의 인스턴스를 만듭니다. 때문에 `WSHttpBinding` 사용 하 여 해당 스키마와 함께 HTTP 전송에는 리소스 URI (Uniform Identifier)를 시작 해야 합니다 또는 Windows Communication Foundation (WCF) 서비스를 열 때 예외가 throw 됩니다.  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5. 구현된 계약 형식 변수 및 URI와 함께 <xref:System.ServiceModel.ServiceHost> 클래스의 새 인스턴스를 만듭니다.  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6. <xref:System.ServiceModel.Description.ServiceEndpoint> 메서드를 사용하여 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>를 서비스에 추가합니다. 다음 코드에서처럼 계약, 바인딩 및 엔드포인트 주소를 생성자에 전달합니다.  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7. 선택 사항입니다. 서비스로부터 메타데이터를 검색하려면 새 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 개체를 만들고 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 속성을 `true`로 설정합니다.  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8. 유효한 인증서를 서비스에 추가하려면 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 클래스의 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 메서드를 사용합니다. 메서드는 인증서를 찾기 위해 여러 메서드 중 하나를 사용할 수 있습니다. 다음 예제에서는 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindBySubjectName> 열거형을 사용합니다. 열거형은 제공된 값이 인증서가 발급된 엔터티의 이름임을 지정합니다.  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. 서비스 수신을 시작하려면 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 메서드를 호출합니다. 콘솔 애플리케이션을 만들려면 수신 상태에서 서비스를 유지하도록 <xref:System.Console.ReadLine%2A> 메서드를 호출합니다.  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 메서드를 사용하여 X.509 인증서와 함께 서비스를 구성합니다.  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 코드를 컴파일하려면 다음 네임스페이스가 필요합니다.  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.Web.Services.Description>  
  
- <xref:System.Security.Cryptography.X509Certificates>  
  
- <xref:System.Runtime.Serialization>  
  
## <a name="see-also"></a>참고자료

- [인증서 작업](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
