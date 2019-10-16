---
title: 영속 인스턴스 컨텍스트
ms.date: 03/30/2017
ms.assetid: 97bc2994-5a2c-47c7-927a-c4cd273153df
ms.openlocfilehash: 4c2e39aa257d4b4b9b3bd28e0cd469f09cae0766
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71351624"
---
# <a name="durable-instance-context"></a>영속 인스턴스 컨텍스트

이 샘플에서는 영 속 인스턴스 컨텍스트를 사용 하도록 WCF (Windows Communication Foundation) 런타임을 사용자 지정 하는 방법을 보여 줍니다. 여기서는 SQL Server 2005를 백업 저장소(이 경우 SQL Server 2005 Express)로 사용합니다. 사용자 지정 스토리지 메커니즘에 액세스하는 방법도 제공합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

이 샘플은 WCF의 채널 계층과 서비스 모델 계층을 모두 확장 하는 과정을 포함 합니다. 따라서 구현 세부 정보를 검토하려면 먼저 기본 개념을 이해해야 합니다.

영속 인스턴스 컨텍스트는 실제 시나리오에서 매우 자주 발견됩니다. 예를 들어, 장바구니 애플리케이션에는 중간에 쇼핑을 일시 중지하고 다른 날 계속 진행할 수 있는 기능이 있습니다. 따라서 다음날 장바구니를 방문하면 원래 컨텍스트가 복원됩니다. 서버의 장바구니 애플리케이션에서는 연결이 끊어진 동안 장바구니 인스턴스를 유지 관리하지 않습니다. 대신 해당 상태를 영속 스토리지 매체에 유지하여 복원된 컨텍스트에 새 인스턴스를 생성할 때 사용합니다. 따라서 동일한 컨텍스트에 대해 제공되는 서비스 인스턴스는 이전 인스턴스와 동일하지 않습니다. 즉, 메모리 주소가 동일하지 않습니다.

영속 인스턴스 컨텍스트는 클라이언트와 서비스 간에 컨텍스트 ID를 교환하는 작은 프로토콜로 만들 수 있습니다. 이 컨텍스트 ID는 클라이언트에서 만들어 서비스로 전송됩니다. 서비스 인스턴스가 만들어지면 서비스 런타임에서는 이 컨텍스트 ID에 해당하는 지속적인 상태를 영구 스토리지(기본적으로 SQL Server 2005 데이터베이스)에서 로드하려고 합니다. 사용 가능한 상태가 없으면 새 인스턴스에 기본 상태가 지정됩니다. 서비스 구현에서는 사용자 지정 특성으로 서비스 구현 상태를 변경하는 작업을 표시하여 런타임에서 작업을 호출한 후 서비스 인스턴스를 저장할 수 있도록 합니다.

앞에서 설명한 대로 다음과 같이 간단하게 두 단계를 구분하여 목표를 달성할 수 있습니다.

1. 네트워크를 통해 컨텍스트 ID를 전달하는 메시지를 변경합니다.

2. 서비스 로컬 동작을 변경하여 사용자 지정 인스턴스 논리를 구현합니다.

전자는 네트워크의 메시지에 영향을 주므로 사용자 지정 채널로 구현하여 채널 계층에 연결해야 합니다. 후자는 서비스 로컬 동작에만 영향을 주므로 여러 서비스 확장 지점을 확장하여 구현할 수 있습니다. 다음 단원에서는 각 확장에 대해 설명합니다.

## <a name="durable-instancecontext-channel"></a>영속 InstanceContext 채널

먼저 채널 계층 확장을 검토합니다. 사용자 지정 채널을 기록하는 첫 단계는 채널의 통신 구조를 결정하는 것입니다. 새로운 유선 프로토콜을 사용할 경우 채널은 채널 스택의 다른 모든 채널과 함께 사용할 수 있어야 합니다. 따라서 모든 메시지 교환 패턴을 지원해야 합니다. 그러나 채널의 핵심 기능은 통신 구조와 관계없이 동일합니다. 즉, 클라이언트에서는 메시지에 컨텍스트 ID를 쓰고 서버에서는 메시지로부터 이 컨텍스트 ID를 읽어 상위 수준으로 전달해야 합니다. 따라서 모든 영속 인스턴스 컨텍스트 채널 구현에서 추상 기본 클래스 역할을 하는 `DurableInstanceContextChannelBase` 클래스가 만들어집니다. 이 클래스에는 메시지에서 컨텍스트 정보를 적용하고 읽는 일반적인 상태 컴퓨터 관리 기능과 보호된 멤버 두 개가 포함됩니다.

```csharp
class DurableInstanceContextChannelBase
{
  //…
  protected void ApplyContext(Message message)
  {
    //…
  }
  protected string ReadContextId(Message message)
  {
    //…
  }
}
```

이러한 두 메서드는 `IContextManager` 구현을 사용하여 메시지에서 컨텍스트 ID를 쓰고 읽습니다. `IContextManager`는 모든 컨텍스트 관리자에 대해 계약을 정의하는 데 사용되는 사용자 지정 인터페이스입니다. 채널에는 사용자 지정 SOAP 헤더나 HTTP 쿠키 헤더의 컨텍스트 ID를 포함할 수 있습니다. 각 컨텍스트 관리자 구현은 모든 컨텍스트 관리자의 공통 기능이 포함된 `ContextManagerBase` 클래스에서 상속됩니다. 이 클래스의 `GetContextId` 메서드는 클라이언트에서 컨텍스트 ID를 가져오는 데 사용됩니다. 컨텍스트 ID를 처음으로 가져오면 이 메서드는 원격 엔드포인트 주소로 이름이 생성되는 텍스트 파일에 컨텍스트 ID를 저장합니다. 일반적인 URI에서 잘못된 파일 이름 문자는 @ 문자로 바뀝니다.

나중에 동일한 원격 엔드포인트에 컨텍스트 ID가 필요하면 적합한 파일이 있는지 확인합니다. 파일이 있으면 컨텍스트 ID를 읽어 반환하고, 그렇지 않으면 새로 생성한 컨텍스트 ID를 반환하여 파일에 저장합니다. 기본 구성을 사용할 경우 이러한 파일은 현재 사용자의 temp 디렉터리의 ContextStore라는 디렉터리에 저장됩니다. 그러나 이 위치는 바인딩 요소를 사용하여 구성할 수 있습니다.

컨텍스트 ID를 전송하는 데 사용되는 메커니즘은 구성 가능합니다. 이 메커니즘은 HTTP 쿠키 헤더 또는 사용자 지정 SOAP 헤더에 기록할 수 있습니다. 사용자 지정 SOAP 헤더 접근 방식에서는 HTTP가 아닌 프로토콜(예: TCP 또는 명명된 파이프)과 함께 이 프로토콜을 사용할 수 있습니다. `MessageHeaderContextManager`와 `HttpCookieContextManager`라는 클래스에서 이 두 옵션을 구현합니다.

두 클래스 모두 컨텍스트 ID를 메시지에 적절하게 기록합니다. 예를 들어, `MessageHeaderContextManager` 클래스는 `WriteContext` 메서드의 SOAP 헤더에 메시지를 기록합니다.

```csharp
public override void WriteContext(Message message)
{
  string contextId = this.GetContextId();

  MessageHeader contextHeader =
    MessageHeader.CreateHeader(DurableInstanceContextUtility.HeaderName,
      DurableInstanceContextUtility.HeaderNamespace,
      contextId,
      true);

  message.Headers.Add(contextHeader);
}
```

`ApplyContext` 클래스의 `ReadContextId` 및 `DurableInstanceContextChannelBase` 메서드는 각각 `IContextManager.ReadContext` 및 `IContextManager.WriteContext`를 호출합니다. 그러나 `DurableInstanceContextChannelBase` 클래스로 이러한 컨텍스트 관리자를 직접 만들 수는 없습니다. 대신 `ContextManagerFactory` 클래스를 사용하여 해당 작업을 수행합니다.

```csharp
IContextManager contextManager =
                ContextManagerFactory.CreateContextManager(contextType,
                this.contextStoreLocation,
                this.endpointAddress);
```

`ApplyContext` 메서드는 보내는 채널에서 호출됩니다. 이 메서드는 나가는 메시지에 컨텍스트 ID를 삽입합니다. `ReadContextId` 메서드는 받는 채널에서 호출됩니다. 이 메서드를 사용하면 들어오는 메시지에서 컨텍스트 ID를 사용할 수 있고 `Properties` 클래스의 `Message` 컬렉션에 추가할 수 있습니다. 또한 컨텍스트 ID를 읽는 데 오류가 발생하면 `CommunicationException`이 throw되어 채널이 중단될 수 있습니다.

```csharp
message.Properties.Add(DurableInstanceContextUtility.ContextIdProperty, contextId);
```

계속하려면 `Properties` 클래스에서 `Message` 컬렉션을 사용하는 방법을 이해해야 합니다. 일반적으로 이 `Properties` 컬렉션은 채널 계층의 하위 수준에서 상위 수준으로 데이터를 전달할 때 사용됩니다. 이렇게 하면 프로토콜 정보에 관계없이 일관된 방식으로 상위 수준에 원하는 데이터를 제공할 수 있습니다. 즉, 채널 계층에서 SOAP 헤더나 HTTP 쿠키 헤더로 컨텍스트 ID를 보내고 받을 수 있습니다. 그러나 채널 계층을 통해 `Properties` 컬렉션에서 이 정보를 사용할 수 있으므로 상위 수준에서는 해당 정보에 대해 알 필요가 없습니다.

이제 `DurableInstanceContextChannelBase` 클래스를 사용하여 필요한 인터페이스 10개(IOutputChannel, IInputChannel, IOutputSessionChannel, IInputSessionChannel, IRequestChannel, IReplyChannel, IRequestSessionChannel, IReplySessionChannel, IDuplexChannel, IDuplexSessionChannel)를 모두 구현해야 합니다. 이러한 인터페이스는 사용 가능한 모든 메시지 교환 패턴(데이터그램, 단방향, 이중 및 세션 변형)과 유사합니다. 이러한 구현은 각각 앞에서 설명한 기본 클래스를 상속하고 `ApplyContext`와 `ReadContextId`를 적절하게 호출합니다. 예를 들어, IOutputChannel 인터페이스를 구현하는 `DurableInstanceContextOutputChannel`은 메시지를 보내는 각 메서드에서 `ApplyContext` 메서드를 호출합니다.

```csharp
public void Send(Message message, TimeSpan timeout)
{
    // Apply the context information before sending the message.
    this.ApplyContext(message);
    //…
}
```

반면, `DurableInstanceContextInputChannel` 인터페이스를 구현하는 `IInputChannel`은 메시지를 받는 각 메서드에서 `ReadContextId` 메서드를 호출합니다.

```csharp
public Message Receive(TimeSpan timeout)
{
    //…
      ReadContextId(message);
      return message;
}
```

이와 달리 다음 채널 구현에서는 메서드 호출을 채널 스택의 아래 채널에 위임합니다. 그러나 세션 변형에는 세션을 만드는 첫 번째 메시지에 대해서만 컨텍스트 ID를 보내고 읽을 수 있는 기본 논리가 있습니다.

```csharp
if (isFirstMessage)
{
//…
    this.ApplyContext(message);
    isFirstMessage = false;
}
```

이러한 채널 구현은 클래스 및 `DurableInstanceContextBindingElement` `DurableInstanceContextBindingElementSection` 클래스에 의해 WCF 채널 런타임에 적절히 추가 됩니다. 바인딩 요소 및 바인딩 요소에 대 한 자세한 내용은 [HttpCookieSession](../../../../docs/framework/wcf/samples/httpcookiesession.md) channel 샘플 설명서를 참조 하세요.

## <a name="service-model-layer-extensions"></a>서비스 모델 계층 확장명

이제 컨텍스트 ID가 채널 계층을 통해 이동했으므로 서비스 동작을 구현하여 인스턴스를 사용자 지정할 수 있습니다. 이 샘플에서는 스토리지 관리자를 사용하여 영구 스토리지에서 상태를 로드하고 저장합니다. 앞에서 설명한 대로 이 샘플에서는 SQL Server 2005를 백업 스토리지로 사용하는 스토리지 관리자를 제공합니다. 그러나 이 확장에 사용자 지정 스토리지 메커니즘을 추가할 수도 있습니다. 해당 작업을 수행하기 위해 모든 스토리지 관리자에 의해 구현되어야 하는 공용 인터페이스를 선언합니다.

```csharp
public interface IStorageManager
{
    object GetInstance(string contextId, Type type);
    void SaveInstance(string contextId, object state);
}
```

`SqlServerStorageManager` 클래스에는 기본 `IStorageManager` 구현이 포함되어 있습니다. 해당 `SaveInstance` 메서드에서 지정된 개체는 XmlSerializer를 사용하여 serialize되고 SQL Server 데이터베이스에 저장됩니다.

```csharp
XmlSerializer serializer = new XmlSerializer(state.GetType());
string data;

using (StringWriter writer = new StringWriter(CultureInfo.InvariantCulture))
{
    serializer.Serialize(writer, state);
    data = writer.ToString();
}

using (SqlConnection connection = new SqlConnection(GetConnectionString()))
{
    connection.Open();

    string update = @"UPDATE Instances SET Instance = @instance WHERE ContextId = @contextId";

    using (SqlCommand command = new SqlCommand(update, connection))
    {
        command.Parameters.Add("@instance", SqlDbType.VarChar, 2147483647).Value = data;
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;

        int rows = command.ExecuteNonQuery();

        if (rows == 0)
        {
            string insert = @"INSERT INTO Instances(ContextId, Instance) VALUES(@contextId, @instance)";
            command.CommandText = insert;
            command.ExecuteNonQuery();
        }
    }
}
```

`GetInstance` 메서드에서는 지정된 컨텍스트 ID에 대해 serialize된 데이터를 읽고 해당 데이터로 생성된 개체를 호출자에게 반환합니다.

```csharp
object data;
using (SqlConnection connection = new SqlConnection(GetConnectionString()))
{
    connection.Open();

    string select = "SELECT Instance FROM Instances WHERE ContextId = @contextId";
    using (SqlCommand command = new SqlCommand(select, connection))
    {
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;
        data = command.ExecuteScalar();
    }
}

if (data != null)
{
    XmlSerializer serializer = new XmlSerializer(type);
    using (StringReader reader = new StringReader((string)data))
    {
        object instance = serializer.Deserialize(reader);
        return instance;
    }
}
```

이러한 스토리지 관리자의 사용자는 해당 관리자를 직접 인스턴스화할 수 없습니다. 따라서 스토리지 관리자 생성 정보에서 추출한 `StorageManagerFactory` 클래스를 사용합니다. 이 클래스에는 지정된 스토리지 관리자 형식의 인스턴스를 만드는 정적 멤버인 `GetStorageManager`가 하나 있습니다. 형식 매개 변수가 `null`이면 이 메서드는 기본 `SqlServerStorageManager` 클래스의 인스턴스를 만들어 반환합니다. 또한 지정된 형식의 유효성을 검사하여 `IStorageManager` 인터페이스가 구현되는지 확인합니다.

```csharp
public static IStorageManager GetStorageManager(Type storageManagerType)
{
IStorageManager storageManager = null;

if (storageManagerType == null)
{
    return new SqlServerStorageManager();
}
else
{
    object obj = Activator.CreateInstance(storageManagerType);

    // Throw if the specified storage manager type does not
    // implement IStorageManager.
    if (obj is IStorageManager)
    {
        storageManager = (IStorageManager)obj;
    }
    else
    {
        throw new InvalidOperationException(
                  ResourceHelper.GetString("ExInvalidStorageManager"));
    }

    return storageManager;
}
}
```

영구 스토리지에서 인터페이스를 읽고 쓰는 데 필요한 인프라를 구현합니다. 이제 서비스 동작을 변경하는 데 필요한 단계를 수행해야 합니다.

이 프로세스의 첫 번째 단계로 채널 계층을 통해 현재 InstanceContext에 도달한 컨텍스트 ID를 저장해야 합니다. InstanceContext는 WCF 디스패처와 서비스 인스턴스 간의 링크 역할을 하는 런타임 구성 요소입니다. 이 구성 요소를 사용하면 서비스 인스턴스에 추가 상태 및 동작을 제공할 수 있습니다. 세션 통신에서는 첫 번째 메시지에 대해서만 컨텍스트 ID를 전송하기 때문에 이 구성 요소가 매우 중요합니다.

WCF를 사용 하면 확장 가능한 개체 패턴을 사용 하 여 새 상태 및 동작을 추가 하 여 InstanceContext 런타임 구성 요소를 확장할 수 있습니다. 확장 가능한 개체 패턴은 새 기능으로 기존 런타임 클래스를 확장 하거나 개체에 새 상태 기능을 추가 하기 위해 WCF에서 사용 됩니다. 확장 가능한 개체 패턴에는 iextensibleobject<t>\<t >, iextension\<t > 및 iextensioncollection\<t >의 세 가지 인터페이스가 있습니다.

- Iextensibleobject<t>\<T > 인터페이스는 해당 기능을 사용자 지정 하는 확장을 허용 하는 개체에 의해 구현 됩니다.

- Iextension\<t > 인터페이스는 t 형식의 클래스를 확장 하는 개체에 의해 구현 됩니다.

- Iextensioncollection\<T > 인터페이스는 형식으로 iextension을 검색할 수 있도록 하는 iextensions의 컬렉션입니다.

따라서 IExtension 인터페이스를 구현하고 필요한 상태를 정의하는 InstanceContextExtension 클래스를 만들어 컨텍스트 ID를 저장해야 합니다. 이 클래스는 사용할 스토리지 관리자를 보유하는 상태도 제공합니다. 새 상태가 저장된 다음에는 수정할 수 없습니다. 따라서 상태가 생성되어 인스턴스에 제공되고 저장된 다음에는 읽기 전용 속성으로만 액세스할 수 있습니다.

```csharp
// Constructor
public DurableInstanceContextExtension(string contextId,
            IStorageManager storageManager)
{
    this.contextId = contextId;
    this.storageManager = storageManager;
}

// Read only properties
public string ContextId
{
    get { return this.contextId; }
}

public IStorageManager StorageManager
{
    get { return this.storageManager; }
}
```

InstanceContextInitializer 클래스는 IInstanceContextInitializer 인터페이스를 구현하고 생성되는 InstanceContext의 Extensions 컬렉션에 인스턴스 컨텍스트 확장명을 추가합니다.

```csharp
public void Initialize(InstanceContext instanceContext, Message message)
{
    string contextId =
  (string)message.Properties[DurableInstanceContextUtility.ContextIdProperty];

    DurableInstanceContextExtension extension =
                new DurableInstanceContextExtension(contextId,
                     storageManager);
    instanceContext.Extensions.Add(extension);
}
```

앞에서 설명한 대로 `Properties` 클래스의 `Message` 컬렉션에서 컨텍스트 ID를 읽고 확장 클래스의 생성자에게 전달합니다. 이 샘플에서는 계층 간에 일관된 방식으로 정보를 교환할 수 있는 방법을 보여 줍니다.

다음으로 중요한 단계는 서비스 인스턴스 생성 프로세스를 재정의하는 단계입니다. WCF를 사용 하면 사용자 지정 인스턴스화 동작을 구현 하 고 IInstanceProvider 인터페이스를 사용 하 여 런타임에 연결할 수 있습니다. 이 작업을 수행하기 위해 새 `InstanceProvider` 클래스가 구현됩니다. 생성자에는 인스턴스 공급자에 필요한 서비스 유형이 허용되며, 이 서비스 유형은 나중에 새 인스턴스를 만드는 데 사용됩니다. `GetInstance` 구현에서는 지속적인 인스턴스를 찾는 스토리지 관리자 인스턴스를 만듭니다. 이 구현에서 `null`을 반환하면 서비스 유형의 새 인스턴스가 인스턴스화되어 호출자에게 반환됩니다.

```csharp
public object GetInstance(InstanceContext instanceContext, Message message)
{
    object instance = null;

    DurableInstanceContextExtension extension =
    instanceContext.Extensions.Find<DurableInstanceContextExtension>();

    string contextId = extension.ContextId;
    IStorageManager storageManager = extension.StorageManager;

    instance = storageManager.GetInstance(contextId, serviceType);

    instance ??= Activator.CreateInstance(serviceType);
    return instance;
}
```

다음으로 중요한 단계는 `InstanceContextExtension`, `InstanceContextInitializer` 및 `InstanceProvider` 클래스를 서비스 모델 런타임에 설치하는 것입니다. 사용자 지정 특성을 사용하면 서비스 구현 클래스를 표시하여 동작을 설치할 수 있습니다. `DurableInstanceContextAttribute`에는 이 특성의 구현이 포함되어 있으며 `IServiceBehavior` 인터페이스를 구현하여 전체 서비스 런타임을 확장합니다.

이 클래스에는 사용할 스토리지 관리자의 형식을 허용하는 속성이 있습니다. 이렇게 하면 구현을 통해 사용자가 고유한 `IStorageManager` 구현을 이 특성의 매개 변수로 지정할 수 있습니다.

`ApplyDispatchBehavior` 구현에서는 현재 `InstanceContextMode` 특성의 `ServiceBehavior`를 확인합니다. 이 속성을 Singleton으로 설정하면 영속 인스턴스를 사용할 수 없으며 `InvalidOperationException`이 throw되어 호스트에 알립니다.

```csharp
ServiceBehaviorAttribute serviceBehavior =
    serviceDescription.Behaviors.Find<ServiceBehaviorAttribute>();

if (serviceBehavior != null &&
     serviceBehavior.InstanceContextMode == InstanceContextMode.Single)
{
    throw new InvalidOperationException(
       ResourceHelper.GetString("ExSingletonInstancingNotSupported"));
}
```

그런 다음 스토리지 관리자, 인스턴스 컨텍스트 이니셜라이저 및 인스턴스 공급자의 인스턴스가 생성되고 모든 엔드포인트에 대해 만들어진 `DispatchRuntime`에 설치됩니다.

```csharp
IStorageManager storageManager =
    StorageManagerFactory.GetStorageManager(storageManagerType);

InstanceContextInitializer contextInitializer =
    new InstanceContextInitializer(storageManager);

InstanceProvider instanceProvider =
    new InstanceProvider(description.ServiceType);

foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)
{
    ChannelDispatcher cd = cdb as ChannelDispatcher;

    if (cd != null)
    {
        foreach (EndpointDispatcher ed in cd.Endpoints)
        {
            ed.DispatchRuntime.InstanceContextInitializers.Add(contextInitializer);
            ed.DispatchRuntime.InstanceProvider = instanceProvider;
        }
    }
}
```

지금까지의 내용을 요약하면 이 샘플에서는 사용자 지정 컨텍스트 ID 교환을 위해 사용자 지정 유선 프로토콜을 사용하는 채널을 생성하고 기본 인스턴스 동작을 덮어써서 영구 스토리지에서 인스턴스를 로드했습니다.

이제 서비스 인스턴스를 영구 스토리지에 저장하는 방법만 남아 있습니다. 앞에서 설명한 대로 상태를 저장하는 데 필요한 기능은 `IStorageManager`에 이미 구현되어 있습니다. 이제이를 WCF 런타임과 통합 해야 합니다. 서비스 구현 클래스의 메서드에 적용할 수 있는 또 다른 특성이 필요합니다. 이 특성은 서비스 인스턴스의 상태를 변경하는 메서드에 적용됩니다.

`SaveStateAttribute` 클래스가 이 기능을 구현합니다. 또한 각 작업 `IOperationBehavior` 에 대해 WCF 런타임을 수정 하는 클래스를 구현 합니다. 메서드가이 특성으로 표시 된 경우 WCF 런타임은 적절 한 `ApplyBehavior` `DispatchOperation` 가 생성 되는 동안 메서드를 호출 합니다. 이 메서드 구현에는 다음과 같은 코드가 한 줄 있습니다.

```csharp
dispatch.Invoker = new OperationInvoker(dispatch.Invoker);
```

이 명령은 `OperationInvoker` 형식의 인스턴스를 만들어 생성할 `Invoker`의 `DispatchOperation` 속성에 할당합니다. `OperationInvoker` 클래스는 `DispatchOperation`에 대해 생성된 기본 작업 호출자의 래퍼입니다. 이 클래스는 `IOperationInvoker` 인터페이스를 구현합니다. `Invoke` 메서드 구현에서 실제 메서드 호출은 내부 작업 호출자에게 위임됩니다. 그러나 결과를 반환하기 전에 `InstanceContext`의 스토리지 관리자를 사용하여 서비스 인스턴스를 저장합니다.

```csharp
object result = innerOperationInvoker.Invoke(instance,
    inputs, out outputs);

// Save the instance using the storage manager saved in the
// current InstanceContext.
InstanceContextExtension extension =
    OperationContext.Current.InstanceContext.Extensions.Find<InstanceContextExtension>();

extension.StorageManager.SaveInstance(extension.ContextId, instance);
return result;
```

## <a name="using-the-extension"></a>확장 사용

채널 계층과 서비스 모델 계층 확장이 모두 수행 되며 이제 WCF 응용 프로그램에서 사용할 수 있습니다. 서비스는 사용자 지정 바인딩을 사용하여 채널 스택에 채널을 추가한 다음 적절한 특성으로 서비스 구현 클래스를 표시해야 합니다.

```csharp
[DurableInstanceContext]
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]
public class ShoppingCart : IShoppingCart
{
//…
     [SaveState]
     public int AddItem(string item)
     {
         //…
     }
//…
 }
```

클라이언트 애플리케이션에서는 사용자 지정 바인딩을 사용하여 채널 스택에 DurableInstanceContextChannel을 추가해야 합니다. 구성 파일에서 선언적으로 채널을 구성하려면 바인딩 요소 섹션을 바인딩 요소 확장명 컬렉션에 추가해야 합니다.

```xml
<system.serviceModel>
 <extensions>
   <bindingElementExtensions>
     <add name="durableInstanceContext"
type="Microsoft.ServiceModel.Samples.DurableInstanceContextBindingElementSection, DurableInstanceContextExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>
   </bindingElementExtensions>
 </extensions>
```

이제 다른 표준 바인딩 요소와 마찬가지로 바인딩 요소를 사용자 지정 바인딩에서 사용할 수 있습니다.

```xml
<bindings>
 <customBinding>
   <binding name="TextOverHttp">
     <durableInstanceContext contextType="HttpCookie"/>
     <reliableSession />
     <textMessageEncoding />
     <httpTransport />
   </binding>
 </customBinding>
</bindings>
```

## <a name="conclusion"></a>결론

이 샘플에서는 사용자 지정 프로토콜 채널을 만드는 방법 및 서비스 동작을 사용자 지정하여 사용하는 방법을 보여 주었습니다.

사용자가 구성 섹션을 사용하여 `IStorageManager` 구현을 지정할 수 있도록 하면 확장을 더 향상시킬 수 있습니다. 이렇게 하면 서비스 코드를 다시 컴파일하지 않고도 백업 저장소를 수정할 수 있습니다.

또한 인스턴스의 상태를 캡슐화하는 클래스(예: `StateBag`)를 구현할 수 있습니다. 이 클래스는 상태가 변경될 때마다 상태를 유지하는 작업을 담당합니다. 따라서 `SaveState` 특성을 사용하지 않고 유지 작업을 보다 정확하게 수행할 수 있습니다. 예를 들어, 메서드를 호출할 때마다 `SaveState` 특성으로 상태를 저장하는 대신 상태가 실제로 변경될 때 해당 상태를 유지할 수 있습니다.

샘플을 실행하면 다음 출력이 표시됩니다. 클라이언트는 장바구니에 항목 두 개를 추가하고 장바구니의 항목 목록을 서비스에서 가져옵니다. 서비스와 클라이언트를 종료하려면 각 콘솔 창에서 Enter 키를 누릅니다.

```console
Enter the name of the product: apples
Enter the name of the product: bananas

Shopping cart currently contains the following items.
apples
bananas
Press ENTER to shut down client
```

> [!NOTE]
> 서비스를 다시 빌드하면 데이터베이스 파일을 덮어씁니다. 샘플을 여러 번 실행하는 동안 상태를 유지하려면 실행할 때마다 샘플을 다시 빌드하지 않아야 합니다.

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따르세요.

3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

> [!NOTE]
> 이 샘플을 실행하려면 SQL Server 2005 또는 SQL Express 2005를 실행하고 있어야 합니다. SQL Server 2005를 실행하고 있는 경우 서비스의 연결 문자열 구성을 수정해야 합니다. 다중 컴퓨터 구성에서 실행하는 경우 SQL Server는 서버 컴퓨터에만 필요합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Durable`
