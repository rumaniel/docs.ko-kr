---
title: ByteStream 인코더를 사용하여 이진 개체 인코딩
ms.date: 03/30/2017
ms.assetid: 020ee981-c889-4b12-a3ea-91823ef46444
ms.openlocfilehash: 09a919e11971f81bc76dca0e45a7eb0e70ef749e
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626934"
---
# <a name="encoding-binary-objects-with-bytestream-encoder"></a>ByteStream 인코더를 사용하여 이진 개체 인코딩
Windows Communication Foundation (WCF)를 사용 하 여 원시 이진 데이터 보내기 및 받기 사용 하 여 구성 된 <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement>합니다.  
  
## <a name="byte-stream-message-encoder-architecture"></a>바이트 스트림 메시지 인코더 아키텍처  
 WCF에서 사용 하는 이진 메시지 인코더에는 처리, 유효성 검사 또는 메시지의 내부 이진 데이터를 식별 하는 것에 대 한 기능이 없습니다. 데이터 패키지는 XML로 인코딩된 후 보내기, 받기 및 디코딩됩니다. 인코더는 데이터가 전송에 전달된 후와 메시지가 메시지 큐에 보내지기 전에 데이터를 처리합니다. 이진 인코더는 메시지 데이터를 `<binary>` 요소에 래핑하고 메시지를 받은 후 이 요소를 제거하는 기능을 제공합니다.  
  
## <a name="using-the-byte-stream-message-encoder"></a>바이트 스트림 메시지 인코더 사용  
 다음 예제에서는 바이트 스트림 메시지 인코더를 구현하는 서비스 계약을 보여 줍니다.  
  
```csharp  
[OperationContract]  
Void Myfunction(Stream stream);  
```  
  
 다음 예제에서는 호출되는 서비스를 보여 줍니다.  
  
```csharp  
proxy.MyFunction(stream);  
```  
  
 라우터와 같은 메시지 인프라를 구현하는 서비스를 사용하는 경우 다음 예제와 같이 메시지가 검사, 유효성 검사 또는 상호 작용 없이 처리됩니다.  
  
```csharp  
[OperationContract]  
void ProcessMessage(Message message) ;  
```  
  
## <a name="scenarios"></a>시나리오  
 바이트 스트림 인코더는 다음과 같은 시나리오에서 유용합니다.  
  
- WCF를 사용 하 여 컴퓨터 간에 JPEG 이미지를 전송 합니다. 이 시나리오에서는 이미지가 외부 소스에서의 전송을 통해 도착하며 전송된 데이터는 이미지를 구성하는 원시 바이트입니다. 서비스는 이진 데이터를 받고 이미지를 표시합니다.  
  
- 메시지 큐에서 정보를 읽고 처리하는 경우. 메시지 큐 관리자에서 메시지를 읽으며 이 메시지는 처리되기 위해 메시지 큐 채널 위로 전달됩니다. 메시지 큐 채널은 WCF 채널 스택에서 큐 관리자 처럼 작동 합니다.  
  
 메시지 큐 채널을 통해 메시지를 보내는 경우 보낸 사람은 큐 관리자에서 받은 바이트를 제어할 수 없습니다. 받는 프로세스에 원시 바이트를 읽는 기능이 없는 경우 메시지가 잘못된 형식으로 수신되고 처리되지 않습니다. 받는 프로세스에는 받은 바이트를 사용 가능한 형식으로 다시 변환하는 기능이 있다고 간주됩니다.
