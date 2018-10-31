---
title: ConcurrencyMode 재진입
ms.date: 03/30/2017
ms.assetid: b2046c38-53d8-4a6c-a084-d6c7091d92b1
ms.openlocfilehash: 94ea62d18fec202a099c2797602224eab43299b4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202018"
---
# <a name="concurrencymode-reentrant"></a>ConcurrencyMode 재진입
이 샘플에서는 서비스 구현에서 ConcurrencyMode.Reentrant 사용의 필요성과 의미를 보여 줍니다. ConcurrencyMode.Reentrant는 서비스나 콜백이 특정 시점에 하나의 메시지만 처리한다는 것을 의미합니다(`ConcurencyMode.Single`과 유사함). 스레드로부터의 안전성을 보장 하기 위해 Windows Communication Foundation (WCF) 잠급니다는 `InstanceContext` 다른 메시지를 처리할 수 있도록 메시지를 처리 합니다. 재진입 모드의 경우 서비스가 나가는 호출을 수행하기 직전에 `InstanceContext`의 잠금이 해제되므로 이 샘플에 나온 것처럼 재진입할 수 있는 후속 호출은 다음에 서비스에 들어갈 때 잠길 수 있습니다. 이 동작을 설명하기 위해 이 샘플에서는 클라이언트와 서비스가 이중 계약을 사용하여 서로 메시지를 보낼 수 있는 방법을 보여 줍니다.  
  
 정의된 계약은 서비스에 의해 구현되는 `Ping` 메서드와 클라이언트에 의해 구현되는 콜백 메서드 `Pong`을 가지는 이중 계약입니다. 클라이언트는 서버의 `Ping` 메서드를 틱 수와 함께 호출하여 호출을 시작합니다. 서비스는 틱 수가 0이 아닌지 확인한 다음 틱 수를 줄이는 동안 콜백의 `Pong` 메서드를 호출합니다. 샘플의 다음 코드에서 이 작업을 수행합니다.  
  
```csharp
public void Ping(int ticks)  
{  
     Console.WriteLine("Ping: Ticks = " + ticks);  
     //Keep pinging back and forth till Ticks reaches 0.  
     if (ticks != 0)  
     {  
         OperationContext.Current.GetCallbackChannel<IPingPongCallback>().Pong((ticks - 1));  
     }  
}  
```  
  
 콜백의 `Pong` 구현은 `Ping` 구현과 동일한 논리를 가집니다. 즉, 틱 수가 0이 아닌지 확인한 다음 1씩 감소하는 틱 수를 사용하여 콜백 채널(이 경우에는 원래 `Ping` 메시지를 보내는 데 사용된 채널)에서 `Ping` 메서드를 호출합니다. 틱 수가 0에 도달하면 메서드가 반환되므로 호출을 시작한 클라이언트의 첫 번째 호출로 모든 회신의 래핑이 해제됩니다. 콜백 구현에서 이를 확인할 수 있습니다.  
  
```csharp
public void Pong(int ticks)  
{  
    Console.WriteLine("Pong: Ticks = " + ticks);  
    if (ticks != 0)  
    {  
        //Retrieve the Callback  Channel (in this case the Channel which was used to send the  
        //original message) and make an outgoing call until ticks reaches 0.  
        IPingPong channel = OperationContext.Current.GetCallbackChannel<IPingPong>();  
        channel.Ping((ticks - 1));  
    }  
}  
```  
  
 `Ping` 및 `Pong` 메서드는 둘 다 요청/회신이므로 `Ping`에 대한 첫 번째 호출은 `CallbackChannel<T>.Pong()`에 대한 호출이 반환될 때까지 반환되지 않습니다. 클라이언트에서 `Pong` 메서드는 다음 `Ping` 호출이 반환될 때까지 반환될 수 없습니다. 콜백과 서비스는 둘 다 보류 중인 요청에 회신할 수 있으려면 먼저 나가는 요청/회신 호출을 수행해야 하므로 두 구현 모두 ConcurrencyMode.Reentrant 동작으로 표시되어야 합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1.  수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.  
  
2.  C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3.  단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.  
  
## <a name="demonstrates"></a>세부 항목  
 샘플을 실행하려면 클라이언트 및 서버 프로젝트를 빌드합니다. 두 개의 명령 창을 열고 디렉터리를 변경 합니다 \<샘플 > \CS\Service\bin\debug 및 \<샘플 > \CS\Client\bin\debug 디렉터리입니다. 다음을 입력 하 여 서비스를 시작 `service.exe` 입력 인수로 전달 된 틱의 초기 값을 사용 하 여 Client.exe를 호출 합니다. 그러면 10개 틱에 대한 샘플 출력이 표시됩니다.  
  
```console  
Prompt>Service.exe  
ServiceHost Started. Press Enter to terminate service.  
Ping: Ticks = 10  
Ping: Ticks = 8  
Ping: Ticks = 6  
Ping: Ticks = 4  
Ping: Ticks = 2  
Ping: Ticks = 0  
  
Prompt>Client.exe 10  
Pong: Ticks = 9  
Pong: Ticks = 7  
Pong: Ticks = 5  
Pong: Ticks = 3  
Pong: Ticks = 1  
```  
  
> [!IMPORTANT]
>  컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Reentrant`  
  
## <a name="see-also"></a>참고 항목
