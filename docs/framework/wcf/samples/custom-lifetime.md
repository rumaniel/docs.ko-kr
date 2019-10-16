---
title: 사용자 지정 수명
ms.date: 08/20/2018
ms.assetid: 52806c07-b91c-48fe-b992-88a41924f51f
ms.openlocfilehash: be6013d568e3625c5eac7e0c145db7df1c6917e3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62003165"
---
# <a name="custom-lifetime"></a>사용자 지정 수명

이 샘플에는 공유 WCF 서비스 인스턴스에 대 한 사용자 지정 수명 서비스를 제공 하는 Windows Communication Foundation (WCF) 확장을 작성 하는 방법을 보여 줍니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 문서의 끝부분에 나와 있습니다.

## <a name="shared-instancing"></a>공유 인스턴스 만들기

WCF는 서비스 인스턴스에 대 한 여러 인스턴스 만들기 모드를 제공합니다. 이 문서에서 다루는 공유 인스턴스 만들기 모드에는 여러 채널 간에 서비스 인스턴스를 공유 하는 방법을 제공 합니다. 클라이언트는 서비스의 팩터리 메서드에 연결 하 고 통신을 시작 하려면 새 채널을 만들 수 있습니다. 다음 코드 조각에서는 클라이언트 응용 프로그램에서 기존 서비스 인스턴스에 새 채널을 만드는 방법을 보여 줍니다.

```csharp
// Create a header for the shared instance id
MessageHeader shareableInstanceContextHeader = MessageHeader.CreateHeader(
        CustomHeader.HeaderName,
        CustomHeader.HeaderNamespace,
        Guid.NewGuid().ToString());

// Create the channel factory
ChannelFactory<IEchoService> channelFactory =
    new ChannelFactory<IEchoService>("echoservice");

// Create the first channel
IEchoService proxy = channelFactory.CreateChannel();

// Call an operation to create shared service instance
using (new OperationContextScope((IClientChannel)proxy))
{
    OperationContext.Current.OutgoingMessageHeaders.Add(shareableInstanceContextHeader);
    Console.WriteLine("Service returned: " + proxy.Echo("Apple"));
}

((IChannel)proxy).Close();

// Create the second channel
IEchoService proxy2 = channelFactory.CreateChannel();

// Call an operation using the same header that will reuse the shared service instance
using (new OperationContextScope((IClientChannel)proxy2))
{
    OperationContext.Current.OutgoingMessageHeaders.Add(shareableInstanceContextHeader);
    Console.WriteLine("Service returned: " + proxy2.Echo("Apple"));
}
```

다른 인스턴스 만들기 모드와 달리 공유 인스턴스 만들기 모드에는 서비스 인스턴스를 해제하는 고유한 방법이 있습니다. 에 대 한 채널을 닫을 때 기본적으로는 <xref:System.ServiceModel.InstanceContext>, WCF 서비스 런타임 있는지 확인 합니다 서비스 <xref:System.ServiceModel.InstanceContextMode> 하도록 구성 된 <xref:System.ServiceModel.InstanceContextMode.PerCall> 또는 <xref:System.ServiceModel.InstanceContextMode.PerSession>, 경우에 따라서 인스턴스를 해제 하 고 리소스를 클레임 합니다. 사용자 지정 하는 경우 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 는 WCF를 호출 하는 데 사용 되는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 인스턴스를 해제 하기 전에 공급자 구현의 메서드. 경우 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 반환 `true` 그렇지 않으면 인스턴스가 해제 되는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 구현은 알릴 책임이 `Dispatcher` 콜백 메서드를 사용 하 여 유휴 상태입니다. 호출 하 여 이렇게는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A> 공급자의입니다.

이 샘플에서는 해제 지연 될 수 있습니다 하는 방법을 보여 줍니다.는 <xref:System.ServiceModel.InstanceContext> 20 초 동안 유휴 시간 제한을 사용 합니다.

## <a name="extending-the-instancecontext"></a>InstanceContext 확장

Wcf의 경우 <xref:System.ServiceModel.InstanceContext> 서비스 인스턴스 간의 링크로 및 `Dispatcher`합니다. WCF를 사용 하면 확장 가능한 개체 패턴을 사용 하 여 새 상태나 동작을 추가 하 여이 런타임 구성 요소를 확장할 수 있습니다. 새로운 기능을 사용 하 여 기존 런타임 클래스를 확장 하거나 또는 개체에 새 상태 기능을 추가할 확장명 가능한 개체 패턴 WCF에서 사용 됩니다. 확장명 가능한 개체 패턴에는 세 가지 인터페이스인 <xref:System.ServiceModel.IExtensibleObject%601>, <xref:System.ServiceModel.IExtension%601> 및 <xref:System.ServiceModel.IExtensionCollection%601>이 있습니다.

<xref:System.ServiceModel.IExtensibleObject%601> 인터페이스는 해당 기능을 사용자 지정 하는 확장을 허용 하도록 개체에 의해 구현 됩니다.

<xref:System.ServiceModel.IExtension%601> 인터페이스는 `T` 형식의 클래스 확장일 수 있는 개체에 의해 구현됩니다.

마지막으로, 합니다 <xref:System.ServiceModel.IExtensionCollection%601> 인터페이스의 컬렉션인 <xref:System.ServiceModel.IExtension%601> 구현의 검색할 수 있도록 구현 <xref:System.ServiceModel.IExtension%601> 형식에 따라 합니다.

따라서 확장 하기 위해 합니다 <xref:System.ServiceModel.InstanceContext>를 구현 해야 합니다는 <xref:System.ServiceModel.IExtension%601> 인터페이스입니다. 이 샘플 프로젝트에는 `CustomLeaseExtension` 클래스에이 구현이 포함 되어 있습니다.

```csharp
class CustomLeaseExtension : IExtension<InstanceContext>
{
}
```

<xref:System.ServiceModel.IExtension%601> 인터페이스에는 <xref:System.ServiceModel.IExtension%601.Attach%2A> 및 <xref:System.ServiceModel.IExtension%601.Detach%2A>의 두 가지 메서드가 있습니다. 이름이 나타내듯이 이 두 메서드는 런타임에서 <xref:System.ServiceModel.InstanceContext> 클래스와 확장을 연결하거나 분리할 때 호출됩니다. 이 샘플에서는 `Attach` 메서드를 사용하여 확장의 현재 인스턴스에 속한 <xref:System.ServiceModel.InstanceContext> 개체를 추적합니다.

```csharp
InstanceContext owner;

public void Attach(InstanceContext owner)
{
    this.owner = owner;
}
```

또한 확장에 필요한 구현을 추가하여 연장된 수명 지원을 제공해야 합니다. 따라서 합니다 `ICustomLease` 인터페이스 원하는 메서드로 선언 및에서 구현 되는 `CustomLeaseExtension` 클래스.

```csharp
interface ICustomLease
{
    bool IsIdle { get; }
    InstanceContextIdleCallback Callback { get; set; }
}

class CustomLeaseExtension : IExtension<InstanceContext>, ICustomLease
{
}
```

WCF가 호출 하는 경우는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 에서 메서드를 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 구현에서는이 호출으로 라우팅됩니다 합니다 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드의 `CustomLeaseExtension`. 그런 다음, `CustomLeaseExtension` 메서드의 전용 상태 참조를 확인 하는지 여부를 <xref:System.ServiceModel.InstanceContext> 유휴 상태입니다. 유휴 상태인 경우, 반환 `true`합니다. 그렇지 않으면 연장된 수명 기간에 대한 타이머를 시작합니다.

```csharp
public bool IsIdle
{
  get
  {
    lock (thisLock)
    {
      if (isIdle)
      {
        return true;
      }
      else
      {
        StartTimer();
        return false;
      }
    }
  }
}
```

타이머의 `Elapsed` 이벤트 발송자의 콜백 함수 다른 정리 주기를 시작 하기 위해 호출 됩니다.

```csharp
void idleTimer_Elapsed(object sender, ElapsedEventArgs args)
{
    lock (thisLock)
    {
        StopTimer();
        isIdle = true;
        Utility.WriteMessageToConsole(
            ResourceHelper.GetString("MsgLeaseExpired"));
        callback(owner);
    }
}
```

유휴 상태로 전환 되는 인스턴스에 대 한 새 메시지가 도착 하는 경우 실행 중인 타이머를 갱신할 방법이 없습니다.

이 샘플에서는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider>을 구현하여 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드에 대한 호출을 가로채고 이를 `CustomLeaseExtension`에 라우트합니다. <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 구현은 `CustomLifetimeLease` 클래스에 포함됩니다. <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드는 WCF 서비스 인스턴스를 해제 하려고 할 때 호출 됩니다. 그러나 ServiceBehavior의 `ISharedSessionInstance` 컬렉션에는 특정 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 구현의 인스턴스가 하나만 있습니다. 즉, 알 수 없으므로 합니다 <xref:System.ServiceModel.InstanceContext> WCF 확인 시 닫혀는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드. 따라서이 샘플에서는 스레드 잠금을 요청을 직렬화 하는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드.

> [!IMPORTANT]
> serialization은 애플리케이션의 성능에 큰 영향을 주므로 스레드 잠금은 사용하지 않는 것이 좋습니다.

전용 멤버 필드에 사용 됩니다는 `CustomLifetimeLease` 유휴 상태를 추적 하는 클래스 및에서 반환 되는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드. 때마다 합니다 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A> 메서드를 호출 합니다 `isIdle` 필드를 반환 하 고 다시 설정 `false`합니다.  디스패처에서 `false` 메서드를 호출할 수 있도록 하려면 이 값을 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A>로 설정해야 합니다.

```csharp
public bool IsIdle(InstanceContext instanceContext)
{
    get
    {
        lock (thisLock)
        {
            //...
            bool idleCopy = isIdle;
            isIdle = false;
            return idleCopy;
        }
    }
}
```

경우는 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A?displayProperty=nameWithType> 메서드가 반환 `false`, 디스패처 콜백 함수를 사용 하 여 등록을 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.NotifyIdle%2A> 메서드. 이 메서드는 해제되는 <xref:System.ServiceModel.InstanceContext>에 대한 참조를 받습니다. 따라서 샘플 코드를 쿼리할 수 있습니다 합니다 `ICustomLease` 확장명을 입력 하 고 확인을 `ICustomLease.IsIdle` 확장 된 상태에서 속성입니다.

```csharp
public void NotifyIdle(InstanceContextIdleCallback callback,
            InstanceContext instanceContext)
{
    lock (thisLock)
    {
       ICustomLease customLease =
           instanceContext.Extensions.Find<ICustomLease>();
       customLease.Callback = callback;
       isIdle = customLease.IsIdle;
       if (isIdle)
       {
             callback(instanceContext);
       }
    }
}
```

전에 `ICustomLease.IsIdle` 속성을 검사, 콜백 속성을이 반드시 설정 해야 `CustomLeaseExtension` 유휴 상태일 때 디스패처를 알립니다. `ICustomLease.IsIdle`이 `true`를 반환하는 경우에는 `isIdle`에서 전용 멤버 `CustomLifetimeLease`이 `true`로 설정되고 callback 메서드를 호출합니다. 코드에서 잠금을 유지 하므로 다른 스레드가이 전용 멤버의 값을 변경할 수 없습니다. 디스패처에서 호출 되며 다음에 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider.IsIdle%2A?displayProperty=nameWithType>를 반환 합니다 `true` 디스패처에서 인스턴스를 해제 수 있습니다.

사용자 지정 확장의 기반이 완성된 후에는 이를 서비스 모델에 후크해야 합니다. 후크 하는 `CustomLeaseExtension` 구현을 <xref:System.ServiceModel.InstanceContext>, WCF는 제공 합니다 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> 의 부트스트래핑을 수행 하는 인터페이스 <xref:System.ServiceModel.InstanceContext>. 샘플에서 `CustomLeaseInitializer` 클래스는 이 인터페이스를 구현하고 유일한 메서드 초기화에서 `CustomLeaseExtension` 컬렉션에 <xref:System.ServiceModel.InstanceContext.Extensions%2A>의 인스턴스를 추가합니다. 이 메서드는 <xref:System.ServiceModel.InstanceContext>를 초기화하는 동안 디스패처에서 호출됩니다.

```csharp
public void InitializeInstanceContext(InstanceContext instanceContext,
    System.ServiceModel.Channels.Message message, IContextChannel channel)

    //...

    IExtension<InstanceContext> customLeaseExtension =
        new CustomLeaseExtension(timeout, headerId);
    instanceContext.Extensions.Add(customLeaseExtension);
}
```

 마지막 합니다 <xref:System.ServiceModel.Dispatcher.IInstanceContextProvider> 구현을 사용 하 여를 서비스 모델에 후크 되어를 <xref:System.ServiceModel.Description.IServiceBehavior> 구현 합니다. 이 구현은 `CustomLeaseTimeAttribute` 클래스에 배치되며 <xref:System.Attribute> 기본 클래스에서도 파생되어 이 동작을 특성으로 노출합니다.

```csharp
public void ApplyDispatchBehavior(ServiceDescription description,
           ServiceHostBase serviceHostBase)
{
    CustomLifetimeLease customLease = new CustomLifetimeLease(timeout);

    foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)
    {
        ChannelDispatcher cd = cdb as ChannelDispatcher;

        if (cd != null)
        {
            foreach (EndpointDispatcher ed in cd.Endpoints)
            {
                ed.DispatchRuntime.InstanceContextProvider = customLease;
            }
        }
    }
}
```

`CustomLeaseTime` 특성으로 주석을 달아 이 동작을 샘플 서비스 클래스에 추가할 수 있습니다.

```csharp
[CustomLeaseTime(Timeout = 20000)]
public class EchoService : IEchoService
{
  //…
}
```

샘플을 실행하면 작업 요청 및 응답이 서비스와 클라이언트 콘솔 창 모두에 표시됩니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](one-time-setup-procedure-for-the-wcf-samples.md)합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](building-the-samples.md)의 지침을 따릅니다.

3. 단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](running-the-samples.md)합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Lifetime`
