---
title: '전송: UDP를 통한 사용자 지정 트랜잭션 샘플'
ms.date: 03/30/2017
ms.assetid: 6cebf975-41bd-443e-9540-fd2463c3eb23
ms.openlocfilehash: aeab56c122cff4c8a1ee87cb067f03ee0c2f3227
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044698"
---
# <a name="transport-custom-transactions-over-udp-sample"></a>전송: UDP를 통한 사용자 지정 트랜잭션 샘플
이 샘플은 전송을 기반으로 [합니다. Windows Communication Foundation](../../../../docs/framework/wcf/samples/transport-udp.md) (WCF)[전송 확장성](../../../../docs/framework/wcf/samples/transport-extensibility.md)의 UDP 샘플입니다. 이 샘플은 사용자 지정 트랜잭션 흐름을 지원하도록 UDP 전송 샘플을 확장하고 <xref:System.ServiceModel.Channels.TransactionMessageProperty> 속성의 사용 방법을 보여 줍니다.  
  
## <a name="code-changes-in-the-udp-transport-sample"></a>UDP 전송 샘플의 코드 변경  
 트랜잭션 흐름을 보여 주기 위해 이 샘플에서는 `ICalculatorContract`의 트랜잭션 범위가 필요하도록 `CalculatorService.Add()`의 서비스 계약을 변경합니다. 또한 `System.Guid` 작업의 계약에 `Add` 매개 변수를 추가합니다. 이 매개 변수는 클라이언트 트랜잭션의 식별자를 서비스에 전달하는 데 사용됩니다.  
  
```  
class CalculatorService : IDatagramContract, ICalculatorContract  
{  
    [OperationBehavior(TransactionScopeRequired=true)]  
    public int Add(int x, int y, Guid clientTransactionId)  
    {  
        if(Transaction.Current.TransactionInformation.DistributedIdentifier == clientTransactionId)  
    {  
        Console.WriteLine("The client transaction has flowed to the service");  
    }  
    else  
    {  
     Console.WriteLine("The client transaction has NOT flowed to the service");  
    }  
  
    Console.WriteLine("   adding {0} + {1}", x, y);              
    return (x + y);  
    }  
  
    [...]  
}  
```  
  
 [전송: Udp](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플에서는 udp 패킷을 사용 하 여 클라이언트와 서비스 간에 메시지를 전달 합니다. [전송: 사용자 지정 전송](../../../../docs/framework/wcf/samples/transport-custom-transactions-over-udp-sample.md) 예제는 동일한 메커니즘을 사용 하 여 메시지를 전송 하지만 트랜잭션이 이동 하면 인코딩된 메시지와 함께 UDP 패킷에 삽입 됩니다.  
  
```  
byte[] txmsgBuffer =                TransactionMessageBuffer.WriteTransactionMessageBuffer(txPropToken, messageBuffer);  
  
int bytesSent = this.socket.SendTo(txmsgBuffer, 0, txmsgBuffer.Length, SocketFlags.None, this.remoteEndPoint);  
```  
  
 `TransactionMessageBuffer.WriteTransactionMessageBuffer`는 현재 트랜잭션의 전파 토큰을 메시지 엔터티와 병합하고 이를 버퍼에 배치하는 새로운 기능이 포함된 도우미 메서드입니다.  
  
 사용자 지정 트랜잭션 흐름 전송의 경우 클라이언트 구현에서 트랜잭션 흐름이 필요한 서비스 작업을 알고이 정보를 WCF에 전달 해야 합니다. 또한 사용자 트랜잭션을 전송 계층으로 전송하기 위한 메커니즘도 있어야 합니다. 이 샘플에서는 "WCF 메시지 검사기"를 사용 하 여이 정보를 가져옵니다. 여기서 구현된 `TransactionFlowInspector`라는 클라이언트 메시지 검사자는 다음 작업을 수행합니다.  
  
- 지정된 메시지 작업에 대해 트랜잭션을 이동해야 하는지 여부를 결정합니다. 이 작업은 `IsTxFlowRequiredForThisOperation()`에서 수행됩니다.  
  
- 트랜잭션을 이동해야 하는 경우 `TransactionFlowProperty`를 사용하여 현재 앰비언트 트랜잭션을 메시지에 연결합니다. 이 작업은 `BeforeSendRequest()`에서 수행됩니다.  
  
```  
public class TransactionFlowInspector : IClientMessageInspector  
{  
   void IClientMessageInspector.AfterReceiveReply(ref           System.ServiceModel.Channels.Message reply, object correlationState)  
  {  
  }  
  
   public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, System.ServiceModel.IClientChannel channel)  
   {  
       // obtain the tx propagation token  
       byte[] propToken = null;             
       if (Transaction.Current != null && IsTxFlowRequiredForThisOperation(request.Headers.Action))  
       {  
           try  
           {  
               propToken = TransactionInterop.GetTransmitterPropagationToken(Transaction.Current);  
           }  
           catch (TransactionException e)  
           {  
              throw new CommunicationException("TransactionInterop.GetTransmitterPropagationToken failed.", e);  
           }  
       }  
  
      // set the propToken on the message in a TransactionFlowProperty  
       TransactionFlowProperty.Set(propToken, request);  
  
       return null;              
    }  
  }  
  
  static bool IsTxFlowRequiredForThisOperation(String action)  
 {  
       // In general, this should contain logic to identify which operations (actions)      require transaction flow.  
      [...]  
 }  
}  
```  
  
 `TransactionFlowInspector` 자체는 사용자 지정 동작인 `TransactionFlowBehavior`를 사용하여 프레임워크에 전달됩니다.  
  
```  
public class TransactionFlowBehavior : IEndpointBehavior  
{  
       public void AddBindingParameters(ServiceEndpoint endpoint,            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
      {  
      }  
  
       public void ApplyClientBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.ClientRuntime clientRuntime)  
      {  
            TransactionFlowInspector inspector = new TransactionFlowInspector();  
            clientRuntime.MessageInspectors.Add(inspector);  
      }  
  
      public void ApplyDispatchBehavior(ServiceEndpoint endpoint, System.ServiceModel.Dispatcher.EndpointDispatcher endpointDispatcher)  
     {  
     }  
  
      public void Validate(ServiceEndpoint endpoint)  
      {  
      }  
}  
```  
  
 위 메커니즘을 유지한 상태에서 사용자 코드는 서비스 작업을 호출하기 전에 `TransactionScope`를 만듭니다. 트랜잭션을 서비스 작업으로 이동해야 하는 경우 메시지 검사자는 트랜잭션이 전송에 전달되는지 확인합니다.  
  
```  
CalculatorContractClient calculatorClient = new CalculatorContractClient("SampleProfileUdpBinding_ICalculatorContract");  
calculatorClient.Endpoint.Behaviors.Add(new TransactionFlowBehavior());               
  
try  
{  
       for (int i = 0; i < 5; ++i)  
      {  
              // call the 'Add' service operation under a transaction scope  
             using (TransactionScope ts = new TransactionScope())  
             {  
        [...]  
        Console.WriteLine(calculatorClient.Add(i, i * 2));  
         }  
      }               
       calculatorClient.Close();  
}  
catch (TimeoutException)  
{  
    calculatorClient.Abort();  
}  
catch (CommunicationException)  
{  
    calculatorClient.Abort();  
}  
catch (Exception)  
{  
    calculatorClient.Abort();  
    throw;  
}  
```  
  
 서비스는 클라이언트로부터 UDP 패킷을 수신한 다음 이 패킷을 deserialize하여 메시지와 트랜잭션을 추출합니다.  
  
```  
count = listenSocket.EndReceiveFrom(result, ref dummy);  
  
// read the transaction and message                       TransactionMessageBuffer.ReadTransactionMessageBuffer(buffer, count, out transaction, out msg);  
```  
  
 `TransactionMessageBuffer.ReadTransactionMessageBuffer()`는 `TransactionMessageBuffer.WriteTransactionMessageBuffer()`가 수행한 serialization 프로세스를 반대로 하는 도우미 메서드입니다.  
  
 트랜잭션이 이동하면 `TransactionMessageProperty`의 메시지에 추가됩니다.  
  
```  
message = MessageEncoderFactory.Encoder.ReadMessage(msg, bufferManager);  
  
if (transaction != null)  
{  
       TransactionMessageProperty.Set(transaction, message);  
}  
```  
  
 이렇게 하면 디스패처가 디스패치할 때 트랜잭션을 선택한 다음 메시지에 설명된 서비스 작업을 호출할 때 이 트랜잭션을 사용합니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.  
  
2. 현재 샘플은 [전송과 유사 하 게 실행 되어야 합니다. UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 샘플. 이 샘플을 실행하려면 UdpTestService.exe를 실행하여 서비스를 시작합니다. [!INCLUDE[windowsver](../../../../includes/windowsver-md.md)]를 실행하는 경우에는 높은 권한으로 서비스를 시작해야 합니다. 이렇게 하려면 파일 탐색기에서 UdpTestService .exe를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 클릭 합니다.  
  
3. 다음과 같은 출력이 표시됩니다.  
  
    ```  
    Testing Udp From Code.  
    Service is started from code...  
    Press <ENTER> to terminate the service and start service from config...  
    ```  
  
4. 이때 UdpTestClient.exe를 실행하여 클라이언트를 시작할 수 있습니다. 클라이언트에서 생성되는 출력은 다음과 같습니다.  
  
    ```  
    0  
    3  
    6  
    9  
    12  
    Press <ENTER> to complete test.  
    ```  
  
5. 서비스 출력은 다음과 같습니다.  
  
    ```  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    Hello, world!  
    The client transaction has flowed to the service  
       adding 0 + 0  
    The client transaction has flowed to the service  
       adding 1 + 2  
    The client transaction has flowed to the service  
       adding 2 + 4  
    The client transaction has flowed to the service  
       adding 3 + 6  
    The client transaction has flowed to the service  
       adding 4 + 8  
    ```  
  
6. 서비스 애플리케이션은 클라이언트가 보낸, `The client transaction has flowed to the service` 작업의 `clientTransactionId` 매개 변수에 포함된 트랜잭션 식별자를 서비스 트랜잭션의 식별자와 일치시킬 수 있는 경우 `CalculatorService.Add()`라는 메시지를 표시합니다. 이 두 식별자는 클라이언트 트랜잭션이 서비스로 이동한 경우에만 일치합니다.  
  
7. 구성을 사용하여 게시된 엔드포인트에 대해 클라이언트 애플리케이션을 실행하려면 서비스 애플리케이션 창에서 Enter 키를 누른 다음 테스트 클라이언트를 다시 실행합니다. 서비스에서 다음과 같이 출력되어야 합니다.  
  
    ```  
    Testing Udp From Config.  
    Service is started from config...  
    Press <ENTER> to terminate the service and exit...  
    ```  
  
8. 서비스에 대해 클라이언트를 실행하면 이전과 비슷한 출력이 표시됩니다.  
  
9. Svcutil.exe를 사용하여 클라이언트 코드 및 구성을 다시 생성하려면 서비스 애플리케이션을 시작한 다음 샘플의 루트 디렉터리에서 다음 Svcutil.exe 명령을 실행합니다.  
  
    ```  
    svcutil http://localhost:8000/udpsample/ /reference:UdpTransport\bin\UdpTransport.dll /svcutilConfig:svcutil.exe.config  
    ```  
  
10. Svcutil.exe는 `sampleProfileUdpBinding`에 대한 바인딩 확장명 구성을 생성하지 않으므로 직접 추가해야 합니다.  
  
    ```xml  
    <configuration>  
        <system.serviceModel>      
            …  
            <extensions>  
                <!-- This was added manually because svcutil.exe does not add this extension to the file -->  
                <bindingExtensions>  
                    <add name="sampleProfileUdpBinding" type="Microsoft.ServiceModel.Samples.SampleProfileUdpBindingCollectionElement, UdpTransport" />  
                </bindingExtensions>  
            </extensions>  
        </system.serviceModel>  
    </configuration>  
    ```  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Transactions\TransactionMessagePropertyUDPTransport`  
  
## <a name="see-also"></a>참고자료

- [트랜스포트가 UDP](../../../../docs/framework/wcf/samples/transport-udp.md)
