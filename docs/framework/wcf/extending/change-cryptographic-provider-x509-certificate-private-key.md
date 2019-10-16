---
title: '방법: X.509 인증서의 프라이빗 키에 대한 암호화 공급 기업 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptographic provider [WCF], changing
- cryptographic provider [WCF]
ms.assetid: b4254406-272e-4774-bd61-27e39bbb6c12
ms.openlocfilehash: 8101c0d1214eed2c6ea42a4faab774207aab3a79
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797283"
---
# <a name="how-to-change-the-cryptographic-provider-for-an-x509-certificates-private-key"></a>방법: X.509 인증서의 프라이빗 키에 대한 암호화 공급 기업 변경
이 항목에서는 x.509 인증서의 개인 키를 제공 하는 데 사용 되는 암호화 공급자를 변경 하는 방법과 공급자를 WCF (Windows Communication Foundation) 보안 프레임 워크에 통합 하는 방법을 보여 줍니다. 인증서를 사용 하는 방법에 대 한 자세한 내용은 [인증서 작업](../feature-details/working-with-certificates.md)을 참조 하세요.  
  
 WCF 보안 프레임 워크는 [방법:에 설명 된 대로 새 보안 토큰 형식을 도입 하는 방법을 제공 합니다. 사용자 지정 토큰](how-to-create-a-custom-token.md)을 만듭니다. 사용자 지정 토큰을 사용하여 시스템에서 제공되는 기존 형식을 대체할 수도 있습니다.  
  
 이 항목에서는 시스템에서 제공되는 X.509 보안 토큰을 인증서 프라이빗 키의 다른 구현을 제공하는 사용자 지정 X.509 토큰으로 대체합니다. 기본 Windows 암호화 공급자와 다른 암호화 공급자에서 실제 프라이빗 키를 제공하는 경우에 유용한 시나리오입니다. 대체 암호화 공급자의 한 예로는 프라이빗 키와 관련된 모든 암호화 작업을 수행하면서 프라이빗 키를 메모리에 저장하지는 않는 방식으로 시스템 보안을 향상시키는 하드웨어 보안 모듈이 있습니다.  
  
 다음 예는 데모용으로만 제공됩니다. 여기서는 기본 Windows 암호화 공급자를 대체하지 않지만 그런 공급자를 통합하는 위치를 보여 줍니다.  
  
## <a name="procedures"></a>절차  
 보안 키가 연결된 모든 보안 토큰에서는 보안 토큰 인스턴스로부터 키 컬렉션을 반환하는 <xref:System.IdentityModel.Tokens.SecurityToken.SecurityKeys%2A> 속성을 구현해야 합니다. 토큰이 X.509 보안 토큰인 경우 컬렉션에는 인증서와 연결된 퍼블릭 및 프라이빗 키를 모두 나타내는 <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> 클래스의 단일 인스턴스가 포함됩니다. 인증서의 키를 제공하는 데 사용되는 기본 암호화 공급자를 대체하려면 이 클래스의 새 구현을 만듭니다.  
  
#### <a name="to-create-a-custom-x509-asymmetric-key"></a>사용자 지정 X.509 비대칭 키를 만들려면  
  
1. <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> 클래스에서 파생된 새 클래스를 정의합니다.  
  
2. <xref:System.IdentityModel.Tokens.SecurityKey.KeySize%2A> 읽기 전용 속성을 재정의합니다. 이 속성에서는 인증서의 퍼블릭/프라이빗 키 쌍의 실제 키 크기를 반환합니다.  
  
3. <xref:System.IdentityModel.Tokens.SecurityKey.DecryptKey%2A> 메서드를 재정의합니다. 이 메서드는 인증서의 개인 키를 사용 하 여 대칭 키의 암호를 해독 하기 위해 WCF 보안 프레임 워크에서 호출 됩니다. 키는 이전에 인증서의 공개 키로 암호화되었습니다.  
  
4. <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetAsymmetricAlgorithm%2A> 메서드를 재정의합니다. 이 메서드는 메서드에 전달 된 매개 변수에 따라 인증서의 개인 또는 공개 키 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 에 대 한 암호화 공급자를 나타내는 클래스의 인스턴스를 가져오기 위해 WCF 보안 프레임 워크에서 호출 됩니다.  
  
5. 선택 사항입니다. <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetHashAlgorithmForSignature%2A> 메서드를 재정의합니다. 다른 <xref:System.Security.Cryptography.HashAlgorithm> 클래스 구현이 필요한 경우 이 메서드를 재정의합니다.  
  
6. <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetSignatureFormatter%2A> 메서드를 재정의합니다. 이 메서드에서는 인증서의 프라이빗 키와 연결된 <xref:System.Security.Cryptography.AsymmetricSignatureFormatter> 클래스의 인스턴스를 반환합니다.  
  
7. <xref:System.IdentityModel.Tokens.SecurityKey.IsSupportedAlgorithm%2A> 메서드를 재정의합니다. 이 메서드는 보안 키 구현에서 특정 암호화 알고리즘이 지원되는지 여부를 나타내는 데 사용됩니다.  
  
     [!code-csharp[c_CustomX509Token#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#1)]
     [!code-vb[c_CustomX509Token#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#1)]  
  
 다음 절차에서는 시스템에서 제공 하는 x.509 보안 토큰을 대체 하기 위해 앞의 절차에서 만든 사용자 지정 x.509 비대칭 보안 키 구현을 WCF 보안 프레임 워크와 통합 하는 방법을 보여 줍니다.  
  
#### <a name="to-replace-the-system-provided-x509-security-token-with-a-custom-x509-asymmetric-security-key-token"></a>시스템에서 제공되는 X.509 보안 토큰을 사용자 지정 X.509 비대칭 보안 키 토큰으로 대체하려면  
  
1. 다음 예와 같이 시스템에서 제공되는 보안 키 대신 사용자 지정 X.509 비대칭 보안 키를 반환하는 사용자 지정 X.509 보안 토큰을 만듭니다. 사용자 지정 보안 토큰 [에 대 한 자세한 내용은 방법: 사용자 지정 토큰](how-to-create-a-custom-token.md)을 만듭니다.  
  
     [!code-csharp[c_CustomX509Token#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#2)]
     [!code-vb[c_CustomX509Token#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#2)]  
  
2. 예와 같이 사용자 지정 X.509 보안 토큰을 반환하는 사용자 지정 보안 토큰 공급자를 만듭니다. 사용자 지정 보안 토큰 공급자 [에 대 한 자세한 내용은 방법: 사용자 지정 보안 토큰 공급자](how-to-create-a-custom-security-token-provider.md)를 만듭니다.  
  
     [!code-csharp[c_CustomX509Token#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#3)]
     [!code-vb[c_CustomX509Token#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#3)]  
  
3. 게시자 쪽에서 사용자 지정 보안 키를 사용해야 하는 경우에는 다음 예와 같이 사용자 지정 클라이언트 보안 토큰 관리자 및 사용자 지정 클라이언트 자격 증명 클래스를 만듭니다. 사용자 지정 클라이언트 자격 증명 및 클라이언트 보안 토큰 관리자 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.  
  
     [!code-csharp[c_CustomX509Token#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#4)]
     [!code-vb[c_CustomX509Token#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#4)]  
  
     [!code-csharp[c_CustomX509Token#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#6)]
     [!code-vb[c_CustomX509Token#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#6)]  
  
4. 받는 사람 쪽에서 사용자 지정 보안 키를 사용해야 하는 경우에는 다음 예와 같이 사용자 지정 서비스 보안 토큰 관리자 및 사용자 지정 서비스 자격 증명 클래스를 만듭니다. 사용자 지정 서비스 자격 증명 및 서비스 보안 토큰 관리자 [에 대 한 자세한 내용은 연습: 사용자 지정 클라이언트 및 서비스 자격](walkthrough-creating-custom-client-and-service-credentials.md)증명을 만드는 중입니다.  
  
     [!code-csharp[c_CustomX509Token#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#5)]
     [!code-vb[c_CustomX509Token#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#5)]  
  
     [!code-csharp[c_CustomX509Token#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#7)]
     [!code-vb[c_CustomX509Token#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#7)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.SecurityKey>
- <xref:System.Security.Cryptography.AsymmetricAlgorithm>
- <xref:System.Security.Cryptography.HashAlgorithm>
- <xref:System.Security.Cryptography.AsymmetricSignatureFormatter>
- [연습: 사용자 지정 클라이언트 및 서비스 자격 증명 만들기](walkthrough-creating-custom-client-and-service-credentials.md)
- [방법: 사용자 지정 보안 토큰 인증자 만들기](how-to-create-a-custom-security-token-authenticator.md)
- [방법: 사용자 지정 보안 토큰 공급자 만들기](how-to-create-a-custom-security-token-provider.md)
- [방법: 사용자 지정 토큰 만들기](how-to-create-a-custom-token.md)
