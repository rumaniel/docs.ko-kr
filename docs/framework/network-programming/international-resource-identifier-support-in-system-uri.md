---
title: System.Uri의 국가별 리소스 식별자 지원
ms.date: 03/30/2017
ms.assetid: b5e994c3-3535-4aff-8e1b-b69be22e9a22
ms.openlocfilehash: 742ea03a62426506f068a9b9e669278d0d4663ec
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50047152"
---
# <a name="international-resource-identifier-support-in-systemuri"></a>System.Uri의 국가별 리소스 식별자 지원
<xref:System.Uri?displayProperty=nameWithType> 클래스는 IRI(International Resource Identifier) 및 IDN(Internationalized Domain Names)을 통해 확장되었습니다. 이러한 향상된 기능은 .NET Framework 3.5, 3.0 SP1 및 2.0 SP1에서 사용할 수 있습니다.  
  
## <a name="iri-and-idn-support"></a>IRI 및 IDN 지원  
 웹 주소는 대개 매우 제한적인 문자 집합으로 구성된 URI(Uniform Resource Identifier)를 사용하여 표현됩니다.  
  
-   영문자의 대문자 및 소문자 ASCII 문자.  
  
-   0~9의 숫자.  
  
-   일부 기타 ASCII 기호.  
  
 URI 사양은 IETF(Internet Engineering Task Force)에서 게시한 RFC 2396 및 RFC 3986에 설명되어 있습니다.  
  
 인터넷이 성장하면서 영어 이외의 언어로 리소스를 식별해야 할 필요성이 증가하고 있습니다. 이 필요성을 가능하게 하고 ASCII 이외 문자(유니코드/ISO 10646 문자 집합의 문자)를 허용하는 식별자를 IRI(International Resource Identifier)라고 합니다. IRI 사양은 IETF에서 게시한 RFC 3987에 설명되어 있습니다. IRI를 사용하면 URL에 유니코드 문자를 포함할 수 있습니다.  
  
 기존 <xref:System.Uri?displayProperty=nameWithType> 클래스는 RFC 3987을 기반으로 IRI 지원을 제공하도록 확장되었습니다. 현재 사용자의 경우 IRI를 사용하도록 설정하지 않는 한 .NET Framework 2.0 동작에서 차이를 느끼지 못할 것입니다. 이 덕분에 .NET Framework 이전 버전과의 응용 프로그램 호환성이 제공됩니다.  
  
 응용 프로그램은 도메인 이름에 적용되는 IDN(다국어 도메인 이름) 구문 분석을 사용할지 여부와 IRI 구문 분석 규칙을 적용할지 여부를 지정할 수 있습니다. 이 설정은 machine.config 또는 app.config 파일에서 지정할 수 있습니다.  
  
 IDN을 사용하면 도메인 이름의 모든 유니코드 레이블이 해당 Punycode 문자로 변환됩니다. Punycode 이름에는 ASCII 문자만 사용되며 항상 xn-- 접두사로 시작합니다. 대부분의 DNS 서버는 ASCII 문자만 지원하므로(RFC 3940 참조) 이렇게 해야 인터넷에서 기존 DNS 서버를 지원할 수 있습니다.  
  
 IRI 및 IDN을 사용하도록 설정하면 <xref:System.Uri.DnsSafeHost%2A?displayProperty=nameWithType> 속성 값에 영향을 줍니다. IRI 및 IDN을 사용하면 <xref:System.Uri.Equals%2A?displayProperty=nameWithType>, <xref:System.Uri.OriginalString%2A?displayProperty=nameWithType>, <xref:System.Uri.GetComponents%2A?displayProperty=nameWithType> 및 <xref:System.Uri.IsWellFormedOriginalString%2A> 메서드의 동작을 변경할 수도 있습니다.  
  
 또한 <xref:System.GenericUriParser?displayProperty=nameWithType> 클래스는 IRI 및 IDN을 지원하는 사용자 지정 가능한 파서를 만들 수 있도록 확장되었습니다. <xref:System.GenericUriParser?displayProperty=nameWithType> 개체의 동작은 <xref:System.GenericUriParserOptions?displayProperty=nameWithType> 열거형에서 사용 가능한 값의 비트 조합을 <xref:System.GenericUriParser?displayProperty=nameWithType> 생성자에 전달하여 지정합니다. <xref:System.GenericUriParserOptions.IriParsing?displayProperty=nameWithType> 형식은 파서가 RFC 3987에 지정된 IRI(International Resource Identifier)에 대한 구문 분석 규칙을 지원함을 나타냅니다. IRI가 실제로 사용되는지 여부는 IRI가 사용하도록 설정되었는지에 따라 다릅니다.  
  
 <xref:System.GenericUriParserOptions.Idn?displayProperty=nameWithType> 형식은 파서가 호스트 이름의 IDN(Internationalized Domain Name) 구문 분석을 지원함을 나타냅니다. IDN이 실제로 사용되는지 여부는 IDN이 사용하도록 설정되었는지에 따라 다릅니다.  
  
 IRI 구문 분석을 사용하도록 설명하면 RFC 3987의 최신 IRI 규칙에 따라 정규화 및 문자 검사가 수행됩니다. IRI 구문 분석의 기본값은 사용하지 않도록 설정되는 것이므로 정규화 및 문자 검사는 RFC 2396 및 RFC 3986에 따라 수행됩니다.  
  
 <xref:System.Uri?displayProperty=nameWithType> 클래스의 IRI 및 IDN 처리는 <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> 및 <xref:System.Configuration.IdnElement?displayProperty=nameWithType> 구성 설정 클래스를 사용하여 제어할 수도 있습니다. <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> 설정은 <xref:System.Uri?displayProperty=nameWithType> 클래스에서 IRI 처리를 사용하거나 사용하지 않도록 설정합니다. <xref:System.Configuration.IdnElement?displayProperty=nameWithType> 설정은 <xref:System.Uri> 클래스에서 IDN 처리를 사용하거나 사용하지 않도록 설정합니다. <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> 설정도 IDN을 간접적으로 제어합니다. IDN 처리가 가능하려면 IRI 처리를 사용하도록 설정해야 합니다. IRI 처리가 사용하지 않도록 설정되면 IDN 처리는 .NET Framework 2.0 동작이 호환성에 사용되고 IDN 이름이 사용되지 않는 기본 설정으로 지정됩니다.  
  
 <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType> 및 <xref:System.Configuration.IdnElement?displayProperty=nameWithType> 구성 클래스에 대한 구성 설정은 첫 번째 <xref:System.Uri?displayProperty=nameWithType> 클래스가 생성될 때 한 번 판독됩니다. 해당 시점 후의 구성 설정 변경 내용은 무시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 <xref:System.Configuration.IdnElement?displayProperty=nameWithType>  
 <xref:System.Configuration.IriParsingElement?displayProperty=nameWithType>  
 <xref:System.Uri?displayProperty=nameWithType>  
 <xref:System.Uri.DnsSafeHost%2A?displayProperty=nameWithType>
