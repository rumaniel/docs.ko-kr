---
title: '방법: 사용자 지정 지속성 참가자 만들기'
ms.date: 03/30/2017
ms.assetid: 1d9cc47a-8966-4286-94d5-4221403d9c06
ms.openlocfilehash: 47283375b618422d91a6279ee9049fae469f540a
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989675"
---
# <a name="how-to-create-a-custom-persistence-participant"></a>방법: 사용자 지정 지속성 참가자 만들기
다음 절차에서는 지속성 참석자를 만드는 단계에 대해 설명합니다. 지 속성 참가자의 샘플 구현에 대 한 내용은 지 속성 샘플 및 [저장소 확장성](store-extensibility.md) [에 참여](https://go.microsoft.com/fwlink/?LinkID=177735) 항목을 참조 하세요.  
  
1. <xref:System.Activities.Persistence.PersistenceParticipant> 또는 <xref:System.Activities.Persistence.PersistenceIOParticipant> 클래스에서 파생되는 클래스를 만듭니다. PersistenceIOParticipant 클래스는 i/o 작업에 참여할 수 있는 것 외에도 PersistenceParticipant 클래스와 동일한 확장 요소를 제공 합니다. 다음 단계 중 하나 이상을 수행합니다.  
  
2. <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> 메서드를 구현합니다. **CollectValues** 메서드에는 두 개의 사전 매개 변수가 있습니다. 하나는 읽기/쓰기 값을 저장 하 고 다른 하나는 쓰기 전용 값을 저장 하는 데 사용 됩니다. 하나는 나중에 쿼리에서 사용 됩니다. 이 메서드에서 이 두 사전 매개 변수를 지속성 참석자 관련 데이터로 채워야 합니다. 각 사전은 값 이름을 키로 포함하고 값을 <xref:System.Runtime.DurableInstancing.InstanceValue> 개체로 포함합니다.  
  
    ReadWriteValues 사전의 값은 **InstanceValue** 개체로 패키지 됩니다. 쓰기 전용 사전의 값은 InstanceValueOptions 및 InstanceValueOption 집합을 사용 하 여 **InstanceValue** 개체로 패키지 됩니다. 모든 지 속성 참가자의 **CollectValues** 구현에서 제공 하는 각 **InstanceValue** 에는 고유한 이름이 있어야 합니다.
  
    ```csharp  
    protected virtual void CollectValues(out IDictionary<XName,Object> readWriteValues, out IDictionary<XName,Object> writeOnlyValues)
    {
    }
    ```  
  
3. <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> 메서드를 구현합니다. **Mapvalues** 메서드는 **CollectValues** 메서드에서 받는 매개 변수와 비슷한 두 개의 매개 변수를 사용 합니다. **CollectValues** 단계에서 수집 되는 모든 값은 이러한 사전 매개 변수를 통해 전달 됩니다. **Mapvalues** 단계에서 추가 된 새 값은 쓰기 전용 값에 추가 됩니다.  쓰기 전용 사전은 인스턴스 값에 직접 연결하지 않고 데이터를 외부 소스에 제공하는 데 사용됩니다. 모든 지 속성 참가자의 **Mapvalues** 메서드 구현에서 제공 하는 각 값에는 고유한 이름이 있어야 합니다.  
  
    ```csharp  
    protected virtual IDictionary<XName,Object> MapValues(IDictionary<XName,Object> readWriteValues,IDictionary<XName,Object> writeOnlyValues)
    {
    }
    ```  
  
     <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> 메서드는 <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A>가 제공하지 않지만, <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A>에서 아직 처리하지 않은 다른 지속성 참석자가 제공한 다른 값에 대한 종속성을 허용하는 기능을 제공합니다.  
  
4. 가 나 **값** 메서드를 구현 합니다. 지 속성 **값** 메서드는 지 속성 저장소에서 로드 된 모든 값을 포함 하는 사전을 받습니다.  
  
    ```csharp  
    protected virtual void PublishValues(IDictionary<XName,Object> readWriteValues)
    {
    }
    ```  
  
5. 참가자가 지 속성 i/o 참가자 인 경우 **beginonsave로** 메서드를 구현 합니다. 이 메서드는 저장 작업 중에 호출됩니다. 이 메서드에서는 보충 모델로 (저장) 워크플로 인스턴스에 i/o를 수행 해야 합니다.  호스트에서 해당 지속성 명령에 대해 트랜잭션을 사용할 경우 동일한 트랜잭션이 Transaction.Current에 제공됩니다.  또한 PersistenceIOParticipants에서는 트랜잭션 일관성 요구 사항을 알릴 수 있습니다. 이 경우 호스트에서는 요구 사항과 달리 사용되지 않는 지속성 에피소드에 대한 트랜잭션을 만듭니다.  
  
    ```csharp  
    protected virtual IAsyncResult BeginOnSave(IDictionary<XName,Object> readWriteValues, IDictionary<XName,Object> writeOnlyValues, TimeSpan timeout, AsyncCallback callback, Object state)
    {
    }
    ```  
  
6. 참가자가 지 속성 i/o 참가자 인 경우 **Beginonload** 메서드를 구현 합니다. 이 메서드는 로드 작업 중에 호출됩니다. 이 방법에서는 워크플로 인스턴스를 로드 하는 데 i/o 보충 모델로를 수행 해야 합니다. 호스트에서 해당 지속성 명령에 대해 트랜잭션을 사용할 경우 동일한 트랜잭션이 Transaction.Current에 제공됩니다. 또한 지 속성 i/o 참가자는 트랜잭션 일관성 요구 사항을 알릴 수 있습니다 .이 경우 다른 방법으로는 사용 되지 않는 경우 호스트가 지 속성 에피소드에 대 한 트랜잭션을 만듭니다.  
  
    ```csharp  
    protected virtual IAsyncResult BeginOnLoad(IDictionary<XName,Object> readWriteValues, TimeSpan timeout, AsyncCallback callback, Object state)
    {
    }
    ```
