---
title: '방법: 대칭 키를 사용하여 XML 요소 해독'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- symmetric keys
- System.Security.Cryptography.EncryptedXml class
- System.Security.Cryptography.RijndaelManaged class
- XML encryption
- Rijndael
- decryption
ms.assetid: 6038aff0-f92c-4e29-a618-d793410410d8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f45ba28a4c2d4ab56abf15f8e8b5ba4c6cb7d611
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64602722"
---
# <a name="how-to-decrypt-xml-elements-with-symmetric-keys"></a>방법: 대칭 키를 사용하여 XML 요소 해독
<xref:System.Security.Cryptography.Xml> 네임스페이스의 클래스를 사용하여 XML 문서 내의 요소를 암호화할 수 있습니다.  XML 암호화를 사용하면 데이터가 쉽게 읽혀질 염려 없이 중요한 XML을 저장하거나 전송할 수 있습니다.  이 코드 예제에서는 Rijndael이라고도 하는 AES(고급 암호화 표준) 알고리즘을 사용하여 XML 요소를 암호 해독합니다.  
  
 이 절차를 사용 하 여 XML 요소를 암호화 하는 방법에 대 한 정보를 참조 하세요. [방법: 대칭 키를 사용 하 여 XML 요소 암호화](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)합니다.  
  
 AES와 같은 대칭 알고리즘을 사용하여 XML 데이터를 암호화하는 경우 동일한 키를 사용하여 XML 데이터를 암호화하고 암호 해독해야 합니다.  이 절차의 예제에서는 동일한 키를 사용하여 암호화된 XML이 암호화되었으며 암호화 및 암호 해독하는 당사자가 알고리즘 및 사용할 키에 대해 동의한다고 가정합니다.  이 예제에서는 암호화된 XML 내의 AES 키를 저장하거나 암호화하지 않습니다.  
  
 이 예제는 단일 애플리케이션에서 메모리에 저장된 세션 키 또는 암호에서 파생된 강력한 암호화 키를 기반으로 하여 데이터를 암호화해야 하는 경우에 적합합니다.  둘 이상의 애플리케이션에서 암호화된 XML 데이터를 공유해야 하는 경우 비대칭 알고리즘 또는 X.509 인증서를 기반으로 하는 암호화 체계를 사용하는 것이 좋습니다.  
  
### <a name="to-decrypt-an-xml-element-with-a-symmetric-key"></a>대칭 키를 사용하여 XML 요소를 암호 해독하려면  
  
1. 에 설명 된 기술을 사용 하 여 이전에 생성 된 키를 사용 하 여 XML 요소 암호화 [방법: 대칭 키를 사용 하 여 XML 요소 암호화](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)합니다.  
  
2. 찾을 <`EncryptedData`> 요소 (XML 암호화 표준에 의해 정의 됨)에 <xref:System.Xml.XmlDocument> 암호화 된 XML을 포함 하는 개체 및 새 <xref:System.Xml.XmlElement> 해당 요소를 나타내는 개체입니다.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#10)]
     [!code-vb[HowToEncryptXMLElementSymmetric#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#10)]  
  
3. 이전에 만든 <xref:System.Xml.XmlElement> 개체에서 원시 XML 데이터를 로드하여 <xref:System.Security.Cryptography.Xml.EncryptedData> 개체를 만듭니다.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#11)]
     [!code-vb[HowToEncryptXMLElementSymmetric#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#11)]  
  
4. 새 <xref:System.Security.Cryptography.Xml.EncryptedXml> 개체를 만들고 암호화에 사용된 것과 동일한 키로 XML 데이터를 암호 해독하는 데 사용합니다.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#12)]
     [!code-vb[HowToEncryptXMLElementSymmetric#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#12)]  
  
5. 암호화된 요소를 XML 문서 내에서 새로 암호 해독된 일반 텍스트 요소로 바꿉니다.  
  
     [!code-csharp[HowToEncryptXMLElementSymmetric#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#13)]
     [!code-vb[HowToEncryptXMLElementSymmetric#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#13)]  
  
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
  
 [!code-csharp[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/cs/sample.cs#1)]
 [!code-vb[HowToEncryptXMLElementSymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToEncryptXMLElementSymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 예제를 컴파일하려면 `System.Security.dll`에 대한 참조를 포함해야 합니다.  
  
- <xref:System.Xml>, <xref:System.Security.Cryptography> 및 <xref:System.Security.Cryptography.Xml> 네임스페이스를 포함합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 암호화 키를 일반 텍스트로 저장하거나 컴퓨터 간에 일반 텍스트로 키를 전송하지 마세요.  
  
 대칭 암호화 키를 사용하여 작업이 완료되면 각 바이트를 0으로 설정하거나 관리되는 암호화 클래스의 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 메서드를 호출하여 메모리에서 지웁니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.Xml>
- [방법: 대칭 키를 사용 하 여 XML 요소 암호화](../../../docs/standard/security/how-to-encrypt-xml-elements-with-symmetric-keys.md)
