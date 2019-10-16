---
title: '방법: 인증서 지문 검색'
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], retrieving thumbprint
ms.assetid: da3101aa-78cd-4c34-9652-d1f24777eeab
ms.openlocfilehash: 51debbbcfec2fd5b82460e1dd1d6ece8e77bfc13
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62000781"
---
# <a name="how-to-retrieve-the-thumbprint-of-a-certificate"></a>방법: 인증서 지문 검색
인증을 위해 X.509 인증서를 사용 하는 Windows Communication Foundation (WCF) 응용 프로그램을 작성, 하는 경우 인증서에 있는 클레임을 지정 하는 데 필요한 경우가 있습니다. 예를 들어 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> 메서드에 <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 열거를 사용하는 경우 지문 클레임을 제공해야 합니다. 클레임 값을 찾는 과정은 두 단계로 이루어집니다. 첫째, 인증서에 대한 MMC(Microsoft Management Console) 스냅인을 엽니다. ([방법: MMC 스냅인을 사용 하 여 인증서를 보려면](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).) 둘째, 여기서 설명하는 대로 적절한 인증서를 찾아 해당 지문(또는 다른 클레임 값)을 복사합니다.  
  
 서비스 인증에 인증서를 사용하는 경우 **발급 대상** 열(콘솔의 첫 번째 열)의 값을 확인하는 것이 중요합니다. SSL(Secure Sockets Layer)을 전송 보안으로 사용하는 경우 수행되는 첫 번째 확인 작업 중 하나는 서비스의 기본 주소 URI(Uniform Resource Identifier)를 **발급 대상** 값과 비교하는 것입니다. 값이 일치해야 하며, 그렇지 않으면 인증 프로세스가 중지됩니다.  
  
 또한 개발 중에 사용할 임시 인증서를 만들려면 Powershell New-selfsignedcertificate cmdlet을 사용할 수 있습니다. 기본적으로 단, 이러한 인증서가 인증 기관에서 발급 되지 않았습니다 및 프로덕션용으로 사용할 수 없습니다. 자세한 내용은 [방법: 개발 중 사용할 임시 인증서 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)합니다.  
  
### <a name="to-retrieve-a-certificates-thumbprint"></a>인증서의 지문을 검색하려면  
  
1. 인증서에 대한 MMC(Microsoft Management Console) 스냅인을 엽니다. ([방법: MMC 스냅인을 사용 하 여 인증서를 보려면](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).)  
  
2. **콘솔 루트** 창의 왼쪽 창에서 **인증서(로컬 컴퓨터)** 를 클릭합니다.  
  
3. **개인** 폴더를 클릭하여 확장합니다.  
  
4. **인증서** 폴더를 클릭하여 확장합니다.  
  
5. 인증서 목록에서 **용도** 제목을 확인합니다. **클라이언트 인증** 을 용도로 표시하는 인증서를 찾습니다.  
  
6. 인증서를 두 번 클릭합니다.  
  
7. **인증서** 대화 상자에서 **자세히** 탭을 클릭합니다.  
  
8. 필드 목록을 스크롤하여 **지문**을 클릭합니다.  
  
9. 상자에서 16진수 문자를 복사합니다. `X509FindType`에 대한 코드에서 이 지문을 사용하는 경우 16진수 사이의 공백을 제거합니다. 예를 들어 지문 "a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a 7b"는 코드에서 "a909502dd82ae41433e6f83886b00d4277a32a7b"로 지정해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>
- [방법: SSL 인증서로 포트 구성](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)
- [방법: MMC 스냅인을 사용 하 여 인증서 보기](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)
- [방법: 개발 중 사용할 임시 인증서 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md)
