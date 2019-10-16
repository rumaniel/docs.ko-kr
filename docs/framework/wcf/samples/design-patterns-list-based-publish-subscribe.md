---
title: '디자인 패턴: 목록 기반 게시-구독'
ms.date: 03/30/2017
ms.assetid: f4257abc-12df-4736-a03b-0731becf0fd4
ms.openlocfilehash: 3c05e66affad8e517b0b1b5001f726abeae7b100
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928834"
---
# <a name="design-patterns-list-based-publish-subscribe"></a>디자인 패턴: 목록 기반 게시-구독
이 샘플에서는 WCF (Windows Communication Foundation) 프로그램으로 구현 된 목록 기반 게시-구독 패턴을 보여 줍니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 목록 기반 게시-구독 디자인 패턴은 Microsoft 패턴 & 사례 게시, [통합 패턴](https://go.microsoft.com/fwlink/?LinkId=95894)에 설명 되어 있습니다. 게시-구독 패턴에서는 정보 항목을 구독한 받는 사람 컬렉션으로 정보를 전달합니다. 목록 기반 게시-구독에서는 구독자 목록을 유지 관리합니다. 공유할 정보가 있으면 목록에 있는 각 구독자에게 복사본이 전송됩니다. 이 샘플에서는 필요할 때마다 클라이언트에서 구독하거나 구독 취소할 수 있는 동적 목록 기반 게시-구독 패턴을 보여 줍니다.  
  
 List-based Publish-Subscribe 샘플은 클라이언트, 서비스 및 데이터 소스 프로그램으로 구성됩니다. 둘 이상의 클라이언트와 둘 이상의 데이터 소스 프로그램이 실행될 수 있습니다. 클라이언트에서는 서비스를 구독하고 알림을 수신하며 구독을 취소합니다. 데이터 소스 프로그램에서는 현재 모든 구독자와 공유할 정보를 서비스로 보냅니다.  
  
 이 샘플에서 클라이언트와 데이터 소스는 콘솔 프로그램(.exe 파일)이고 서비스는 IIS(인터넷 정보 서비스)에서 호스트되는 라이브러리(.dll)입니다. 클라이언트와 데이터 소스 동작은 데스크톱에 표시됩니다.  
  
 서비스에서는 이중 통신을 사용합니다. `ISampleContract` 서비스 계약은 `ISampleClientCallback` 콜백 계약과 쌍을 이룹니다. 서비스는 클라이언트가 구독자 목록에 가입하거나 해제하는 데 사용하는 Subscribe 및 Unsubscribe 서비스 작업을 구현합니다. 또한 서비스는 데이터 소스 프로그램에서 서비스에 새 정보를 제공하기 위해 호출하는 `PublishPriceChange` 서비스 작업을 구현합니다. 클라이언트 프로그램은 서비스에서 모든 구독자에게 가격 변경을 알리기 위해 호출하는 `PriceChange` 서비스 작업을 구현합니다.  
  
```csharp  
// Create a service contract and define the service operations.  
// NOTE: The service operations must be declared explicitly.  
[ServiceContract(SessionMode=SessionMode.Required,  
      CallbackContract=typeof(ISampleClientContract))]  
public interface ISampleContract  
{  
    [OperationContract(IsOneWay = false, IsInitiating=true)]  
    void Subscribe();  
    [OperationContract(IsOneWay = false, IsTerminating=true)]  
    void Unsubscribe();  
    [OperationContract(IsOneWay = true)]  
    void PublishPriceChange(string item, double price,   
                                     double change);  
}  
  
public interface ISampleClientContract  
{  
    [OperationContract(IsOneWay = true)]  
    void PriceChange(string item, double price, double change);  
}  
```  
  
 서비스는 모든 구독자에게 새 정보에 대해 알리는 메커니즘으로 .NET Framework 이벤트를 사용합니다. 클라이언트에서 Subscribe를 호출하여 서비스에 가입하면 이벤트 처리기가 제공됩니다. 클라이언트가 해제되면 이벤트에서 이벤트 처리기가 구독 취소됩니다. 데이터 소스에서 서비스를 호출하여 가격 변경을 보고하면 서비스에서 이벤트가 발생합니다. 그러면 구독한 각 클라이언트에 대해 하나씩 서비스 인스턴스가 각각 호출되고 해당 이벤트 처리기가 실행됩니다. 각 이벤트 처리기에서는 콜백 함수를 통해 해당 클라이언트로 정보를 전달합니다.  
  
```csharp  
public class PriceChangeEventArgs : EventArgs  
    {  
        public string Item;  
        public double Price;  
        public double Change;  
    }  
  
    // The Service implementation implements your service contract.  
    [ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
    public class SampleService : ISampleContract  
    {  
        public static event PriceChangeEventHandler PriceChangeEvent;  
        public delegate void PriceChangeEventHandler(object sender, PriceChangeEventArgs e);  
  
        ISampleClientContract callback = null;  
  
        PriceChangeEventHandler priceChangeHandler = null;  
  
        //Clients call this service operation to subscribe.  
        //A price change event handler is registered for this client instance.  
  
        public void Subscribe()  
        {  
            callback = OperationContext.Current.GetCallbackChannel<ISampleClientContract>();  
            priceChangeHandler = new PriceChangeEventHandler(PriceChangeHandler);  
            PriceChangeEvent += priceChangeHandler;  
        }  
  
        //Clients call this service operation to unsubscribe.  
        //The previous price change event handler is unregistered.  
  
        public void Unsubscribe()  
        {  
            PriceChangeEvent -= priceChangeHandler;  
        }  
  
        //Information source clients call this service operation to report a price change.  
        //A price change event is raised. The price change event handlers for each subscriber will execute.  
  
        public void PublishPriceChange(string item, double price, double change)  
        {  
            PriceChangeEventArgs e = new PriceChangeEventArgs();  
            e.Item = item;  
            e.Price = price;  
            e.Change = change;  
            PriceChangeEvent(this, e);  
        }  
  
        //This event handler runs when a PriceChange event is raised.  
        //The client's PriceChange service operation is invoked to provide notification about the price change.  
  
        public void PriceChangeHandler(object sender, PriceChangeEventArgs e)  
        {  
            callback.PriceChange(e.Item, e.Price, e.Change);  
        }  
  
    }  
```  
  
 샘플을 실행하면 여러 클라이언트가 시작됩니다. 클라이언트는 서비스를 구독합니다. 그런 다음 서비스로 정보를 보내는 데이터 소스 프로그램이 실행됩니다. 서비스는 정보를 모든 구독자에게 전달합니다. 정보가 수신되었는지를 확인하는 동작을 각 클라이언트 콘솔에 표시할 수 있습니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
### <a name="to-set-up-and-build-the-sample"></a>샘플을 설치하고 빌드하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>단일 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 다음 주소 `http://localhost/servicemodelsamples/service.svc`를 입력 하 여 브라우저를 사용 하 여 서비스에 액세스할 수 있는지 테스트 합니다. 확인 페이지가 응답으로 표시됩니다.  
  
2. 언어별 폴더의 \client\bin\\에서 setup.exe를 실행 합니다. 클라이언트 콘솔 창에 클라이언트 동작이 표시됩니다. 여러 클라이언트가 시작됩니다.  
  
3. 언어별 폴더의 \datasource\bin\\에서 Datasource를 실행 합니다. 데이터 소스 동작이 콘솔 창에 표시됩니다. 데이터 소스에서 서비스로 정보를 보내면 각 클라이언트로 전달되어야 합니다.  
  
4. 클라이언트, 데이터 원본 및 서비스 프로그램이 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
### <a name="to-run-the-sample-across-machines"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 서비스 컴퓨터를 설정합니다.  
  
    1. 서비스 컴퓨터에서 ServiceModelSamples라는 가상 디렉터리를 만듭니다. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) 의 배치 파일을 사용 하 여 디스크 디렉터리와 가상 디렉터리를 만들 수 있습니다.  
  
    2. %SystemDrive%\Inetpub\wwwroot\servicemodelsamples에서 서비스 컴퓨터의 ServiceModelSamples 가상 디렉터리로 서비스 프로그램 파일을 복사합니다. \bin 디렉터리에 파일을 포함해야 합니다.  
  
    3. 클라이언트 컴퓨터에서 브라우저를 사용하여 서비스에 액세스할 수 있는지 테스트합니다.  
  
2. 클라이언트 컴퓨터를 설정합니다.  
  
    1. 언어별 폴더의 \client\bin\ 폴더에서 클라이언트 프로그램 파일을 클라이언트 컴퓨터로 복사합니다.  
  
    2. 각 클라이언트 구성 파일에서 엔드포인트 정의의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다. 주소에서 "localhost"에 대한 참조를 정규화된 도메인 이름으로 바꿉니다.  
  
3. 데이터 소스 컴퓨터를 설정합니다.  
  
    1. 언어별 폴더의 \datasource\bin\ 폴더에서 데이터 소스 프로그램 파일을 데이터 소스 컴퓨터로 복사합니다.  
  
    2. 데이터 소스 구성 파일에서 엔드포인트 정의의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다. 주소에서 "localhost"에 대한 참조를 정규화된 도메인 이름으로 바꿉니다.  
  
4. 클라이언트 컴퓨터의 명령 프롬프트에서 Client.exe를 실행합니다.  
  
5. 데이터 소스 컴퓨터의 명령 프롬프트에서 Datasource.exe를 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DesignPatterns/ListBasedPublishSubscribe`  
