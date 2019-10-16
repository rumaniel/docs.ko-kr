---
title: '방법: XML 문서의 디지털 서명 확인'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.SignedXml class
- signatures, cryptographic
- System.Security.Cryptography.RSACryptoServiceProvider class
- verifying signatures
- checking signatures
- XML digital signatures
- digital signatures, verifying
ms.assetid: a4d5ceb1-b9f5-47e8-9e4a-a2b39110002f
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8be946a7d4937a00b8c1738735362c7cc0ecb163
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64602550"
---
# <a name="how-to-verify-the-digital-signatures-of-xml-documents"></a>방법: XML 문서의 디지털 서명 확인
<xref:System.Security.Cryptography.Xml> 네임스페이스의 클래스를 사용하여 디지털 서명으로 서명된 XML 데이터를 확인할 수 있습니다. XML 디지털 서명(XMLDSIG)을 사용하면 서명된 후 데이터가 변경되지 않았음을 확인할 수 있습니다. XMLDSIG 표준에 대 한 자세한 내용은 World Wide Web Consortium (W3C) 사양을 참조 <https://www.w3.org/TR/xmldsig-core/>합니다.
  
 이 절차의 코드 예제에 포함 된 XML 디지털 서명을 확인 하는 방법에 설명 된 <`Signature`> 요소입니다.  이 예제에서는 키 컨테이너에서 RSA 공개 키를 검색한 다음 키를 사용하여 서명을 확인합니다.  
  
 이 기술을 사용 하 여 확인할 수 있는 디지털 서명을 만드는 하는 방법에 대 한 정보를 참조 [방법: 디지털 서명 사용 하 여 XML 문서 서명](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)합니다.  
  
### <a name="to-verify-the-digital-signature-of-an-xml-document"></a>XML 문서의 디지털 서명을 확인하려면  
  
1. 문서를 확인하려면 서명에 사용된 것과 동일한 비대칭 키를 사용해야 합니다.  <xref:System.Security.Cryptography.CspParameters> 개체를 만들고 서명에 사용된 키 컨테이너의 이름을 지정합니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#2)]  
  
2. <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스를 사용하여 공개 키를 검색합니다.  <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스의 생성자에 <xref:System.Security.Cryptography.CspParameters> 개체를 전달하면 키가 이름을 기준으로 자동으로 키 컨테이너에서 로드됩니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#3)]  
  
3. 디스크에서 XML 파일을 로드하여 <xref:System.Xml.XmlDocument> 개체를 만듭니다.  <xref:System.Xml.XmlDocument> 개체에는 확인할 서명된 XML 문서가 들어 있습니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#4)]  
  
4. 새 <xref:System.Security.Cryptography.Xml.SignedXml> 개체를 만들고 <xref:System.Xml.XmlDocument> 개체를 전달합니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#5)]  
  
5. 찾을 <`signature`> 요소를 새 <xref:System.Xml.XmlNodeList> 개체입니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#6)]  
  
6. 첫 번째 XML을 로드 <`signature`> 요소는 <xref:System.Security.Cryptography.Xml.SignedXml> 개체입니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#7)]  
  
7. <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignature%2A> 메서드 및 RSA 공개 키를 사용하여 서명을 확인합니다.  이 메서드는 성공 또는 실패를 나타내는 부울 값을 반환합니다.  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#8)]  
  
## <a name="example"></a>예제  
 이 예제에서는 `"test.xml"`이라는 파일이 컴파일된 프로그램과 동일한 디렉터리에 있다고 가정합니다.  합니다 `"test.xml"` 에 설명 된 기술을 사용 하 여 파일에 서명 해야 [방법: 디지털 서명 사용 하 여 XML 문서 서명](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)합니다.  
  
 [!code-csharp[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 예제를 컴파일하려면 `System.Security.dll`에 대한 참조를 포함해야 합니다.  
  
- <xref:System.Xml>, <xref:System.Security.Cryptography> 및 <xref:System.Security.Cryptography.Xml> 네임스페이스를 포함합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 비대칭 키 쌍의 프라이빗 키를 일반 텍스트로 저장하거나 전송하지 마세요.  대칭 및 비대칭 암호화 키에 대 한 자세한 내용은 참조 하세요. [암호화 및 암호 해독용 키 생성](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)합니다.  
  
 소스 코드에 직접 프라이빗 키를 포함하지 마세요.  포함 된 키를 사용 하 여 어셈블리에서 쉽게 읽을 수 있습니다 합니다 [Ildasm.exe (IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 또는 메모장과 같은 텍스트 편집기에서 어셈블리를 열어.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Security.Cryptography.Xml>
- [방법: 디지털 서명 사용 하 여 XML 문서 서명](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)
