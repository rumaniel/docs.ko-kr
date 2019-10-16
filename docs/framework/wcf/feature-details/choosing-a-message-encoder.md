---
title: 메시지 인코더 선택
ms.date: 03/30/2017
ms.assetid: 2204d82d-d962-4922-a79e-c9a231604f19
ms.openlocfilehash: 93024258ddcf76444d48a19c071b0a18248ea46b
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645475"
---
# <a name="choosing-a-message-encoder"></a>메시지 인코더 선택
이 항목에서는 Windows Communication Foundation (WCF)에 포함 된 메시지 인코더 선택 기준에 설명 합니다: 이진, 텍스트 및 전송 최적화 메커니즘 MTOM (Message).  
  
 Wcf에서 이용 하 여 끝점 간에 네트워크를 통해 데이터를 전송 하는 방법을 지정할를 *바인딩*, 시퀀스로 구성 됩니다 *바인딩 요소*합니다. 메시지 인코더는 바인딩 스택에서 바인딩 요소를 인코딩하는 메시지로 표시됩니다. 바인딩에는 보안 바인딩 요소 또는 신뢰할 수 있는 메시징 바인딩 요소, 필수 메시지 인코딩 바인딩 요소, 필수 전송 바인딩 요소와 같은 선택적 프로토콜 바인딩 요소가 포함됩니다.  
  
 메시지 인코딩 바인딩 요소는 선택적 프로토콜 바인딩 요소보다는 아래에, 필수 전송 바인딩 요소보다는 위에 있습니다. 나가는 쪽에서는 메시지 인코더가 나가는 <xref:System.ServiceModel.Channels.Message>를 serialize하고 이를 전송에 전달합니다. 들어오는 쪽에서는 메시지 인코더가 전송으로부터 <xref:System.ServiceModel.Channels.Message>의 serialize된 형식을 받고, 더 높은 프로토콜 계층이 있으면 해당 계층으로 이를 전달하며, 더 높은 계층이 없으면 이를 애플리케이션으로 전달합니다.  
  
 기존 클라이언트 또는 서버에 연결할 때는 다른 쪽에서 원하는 방식으로 메시지를 인코딩해야 하므로 특정 메시지의 인코딩 사용을 선택하지 못할 수도 있습니다. 그러나 WCF 서비스를 작성 하는 경우 노출할 수 있습니다 여러 끝점을 통해 서비스 각각 다른 메시지 인코딩을 사용 하 여. 이를 통해 클라이언트는 가장 적합한 인코딩을 선택할 수 있는 유연성을 가질 뿐만 아니라 가장 적합한 엔드포인트를 통해 서비스와 통신하기 위한 최적의 인코딩을 선택할 수 있습니다. 여러 엔드포인트를 사용하면 여러 메시지 인코딩의 이점을 다른 바인딩 요소와 결합할 수도 있습니다.  
  
## <a name="system-provided-encoders"></a>시스템 제공 인코더  
 WCF에는 다음 세 가지 클래스로 표현 되는 세 가지 메시지 인코더가 포함 됩니다.  
  
- <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>: 텍스트 메시지 인코더로, 일반 XML 인코딩 및 SOAP 인코딩을 모두 지원합니다. 텍스트 메시지 인코더의 일반 XML 인코딩 모드는 텍스트 기반 SOAP 인코딩과 구별하기 위해 POX("Plain Old Xml")라고 합니다. POX를 사용하도록 설정하려면 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement.MessageVersion%2A> 속성을 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>으로 설정합니다. 비 WCF 끝점을 사용 하 여 상호 운용 하도록 텍스트 메시지 인코더를 사용 합니다.  
  
- <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>이진 메시지 인코더로, 간단한 이진 형식을 사용 하 여 WCF 통신 하도록 WCF에 대 한 최적화 및 상호 운용은 불가능 합니다. WCF에서 제공 하는 모든 인코더 중 대부분의 성능이 좋은 인코더 이기도 합니다.  
  
- <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>: 바인딩 요소로, MTOM 인코딩을 사용하여 메시지에 대해 메시지 버전 및 문자 인코딩을 지정합니다. MTOM은 WCF 메시지의 이진 데이터를 전송하기 위한 효율적인 기술입니다. MTOM 인코더는 효율성과 상호 운용성 간의 균형을 유지하려고 합니다. MTOM 인코딩은 대부분의 XML을 텍스트 형식으로 전송하지만, 큰 이진 데이터 블록의 경우에는 텍스트로 변환하지 않고 있는 그대로 전송하여 최적화합니다. WCF는 제공 인코더 중 효율성 측면에서 MTOM은 중간 텍스트 (가장 느림) 및 이진 (가장 빠름)입니다.  
  
## <a name="how-to-choose-a-message-encoder"></a>메시지 인코더를 선택하는 방법  
 다음 표에서는 메시지 인코더를 선택하는 데 사용하는 일반 요소에 대해 설명합니다. 애플리케이션의 중요한 요소에 우선 순위를 지정한 다음 이러한 요소에 가장 적합한 메시지 인코더를 선택합니다. 이 표에 나열되지 않은 모든 추가 요소 및 애플리케이션에 필요할 수 있는 모든 사용자 지정 메시지 인코더를 고려해야 합니다.  
  
|요소|설명|이 요소를 지원하는 인코더|  
|------------|-----------------|---------------------------------------|  
|지원되는 문자 집합|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 및 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> UTF8 및 UTF16 유니코드 지원 (*big endian* 하 고 *little endian*) 인코딩. UTF7 또는 ASCII와 같은 다른 인코딩이 필요한 경우 사용자 지정 인코더를 사용해야 합니다. 샘플 사용자 지정 인코더를 참조 하세요 [사용자 지정 메시지 인코더](https://go.microsoft.com/fwlink/?LinkId=119857)합니다.|텍스트|  
|검사|검사는 전송을 하는 동안 메시지를 검사하는 기능입니다. SOAP의 사용 여부에 관계없이 특수화된 도구를 사용하지 않고도 텍스트 인코딩을 통해 많은 애플리케이션에서 메시지를 검사 및 분석할 수 있습니다. 메시지 수준 또는 전송 수준에서 전송 보안을 사용하면 메시지 검사 기능에 영향을 줍니다. 기밀성은 메시지를 검사하지 않도록 보호해주며 무결성은 메시지를 수정하지 않도록 보호해줍니다.|텍스트|  
|안정성|안정성은 전송 오류에 대한 인코더의 유연성을 말합니다. 안정성을 메시지, 전송 또는 애플리케이션 계층에서 제공할 수도 있습니다. 표준 WCF 인코더의 모든 다른 계층이 안정성 제공 하는 것을 가정 합니다. 인코더에는 전송 오류를 복구하는 기능이 거의 없습니다.|없음|  
|단순성|단순성은 인코딩 사양에 대해 인코더 및 디코더를 쉽게 만들 수 있음을 나타냅니다. 텍스트 인코딩은 특히 단순성을 위해 도움이 되며, POX 텍스트 인코딩은 SOAP 처리에 대한 지원을 필요로 하지 않는다는 추가 이점도 제공합니다.|텍스트(POX)|  
|크기|인코딩은 콘텐츠에 적용되는 오버헤드의 양을 결정합니다. 인코딩된 메시지의 크기는 서비스 작업의 최대 처리량과 직접적으로 연관됩니다. 일반적으로 이진 인코딩이 텍스트 인코딩보다 간결합니다. 메시지 크기가 최상일 경우 인코딩을 하는 동안 메시지 내용을 압축하는 것도 고려하십시오. 그러나 압축을 하면 메시지 발신자와 수신자 둘 다의 처리 공간이 추가됩니다.|이항|  
|스트리밍|스트리밍을 통해 전체 메시지가 도착하기 전에 애플리케이션에서 메시지 처리를 시작할 수 있습니다. 스트리밍을 효과적으로 사용하려면 수신 애플리케이션에서 메시지가 전부 도착할 때까지 기다리지 않아도 되도록 메시지의 시작 부분에서 메시지의 중요 데이터를 사용할 수 있어야 합니다. 또한 스트리밍 전송을 사용하는 애플리케이션은 해당 콘텐츠가 정방향 종속성을 가지지 않도록 메시지의 데이터를 점증적으로 구성해야 합니다. 대부분의 경우 콘텐츠를 스트리밍하는 것과 해당 콘텐츠의 가능한 최소 전송 크기를 갖는 것 중에 선택해야 합니다.|없음|  
|타사 도구 지원|인코딩에 대한 지원 영역에는 개발 및 진단이 포함됩니다. 타사 개발자는 POX 형식으로 인코딩된 메시지를 처리하기 위해 라이브러리 및 도구 키트에 대규모 투자를 해왔습니다.|텍스트(POX)|  
|상호 운용성|이 요소는 비 WCF 서비스와 상호 운용 하도록 WCF 인코더의 기능을 참조 합니다.|텍스트<br /><br /> MTOM(부분)|  
  
참고: 이진 인코더를 사용할 경우 XMLReader를 만들 때 IgnoreWhitespace 설정을 사용 하는 효과가 없습니다.  예를 들어, 서비스 작업 안에서 다음을 수행하는 경우를 가정해 봅니다.  

```csharp
public void OperationContract(XElement input)
{
    Console.WriteLine("{0}", input.Value);
    int counter = 0;
    var xreader = input.CreateReader();
    var reader = XmlReader.Create(xreader, new XmlReaderSettings() { IgnoreWhitespace = true });
    while (reader.Read())
    {
        counter++;
    }

    Console.WriteLine("Read {0} lines with reader", counter);
}
```  
  
IgnoreWhitespace 설정이 무시됩니다.  
  
## <a name="compression-and-the-binary-encoder"></a>압축 및 이진 인코더

WCF 4.5부터는 WCF 이진 인코더에서 압축을 추가 지원합니다. 그러면 WCF 클라이언트에서 압축 메시지를 보낼 때 gzip/deflate 알고리즘을 사용하고 자체 호스팅된 WCF 서비스의 압축 메시지에 응답할 수 있습니다. 이 기능을 사용하면 HTTP 및 TCP 전송 모두에서 압축이 가능합니다. IIS 호스트 서버를 구성하면 IIS에서 호스팅된 WCF 서비스에서 언제나 압축된 응답을 보낼 수 있습니다. 압축 형식은 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.CompressionFormat%2A?displayProperty=nameWithType> 속성에서 구성합니다. 이 속성은 <xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=nameWithType> 열거형의 값 중 하나로 설정됩니다.

- <xref:System.ServiceModel.Channels.CompressionFormat.Deflate>
- <xref:System.ServiceModel.Channels.CompressionFormat.GZip>
- <xref:System.ServiceModel.Channels.CompressionFormat.None>
  
이 속성은 binaryMessageEncodingBindingElement에 노출만 있으므로이 기능을 사용 하려면 다음과 같은 사용자 지정 바인딩을 만드는 해야 합니다.

 ```xml
 <customBinding>
   <binding name="BinaryCompressionBinding">
     <binaryMessageEncoding compressionFormat ="GZip" />
     <httpTransport />
  </binding>
</customBinding>
 ```

클라이언트와 서비스 모두 압축된 메시지를 받고 보내는 데 동의 해야 하 고 따라서 compressionFormat 속성은 클라이언트와 서비스 둘 다의 binaryMessageEncoding 요소에 구성 되어야 합니다. 서비스 또는 클라이언트가 압축에 대해 구성되지 않은 경우 ProtocolException이 throw되지만 다른 측의 is.Enabling 압축은 주의하여 고려해야 합니다. 네트워크 대역폭이 병목인 경우 압축이 가장 유용합니다. CPU가 병목인 경우 압축을 수행하면 처리량이 감소합니다. 이렇게 하는 것이 애플리케이션에 좋은지 알아 보려면 시뮬레이션 환경에서 적절한 테스트를 수행해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [바인딩](../../../../docs/framework/wcf/feature-details/bindings.md)
