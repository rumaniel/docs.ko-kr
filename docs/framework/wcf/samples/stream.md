---
title: 스트림
ms.date: 03/30/2017
ms.assetid: 58a3db81-20ab-4627-bf31-39d30b70b4fe
ms.openlocfilehash: 3f52ba01dfd3290e4b0f728e5832a11f2f9c3eeb
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045464"
---
# <a name="stream"></a>스트림
Stream 샘플에서는 스트리밍 전송 모드 통신의 사용 방법을 보여 줍니다. 이 서비스는 스트림을 보내고 받는 몇 가지 작업을 노출합니다. 이 샘플은 자체 호스팅됩니다. 클라이언트와 서버는 모두 콘솔 프로그램입니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 WCF (Windows Communication Foundation)는 두 전송 모드 (버퍼링 또는 스트리밍)로 통신할 수 있습니다. 기본 설정인 버퍼링 전송 모드에서는 메시지가 완전히 전달되어야 수신자가 읽을 수 있습니다. 스트리밍 전송 모드에서는 메시지가 완전히 전달되기 전에 수신자가 메시지 처리를 시작할 수 있습니다. 전달되는 정보가 길고 순차적으로 처리 가능한 경우 스트리밍 모드가 유용합니다. 또한 전체를 버퍼링하기에는 메시지가 너무 큰 경우에도 스트리밍 모드가 효과적입니다.  
  
## <a name="streaming-and-service-contracts"></a>스트리밍 및 서비스 계약  
 스트리밍은 서비스 계약을 설계할 때 고려할 사항입니다. 어떤 작업에서 많은 양의 데이터를 수신하거나 반환할 경우 입출력 메시지의 버퍼링 때문에 지나치게 많은 메모리가 사용되지 않도록 이 데이터를 스트리밍하는 것을 고려할 필요가 있습니다. 데이터를 스트리밍하려면 그 데이터를 포함하는 매개 변수가 메시지에서 유일한 매개 변수가 되어야 합니다. 예를 들어, 입력 메시지를 스트리밍할 경우 해당 작업은 단 하나의 입력 매개 변수만 가져야 합니다. 마찬가지로, 출력 메시지를 스트리밍할 경우 해당 작업에는 출력 매개 변수 또는 반환 값이 하나만 있어야 합니다. 두 경우 모두 매개 변수 또는 반환 값 형식은 `Stream`, `Message` 또는 `IXmlSerializable`이어야 합니다. 다음은 이 스트리밍 샘플에서 사용된 서비스 계약입니다.  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IStreamingSample  
{  
    [OperationContract]  
    Stream GetStream(string data);  
    [OperationContract]  
    bool UploadStream(Stream stream);  
    [OperationContract]  
    Stream EchoStream(Stream stream);  
    [OperationContract]  
    Stream GetReversedStream();  
  
}  
```  
  
 `GetStream` 작업은 버퍼링되는 문자열로 입력 데이터를 받고, 스트리밍되는 `Stream`을 반환합니다. 반대로, `UploadStream`은 스트리밍된 `Stream`을 받아 버퍼링된 `bool`을 반환합니다. `EchoStream`은 `Stream`을 받고 반환하므로 입출력 메시지 모두 스트리밍되는 작업의 예입니다. 마지막으로, `GetReversedStream`은 어떤 입력도 받지 않고 스트리밍되는 `Stream`을 반환합니다.  
  
## <a name="enabling-streamed-transfers"></a>스트리밍 전송 사용  
 앞서 설명한 대로 작업 계약을 정의하면 프로그래밍 모델 수준에서 스트리밍을 제공합니다. 여기서 중지하면 전송에서는 계속 메시지의 내용 전체를 버퍼링합니다. 전송 스트리밍을 사용하려면 전송의 바인딩 요소에서 전송 모드를 선택합니다. 바인딩 요소에는 `TransferMode`, `Buffered`, `Streamed` 또는 `StreamedRequest`로 설정할 수 있는 `StreamedResponse` 속성이 있습니다. 전송 모드를 `Streamed`로 설정하면 양방향 스트리밍 통신이 가능합니다. 전송 모드를 `StreamedRequest` 또는 `StreamedResponse`로 설정하면 각각 요청 또는 응답에서만 스트리밍 통신을 사용합니다.  
  
 `basicHttpBinding`은 `TransferMode` 및 `NetTcpBinding`과 같이 바인딩의 `NetNamedPipeBinding` 속성입니다. 다른 전송의 경우 전송 모드를 설정하려면 사용자 지정 바인딩을 만들어야 합니다.  
  
 샘플 중 다음 구성 코드에서는 `TransferMode` 및 사용자 지정 HTTP 바인딩에서 `basicHttpBinding` 속성을 스트리밍으로 설정하는 것을 보여 줍니다.  
  
```xml  
<!-- An example basicHttpBinding using streaming. -->  
<basicHttpBinding>  
  <binding name="HttpStreaming" maxReceivedMessageSize="67108864"  
           transferMode="Streamed"/>  
</basicHttpBinding>  
<!-- An example customBinding using HTTP and streaming.-->  
<customBinding>  
  <binding name="Soap12">  
    <textMessageEncoding messageVersion="Soap12WSAddressing10" />  
    <httpTransport transferMode="Streamed"  
                   maxReceivedMessageSize="67108864"/>  
  </binding>  
</customBinding>  
```  
  
 앞의 구성 코드는 `transferMode`를 `Streamed`로 설정할 뿐 아니라 `maxReceivedMessageSize`를 64MB로 설정합니다. 보호 장치 차원에서 `maxReceivedMessageSize`는 받을 수 있는 최대 메시지 크기를 설정합니다. 기본 `maxReceivedMessageSize`는 64KB이며, 이는 스트리밍 시나리오에서는 일반적으로 너무 낮은 수준입니다.  
  
## <a name="processing-data-as-it-is-streamed"></a>스트리밍 과정에서 데이터 처리  
 `GetStream`, `UploadStream` 및 `EchoStream` 작업 모두 파일로부터 바로 데이터를 보내거나 받은 데이터를 파일에 바로 저장하는 일을 담당합니다. 그러나 많은 양의 데이터를 보내거나 받을 필요가 있어 보내거나 받는 과정에 데이터의 청크를 대상으로 처리 작업을 수행하는 경우가 있습니다. 그러나 시나리오를 해결하는 방법 중 하나는 읽거나 기록하는 과정에서 데이터를 처리하는 사용자 지정 스트림(<xref:System.IO.Stream>에서 파생되는 클래스)을 작성하는 것입니다. `GetReversedStream` 작업 및 `ReverseStream` 클래스가 해당됩니다.  
  
 `GetReversedStream`은 `ReverseStream`의 새 인스턴스를 만들어 반환합니다. 시스템이 해당 `ReverseStream` 개체로부터 읽을 때 실제 처리가 이루어집니다. `ReverseStream.Read` 구현은 기본 파일로부터 바이트 청크를 읽고 이를 반대로 바꾼 다음 그 바이트를 반환합니다. 여기서 파일의 내용 전체를 반대로 바꾸지는 않습니다. 한 번에 하나의 바이트 청크를 반대로 바꿉니다. 이는 스트림에서 콘텐츠를 읽거나 기록하는 중에 스트림 처리를 수행하는 방법을 보여 주는 예제입니다.  
  
```csharp
class ReverseStream : Stream  
{  
  
    FileStream inStream;  
    internal ReverseStream(string filePath)  
    {  
        //Opens the file and places a StreamReader around it.  
        inStream = File.OpenRead(filePath);  
    }  
  
    // Other methods removed for brevity.  
  
    public override int Read(byte[] buffer, int offset, int count)  
    {  
        int countRead=inStream.Read(buffer, offset,count);  
        ReverseBuffer(buffer, offset, countRead);  
        return countRead;  
    }  
  
    public override void Close()  
    {  
        inStream.Close();  
        base.Close();  
    }  
    protected override void Dispose(bool disposing)  
    {  
        inStream.Dispose();  
        base.Dispose(disposing);  
    }  
    void ReverseBuffer(byte[] buffer, int offset, int count)  
    {  
        int i, j;  
        for (i = offset, j = offset + count - 1; i < j; i++, j--)  
        {  
            byte currenti = buffer[i];  
            buffer[i] = buffer[j];  
            buffer[j] = currenti;  
        }  
  
    }  
}  
```  
  
## <a name="running-the-sample"></a>샘플 실행  
 샘플을 실행하려면 먼저 이 문서 끝부분의 지침대로 서비스와 클라이언트를 모두 빌드합니다. 그런 다음 각기 다른 콘솔 창에서 서비스와 클라이언트를 시작합니다. 클라이언트가 시작하면 서비스가 준비되어 사용자가 Enter 키를 누를 때까지 대기합니다. 그런 다음 클라이언트는 `GetStream()`, `UploadStream()` 및 `GetReversedStream()` 메서드를 처음에는 HTTP를 통해 그리고 나서 TCP를 통해 호출합니다. 서비스 출력의 예제와 클라이언트 출력의 예제를 차례로 소개합니다.  
  
 서비스 출력:  
  
```console  
The streaming service is ready.  
Press <ENTER> to terminate service.  
  
Saving to file D:\...\uploadedfile  
......................  
File D:\...\uploadedfile saved  
Saving to file D:\...\uploadedfile  
...............  
File D:\...\uploadedfile saved  
```  
  
 클라이언트 출력:  
  
```console  
Press <ENTER> when service is ready  
------ Using HTTP ------   
Calling GetStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
------ Using Custom HTTP ------  
Calling GetStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
  
Press <ENTER> to terminate client.  
```  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!NOTE]
> Svcutil.exe를 사용하여 이 샘플에 대한 구성을 다시 생성할 경우 클라이언트 구성에서 엔드포인트 이름을 클라이언트 코드와 일치하도록 수정해야 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Stream`  
