---
title: 확장 가능한 개체
ms.date: 03/30/2017
helpviewer_keywords:
- extensible objects [WCF]
ms.assetid: bc88cefc-31fb-428e-9447-6d20a7d452af
ms.openlocfilehash: 682c391e7b3c68de5bf799f77a93df7539681a37
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654498"
---
# <a name="extensible-objects"></a>확장 가능한 개체

새 기능과 함께 기존 런타임 클래스를 확장하거나 새 상태를 개체에 추가하기 위해 확장명 가능한 개체 패턴이 사용됩니다. 확장명 가능한 개체 중 하나에 연결된 확장은 이 개체에서 액세스할 수 있는 확장명 가능한 일반 개체에 연결된 공유 상태 및 기능에 액세스하는 처리 시에 매우 다른 단계에서 동작을 활성화합니다.

## <a name="the-iextensibleobjectt-pattern"></a>IExtensibleObject\<T > 패턴

확장명 가능한 개체 패턴에는 세 가지 인터페이스인 <xref:System.ServiceModel.IExtensibleObject%601>, <xref:System.ServiceModel.IExtension%601> 및 <xref:System.ServiceModel.IExtensionCollection%601>이 있습니다.

<xref:System.ServiceModel.IExtensibleObject%601> 인터페이스는 <xref:System.ServiceModel.IExtension%601> 개체가 해당 기능을 사용자 지정할 수 있도록 하는 형식에 의해 구현됩니다.

확장 가능한 개체를 사용하면 <xref:System.ServiceModel.IExtension%601> 개체를 동적으로 집계할 수 있습니다. <xref:System.ServiceModel.IExtension%601> 개체는 다음 인터페이스로 구분됩니다.

```csharp
public interface IExtension<T>
where T : IExtensibleObject<T>
{
    void Attach(T owner);
    void Detach(T owner);
}
```

형식 제한은 <xref:System.ServiceModel.IExtensibleObject%601>인 클래스에 대해서만 확장이 정의될 수 있도록 합니다. <xref:System.ServiceModel.IExtension%601.Attach%2A> 및 <xref:System.ServiceModel.IExtension%601.Detach%2A>는 집계 또는 분배 알림을 제공합니다.

구현에서 확장을 추가하고 소유자에서 제거할 수 있는 시기를 제한할 수 있습니다. 예를 들어 완전히 제거를 허용하지 않거나, 소유자 또는 확장이 특정 상태에 있을 때 확장 추가 또는 제거를 허용하지 않거나, 여러 소유자에 동시에 추가하는 것을 허용하지 않거나, 단일 추가 후에만 단일 제거를 허용할 수 있습니다.

<xref:System.ServiceModel.IExtension%601>에서는 다른 관리되는 표준 인터페이스와의 상호 작용을 나타내지 않습니다. 특히 소유자 개체의 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 메서드는 일반적으로 확장을 분리하지 않습니다.

확장명 컬렉션에 추가 되 면 <xref:System.ServiceModel.IExtension%601.Attach%2A> 컬렉션으로 이동 하기 전에 호출 됩니다. 컬렉션에서 확장 제거 되 면 <xref:System.ServiceModel.IExtension%601.Detach%2A> 제거 된 후 호출 됩니다. (적절 한 동기화를 가정할 경우) 하는 방법을 확장 수만 해당 하는 동안 컬렉션에서 발견 되 고 이것이 간의 <xref:System.ServiceModel.IExtension%601.Attach%2A> 고 <xref:System.ServiceModel.IExtension%601.Detach%2A>입니다.

<xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> 또는 <xref:System.ServiceModel.IExtensionCollection%601.Find%2A>에 전달된 개체가 <xref:System.ServiceModel.IExtension%601>일 필요는 없지만(예를 들어 아무 개체나 전달할 수 있음) 반환되는 확장은 <xref:System.ServiceModel.IExtension%601>입니다.

확장명이 컬렉션에 없는 경우는 <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> null을 반환 하 고 <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> 빈 컬렉션을 반환 합니다. 여러 확장을 구현 하는 경우 <xref:System.ServiceModel.IExtension%601>, <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> 그 중 하나를 반환 합니다. <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A>에서 반환되는 값은 스냅샷입니다.

두 가지 주요 시나리오가 있습니다. 첫 번째 시나리오에서는 <xref:System.ServiceModel.IExtensibleObject%601.Extensions%2A> 속성을 개체에 상태를 삽입하는 형식 기반 사전으로 사용하여 다른 구성 요소에서 해당 형식으로 개체를 조회할 수 있게 합니다.

두 번째 시나리오에서는 <xref:System.ServiceModel.IExtension%601.Attach%2A> 및 <xref:System.ServiceModel.IExtension%601.Detach%2A> 속성을 사용하여 개체가 이벤트 등록, 상태 전환 감시 등의 사용자 지정 동작에 참여할 수 있게 합니다.

<xref:System.ServiceModel.IExtensionCollection%601> 인터페이스는 <xref:System.ServiceModel.IExtension%601>을 형식별로 검색할 수 있는 <xref:System.ServiceModel.IExtension%601> 개체의 컬렉션입니다. <xref:System.ServiceModel.IExtensionCollection%601.Find%2A?displayProperty=nameWithType>는 해당 형식의 <xref:System.ServiceModel.IExtension%601> 중에서 최근 추가된 개체만 반환합니다.

### <a name="extensible-objects-in-windows-communication-foundation"></a>Windows Communication Foundation의 확장 가능한 개체

Windows Communication Foundation (WCF)에 네 개의 확장 가능한 개체:

- <xref:System.ServiceModel.ServiceHostBase> – 서비스 호스트의 기본 클래스입니다.  이 클래스의 확장을 사용하여 <xref:System.ServiceModel.ServiceHostBase> 자체의 동작을 확장하거나 각 서비스의 상태를 저장할 수 있습니다.

- <xref:System.ServiceModel.InstanceContext> – 이 클래스는 서비스 형식의 인스턴스를 서비스 런타임과 연결합니다.  인스턴스에 대한 정보와 <xref:System.ServiceModel.InstanceContext>의 포함 <xref:System.ServiceModel.ServiceHostBase>에 대한 참조가 들어 있습니다. 이 클래스의 확장을 사용하여 <xref:System.ServiceModel.InstanceContext>의 동작을 확장하거나 각 서비스의 상태를 저장할 수 있습니다.

- <xref:System.ServiceModel.OperationContext> – 이 클래스는 런타임에서 각 작업에 대해 수집하는 작업 정보를 나타냅니다.  여기에는 들어오는 메시지 헤더, 들어오는 메시지 속성, 들어오는 보안 ID, 기타 정보 등이 포함됩니다.  이 클래스의 확장은 <xref:System.ServiceModel.OperationContext>의 동작을 확장하거나 각 작업의 상태를 저장할 수 있습니다.

- <xref:System.ServiceModel.IContextChannel> –이 인터페이스는 채널 및 프록시에서 WCF 런타임에 의해 작성에 대 한 각 상태 검사에 대 한 허용 합니다.  이 클래스의 확장은 <xref:System.ServiceModel.IClientChannel>의 동작을 확장하거나 이 동작을 사용하여 각 채널의 상태를 저장할 수 있습니다.

다음 코드 예제에서는 단순한 확장을 사용하여 <xref:System.ServiceModel.InstanceContext> 개체를 추적하는 방법을 보여 줍니다.

[!code-csharp[IInstanceContextInitializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/iinstancecontextinitializer/cs/initializer.cs#1)]

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.IExtensibleObject%601>
- <xref:System.ServiceModel.IExtension%601>
- <xref:System.ServiceModel.IExtensionCollection%601>
