---
title: 큰 데이터 및 스트리밍
ms.date: 03/30/2017
ms.assetid: ab2851f5-966b-4549-80ab-c94c5c0502d2
ms.openlocfilehash: 70e43eaf4dc77e07af8ec65faf9cf0fa9a7a0fe4
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991515"
---
# <a name="large-data-and-streaming"></a>큰 데이터 및 스트리밍
WCF (Windows Communication Foundation)는 XML 기반 통신 인프라입니다. XML 데이터는 일반적으로 [xml 1.0 사양](https://go.microsoft.com/fwlink/?LinkId=94838)에 정의 된 표준 텍스트 형식으로 인코딩되어 있으므로 연결 된 시스템 개발자와 설계자는 일반적으로 네트워크를 통해 전송 되는 메시지의 공간 (또는 크기)에 대해 염려 하 고 XML의 텍스트 기반 인코딩을 사용 하면 이진 데이터를 효율적으로 전송할 때 특별 한 과제가 발생 합니다.  
  
## <a name="basic-considerations"></a>기본 고려 사항  
 WCF에 대 한 다음 정보에 대 한 배경 정보를 제공 하기 위해이 섹션에서는 일반적으로 연결 된 시스템 인프라에 적용 되는 인코딩, 이진 데이터 및 스트리밍에 대 한 몇 가지 일반적인 문제 및 고려 사항을 강조 표시 합니다.  
  
### <a name="encoding-data-text-vs-binary"></a>데이터 인코딩: 텍스트 및 이항  
 개발자가 일반적으로 말하는 고려 사항에는 XML에 시작 태그와 끝 태그가 반복된다는 점 때문에 이진 형식에 비해 오버헤드가 크다는 점, 숫자 값의 인코딩이 텍스트 값으로 표현되기 때문에 너무 크다는 점, 이진 데이터를 텍스트 형식으로 포함하려면 특수 인코딩이 필요하기 때문에 효과적인 표현이 어렵다는 점 등이 있습니다.  
  
 이러한 종류의 고려 사항 중에는 유용한 것도 많지만, XML 웹 서비스 환경의 XML 텍스트 인코딩 메시지와 레거시 RPC(원격 프로시저 호출) 환경의 이진 인코딩 메시지 사이의 실질적인 차이는 초기 고려 사항에서 제안하는 것만큼 심각하지는 않습니다.  
  
 XML 텍스트 인코딩 메시지는 투명하며, "사람이 인식할 수 있는" 형태로 되어 있지만, 이진 메시지는 그보다 모호해서 도구가 없이는 해독하기가 어렵습니다. 이러한 가독성의 차이 때문에 이진 메시지 역시 페이로드 내에 인라인 메타데이터가 포함되어 XML 텍스트 메시지와 마찬가지로 오버헤드를 가중시키는 일이 많다는 것을 간과하기가 쉽습니다. 느슨한 결합 및 동적 호출 기능을 제공할 목적으로 사용되는 이진 형식의 경우 특히 그러합니다.  
  
 이진 형식 역시 뒤에 있는 데이터 레코드의 데이터 레이아웃을 선언하는 그러한 설명 메타데이터 정보를 "헤더"에 포함합니다. 그러면 이 공용 메타데이터 블록 선언 뒤에 페이로드가 오며 추가 오버헤드를 최소화합니다. 한편, XML은 요소 또는 특성에 있는 각 데이터 항목을 기호로 묶어 serialize되는 각 페이로드 개체에 묶는 메타데이터를 반복적으로 포함합니다. 따라서 텍스트와 이진 표현 모두에서 몇 가지 설명적인 메타데이터를 나타내야 하기 때문에 serialize된 단일 페이로드 개체의 크기가 매우 비슷하지만, 전송되는 각각의 추가 페이로드 개체가 있는 경우 이진 형식은 공유 메타데이터 설명을 활용할 때 전체적인 오버헤드가 낮아진다는 이점이 있습니다.  
  
 하지만 숫자와 같은 특정 데이터 형식의 경우 일반 텍스트 대신 128비트 10진수 형식을 사용하는 등 고정된 크기의 이진 숫자 표현을 사용하는 것이 불리할 수도 있습니다. 일반 텍스트 표현이 몇 바이트라도 더 작을 수가 있기 때문입니다. 일부 이진 형식이 기본적으로 16비트 또는 32비트 유니코드를 사용하는 반면, 일반적으로 XML 텍스트 인코딩 선택은 더 유연하기 때문에 텍스트 데이터에도 크기 상의 이점이 있을 수 있습니다. 하지만 .NET 이진 XML 형식에는 이 사항이 적용되지 않습니다.  
  
 따라서 텍스트와 이진 사이에서 선택할 때 이진 메시지가 항상 XML 텍스트 메시지보다 작을 것이라고 쉽게 가정할 수가 없습니다.  
  
 XML 텍스트 메시지의 분명한 이점은 표준 기반이며 넓은 상호 운용성 옵션 및 플랫폼 지원을 제공한다는 것입니다. 자세한 내용은이 항목의 뒷부분에 나오는 "인코딩" 단원을 참조 하십시오.  
  
### <a name="binary-content"></a>이진 콘텐츠  
 결과 메시지의 크기 면에서 이진 인코딩이 텍스트 기반 인코딩보다 우수한 영역은 그림, 비디오, 사운드 클립 또는 서비스와 소비자 사이에서 교환해야 하는 기타 형식의 불투명한 이진 데이터입니다. 이러한 형식의 데이터를 XML 텍스트에 넣기 위해 일반적으로 사용하는 방법은 Base64 인코딩을 사용하여 인코딩하는 것입니다.  
  
 Base64 인코딩된 문자열에서 각 문자는 원래 8비트 데이터 중 6비트를 나타내며, 따라서 규칙에 따라 일반적으로 추가되는 추가 형식 문자(캐리지 리턴/줄 바꿈)를 제외하고 Base64에서 인코딩 오버헤드 비율은 4:3이 됩니다. XML과 이진 인코딩 사이의 차이가 갖는 심각도는 일반적으로 시나리오에 따라 결정되지만, 500MB의 페이로드를 전송하면서 크기가 33% 이상 증가한다면 보통은 적절하지 못한 것으로 봅니다.  
  
 이 인코딩 오버헤드를 방지하기 위해 MTOM(Message Transmission Optimization Mechanism) 표준에서는 메시지에 포함된 큰 데이터 요소를 구체화하여 특별한 인코딩 없이도 메시지와 함께 이진 데이터로서 전달할 수 있습니다. MTOM을 사용 하는 경우 메시지는 첨부 파일이 나 포함 된 콘텐츠 (그림 및 기타 포함 된 콘텐츠)를 포함 하는 SMTP (Simple Mail Transfer Protocol) 전자 메일 메시지와 비슷한 방식으로 교환 됩니다. MTOM 메시지는 루트 부분을 실제 SOAP 메시지로 사용 하는 다중 파트/관련 MIME 시퀀스로 패키지 됩니다.  
  
 MTOM SOAP 메시지는 해당 MIME 부분을 참조하는 특수 요소 태그가 이진 데이터를 포함하는 메시지에서 원래 요소의 자리를 차지하도록 인코딩되지 않은 버전에서 수정됩니다. 따라서 SOAP 메시지는 함께 전송되는 MIME을 가리키는 방식으로 이진 콘텐츠를 참조하고, 그 외의 경우에는 XML 텍스트 데이터만 전달합니다. 이 모델이 잘 구성된 SMTP 모델과 매우 가깝기 때문에 MTOM 메시지의 인코딩 및 디코딩 도구를 폭 넓게 지원하여 상호 운용성을 극대화하는 플랫폼도 많습니다.  
  
 하지만 Base64와 마찬가지로, MTOM 역시 MIME 형식에 필요한 몇 가지 오버헤드를 동반하기 때문에 MTOM을 사용하는 경우의 장점은 이진 데이터 요소의 크기가 약 1KB를 넘는 경우에만 실감할 수 있습니다. 이진 페이로드가 이 임계값 아래로만 유지되는 경우에는 오버헤드로 인해 MTOM 인코딩 메시지가 이진 데이터에 Base64 인코딩을 사용하는 메시지보다 커질 수 있습니다. 자세한 내용은이 항목의 뒷부분에 나오는 "인코딩" 단원을 참조 하십시오.  
  
### <a name="large-data-content"></a>큰 데이터 콘텐츠  
 와이어 크기를 고려하지 않더라도, 앞에서 언급한 500MB 페이로드는 서비스 및 클라이언트에 큰 로컬 과제를 남깁니다. 기본적으로 WCF는 *버퍼링 모드로*메시지를 처리 합니다. 즉, 메시지의 전체 콘텐츠가 보내기 전과 받은 후에 메모리에 보관됩니다. 대부분의 시나리오에서는 좋은 전략이며, 디지털 서명 및 안정적인 배달 등의 메시징 기능에 필수적인 방법이지만, 큰 메시지를 전달하는 경우에는 시스템 리소스가 빠른 속도로 소모될 수 있습니다.  
  
 큰 페이로드를 처리하는 전략은 스트리밍입니다. 메시지, 특히 XML로 표현되는 메시지는 일반적으로 비교적 압축된 데이터 패키지로 인식되지만, 메시지의 크기가 여러 기가바이트에 달할 수도 있으며, 데이터 패키지보다는 연속적인 데이터 스트림과 비슷한 경우도 있습니다. 버퍼링 모드 대신 스트리밍 모드를 사용하여 데이터를 전송하면 보내는 사람은 메시지 본문의 콘텐츠를 스트림의 형태로 받는 사람이 사용할 수 있게 만들고, 메시지 인프라에서는 데이터를 사용할 수 있게 되는대로 보내는 사람에게서 받는 사람에게로 계속 전달합니다.  
  
 그러한 큰 데이터 콘텐츠의 전송이 이루어지는 가장 흔한 시나리오는 다음과 같은 이진 데이터 개체를 전송하는 경우입니다.  
  
- 메시지 시퀀스로 쉽게 분해할 수 없음  
  
- 시기 적절하게 배달되어야 함  
  
- 전송을 시작할 때 전체를 사용할 수 없는 데이터.  
  
 이러한 제약이 없는 데이터의 경우에는 보통 큰 메시지 하나보다 세션 범위 내의 메시지 시퀀스로 보내는 것이 더 좋습니다. 자세한 내용은이 항목의 뒷부분에 나오는 "스트리밍 데이터" 섹션을 참조 하세요.  
  
 많은 양의 데이터를 전송 하는 경우 `maxAllowedContentLength` iis 설정 (자세한 내용은 [iis 요청 제한 구성](https://go.microsoft.com/fwlink/?LinkId=253165)참조) 및 `maxReceivedMessageSize` 바인딩 설정 (예: [)을 설정 해야 합니다. MaxReceivedMessageSize](xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A) 또는 <xref:System.ServiceModel.NetTcpBinding.MaxReceivedMessageSize%2A>). 속성 `maxAllowedContentLength` 의 기본값은 28.6 M 이며 기본값 `maxReceivedMessageSize` 은 64kb입니다.  
  
## <a name="encodings"></a>인코딩  
 *인코딩은* 통신 중에 메시지를 표시 하는 방법에 대 한 규칙 집합을 정의 합니다. *인코더* 는 이러한 인코딩을 구현 하 고 발신자 쪽에서 메모리 <xref:System.ServiceModel.Channels.Message> 내를 바이트 스트림 또는 네트워크를 통해 전송 될 수 있는 바이트 버퍼로 전환 하는 일을 담당 합니다. 받는 쪽에서는 인코더가 바이트 시퀀스를 메모리 내 메시지로 변환합니다.  
  
 WCF는 세 개의 인코더를 포함 하며 필요한 경우 사용자 고유의 인코더를 작성 하 고 연결할 수 있습니다.  
  
 각각의 표준 바인딩에는 미리 구성된 인코더가 포함되며, Net* 접두사가 있는 바인딩에서는 이진 인코더를 사용하고(<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> 클래스를 포함하는 방법으로) <xref:System.ServiceModel.BasicHttpBinding> 및 <xref:System.ServiceModel.WSHttpBinding> 클래스에서는 기본적으로 텍스트 메시지 인코더(<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 클래스 사용)를 사용합니다.  
  
|인코더 바인딩 요소|Description|  
|-----------------------------|-----------------|  
|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>|텍스트 메시지 인코더는 모든 HTTP 기반 바인딩의 기본 인코더이며 상호 운용성이 중요한 모든 사용자 지정 바인딩에 적절합니다. 이 인코더에서는 이진 데이터를 특수 처리하지 않는 표준 SOAP 1.1/SOAP 1.2 텍스트 메시지를 읽고 씁니다. 메시지의 <xref:System.ServiceModel.Channels.MessageVersion.None?displayProperty=nameWithType>속성이로 설정 된 경우 SOAP 봉투 래퍼가 출력에서 생략 되 고 메시지 본문 내용만 serialize 됩니다. <xref:System.ServiceModel.Channels.MessageVersion?displayProperty=nameWithType>|  
|<xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>|MTOM 메시지 인코더는 이진 데이터의 특수 처리를 구현하는 텍스트 인코더이며, 엄격한 경우별 최적화 유틸리티이기 때문에 표준 바인딩에서는 전혀 기본으로 사용되지 않습니다. MTOM 인코딩이 장점을 제공하는 임계값을 초과하는 이진 데이터가 메시지에 포함되어 있으면, 데이터가 메시지 봉투 뒤의 MIME 부분에 구체화됩니다. 이 단원의 뒷부분에 있는 MTOM 활성화를 참조하십시오.|  
|<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>|이진 메시지 인코더는 Net * 바인딩의 기본 인코더 이며 통신 당사자가 모두 WCF를 기반으로 하는 경우 적절 한 선택입니다. 이진 메시지 인코더에서는 .NET 이진 XML 형식을 사용합니다. 이 형식은 일반적으로 동급 XML 1.0 표현보다 크기가 작으며 이진 데이터를 바이트 스트림으로 인코딩하는 XML Infoset을 나타내는 Microsoft만의 이진 표현입니다.|  
  
 텍스트 메시지 인코딩은 보통 상호 운용성이 필요한 모든 통신 경로에 적합하고, 이진 메시지 인코딩은 다른 모든 통신 경로에 적합합니다. 이진 메시지 인코딩은 보통 단일 메시지의 텍스트보다 메시지 크기가 작으며, 통신 세션이 진행될수록 점점 더 메시지 크기가 작아집니다. 텍스트 인코딩과 달리, 이진 인코딩에서는 Base64 사용과 같은 특수 이진 데이터 처리를 수행할 필요가 없으며 바이트를 바이트로 표현합니다.  
  
 솔루션에 상호 운용성이 필요 없지만 여전히 HTTP 전송을 사용하려는 경우에는 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>를 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 클래스를 전송에 사용하는 사용자 지정 바인딩에 작성할 수 있습니다. 서비스에 상호 운용성이 필요한 클라이언트가 많은 경우에는 활성화된 클라이언트에 각각에 적절한 전송 및 인코딩 선택 항목이 있는 병렬 엔드포인트를 노출하는 것이 좋습니다.  
  
### <a name="enabling-mtom"></a>MTOM 활성화  
 상호 운용성이 필요하며 큰 이진 데이터를 전송해야 하는 경우 MTOM 메시지 인코딩은 표준 <xref:System.ServiceModel.BasicHttpBinding> 또는 <xref:System.ServiceModel.WSHttpBinding> 바인딩에서 해당 `MessageEncoding` 속성을 <xref:System.ServiceModel.WSMessageEncoding.Mtom>으로 설정하거나 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>를 <xref:System.ServiceModel.Channels.CustomBinding>에 작성하여 활성화할 수 있는 대체 인코딩 전략입니다. [Mtom Encoding](../../../../docs/framework/wcf/samples/mtom-encoding.md) 샘플에서 추출 된 다음 예제 코드는 구성에서 MTOM을 사용 하도록 설정 하는 방법을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
     …  
    <bindings>  
      <wsHttpBinding>  
        <binding name="ExampleBinding" messageEncoding="Mtom"/>  
      </wsHttpBinding>  
    </bindings>  
     …  
<system.serviceModel>  
```  
  
 앞에서 언급한 것과 같이, MTOM 인코딩의 사용 결정 사항은 보내는 데이터의 볼륨에 따라 달라집니다. 또한 MTOM이 바인딩 수준에서 활성화되기 때문에 MTOM을 활성화하면 지정된 엔드포인트의 모든 작업에 영향을 줍니다.  
  
 MTOM 인코더가 이진 데이터의 구체화 여부에 관계없이 항상 MTOM 인코딩 MIME/multipart 메시지를 내보내는 것과 상관없이 일반적으로 이진 데이터가 1KB 이상 포함된 메시지를 교환하는 엔드포인트의 MTOM만 활성화해야 합니다. 또한 MTOM이 활성화된 엔드포인트에 사용하도록 디자인된 서비스 계약은 가능한 경우 그러한 데이터 전송 작업을 지정하는 범위로 제한되어야 합니다. 관련 제어 기능은 별도의 계약에 있어야 합니다. 이 "MTOM 전용" 규칙은 MTOM이 활성화된 엔드포인트를 통해 전송되는 메시지에만 적용됩니다. MTOM 인코더에서는 들어오는 MTOM 외의 메시지도 디코딩하고 구문 분석할 수 있습니다.  
  
 MTOM 인코더를 사용 하는 것은 다른 모든 WCF 기능을 준수 합니다. 세션 지원이 필요한 경우와 같이 이 규칙을 따를 수 없는 경우도 있습니다.  
  
### <a name="programming-model"></a>프로그래밍 모델  
 애플리케이션에서 세 개의 기본 제공 인코더 중 어느 것을 사용해도, 이진 데이터 전송에 대한 프로그래밍 경험은 동일합니다. 데이터 형식을 기반으로 WCF가 데이터를 처리 하는 방법에 차이가 있습니다.  
  
```csharp
[DataContract]  
class MyData  
{  
    [DataMember]  
    byte[] binaryBuffer;  
    [DataMember]  
    string someStringData;  
}   
```  
  
 MTOM의 경우 앞의 데이터 계약이 다음 규칙에 따라 serialize됩니다.  
  
- `binaryBuffer`가 `null`이 아니며 각각 Base64 인코딩에 비해 MTOM 구체화 오버헤드를 정당화하기에 충분한 데이터를 포함한 경우(MIME 헤더 등) 데이터는 구체화되어 메시지와 함께 이진 MIME 부분으로 전송됩니다. 임계값을 초과하지 않은 경우 데이터는 Base64로 인코딩됩니다.  
  
- 문자열과 이진이 아닌 다른 모든 형식은 크기에 관계없이 항상 메시지 본문 내의 문자열로 표현됩니다.  
  
 앞의 예처럼 명시적인 데이터 계약을 사용하는 경우나, 작업에서 매개 변수 목록을 사용하는 경우나, 중첩된 데이터 계약이 있는 경우나, 컬렉션 내에 데이터 계약 개체를 전송하는 경우나 MTOM 인코딩에 대한 영향은 동일합니다. 바이트 배열은 항상 최적화 후보이며 최적화 임계값을 충족하면 최적화됩니다.  
  
> [!NOTE]
> 데이터 계약 내에서는 <xref:System.IO.Stream?displayProperty=nameWithType> 파생 형식을 사용하지 말아야 합니다. 스트림 데이터는 다음 "스트리밍 데이터" 단원에 설명된 대로 스트리밍 모델을 사용하여 통신해야 합니다.  
  
## <a name="streaming-data"></a>스트리밍 데이터  
 전송할 데이터가 많은 경우 WCF의 스트리밍 전송 모드는 메모리에서 메시지를 전체적으로 버퍼링 하 고 처리 하는 기본 동작에 대 한 적절 한 대안입니다.  
  
 앞에서 언급한 것과 같이, 데이터를 세그먼트로 나눌 수 없거나, 메시지를 시기 적절하게 배달해야 하거나, 전송을 시작했을 때 데이터 전체를 사용할 수 없는 경우에 텍스트 또는 이진 콘텐츠가 있는 큰 메시지에 대해서만 스트리밍 활성화를 고려해야 합니다.  
  
### <a name="restrictions"></a>Restrictions  
 스트리밍을 사용 하는 경우 많은 수의 WCF 기능을 사용할 수 없습니다.  
  
- 메시지 본문의 디지털 서명은 메시지 콘텐츠 전체의 해시 계산을 필요로 하기 때문에 수행할 수 없습니다. 스트리밍을 사용하면 메시지 헤더를 생성하여 보낼 때 콘텐츠를 전부 사용할 수 없기 때문에 디지털 서명을 계산할 수 없습니다.  
  
- 암호화에서는 디지털 서명에 의존하여 데이터가 올바르게 생성되었는지 확인합니다.  
  
- 신뢰할 수 있는 세션에서는 전송 중에 메시지가 손실된 경우 다시 배달할 수 있도록 클라이언트에 보낸 메시지를 버퍼링하고, 메시지를 서비스 구현으로 전달하기 전에 서비스에 보관하여 메시지가 시퀀스에 맞지 않게 수신된 경우 메시지 시퀀스를 보존합니다.  
  
 이러한 기능적 제약 때문에 스트리밍에는 전송 수준 보안 옵션만 사용할 수 있으며 신뢰할 수 있는 세션을 켤 수 없습니다. 스트리밍은 다음 시스템 정의 바인딩에서만 사용할 수 있습니다.  
  
- <xref:System.ServiceModel.BasicHttpBinding>  
  
- <xref:System.ServiceModel.NetTcpBinding>  
  
- <xref:System.ServiceModel.NetNamedPipeBinding>  
  
- <xref:System.ServiceModel.WebHttpBinding>  
  
 <xref:System.ServiceModel.NetTcpBinding> 및 <xref:System.ServiceModel.NetNamedPipeBinding>의 기본 전송에는 신뢰할 수 있는 고유한 배달 및 연결 기반 세션 지원이 있기 때문에 HTTP와 달리 이 두 바인딩은 실제로 이러한 제약 조건에 의해 최소한의 영향만 받습니다.  
  
 스트리밍은 MSMQ(메시지 큐) 전송에서 사용할 수 없기 때문에 <xref:System.ServiceModel.NetMsmqBinding> 또는 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 클래스에서 사용할 수 없습니다. 다른 모든 전송에서는 대부분의 시나리오에 대해 실제 메시지 크기 제한이 없는 반면, 메시지 큐 전송에서는 메시지 크기가 제한된 버퍼링 데이터 전송만 지원합니다.  
  
 스트리밍은 피어 채널 전송을 사용할 때 사용할 수 없기 때문에 <xref:System.ServiceModel.NetPeerTcpBinding>에서 사용할 수도 없습니다.  
  
#### <a name="streaming-and-sessions"></a>스트리밍 및 세션  
 세션 기반 바인딩을 통해 스트리밍 호출이 수행될 경우 예기치 못한 동작이 발생할 수 있습니다. 모든 스트리밍 호출은 사용 중인 바인딩이 세션을 사용하도록 구성된 경우에도 세션을 지원하지 않는 하나의 채널(데이터그램 채널)을 통해 수행됩니다. 여러 클라이언트에서 세션 기반 바인딩을 통해 동일한 서비스 개체에 대한 스트리밍 호출을 수행하고, 서비스 개체의 동시성 모드가 단일 모드로 설정되고, 서비스 개체의 인스턴스 컨텍스트 모드가 PerSession으로 설정된 경우, 모든 호출은 데이터그램 채널을 통해 수행되므로 한 번에 하나의 호출만 처리됩니다. 하나 이상의 클라이언트의 제한 시간이 초과될 수 있습니다. 이 문제는 서비스 개체의 인스턴스 컨텍스트 모드를 PerCall로 설정하거나 동시성 모드를 다중 모드로 설정하여 해결할 수 있습니다.  
  
> [!NOTE]
> 이 경우 사용할 수 있는 "세션"이 하나이기 때문에 MaxConcurrentSessions에는 영향을 주지 않습니다.  
  
### <a name="enabling-streaming"></a>스트리밍 활성화  
 다음 방법을 사용하여 스트리밍을 활성화할 수 있습니다.  
  
- 스트리밍 모드에서 요청을 보내기 및 승인, 버퍼링 모드에서 응답 승인 및 반환(<xref:System.ServiceModel.TransferMode.StreamedRequest>).  
  
- 버퍼링 모드에서 요청을 보내기 및 승인, 스트리밍 모드에서 응답 승인 및 반환(<xref:System.ServiceModel.TransferMode.StreamedResponse>).  
  
- 스트리밍 모드에서 양방향으로 요청 및 응답을 보내고 받기. (<xref:System.ServiceModel.TransferMode.Streamed>).  
  
 전송 모드를 모든 바인딩의 기본 설정인 <xref:System.ServiceModel.TransferMode.Buffered>로 설정하면 스트리밍을 비활성화할 수 있습니다. 다음 코드에서는 구성에 전송 모드를 설정하는 방법을 보여 줍니다.  
  
```xml  
<system.serviceModel>  
     …  
    <bindings>  
      <basicHttpBinding>  
        <binding name="ExampleBinding" transferMode="Streamed"/>  
      </basicHttpBinding>  
    </bindings>  
     …  
<system.serviceModel>  
```  
  
 바인딩을 코드에 인스턴스화하는 경우에는 바인딩의 해당 `TransferMode` 속성(또는 사용자 지정 바인딩을 작성하는 경우 전송 바인딩 요소)을 앞에서 언급한 값 중 하나로 설정해야 합니다.  
  
 요청 및 응답의 스트리밍을 켜거나 양방향 모두에 대해 통신 참가자 중 어느 쪽에서나 기능에 영향을 주지 않고 독립적으로 스트리밍을 켤 수 있습니다. 하지만 전송 데이터 크기가 너무 커서 통신 링크의 양 엔드포인트 모두에서 스트리밍을 활성화하는 것이 적합하다고 항상 가정해야 합니다. 끝점 중 하나가 WCF를 사용 하 여 구현 되지 않은 플랫폼 간 통신의 경우 스트리밍을 사용 하는 기능은 플랫폼의 스트리밍 기능에 따라 달라 집니다. 다른 흔치 않은 예외로는 클라이언트 또는 서비스에서 작업 집합을 최소화해야 하며 작은 버퍼 크기만 사용할 수 있는 메모리 소비 구동 시나리오가 있습니다.  
  
### <a name="enabling-asynchronous-streaming"></a>비동기 스트리밍 사용  
 비동기 스트리밍을 사용하려면 <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> 엔드포인트 동작을 서비스 호스트에 추가하고 <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> 속성을 `true`로 설정합니다. 또한 전송 측에 진정한 의미의 비동기 스트리밍 기능을 추가했습니다. 이에 따라 메시지를 복수 클라이언트로 스트리밍하고 그 중 일부는 네트워크 혼잡으로 인해 읽는 속도가 느리거나 전혀 읽고 있지 않은 시나리오에서 서비스 확장성이 향상되었습니다. 이러한 시나리오에서는 이제 클라이언트당 서비스에서 개별 스레드를 차단하지 않습니다. 그러므로 서비스가 훨씬 더 많은 클라이언트를 처리해서 서비스 확장성이 향상됩니다.  
  
### <a name="programming-model-for-streamed-transfers"></a>스트리밍 전송의 프로그래밍 모델  
 스트리밍의 프로그래밍 모델은 간단합니다. 스트리밍 데이터를 받으려면 단일 <xref:System.IO.Stream> 형식 입력 매개 변수가 있는 작업 계약을 지정합니다. 스트리밍 데이터를 반환하려면 <xref:System.IO.Stream> 참조를 반환합니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IStreamedService  
{  
    [OperationContract]  
    Stream Echo(Stream data);  
    [OperationContract]  
    Stream RequestInfo(string query);  
    [OperationContract(OneWay=true)]  
    void ProvideInfo(Stream data);  
}  
```  
  
 위 예의 `Echo` 작업에서는 스트림을 받아서 반환하기 때문에 <xref:System.ServiceModel.TransferMode.Streamed>의 바인딩에서 사용해야 합니다. `RequestInfo` 작업의 경우 <xref:System.ServiceModel.TransferMode.StreamedResponse>가 <xref:System.IO.Stream>만 반환하기 때문에 가장 적절합니다. 단방향 작업은 <xref:System.ServiceModel.TransferMode.StreamedRequest>에 가장 적절합니다.  
  
 다음 `Echo` 또는 `ProvideInfo` 작업에 두 번째 매개 변수를 추가하면 서비스 모델이 버퍼링 전략으로 돌아가며 스트림의 런타임 serialization 표현을 사용합니다. 입력 스트림 매개 변수가 하나인 작업만을 엔드투엔드 요청 스트리밍에 사용할 수 있습니다.  
  
 이 규칙은 메시지 계약에도 비슷하게 적용됩니다. 다음 메시지 계약에 표시되어 있는 것과 같이, 스트림에 해당되는 메시지 계약에는 본문 멤버가 하나만 있을 수 있습니다. 스트리밍으로 추가 정보를 전달하려는 경우 이 정보는 메시지 헤더에 포함되어 있어야 합니다. 메시지 본문은 스트림 콘텐츠용으로 단독으로 예약되었습니다.  
  
```csharp
[MessageContract]  
public class UploadStreamMessage  
{  
   [MessageHeader]  
   public string appRef;  
   [MessageBodyMember]  
   public Stream data;  
}   
```  
  
 스트림이 EOF(파일의 끝)에 도달하면 스트리밍 전송이 끝나고 메시지가 닫힙니다. 메시지를 보낼 때 (값 반환 또는 작업 호출),를 <xref:System.IO.FileStream> 전달할 수 있으며, 그런 다음 WCF 인프라는 스트림을 완전히 읽고 EOF에 도달할 때까지 해당 스트림의 모든 데이터를 가져옵니다. 그러한 기본 제공되는 <xref:System.IO.Stream> 파생 클래스가 없는 소스에 스트리밍 데이터를 전달하려면 그러한 클래스를 생성하고, 스트림 소스 위에 해당 클래스를 오버레이하고, 그 결과를 인수 또는 반환 값으로 사용합니다.  
  
 WCF는 메시지를 받을 때 b a s e 64로 인코딩된 메시지 본문 콘텐츠나 MTOM을 사용 하는 경우 해당 MIME 부분에 대해 스트림을 생성 하며 콘텐츠를 읽을 때 스트림은 EOF에 도달 합니다.  
  
 전송 수준 스트리밍은 다른 메시지 계약 형식(매개 변수 목록, 데이터 계약 인수 및 명시적 메시지 계약)에도 적용되지만 그러한 메시지 형식의 serialization 및 deserialization에는 serializer의 버퍼링이 필요하기 때문에, 그러한 계약 variant는 좋지 않습니다.  
  
### <a name="special-security-considerations-for-large-data"></a>큰 데이터의 특수 보안 고려 사항  
 모든 바인딩에서는 들어오는 메시지의 크기를 제한하여 서비스 거부 공격을 방지할 수 있습니다. 예 <xref:System.ServiceModel.BasicHttpBinding>를 들어는 들어오는 메시지의 크기를 제한 하는 [MaxReceivedMessageSize](xref:System.ServiceModel.HttpBindingBase.MaxReceivedMessageSize%2A) 속성을 노출 하므로를 처리할 때 액세스할 수 있는 최대 메모리 양을 제한 합니다. 메시지. 이 단위는 바이트로 설정되며 기본값은 65,536바이트입니다.  
  
 큰 데이터 스트리밍 시나리오에 해당되는 보안 위험은 수신기에서 스트리밍을 예상할 때 데이터를 버퍼링하게 만들어 서비스 거부를 일으킵니다. 예를 들어 WCF는 항상 메시지의 SOAP 헤더를 버퍼링 하므로 공격자는 완전히 헤더로 구성 된 대량 악의적인 메시지를 생성 하 여 데이터가 버퍼링 되도록 할 수 있습니다. 스트리밍이 활성화되면 수신기에서 전체 메시지가 한 번에 메시지에 버퍼링될 것이라고 예상하지 않기 때문에 `MaxReceivedMessageSize`를 매우 큰 값으로 설정할 수 있습니다. WCF가 강제로 메시지를 버퍼링 하는 경우 메모리 오버플로가 발생 합니다.  
  
 따라서 이 경우에는 들어오는 메시지 크기를 제한하는 것만으로는 부족합니다. `MaxBufferSize` 속성은 WCF에서 버퍼링 하는 메모리를 제한 하는 데 필요 합니다. 스트리밍을 수행할 때 이 값을 안전한 값으로 설정하거나 기본값으로 유지하는 것이 중요합니다. 예를 들어, 서비스에서 크기 4GB까지의 파일을 받아 로컬 디스크에 저장해야 하는 경우를 가정할 수 있습니다. 한 번에 64KB까지의 데이터만 버퍼링할 수 있는 방법으로 메모리가 제한된 경우도 가정할 수 있습니다. 그러면 `MaxReceivedMessageSize`는 4GB로 설정하고 `MaxBufferSize`는 64KB로 설정합니다. 또한 서비스 구현에서 64KB 청크의 들어오는 스트림에서만 읽으며 이전 부분이 디스크에 기록된 후 메모리에서 폐기되기 전에는 다음 청크를 읽지 않는지 확인해야 합니다.  
  
 이 할당량은 WCF에서 수행 하는 버퍼링만 제한 하며 자체 서비스나 클라이언트 구현에서 수행 하는 버퍼링에 대해서는 보호할 수 없다는 것을 이해 하는 것도 중요 합니다. 추가 보안 고려 사항에 대 한 자세한 내용은 [데이터의 보안 고려 사항](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)을 참조 하세요.  
  
> [!NOTE]
> 버퍼링 또는 스트리밍 전송 중 어느 것을 사용할 것인지를 결정하는 것은 엔드포인트의 로컬 결정입니다. HTTP 전송의 경우 전송 모드는 연결 전체 또는 프록시 서버 및 다른 매개로 전파되지 않습니다. 서비스 인터페이스의 설명에 전송 모드 설정이 반영되지 않았습니다. WCF 클라이언트를 서비스에 생성 한 후에는 스트리밍 전송에서 사용 하도록 설정 된 서비스의 구성 파일을 편집 하 여 모드를 설정 해야 합니다. TCP 및 명명된 파이프 전송의 경우에는 전송 모드가 정책 어설션으로 전파됩니다.  
  
## <a name="see-also"></a>참고자료

- [방법: 스트리밍 사용](../../../../docs/framework/wcf/feature-details/how-to-enable-streaming.md)
