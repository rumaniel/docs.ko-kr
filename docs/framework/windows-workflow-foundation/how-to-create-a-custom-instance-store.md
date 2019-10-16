---
title: '방법: 사용자 지정 인스턴스 저장소 만들기'
ms.date: 03/30/2017
ms.assetid: 593c4e9d-8a49-4e12-8257-cee5e6b4c075
ms.openlocfilehash: cacee7d95a543525ba031de0cc0636d05fc72fc8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945641"
---
# <a name="how-to-create-a-custom-instance-store"></a>방법: 사용자 지정 인스턴스 저장소 만들기

[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에는 SQL Server을 사용하여 워크플로 데이터를 유지하는 인스턴스 저장소인 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>가 있습니다. 애플리케이션에서 워크플로 데이터를 다른 매체(예: 다른 데이터베이스 또는 파일 시스템)에 유지해야 할 경우 사용자 지정 인스턴스 스토리지를 구현할 수 있습니다. 사용자 지정 인스턴스 저장소는 추상 <xref:System.Runtime.DurableInstancing.InstanceStore> 클래스를 확장하고 구현에 필요한 메서드를 구현하여 만듭니다. 사용자 지정 인스턴스 저장소의 완전 한 구현에 대 한 참조를 [기업 구매 프로세스](./samples/corporate-purchase-process.md) 샘플입니다.

## <a name="implementing-the-begintrycommand-method"></a>BeginTryCommand 메서드 구현

지속성 엔진은 <xref:System.Runtime.DurableInstancing.InstanceStore.BeginTryCommand%2A>을 인스턴스 저장소에 보냅니다. `command` 매개 변수의 형식은 실행될 명령을 나타냅니다. 이 매개 변수는 다음 형식일 수 있습니다.

- <xref:System.Activities.DurableInstancing.SaveWorkflowCommand>: 지 속성 엔진은 워크플로 저장 매체에 유지 되어야 하는 경우이 명령을 인스턴스 저장소에 보냅니다. 워크플로 지속성 데이터는 <xref:System.Activities.DurableInstancing.SaveWorkflowCommand.InstanceData%2A> 매개 변수의 `command` 멤버의 메서드에 제공됩니다.

- <xref:System.Activities.DurableInstancing.LoadWorkflowCommand>: 지 속성 엔진은 워크플로를 저장 매체에 로드할 때이 명령을 인스턴스 저장소에 보냅니다. 로드되는 워크플로의 인스턴스 ID가 `instanceId` 매개 변수의 <xref:System.Runtime.DurableInstancing.InstancePersistenceContext.InstanceView%2A> 속성의 `context` 매개 변수의 메서드에 제공됩니다.

- <xref:System.Activities.DurableInstancing.CreateWorkflowOwnerCommand>: 이 명령은 인스턴스를 저장할 때 지 속성 엔진 보냅니다는 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 잠금 소유자로 등록 해야 합니다. <xref:System.Runtime.DurableInstancing.InstancePersistenceContext.BindInstanceOwner%2A> 매개 변수의 `context` 메서드를 사용하여 현재 워크플로의 인스턴스 ID를 인스턴스 저장소에 제공해야 합니다.

     다음 코드 조각에서는 CreateWorkflowOwner 명령을 구현하여 명시적 잠금 소유자를 할당하는 방법을 보여 줍니다.

    ```csharp
    XName WFInstanceScopeName = XName.Get(scopeName, "<namespace>");
    ...
    CreateWorkflowOwnerCommand createCommand = new CreateWorkflowOwnerCommand()
    {
        InstanceOwnerMetadata =
        {
            { WorkflowHostTypeName, new InstanceValue(WFInstanceScopeName) },
        }
    };
    InstanceHandle ownerHandle = store.CreateInstanceHandle();
    store.DefaultInstanceOwner = store.Execute(
                                   ownerHandle,
                                   createCommand,
                                   TimeSpan.FromSeconds(30)).InstanceOwner;
    childInstance.AddInitialInstanceValues(new Dictionary<XName, object>() { { WorkflowHostTypeName, WFInstanceScopeName } });
    ```

- <xref:System.Activities.DurableInstancing.DeleteWorkflowOwnerCommand>: 지 속성 엔진은 잠금 소유자의 인스턴스 ID를 인스턴스 저장소에서 제거할 수 있습니다 하는 경우이 명령을 인스턴스 저장소에 보냅니다. <xref:System.Activities.DurableInstancing.CreateWorkflowOwnerCommand>를 사용하기 때문에 잠금 소유자의 ID를 애플리케이션에 제공해야 합니다.

     다음 코드 조각에서는 <xref:System.Activities.DurableInstancing.DeleteWorkflowOwnerCommand>를 사용하여 잠금을 해제하는 방법에 대해 설명합니다.

    ```csharp
    static void FreeHandleAndDeleteOwner(InstanceStore store, InstanceHandle handle)
    {
        handle.Free();
        handle = store.CreateInstanceHandle(store.DefaultInstanceOwner);
        try
        {
            // We need this sleep so that we dont prematurely delete the owner, we need time to update the database.
            Thread.Sleep(10000);
            store.Execute(handle, new DeleteWorkflowOwnerCommand(), TimeSpan.FromSeconds(10));
        }
        catch (InstancePersistenceCommandException ex) { Log.Inform(ex.Message); }
        catch (InstanceOwnerException ex) { Log.Inform(ex.Message); }
        catch (OperationCanceledException ex) { Log.Inform(ex.Message); }
        catch (Exception ex) { Log.Inform(ex.Message); }
        finally
        {
            handle.Free();
            store.DefaultInstanceOwner = null;
        }
    }
    ```

     자식 인스턴스가 실행될 때 위의 메서드는 Try/Catch 블록에서 호출되어야 합니다.

    ```csharp
    try
    {
        childInstance.Run();
    }
    catch (Exception)
    {
        throw ;
    }
    finally
    {
        FreeHandleAndDeleteOwner(store, ownerHandle);
    }
    ```

- <xref:System.Activities.DurableInstancing.LoadWorkflowByInstanceKeyCommand>: 지 속성 엔진은 워크플로 인스턴스가 워크플로 인스턴스 키를 사용 하 여 로드할 때이 명령을 인스턴스 저장소에 보냅니다. 인스턴스 키의 ID는 명령의 <xref:System.Activities.DurableInstancing.LoadWorkflowByInstanceKeyCommand.LookupInstanceKey%2A> 매개 변수를 사용하여 확인할 수 있습니다.

- <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>: 지 속성 엔진은 워크플로 로드할 수 있는 워크플로 호스트를 만들기 위해 지속형된 워크플로에 대 한 활성화 매개 변수를 검색할 인스턴스 저장소에이 명령을 보냅니다. 활성화할 수 있는 인스턴스를 찾을 때 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent>를 발생시키는 인스턴스 저장소에 대한 응답으로 엔진은 호스트로 이 명령을 보냅니다. 인스턴스 저장소는 활성화할 수 있는 워크플로가 있는지 확인하기 위해 폴링되어야 합니다.

- <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>: 지 속성 엔진은 실행 가능한 워크플로 인스턴스를 로드 하도록 인스턴스 저장소에이 명령을 보냅니다. 실행할 수 있는 인스턴스를 찾을 때 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent>를 발생시키는 인스턴스 저장소에 대한 응답으로 엔진은 호스트로 이 명령을 보냅니다. 인스턴스 저장소는 실행할 수 있는 워크플로에 대해 폴링해야 합니다. 다음 코드 조각에서는 실행 또는 활성화할 수 있는 워크플로의 인스턴스 저장소를 폴링하는 방법을 보여 줍니다.

    ```csharp
    public void PollForEvents()
    {
        InstanceOwner[] storeOwners = this.GetInstanceOwners();

        foreach (InstanceOwner owner in storeOwners)
        {
            foreach (InstancePersistenceEvent ppEvent in this.GetEvents(owner))
            {
                if (ppEvent.Equals(HasRunnableWorkflowEvent.Value))
                {
                    bool hasRunnable = GetRunnableEvents(this.StoreId, owner.InstanceOwnerId, isActivatable);
                    if (hasRunnable)
                    {
                        this.SignalEvent(ppEvent, owner);
                    }
                    else
                    {
                        this.ResetEvent(ppEvent, owner);
                    }
                }
                else if(ppEvent.Equals(HasActivatableWorkflowEvent.Value))
                {
                   bool hasActivatable = GetActivatableEvents(this.StoreId, owner.InstanceOwnerId);
                   if (hasActivatable)
                    {
                        this.SignalEvent(ppEvent, owner);
                    }
                    else
                    {
                        this.ResetEvent(ppEvent, owner);
                    }
                }
            }
        }
    }
    ```

     위의 코드 조각에서 인스턴스 저장소는 사용 가능한 이벤트를 쿼리하고 각 이벤트를 검사하여 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> 이벤트인지 확인합니다. 해당 이벤트가 발견되면 호스트에 알려 명령을 인스턴스 저장소에 보내도록 <xref:System.Runtime.DurableInstancing.InstanceStore.SignalEvent%2A>가 호출됩니다. 다음 코드 조각에서는 이 명령의 처리기를 구현하는 방법을 보여 줍니다.

    ```csharp
    If (command is TryLoadRunnableWorkflowCommand)
    {
        Owner owner;
        CheckOwner(context, command.Name, out owner);
        // Checking instance.Owner is like an InstanceLockQueryResult.
        context.QueriedInstanceStore(new InstanceLockQueryResult(context.InstanceView.InstanceId, context.InstanceView.InstanceOwner.InstanceOwnerId));

        XName ownerService = null;
        InstanceValue value;
        Instance runnableInstance = default(Instance);
        bool foundRunnableInstance = false;

        value = QueryPropertyBag(WorkflowNamespace.WorkflowHostType, owner.Data);
        if (value != null && value.Value is XName)
        {
            ownerService = (XName)value.Value;
        }

        foreach (KeyValuePair<Guid, Instance> instance in MemoryStore.instances)
        {
            if (instance.Value.Owner != Guid.Empty || instance.Value.Completed)
            {
                continue;
            }

            if (ownerService != null)
            {
                value = QueryPropertyBag(WorkflowNamespace.WorkflowHostType, instance.Value.Metadata);
                if (value == null || ((XName)value.Value) != ownerService)
                {
                    continue;
                }
            }

            value = QueryPropertyBag(WorkflowServiceNamespace.SuspendReason, instance.Value.Metadata);
            if (value != null && value.Value != null && value.Value is string)
            {
                continue;
            }

            value = QueryPropertyBag(WorkflowNamespace.Status, instance.Value.Data);
            if (value != null && value.Value is string && ((string)value.Value) == "Executing")
            {
                runnableInstance = instance.Value;
                foundRunnableInstance = true;
            }

            if (!foundRunnableInstance)
            {
                value = QueryPropertyBag(XNamespace.Get("urn:schemas-microsoft-com:System.Activities/4.0/properties").GetName("TimerExpirationTime"), instance.Value.Data);
                if (value != null && value.Value is DateTime && ((DateTime)value.Value) <= DateTime.UtcNow)
                {
                    runnableInstance = instance.Value;
                    foundRunnableInstance = true;
                }
            }

            if (foundRunnableInstance)
            {
                runnableInstance.LockVersion++;
                runnableInstance.Owner = context.InstanceView.InstanceOwner.InstanceOwnerId;
                MemoryStore.instances[instance.Key] = runnableInstance;
                context.BindInstance(instance.Key);
                context.BindAcquiredLock(runnableInstance.LockVersion);

                Dictionary<Guid, IDictionary<XName, InstanceValue>> associatedKeys = new Dictionary<Guid, IDictionary<XName, InstanceValue>>();
                Dictionary<Guid, IDictionary<XName, InstanceValue>> completedKeys = new Dictionary<Guid, IDictionary<XName, InstanceValue>>();
                foreach (KeyValuePair<Guid, Key> keyEntry in MemoryStore.keys)
                {
                if (keyEntry.Value.Instance == context.InstanceView.InstanceId)
                {
                    if (keyEntry.Value.Completed)
                    {
                        completedKeys.Add(keyEntry.Key, DeserializePropertyBag(keyEntry.Value.Metadata));
                    }
                    else
                    {
                        associatedKeys.Add(keyEntry.Key, DeserializePropertyBag(keyEntry.Value.Metadata));
                    }
                }
            }

            context.LoadedInstance(InstanceState.Initialized, DeserializePropertyBag(runnableInstance.Data), DeserializePropertyBag(runnableInstance.Metadata), associatedKeys, completedKeys);
            break;
        }
    }
    ```

    위의 코드 조각에서 인스턴스 저장소는 실행 가능한 인스턴스를 검색합니다. 인스턴스가 있으면 실행 컨텍스트에 바인딩되어 로드됩니다.

## <a name="using-a-custom-instance-store"></a>사용자 지정 인스턴스 저장소 사용

사용자 지정 인스턴스 저장소를 구현하려면 인스턴스 저장소의 인스턴스를 <xref:System.Activities.WorkflowApplication.InstanceStore%2A>에 할당하고 <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> 메서드를 구현합니다. 참조 된 [방법: 만들기 및 장기 실행 워크플로 실행](how-to-create-and-run-a-long-running-workflow.md) 세부 사항에 대 한 자습서입니다.

## <a name="a-sample-instance-store"></a>샘플 인스턴스 저장소

다음 코드 샘플에서 가져온 전체 인스턴스 저장소 구현 되는 [기업 구매 프로세스](./samples/corporate-purchase-process.md) 샘플입니다. 이 인스턴스 저장소는XML을 사용하여 워크플로 데이터를 파일에 유지합니다.

```csharp
using System;
using System.Activities.DurableInstancing;
using System.Collections.Generic;
using System.IO;
using System.Runtime.DurableInstancing;
using System.Runtime.Serialization;
using System.ServiceModel.Persistence;
using System.Xml;
using System.Xml.Linq;

namespace Microsoft.Samples.WF.PurchaseProcess
{

    public class XmlWorkflowInstanceStore : InstanceStore
    {
        Guid ownerInstanceID;

        public XmlWorkflowInstanceStore() : this(Guid.NewGuid())
        {

        }

        public XmlWorkflowInstanceStore(Guid id)
        {
            ownerInstanceID = id;
        }

        //Synchronous version of the Begin/EndTryCommand functions
        protected override bool TryCommand(InstancePersistenceContext context, InstancePersistenceCommand command, TimeSpan timeout)
        {
            return EndTryCommand(BeginTryCommand(context, command, timeout, null, null));
        }

        //The persistence engine will send a variety of commands to the configured InstanceStore,
        //such as CreateWorkflowOwnerCommand, SaveWorkflowCommand, and LoadWorkflowCommand.
        //This method is where we will handle those commands
        protected override IAsyncResult BeginTryCommand(InstancePersistenceContext context, InstancePersistenceCommand command, TimeSpan timeout, AsyncCallback callback, object state)
        {
            IDictionary<XName, InstanceValue> data = null;

            //The CreateWorkflowOwner command instructs the instance store to create a new instance owner bound to the instanace handle
            if (command is CreateWorkflowOwnerCommand)
            {
                context.BindInstanceOwner(ownerInstanceID, Guid.NewGuid());
            }
            //The SaveWorkflow command instructs the instance store to modify the instance bound to the instance handle or an instance key
            else if (command is SaveWorkflowCommand)
            {
                SaveWorkflowCommand saveCommand = (SaveWorkflowCommand)command;
                data = saveCommand.InstanceData;

                Save(data);
            }
            //The LoadWorkflow command instructs the instance store to lock and load the instance bound to the identifier in the instance handle
            else if (command is LoadWorkflowCommand)
            {
                string fileName = IOHelper.GetFileName(this.ownerInstanceID);

                try
                {
                    using (FileStream inputStream = new FileStream(fileName, FileMode.Open))
                    {
                        data = LoadInstanceDataFromFile(inputStream);
                        //load the data into the persistence Context
                        context.LoadedInstance(InstanceState.Initialized, data, null, null, null);
                    }
                }
                catch (Exception exception)
                {
                    throw new PersistenceException(exception.Message);
                }
            }

            return new CompletedAsyncResult<bool>(true, callback, state);
        }

        protected override bool EndTryCommand(IAsyncResult result)
        {
            return CompletedAsyncResult<bool>.End(result);
        }

        //Reads data from xml file and creates a dictionary based off of that.
        IDictionary<XName, InstanceValue> LoadInstanceDataFromFile(Stream inputStream)
        {
            IDictionary<XName, InstanceValue> data = new Dictionary<XName, InstanceValue>();

            NetDataContractSerializer s = new NetDataContractSerializer();

            XmlReader rdr = XmlReader.Create(inputStream);
            XmlDocument doc = new XmlDocument();
            doc.Load(rdr);

            XmlNodeList instances = doc.GetElementsByTagName("InstanceValue");
            foreach (XmlElement instanceElement in instances)
            {
                XmlElement keyElement = (XmlElement)instanceElement.SelectSingleNode("descendant::key");
                XName key = (XName)DeserializeObject(s, keyElement);

                XmlElement valueElement = (XmlElement)instanceElement.SelectSingleNode("descendant::value");
                object value = DeserializeObject(s, valueElement);
                InstanceValue instVal = new InstanceValue(value);

                data.Add(key, instVal);
            }

            return data;
        }

        object DeserializeObject(NetDataContractSerializer serializer, XmlElement element)
        {
            object deserializedObject = null;

            MemoryStream stm = new MemoryStream();
            XmlDictionaryWriter wtr = XmlDictionaryWriter.CreateTextWriter(stm);
            element.WriteContentTo(wtr);
            wtr.Flush();
            stm.Position = 0;

            deserializedObject = serializer.Deserialize(stm);

            return deserializedObject;
        }

        //Saves the persistence data to an xml file.
        void Save(IDictionary<XName, InstanceValue> instanceData)
        {
            string fileName = IOHelper.GetFileName(this.ownerInstanceID);
            XmlDocument doc = new XmlDocument();
            doc.LoadXml("<InstanceValues/>");

            foreach (KeyValuePair<XName,InstanceValue> valPair in instanceData)
            {
                XmlElement newInstance = doc.CreateElement("InstanceValue");

                XmlElement newKey = SerializeObject("key", valPair.Key, doc);
                newInstance.AppendChild(newKey);

                XmlElement newValue = SerializeObject("value", valPair.Value.Value, doc);
                newInstance.AppendChild(newValue);

                doc.DocumentElement.AppendChild(newInstance);
            }
            doc.Save(fileName);
       }

        XmlElement SerializeObject(string elementName, object o, XmlDocument doc)
        {
            NetDataContractSerializer s = new NetDataContractSerializer();
            XmlElement newElement = doc.CreateElement(elementName);
            MemoryStream stm = new MemoryStream();

            s.Serialize(stm, o);
            stm.Position = 0;
            StreamReader rdr = new StreamReader(stm);
            newElement.InnerXml = rdr.ReadToEnd();

            return newElement;
        }
    }
}
```
