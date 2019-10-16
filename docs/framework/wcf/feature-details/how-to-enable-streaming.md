---
title: '방법: 스트리밍 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6ca2cf4b-c7a1-49d8-a79b-843a90556ba4
ms.openlocfilehash: bd1a52f1ce0f656af79928a20e3badc73661e89a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64635297"
---
# <a name="how-to-enable-streaming"></a>방법: 스트리밍 사용
Windows Communication Foundation (WCF) 버퍼링 또는 스트리밍 전송을 사용 하 여 메시지를 보낼 수 있습니다. 기본 설정인 버퍼링된 전송 모드에서는 메시지가 완전히 전달되어야 수신자가 읽을 수 있습니다. 스트리밍 전송 모드에서는 메시지가 완전히 전달되기 전에 수신자가 메시지 처리를 시작할 수 있습니다. 전달되는 정보가 길고 순차적으로 처리 가능한 경우 스트리밍 모드가 유용합니다. 또한 전체를 버퍼링하기에는 메시지가 너무 큰 경우에도 스트리밍 모드가 효과적입니다.  
  
 스트리밍을 사용하려면 `OperationContract`를 적절히 정의하고 전송 수준에서 스트리밍을 사용합니다.  
  
### <a name="to-stream-data"></a>데이터를 스트리밍하려면  
  
1. 데이터를 스트리밍하려면 서비스에 대한 `OperationContract`가 두 가지 요구 사항을 충족해야 합니다.  
  
    1. 전송할 데이터를 보유하는 매개 변수가 메서드의 유일한 매개 변수이어야 합니다. 예를 들어, 입력 메시지를 스트리밍할 경우 해당 작업은 단 하나의 입력 매개 변수만 가져야 합니다. 마찬가지로, 출력 메시지를 스트리밍할 경우 해당 작업에는 출력 매개 변수 또는 반환 값이 하나만 있어야 합니다.  
  
    2. 반환 값과 매개 변수 유형 중 하나 이상이 <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message> 또는 <xref:System.Xml.Serialization.IXmlSerializable>이어야 합니다.  
  
     다음은 스트리밍된 데이터의 계약 예제입니다.  
  
     [!code-csharp[c_HowTo_EnableStreaming#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#1)]
     [!code-vb[c_HowTo_EnableStreaming#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#1)]  
  
     `GetStream` 작업은 버퍼링되는 `string`으로 버퍼링된 입력 데이터를 받고, 스트리밍되는 `Stream`을 반환합니다. 반대로 `UploadStream`은 스트리밍된 `Stream`을 받아 버퍼링된 `bool`을 반환합니다. `EchoStream`은 `Stream`을 받고 반환하므로 입출력 메시지 모두 스트리밍되는 작업의 예입니다. 마지막으로, `GetReversedStream`은 어떤 입력도 받지 않고 스트리밍되는 `Stream`을 반환합니다.  
  
2. 바인딩에서 스트리밍을 사용하도록 설정해야 합니다. 다음 값 중 하나를 가져올 수 있는 `TransferMode` 속성을 설정합니다.  
  
    1. `Buffered`,  
  
    2. `Streamed`. 양 방향으로 스트리밍 통신이 가능합니다.  
  
    3. `StreamedRequest`. 요청만 스트리밍이 가능합니다.  
  
    4. `StreamedResponse`. 응답만 스트리밍이 가능합니다.  
  
     `BasicHttpBinding`은 `TransferMode` 및 `NetTcpBinding`과 같이 바인딩에 `NetNamedPipeBinding` 속성을 노출합니다. `TransferMode` 속성은 전송 바인딩 요소에서 설정하고 사용자 지정 바인딩에서 사용할 수도 있습니다.  
  
     다음 샘플에서는 코드를 사용하거나 구성 파일을 변경하여 `TransferMode`를 설정하는 방법에 대해 보여 줍니다. 또한 이 샘플에서는 두 방법 모두 `maxReceivedMessageSize` 속성을 64MB로 설정하여 받을 수 있는 최대 메시지 크기를 설정합니다. 기본 `maxReceivedMessageSize`는 64KB이며, 이는 스트리밍 시나리오에서는 일반적으로 너무 낮은 수준입니다. 이 할당량을 애플리케이션이 받을 최대 메시지 크기에 따라 적절히 설정합니다. 또한 `maxBufferSize`는 버퍼링되는 최대 크기를 제어하고 이를 적절히 설정합니다.  
  
    1. 샘플 중 다음 구성 조각은 `TransferMode` 및 사용자 지정 HTTP 바인딩에서 `basicHttpBinding` 속성을 스트리밍으로 설정하는 방법에 대해 보여 줍니다.  
  
         [!code-xml[c_HowTo_EnableStreaming#103](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/common/app.config#103)]   
  
    2. 다음 코드 조각은 `TransferMode` 및 사용자 지정 HTTP 바인딩에서 `basicHttpBinding` 속성을 스트리밍으로 설정하는 방법에 대해 보여 줍니다.  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#2)]
         [!code-vb[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#2)]  
  
    3. 다음 코드 조각은 사용자 지정 HTTP 바인딩에서 `TransferMode` 속성을 스트리밍으로 설정하는 것 방법에 대해 보여 줍니다.  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#3)]
         [!code-vb[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#3)]  
  
3. `GetStream`, `UploadStream` 및 `EchoStream` 작업 모두 파일로부터 데이터를 직접 보내거나 받은 데이터를 파일에 바로 저장합니다. 다음 코드는 `GetStream`에 대한 것입니다.  
  
     [!code-csharp[c_HowTo_EnableStreaming#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#4)]
     [!code-vb[c_HowTo_EnableStreaming#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#4)]  
  
### <a name="writing-a-custom-stream"></a>사용자 지정 스트림 쓰기  
  
1. 데이터 스트림의 각 청크에서 데이터를 보내고 받을 때 특수한 처리를 수행하려면 <xref:System.IO.Stream>에서 사용자 지정 스트림 클래스를 파생시킵니다. 사용자 지정 스트림의 예로 다음 코드에 `GetReversedStream` 메서드와 `ReverseStream` 클래스가 포함되어 있습니다.  
  
     `GetReversedStream`은 `ReverseStream`의 새 인스턴스를 만들어 반환합니다. 시스템이 `ReverseStream` 개체에서 읽을 때 실제 처리가 이루어집니다. `ReverseStream.Read` 메서드는 기본 파일에서 바이트 청크를 읽고 이를 되돌린 다음, 되돌린 해당 바이트를 반환합니다. 이 메서드는 파일의 전체 내용을 되돌리지 않으며, 한 번에 하나의 바이트 청크를 되돌립니다. 이는 스트림에서 콘텐츠를 읽거나 쓰는 중에 스트림 처리를 수행하는 방법에 대해 보여 주는 예제입니다.  
  
     [!code-csharp[c_HowTo_EnableStreaming#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#2)]
     [!code-vb[c_HowTo_EnableStreaming#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#2)]  
  
## <a name="see-also"></a>참고자료

- [큰 데이터 및 스트리밍](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)
- [Stream](../../../../docs/framework/wcf/samples/stream.md)
