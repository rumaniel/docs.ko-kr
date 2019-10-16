---
title: '방법: X.509 인증서로 XML 요소 해독'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- System.Security.Cryptography.X509Certificate2 class
- decryption
- X.509 certificates
- certificates, X.509 certificates
ms.assetid: bd015722-d88d-408d-8ca8-e4e475c441ed
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4d033911151ef5cdf8143ad9d64f9c21897fc975
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654103"
---
# <a name="how-to-decrypt-xml-elements-with-x509-certificates"></a>방법: X.509 인증서로 XML 요소 해독
<xref:System.Security.Cryptography.Xml> 네임스페이스의 클래스를 사용하여 XML 문서 내의 요소를 암호화 및 암호 해독할 수 있습니다.  XML 암호화는 데이터가 쉽게 읽혀질 염려 없이 암호화된 XML 데이터를 교환하거나 저장하는 표준 방법입니다.  XML 암호화 표준에 대 한 자세한 내용은 World Wide Web Consortium (W3C) 사양을 참조에 있는 XML 암호화에 대 한 <https://www.w3.org/TR/xmldsig-core/>합니다.  
  
 이 예제에 설명 된 메서드를 사용 하 여 암호화 된 XML 요소를 암호 해독: [방법: X.509 인증서로 XML 요소 암호화](../../../docs/standard/security/how-to-encrypt-xml-elements-with-x-509-certificates.md)합니다.  <`EncryptedData`> 요소를 찾아 암호 해독한 다음 이 요소를 원래의 일반 텍스트 XML 요소로 바꿉니다.  
  
 이 절차의 코드 예제에서는 현재 사용자 계정의 로컬 인증서 저장소에 있는 X.509 인증서를 사용하여 XML 요소를 암호 해독합니다.  이 예제에서는 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 메서드를 사용하여 X.509 인증서를 자동으로 검색하고 <`EncryptedKey`> 요소의 <`EncryptedData`> 요소에 저장된 세션 키를 암호 해독합니다.  <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 메서드는 자동으로 세션 키를 사용하여 XML 요소를 암호 해독합니다.  
  
 이 예제는 여러 애플리케이션이 암호화된 데이터를 공유해야 하거나 애플리케이션이 실행되는 시간 사이에 암호화된 데이터를 저장해야 경우에 적합합니다.  
  
### <a name="to-decrypt-an-xml-element-with-an-x509-certificate"></a>X.509 인증서로 XML 요소를 암호 해독하려면  
  
1. 디스크에서 XML 파일을 로드하여 <xref:System.Xml.XmlDocument> 개체를 만듭니다.  <xref:System.Xml.XmlDocument> 개체는 암호 해독할 XML 요소를 포함합니다.  
  
     [!code-csharp[HowToDecryptXMLElementX509#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementX509#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#2)]  
  
2. <xref:System.Xml.XmlDocument> 개체를 생성자에 전달하여 새 <xref:System.Security.Cryptography.Xml.EncryptedXml>개체를 만듭니다.  
  
     [!code-csharp[HowToDecryptXMLElementX509#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementX509#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#3)]  
  
3. <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 메서드를 사용하여 XML 문서를 암호 해독합니다.  
  
     [!code-csharp[HowToDecryptXMLElementX509#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#4)]
     [!code-vb[HowToDecryptXMLElementX509#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#4)]  
  
4. <xref:System.Xml.XmlDocument> 개체를 저장합니다.  
  
     [!code-csharp[HowToDecryptXMLElementX509#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementX509#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#5)]  
  
## <a name="example"></a>예제  
 이 예제에서는 `"test.xml"`이라는 파일이 컴파일된 프로그램과 동일한 디렉터리에 있다고 가정합니다.  또한 `"test.xml"`에 `"creditcard"` 요소가 포함되어 있다고 가정합니다.  `test.xml`이라는 파일에 다음 XML을 배치하고 이 예제에서 사용할 수 있습니다.  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToDecryptXMLElementX509#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementX509/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementX509#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementX509/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 예제를 컴파일하려면 `System.Security.dll`에 대한 참조를 포함해야 합니다.  
  
- <xref:System.Xml>, <xref:System.Security.Cryptography> 및 <xref:System.Security.Cryptography.Xml> 네임스페이스를 포함합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 이 예제에서 사용된 X.509 인증서는 테스트 전용입니다.  애플리케이션은 신뢰할 수 있는 인증 기관에서 생성된 X.509 인증서를 사용하거나 Microsoft Windows 인증서 서버에서 생성된 인증서를 사용해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.Xml>
- [방법: X.509 인증서로 XML 요소 암호화](../../../docs/standard/security/how-to-encrypt-xml-elements-with-x-509-certificates.md)
