---
title: '방법: 비대칭 키를 사용하여 XML 요소 암호화'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [.NET Framework], asymmetric keys
- AES algorithm
- System.Security.Cryptography.RSACryptoServiceProvider class
- asymmetric keys [.NET Framework]
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- key containers
- Advanced Encryption Standard algorithm
- Rijndael
- encryption [.NET Framework], asymmetric keys
ms.assetid: a164ba4f-e596-4bbe-a9ca-f214fe89ed48
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4fc959ee2e29224d6d2598291141e6c922223529
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645345"
---
# <a name="how-to-encrypt-xml-elements-with-asymmetric-keys"></a>방법: 비대칭 키를 사용하여 XML 요소 암호화
<xref:System.Security.Cryptography.Xml> 네임스페이스의 클래스를 사용하여 XML 문서 내의 요소를 암호화할 수 있습니다.  XML 암호화는 데이터가 쉽게 읽혀질 염려 없이 암호화된 XML 데이터를 교환하거나 저장하는 표준 방법입니다.  XML 암호화 표준에 대 한 자세한 내용은 World Wide Web Consortium (W3C) 사양을 참조에 있는 XML 암호화에 대 한 <https://www.w3.org/TR/xmldsig-core/>합니다.  
  
 XML 암호화를 사용하여 암호화된 XML 데이터가 포함된 <`EncryptedData`> 요소의 문서나 XML 요소를 대체할 수 있습니다.  <`EncryptedData`> 요소는 암호화 중에 사용된 키와 프로세스에 대한 정보가 들어 있는 하위 요소를 포함할 수도 있습니다.  XML 암호화를 사용하면 문서에 암호화된 여러 요소가 포함될 수 있고 한 요소가 여러 번 암호화될 수 있습니다.  이 절차의 코드 예제에서는 나중에 암호 해독 과정에서 사용할 수 있는 다른 여러 하위 요소와 함께 <`EncryptedData`> 요소를 생성하는 방법을 보여 줍니다.  
  
 이 예제에서는 두 키를 사용하여 XML 요소를 암호화합니다.  RSA 퍼블릭/프라이빗 키 쌍을 생성하고 보안 키 컨테이너에 키 쌍을 저장합니다.  다음 예제에서는 Rijndael 알고리즘이라고도 하는 AES(고급 암호화 표준) 알고리즘을 사용하여 별도 세션 키를 만듭니다.  이 예제에서는 AES 세션 키를 사용하여 XML 문서를 암호화한 다음 RSA 공개 키를 사용하여 AES 세션 키를 암호화합니다.  끝으로, 예제에서는 암호화된 AES 세션 키와 암호화된 XML 데이터를 XML 문서의 새로운 <`EncryptedData`> 요소 내에 저장합니다.  
  
 XML 요소를 암호 해독하려면 키 컨테이너에서 RSA 프라이빗 키를 검색하고 세션 키를 암호 해독하는 데 사용한 다음 세션 키를 사용하여 문서를 암호 해독합니다.  이 절차를 사용 하 여 암호화 된 XML 요소 암호 해독 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 비대칭 키를 사용 하 여 XML 요소 암호 해독](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md)합니다.  
  
 이 예제는 여러 애플리케이션이 암호화된 데이터를 공유해야 하거나 애플리케이션이 실행되는 시간 사이에 암호화된 데이터를 저장해야 경우에 적합합니다.  
  
### <a name="to-encrypt-an-xml-element-with-an-asymmetric-key"></a>비대칭 키를 사용하여 XML 요소를 암호화하려면  
  
1. <xref:System.Security.Cryptography.CspParameters> 개체를 만들고 키 컨테이너의 이름을 지정합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2. <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스를 사용하여 대칭 키를 생성합니다.  <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스의 생성자에 <xref:System.Security.Cryptography.CspParameters> 개체를 전달하면 키가 자동으로 키 컨테이너에 저장됩니다.  이 키는 AES 세션 키를 암호화하는 데 사용되며, 나중에 검색하여 암호 해독할 수 있습니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3. 디스크에서 XML 파일을 로드하여 <xref:System.Xml.XmlDocument> 개체를 만듭니다.  <xref:System.Xml.XmlDocument> 개체는 암호화할 XML 요소를 포함합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#4)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#4)]  
  
4. <xref:System.Xml.XmlDocument> 개체에서 지정된 요소를 찾고 암호화할 요소를 나타내는 <xref:System.Xml.XmlElement> 개체를 새로 만듭니다. 이 예제에서는 `"creditcard"` 요소가 암호화됩니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
5. <xref:System.Security.Cryptography.RijndaelManaged> 클래스를 사용하여 새 세션 키를 만듭니다.  이 키는 XML 요소를 암호화한 다음 자체 암호화되어 XML 문서에 배치됩니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
6. <xref:System.Security.Cryptography.Xml.EncryptedXml> 클래스의 새 인스턴스를 만들고 세션 키를 사용하여 지정된 요소를 암호화하는 데 사용합니다.  <xref:System.Security.Cryptography.Xml.EncryptedXml.EncryptData%2A> 메서드는 암호화된 요소를 암호화된 바이트 배열로 반환합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
7. <xref:System.Security.Cryptography.Xml.EncryptedData> 개체를 생성하고 암호화된 XML 요소의 URL 식별자로 채웁니다.  이 URL 식별자를 통해 암호 해독하는 당사자가 XML에 암호화된 요소가 들어 있음을 알 수 있습니다.  <xref:System.Security.Cryptography.Xml.EncryptedXml.XmlEncElementUrl> 필드를 사용하여 URL 식별자를 지정할 수 있습니다.  일반 텍스트 XML 요소는 이 <xref:System.Security.Cryptography.Xml.EncryptedData> 개체에 의해 캡슐화된 <`EncryptedData`> 요소로 대체됩니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
8. 세션 키를 생성하는 데 사용되는 암호화 알고리즘의 URL 식별자로 초기화되는 <xref:System.Security.Cryptography.Xml.EncryptionMethod> 개체를 만듭니다.  <xref:System.Security.Cryptography.Xml.EncryptionMethod> 개체를 <xref:System.Security.Cryptography.Xml.EncryptedType.EncryptionMethod%2A> 속성에 전달합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#9)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#9)]  
  
9. 암호화된 세션 키를 포함할 <xref:System.Security.Cryptography.Xml.EncryptedKey> 개체를 만듭니다.  세션 키를 암호화하고, <xref:System.Security.Cryptography.Xml.EncryptedKey> 개체에 추가하고, 세션 키 이름 및 키 식별자 URL을 입력합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#10)]  
  
10. 암호화된 데이터를 특정 세션 키로 매핑하는 새로운 <xref:System.Security.Cryptography.Xml.DataReference> 개체를 만듭니다.  이 선택적 단계를 사용하면 XML 문서의 여러 부분이 단일 키로 암호화되었음을 쉽게 지정할 수 있습니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#11)]  
  
11. <xref:System.Security.Cryptography.Xml.EncryptedData> 개체에 암호화된 키를 추가합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#12)]  
  
12. 새로운 <xref:System.Security.Cryptography.Xml.KeyInfo> 개체를 만들어 RSA 키의 이름을 지정합니다.  <xref:System.Security.Cryptography.Xml.EncryptedData> 개체에 추가합니다. 이렇게 하면 암호 해독하는 당사자가 세션 키를 암호 해독할 때 사용할 올바른 비대칭 키를 식별하는 데 도움이 됩니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#13)]  
  
13. <xref:System.Security.Cryptography.Xml.EncryptedData> 개체에 암호화된 요소 데이터를 추가합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#14)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#14)]  
  
14. 원본 <xref:System.Xml.XmlDocument> 개체의 요소를 <xref:System.Security.Cryptography.Xml.EncryptedData> 요소로 바꿉니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#15)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#15)]  
  
15. <xref:System.Xml.XmlDocument> 개체를 저장합니다.  
  
     [!code-csharp[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#16)]
     [!code-vb[HowToEncryptXMLElementAsymmetric#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#16)]  
  
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
  
 [!code-csharp[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 예제를 컴파일하려면 `System.Security.dll`에 대한 참조를 포함해야 합니다.  
  
- <xref:System.Xml>, <xref:System.Security.Cryptography> 및 <xref:System.Security.Cryptography.Xml> 네임스페이스를 포함합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 대칭 암호화 키를 일반 텍스트로 저장하거나 컴퓨터 간에 일반 텍스트로 대칭 키를 전송하지 마세요.  또한 비대칭 키 쌍의 프라이빗 키를 일반 텍스트로 저장하거나 전송하지 마세요.  대칭 및 비대칭 암호화 키에 대 한 자세한 내용은 참조 하세요. [암호화 및 암호 해독용 키 생성](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)합니다.  
  
 소스 코드에 직접 키를 포함하지 마세요.  포함 된 키를 사용 하 여 어셈블리에서 쉽게 읽을 수 있습니다 합니다 [Ildasm.exe (IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 또는 메모장과 같은 텍스트 편집기에서 어셈블리를 열어.  
  
 암호화 키를 사용하여 작업이 완료되면 각 바이트를 0으로 설정하거나 관리되는 암호화 클래스의 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 메서드를 호출하여 메모리에서 지웁니다.  디버거가 메모리에서 암호화 키를 읽거나 메모리 위치가 디스크에 페이징된 경우 하드 드라이브에서 읽을 수 있는 경우도 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.Xml>
- [방법: 비대칭 키로 XML 요소 해독](../../../docs/standard/security/how-to-decrypt-xml-elements-with-asymmetric-keys.md)
