---
title: 서비스 프레임워크 데이터
ms.date: 03/30/2017
ms.assetid: 2a2c8ddc-4e82-4e7f-a79f-97085c469517
ms.openlocfilehash: 5c65e9d473b5fe3f2b1c29824dcc1151abb0c3f6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61780811"
---
# <a name="service-framework-data"></a>서비스 프레임워크 데이터
이 항목에서는 서비스 프레임워크 데이터에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|AddressingExtensionInBadNS|지정한 네임스페이스에서 지정된 요소가 유효하지 않습니다. 이는 확장명 요소가 주소 지정 네임스페이스에 있을 수 없으므로 지정된 요소가 중복 요소이거나 적합한 확장명이 아님을 의미합니다.|  
|BinaryEncoderSessionInvalid|이전 메시지를 디코딩하는 동안 오류가 발생했으므로 이진 인코더 세션이 유효하지 않습니다.|  
|CannotDetectAddressingVersion|WS-Addressing 버전을 감지할 수 없습니다. EndpointAddress가 요소를 사용하여 시작되지 않습니다.|  
|CouldNotFindNamespaceForPrefix|지정한 접두사에 범위 내의 네임스페이스 바인딩이 없습니다.|  
|EncoderBadContentType|contentType을 처리할 수 없습니다.|  
|EncoderEnvelopeVersionMismatch|지정한 들어오는 메시지의 봉투 버전이 지정한 인코더와 일치하지 않습니다. 바인딩이 예상 메시지와 동일한 버전으로 구성되어 있는지 확인하십시오.|  
|EncoderMessageVersionMismatch|지정한 나가는 메시지의 메시지 버전이 지정한 인코더와 일치하지 않습니다. 바인딩이 메시지와 동일한 버전으로 구성되어 있는지 확인하십시오.|  
|ExtraContentIsPresentInFaultDetail|추가 XML(Extensible Markup Language) 콘텐츠가 오류 정보 요소에 있습니다. 하나의 요소만 허용됩니다.|  
|FilterBadTableType|필터에 대해 만들어진 IMessageFilterTable은 MessageFilterTable일 수 없으며, MessageFilterTable로부터 파생될 수도 없습니다.|  
|FilterTableInvalidForLookup|MessageFilterTable 상태가 손상되었습니다. 요청한 검색을 수행할 수 없습니다.|  
|MandatoryHeaderNotUnderstood|요청된 하나 이상의 단순 개체 액세스 프로토콜 헤더 블록이 인식되지 않았습니다.|  
|MessageBodyIsStream|메시지 본문이 스트림입니다.|  
|MessageBodyIsUnknown|알려지지 않은 메시지 본문 형식입니다.|  
|MessageBodyReaderInvalidReadState|메시지 본문 판독기의 지정한 ReadState를 사용할 수 없습니다.|  
|MessageTextEncodingNotSupported|텍스트 메시지 형식에서 사용하는 지정된 텍스트 인코딩이 지원되지 않습니다.|  
|MissingMessageID|요청 메시지에 MessageID 헤더가 없습니다. 회신을 상호 연결하려면 MessageID 헤더가 필요합니다.|  
|MultipleMessageHeaders|지정된 이름 및 네임스페이스를 가진 헤더가 두 개 이상입니다.|  
|MultipleMessageHeadersWithActor|지정된 이름, 네임스페이스 및 역할을 가진 헤더가 두 개 이상입니다.|  
|MultipleRelatesToHeaders|지정된 관계를 가진 RelatesTo 헤더가 두 개 이상입니다. 각 관계에 대해 하나의 헤더만 허용됩니다.|  
|QueryFunctionTypeNotSupported|IXsltContextFunction에 대해 지정된 반환 형식이 지원되지 않습니다.|  
|QueryIteratorOutOfScope|XPathNodeIterator가 무효화되었습니다. IXsltContextFunctions에 인수로 전달되는 XPathNodeIterators는 함수 내에서만 유효합니다. 이들은 나중에 사용하도록 캐시되거나 함수에 의해 반환될 수 없습니다.|  
|QueryVariableNull|IXsltContextVariable 메서드는 null을 반환할 수 없습니다.|  
|QueryVariableTypeNotSupported|지정된 IXsltContextVariable 파생 형식이 지원되지 않습니다.|  
|ReceiveShutdownReturnedMessage|채널이 닫히는 동안 지정된 동작이 있는 예기치 않은 입력 메시지를 받았습니다. 추가 입력 메시지가 필요하지 않으면 채널을 닫으십시오.|  
|XmlBufferInInvalidState|내부 오류가 발생했습니다. XML 버퍼의 상태로 인해 작업을 수행할 수 없습니다.|  
|XmlBufferQuotaExceeded|XML(Extensible Markup Language) 콘텐츠를 버퍼링하는 데 필요한 크기가 버퍼 할당량을 초과했습니다.|
