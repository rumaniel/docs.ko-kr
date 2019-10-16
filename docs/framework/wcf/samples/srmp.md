---
title: SRMP
ms.date: 03/30/2017
ms.assetid: cf37078c-dcb4-45e0-acaf-2f196521b226
ms.openlocfilehash: e3015e7185fd52a1161b91c74dee57f694fbeebd
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044712"
---
# <a name="srmp"></a>SRMP
이 샘플에서는 HTTP를 통해 MSMQ(메시지 큐)를 사용하여 트랜잭션된 대기 중인 통신을 수행하는 방법을 보여 줍니다.  
  
 대기 중인 통신에서 클라이언트는 큐를 사용하여 서비스와 통신합니다. 좀더 정확하게 말하면 클라이언트는 큐에 메시지를 보내고, 서비스는 큐에서 보낸 메시지를 받습니다. 따라서 서비스와 클라이언트가 동시에 실행되고 있지 않더라도 큐를 사용하여 통신할 수 있습니다.  
  
 MSMQ는 HTTP 사용(HTTPS 사용 포함)을 통해 큐에 메시지를 보낼 수 있게 합니다. 이 예제에서는 Windows Communication Foundation (WCF) 대기 중인 통신을 사용 하 고 HTTP를 통해 메시지를 보내는 방법을 보여 줍니다. MSMQ는 HTTP를 통한 통신에 사용되는 SOAP 기반 프로토콜인 SRMP라는 프로토콜을 사용합니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
4. **Windows 구성 요소 추가/제거**에서 샘플을 실행 하기 전에 MSMQ가 HTTP 지원과 함께 설치 되어 있는지 확인 합니다. HTTP 지원을 설치하면 IIS(인터넷 정보 서비스)가 자동으로 설치되고 MSMQ용 IIS에서 프로토콜 지원이 추가됩니다.  
  
5. HTTP를 통신에 사용하도록 하려면 MSMQ를 강화된 모드에서 실행할 수 있도록 설정합니다. 이렇게 하면 컴퓨터에서 호스트되는 큐에 보내는 어떠한 메시지도 HTTP가 아닌 전송을 사용하여 도달할 수 없습니다.  
  
6. MSMQ를 강화된 모드에서 실행되도록 선택한 후 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]에서는 컴퓨터를 다시 부팅해야 합니다.  
  
7. 서비스를 실행합니다.  
  
8. 클라이언트를 실행합니다. localhost 대신 컴퓨터 이름이나 IP 주소를 가리키도록 엔드포인트 주소를 변경해야 합니다. 클라이언트는 메시지를 보내고 종료합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 샘플을 실행하려면 MSMQ 외에 서비스와 클라이언트 컴퓨터 둘 다에 IIS가 설치되어 있어야 합니다.  
  
## <a name="demonstrates"></a>세부 항목  
 이 샘플에서는 HTTP를 통해 MSMQ를 사용 하 여 대기 중인 WCF 메시지를 보내는 방법을 보여 줍니다. 이를 SRMP 메시징이라고도 합니다. 대기 중인 메시지를 보낼 경우 보내는 컴퓨터의 MSMQ는 TCP 또는 HTTP 전송을 통해 수신 큐 관리자에게 메시지를 전송합니다. 사용자는 SRMP를 선택하여 큐 전송을 위한 전송 프로토콜로 HTTP가 사용된다는 것을 나타냅니다. SRMP 보안에서는 HTTPS 사용이 허용됩니다.  
  
## <a name="example"></a>예제  
 이 샘플 코드는 트랜잭션된 샘플에 기반을 둡니다. SRMP를 사용하여 큐에 메시지를 보내고 큐에서 메시지를 받는 방법은 네이티브 프로토콜을 사용하여 메시지를 보내고 받는 방법과 동일합니다.  
  
 클라이언트에 대한 구성은 선택된 큐 전송 프로토콜을 나타내도록 변경됩니다. 큐 전송 프로토콜은 Native, SRMP 또는 SrmpSecure 중 하나가 될 수 있습니다. 기본적으로 전송 프로토콜은 Native입니다. 이 예제에서 클라이언트와 서비스는 SRMP를 사용한다는 것을 구성에서 지정합니다.  
  
 전송 보안과 관련하여 SRMP에는 몇 가지 제한 사항이 있습니다. 기본 MSMQ 전송 보안의 경우 전송 큐 관리자와 수신 큐 관리자가 동일한 Windows 도메인에 있어야 한다는 것을 요구하는 Active Directory가 필요합니다. HTTP 경계를 통해 메시지를 보낼 경우 이 요구 사항을 충족할 수 없습니다. 따라서 기본 전송 보안이 작동하지 않습니다. 이 경우 전송 보안을 사용하려면 전송 보안을 Certificate로 설정해야 합니다. 또한 메시지 보안을 사용하여 메시지를 보안할 수도 있습니다. 이 샘플에서는 SRMP 메시징을 보여 주기 위해 전송 보안과 메시지 보안이 모두 해제됩니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
  <system.serviceModel>  
  
    <client>  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint name="OrderProcessorEndpoint"  
           address=  
          "net.msmq://localhost/private/ServiceModelSamplesSrmp"   
           bindingConfiguration="srmpBinding"   
           binding="netMsmqBinding"   
           contract="IOrderProcessor" />  
    </client>  
    <bindings>  
      <netMsmqBinding>  
        <binding name="srmpBinding"  
                 queueTransferProtocol="Srmp">  
          <security mode="None" />  
        </binding>  
      </netMsmqBinding>  
    </bindings>  
  </system.serviceModel>  
  
</configuration>  
```  
  
 샘플을 실행하면 다음 출력이 생성됩니다.  
  
```  
Processing Purchase Order: 556b70be-31ee-4a3b-8df4-ed5e538015a4   
Customer: somecustomer.com   
OrderDetails   
    Order LineItem: 54 of Blue Widget @unit price: $29.99   
    Order LineItem: 890 of Red Widget @unit price: $45.89   
    Total cost of this order: $42461.56   
    Order status: Pending  
```  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\SRMP`  
