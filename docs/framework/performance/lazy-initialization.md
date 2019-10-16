---
title: 초기화 지연
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lazy initialization in .NET, introduction
ms.assetid: 56b4ae5c-4745-44ff-ad78-ffe4fcde6b9b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 549030b7e5f7544f593e5aa481a6dc85d5a85329
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046405"
---
# <a name="lazy-initialization"></a>초기화 지연
개체 *초기화 지연*은 개체를 처음 사용할 때까지 생성이 지연된다는 의미입니다. (이 항목의 경우 *초기화 지연*과 *인스턴스화 지연*은 동의어임). 초기화 지연은 기본적으로 성능을 향상시키는 데 사용하며, 불필요한 계산을 방지하고, 프로그램 메모리 요구 사항을 줄입니다. 다음은 가장 일반적인 시나리오입니다.  
  
- 만드는 데 비용이 많이 드는 개체가 있으며 프로그램에서 이 개체를 사용하지 않는 경우가 있습니다. 예를 들어 초기화되기 위해 데이터베이스 연결이 필요한 큰 `Order` 개체 배열이 포함된 `Orders` 속성이 있는 `Customer` 개체가 메모리에 있다고 가정합니다. 사용자는 주문을 표시하거나 계산에서 데이터를 사용하도록 요청하지 않으면 시스템 메모리 또는 계산 주기를 사용하여 만들 이유가 없습니다. `Lazy<Orders>`를 사용하여 `Orders` 개체의 초기화 지연을 선언하면 개체를 사용하지 않을 때 시스템 리소스 낭비를 방지할 수 있습니다.  
  
- 만드는 데 비용이 많이 드는 개체가 있고 다른 비용이 많이 드는 작업이 완료될 때까지 생성을 지연시키려는 경우가 있습니다. 예를 들어, 프로그램을 시작할 때 여러 개체 인스턴스를 로드하지만 그중 일부만 즉시 필요합니다. 필요한 개체를 만들 때까지 필요하지 않은 개체의 초기화를 지연하여 프로그램의 시작 성능을 향상시킬 수 있습니다.  
  
 초기화 지연을 수행하도록 고유 코드를 작성할 수 있지만 <xref:System.Lazy%601>를 대신 사용하는 것이 좋습니다. <xref:System.Lazy%601> 및 관련 유형에서도 스레드로부터 안전을 지원하고 일관된 예외 전파 정책을 제공합니다.  
  
 다음 표에는 다양한 시나리오에서 초기화 지연을 사용하도록 .NET Framework 버전 4에서 제공하는 유형이 나열되어 있습니다.  
  
|형식|Description|  
|----------|-----------------|  
|<xref:System.Lazy%601>|클래스 라이브러리 또는 사용자 정의 형식에 대한 초기화 지연 의미 체계를 제공하는 래퍼 클래스입니다.|  
|<xref:System.Threading.ThreadLocal%601>|스레드-로컬 기반으로 초기화 지연 의미 체계를 제공한다는 점을 제외하고는 <xref:System.Lazy%601>와 비슷합니다. 모든 스레드는 고유 값에 액세스할 수 있습니다.|  
|<xref:System.Threading.LazyInitializer>|클래스의 오버헤드 없이 개체의 초기화 지연을 위한 고급 `static`(Visual Basic의 `Shared`) 메서드를 제공합니다.|  
  
## <a name="basic-lazy-initialization"></a>기본 초기화 지연  
 초기화 지연 형식(예: `MyType`)을 지정하려면 다음 예에 표시된 대로 `Lazy<MyType>`(Visual Basic에서 `Lazy(Of MyType)`)을 사용하세요. <xref:System.Lazy%601> 생성자에 대리자가 전달되지 않으면 값 속성에 처음 액세스할 때 <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>을 사용하여 래핑된 형식이 생성됩니다. 형식에 매개 변수가 없는 생성자가 없는 경우 런타임 예외가 throw 됩니다.  
  
 다음 예에서 `Orders`는 데이터베이스에서 검색된 `Order` 개체의 배열을 포함하는 클래스라고 가정합니다. `Customer` 개체에는 `Orders`의 인스턴스가 포함되어 있지만 사용자 작업에 따라 `Orders` 개체의 데이터가 필요하지 않을 수 있습니다.  
  
 [!code-csharp[Lazy#1](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#1)]
 [!code-vb[Lazy#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#1)]  
  
 생성 시 래핑된 형식에서 특정 생성자 오버로드를 호출하는 <xref:System.Lazy%601> 생성자에서 대리자를 전달할 수도 있고, 다음 예에 표시된 대로 필수인 기타 초기화 단계를 수행할 수 있습니다.  
  
 [!code-csharp[Lazy#2](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#2)]
 [!code-vb[Lazy#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#2)]  
  
 지연 개체를 만들고 나면 지연 변수의 <xref:System.Lazy%601.Value%2A> 속성에 처음으로 액세스할 때까지 `Orders`의 인스턴스가 생성되지 않습니다. 처음 액세스할 때 래핑된 형식이 생성되고 반환되며 나중에 액세스하는 데 사용하기 위해 저장됩니다.  
  
 [!code-csharp[Lazy#3](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#3)]
 [!code-vb[Lazy#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#3)]  
  
 <xref:System.Lazy%601> 개체는 항상 초기화 시 사용된 값 또는 개체와 동일한 값 또는 개체를 반환합니다. 따라서 <xref:System.Lazy%601.Value%2A> 속성은 읽기 전용입니다. <xref:System.Lazy%601.Value%2A>에서 참조 형식을 저장하면 새로운 개체를 할당할 수 없습니다. (그러나 설정 가능한 공용 필드와 속성 값은 변경할 수 있습니다.) <xref:System.Lazy%601.Value%2A>에서 값 형식을 저장하는 경우 해당 값을 수정할 수 없습니다. 그렇지만 새 인수를 사용하여 변수 생성자를 다시 호출하면 새 변수를 만들 수 있습니다.  
  
 [!code-csharp[Lazy#4](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#4)]
 [!code-vb[Lazy#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#4)]  
  
 이전 지연 인스턴스와 같이 새로운 지연 인스턴스는 <xref:System.Lazy%601.Value%2A> 속성에 처음 액세스할 때까지 `Orders`를 인스턴스화하지 않습니다.  
  
### <a name="thread-safe-initialization"></a>스레드로부터 안전한 초기화  
 기본적으로 <xref:System.Lazy%601> 개체는 스레드로부터 안전합니다. 즉, 생성자가 스레드 보안 유형을 지정하지 않으면 생성된 <xref:System.Lazy%601> 개체는 스레드로부터 안전합니다. 다중 스레드 시나리오에서 스레드로부터 안전한 <xref:System.Lazy%601> 개체의 <xref:System.Lazy%601.Value%2A> 속성에 액세스하는 첫 번째 스레드가 모든 스레드에서의 모든 후속 액세스를 위해 개체를 초기화하고 모든 스레드에서 동일한 데이터를 공유합니다. 따라서 어떤 스레드가 개체를 초기화하는지는 중요하지 않으며 경합 상태는 심각하지 않습니다.  
  
> [!NOTE]
> 예외 캐싱을 사용하여 이러한 일관성을 오류 조건까지 확장할 수 있습니다. 자세한 내용은 다음 섹션인 [Lazy 개체의 예외](lazy-initialization.md#ExceptionsInLazyObjects)를 참조하세요.  
  
 다음 예에서는 동일한 `Lazy<int>` 인스턴스에서는 개별 스레드의 값이 동일함을 보여 줍니다.  
  
 [!code-csharp[Lazy#8](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#8)]
 [!code-vb[Lazy#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#8)]  
  
 스레드마다 개별 데이터가 필요한 경우 이 항목의 뒷부분에 설명된 대로 <xref:System.Threading.ThreadLocal%601> 형식을 사용합니다.  
  
 일부 <xref:System.Lazy%601> 생성자에는 여러 스레드에서 <xref:System.Lazy%601.Value%2A> 속성에 액세스할지 지정하는 데 사용하는 `isThreadSafe`라는 부울 매개 변수가 있습니다. 하나의 스레드에서만 속성에 액세스하게 하려는 경우 `false`를 전달하여 보통 수준의 성능 이점을 얻을 수 있습니다. 여러 스레드에서 속성에 액세스하게 하려면 `true`를 전달하여 초기화 시 한 스레드에서 예외 처리를 하는 경합 상태를 올바르게 처리하도록 <xref:System.Lazy%601> 인스턴스에 지시합니다.  
  
 일부 <xref:System.Lazy%601> 생성자에는 `mode`라는 <xref:System.Threading.LazyThreadSafetyMode> 매개 변수가 있습니다. 이러한 생성자는 추가 스레드 보안 모드를 제공합니다. 다음 표에서는 스레드 보안을 지정하는 생성자 매개 변수가 <xref:System.Lazy%601> 개체의 스레드 보안에 미치는 영향을 보여 줍니다. 각 생성자에는 이러한 매개 변수가 최대 한 개 있습니다.  
  
|개체의 스레드 보안|`LazyThreadSafetyMode` `mode` 매개 변수|부울 `isThreadSafe` 매개 변수|스레드 보안 매개 변수 없음|  
|---------------------------------|---------------------------------------------|--------------------------------------|---------------------------------|  
|완벽하게 스레드로부터 안전. 한 번에 하나의 스레드만 값을 초기화하려고 합니다.|<xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication>|`true`|예.|  
|스레드로부터 안전하지 않음.|<xref:System.Threading.LazyThreadSafetyMode.None>|`false`|이 오류에는 이 작업을 적용할 수 없습니다.|  
|완벽하게 스레드로부터 안전. 스레드에서 값을 초기화하기 위해 경합합니다.|<xref:System.Threading.LazyThreadSafetyMode.PublicationOnly>|이 오류에는 이 작업을 적용할 수 없습니다.|이 오류에는 이 작업을 적용할 수 없습니다.|  
  
 표에 표시된 바와 같이 `mode` 매개 변수에 대해 <xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?displayProperty=nameWithType>을 지정하면 `isThreadSafe` 매개 변수에 대해 `true`를 지정하는 것과 같으며 <xref:System.Threading.LazyThreadSafetyMode.None?displayProperty=nameWithType>을 지정하면 `false`를 지정하는 것과 같습니다.  
  
 <xref:System.Threading.LazyThreadSafetyMode.PublicationOnly?displayProperty=nameWithType>을 지정하면 여러 스레드에서 <xref:System.Lazy%601> 인스턴스를 초기화하려고 시도할 수 있습니다. 하나의 스레드만 이 경합에서 이길 수 있고 다른 모든 스레드는 성공한 스레드를 통해 초기화된 값을 받습니다. 초기화 중에 스레드에서 예외가 throw되면 해당 스레드는 성공한 스레드를 통해 설정된 값을 받지 못합니다. 예외가 캐시되지 않으므로 다음에 <xref:System.Lazy%601.Value%2A> 속성에 액세스하려고 하면 초기화할 수 있습니다. 이 방식은 다음 섹션에 설명된 대로 다른 모드에서 예외를 처리하는 방식과는 다릅니다. 자세한 내용은 <xref:System.Threading.LazyThreadSafetyMode> 열거형을 참조하세요.  
  
<a name="ExceptionsInLazyObjects"></a>   
## <a name="exceptions-in-lazy-objects"></a>Lazy 개체의 예외  
 앞에서 설명한 것처럼 <xref:System.Lazy%601> 개체는 항상 초기화 시와 동일한 개체 또는 값을 반환하므로 <xref:System.Lazy%601.Value%2A> 속성은 읽기 전용입니다. 예외 캐싱을 사용하도록 설정하면 이 불변성이 예외 동작까지 확장됩니다. 지연 초기화 된 개체에 예외 캐싱이 설정 되어 있고 속성에 <xref:System.Lazy%601.Value%2A> 처음 액세스할 때 초기화 메서드에서 예외를 throw 하는 경우 모든 후속 시도에서 <xref:System.Lazy%601.Value%2A> 속성에 대 한 액세스를 다시 시도할 때마다 동일한 예외가 throw 됩니다. . 즉, 다중 스레드 시나리오에서도 래핑된 형식의 생성자가 다시 호출되지 않습니다. 따라서 <xref:System.Lazy%601> 개체는 한 번의 액세스에서 예외 처리를 할 수 없으며 후속 액세스에서 값을 반환할 수 없습니다.  
  
 초기화 메서드(`valueFactory` 매개 변수)를 사용하는 <xref:System.Lazy%601?displayProperty=nameWithType> 생성자를 사용할 때 예외 캐싱이 사용됩니다. 예를 들어 `Lazy(T)(Func(T))` 생성자를 사용할 때 사용됩니다. 생성자에서 <xref:System.Threading.LazyThreadSafetyMode> 값(`mode` 매개 변수)도 사용하는 경우 <xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication?displayProperty=nameWithType> 또는 <xref:System.Threading.LazyThreadSafetyMode.None?displayProperty=nameWithType>을 지정하세요. 초기화 메서드를 지정하면 이 두 모드에 대해 예외 캐싱을 사용합니다. 초기화 메서드는 매우 간단할 수 있습니다. `T`예를 들어, `new Lazy<Contents>(() => new Contents(), mode)` 에서 C#또는 `New Lazy(Of Contents)(Function() New Contents())` Visual Basic에 대해 매개 변수가 없는 생성자를 호출할 수 있습니다. 초기화 메소드를 지정하지 않는 <xref:System.Lazy%601?displayProperty=nameWithType> 생성자를 사용하는 경우 `T`의 매개 변수가 없는 생성자가 throw하는 예외는 캐싱되지 않습니다. 자세한 내용은 <xref:System.Threading.LazyThreadSafetyMode> 열거형을 참조하세요.  
  
> [!NOTE]
> `isThreadSafe` 생성자 매개 변수를 `false`로 설정하거나 `mode` 생성자 매개 변수를 <xref:System.Threading.LazyThreadSafetyMode.None?displayProperty=nameWithType>으로 설정하여 <xref:System.Lazy%601> 개체를 만들면 단일 스레드에서 <xref:System.Lazy%601> 개체에 액세스하거나 고유 동기화를 제공해야 합니다. 그러면 예외 캐싱을 포함하여 개체의 모든 요소에 적용됩니다.  
  
 이전 섹션에서 설명한 대로 <xref:System.Threading.LazyThreadSafetyMode.PublicationOnly?displayProperty=nameWithType>을 지정하여 만든 <xref:System.Lazy%601> 개체는 예외를 다르게 처리합니다. <xref:System.Threading.LazyThreadSafetyMode.PublicationOnly>를 사용하면 여러 스레드에서 <xref:System.Lazy%601> 인스턴스를 초기화하기 위해 경쟁할 수 있습니다. 이 경우 예외가 캐시되지 않고, 초기화에 성공할 때까지 <xref:System.Lazy%601.Value%2A> 속성에 계속 액세스하려고 시도할 수 있습니다.  
  
 다음 표에는 <xref:System.Lazy%601> 생성자가 예외 캐싱을 제어하는 방식이 요약되어 있습니다.  
  
|생성자|스레드 보안 모드|초기화 메서드 사용|예외가 캐시됨|  
|-----------------|------------------------|--------------------------------|---------------------------|  
|Lazy(T)()|(<xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication>)|아니요|아니요|  
|Lazy(T)(Func(T))|(<xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication>)|예|예|  
|Lazy(T)(Boolean)|`True`(<xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication>) 또는 `false`(<xref:System.Threading.LazyThreadSafetyMode.None>)|아니요|아니요|  
|Lazy(T)(Func(T), Boolean)|`True`(<xref:System.Threading.LazyThreadSafetyMode.ExecutionAndPublication>) 또는 `false`(<xref:System.Threading.LazyThreadSafetyMode.None>)|예|예|  
|Lazy(T)(LazyThreadSafetyMode)|사용자 지정|아니요|아니요|  
|Lazy(T)(Func(T), LazyThreadSafetyMode)|사용자 지정|예|사용자가 <xref:System.Threading.LazyThreadSafetyMode.PublicationOnly>를 지정하는 경우 No, 지정하지 않으면 Yes.|  
  
## <a name="implementing-a-lazy-initialized-property"></a>초기화 지연 속성 구현  
 초기화 지연을 사용하여 공용 속성을 구현하려면 속성의 지원 필드를 <xref:System.Lazy%601>로 정의하고 속성의 `get` 접근자에서 <xref:System.Lazy%601.Value%2A> 속성을 반환합니다.  
  
 [!code-csharp[Lazy#5](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#5)]
 [!code-vb[Lazy#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#5)]  
  
 <xref:System.Lazy%601.Value%2A> 속성은 읽기 전용입니다. 따라서 이 속성을 노출하는 속성에는 `set` 접근자가 없습니다. <xref:System.Lazy%601> 개체에서 지원하는 읽기/쓰기 속성이 필요하면 `set` 접근자가 새로운 <xref:System.Lazy%601> 개체를 만들어 백업 저장소에 할당해야 합니다. `set` 접근자는 `set` 접근자에 전달된 새 속성 값을 반환하는 람다 식을 생성해야 하며 이 람다 식을 새로운 <xref:System.Lazy%601> 개체의 생성자에 전달해야 합니다. 다음번에 <xref:System.Lazy%601.Value%2A> 속성에 액세스하면 새로운 <xref:System.Lazy%601>가 초기화되고, 그 이후로 <xref:System.Lazy%601.Value%2A> 속성이 속성에 할당된 새 값을 반환합니다. 이와 같이 복잡하게 배열하는 이유는 <xref:System.Lazy%601>에 기본 제공된 다중 스레딩 보호를 유지하기 위해서입니다. 그러지 않으면 속성 접근자가 <xref:System.Lazy%601.Value%2A> 속성을 통해 반환된 첫 번째 값을 캐시하고 캐시된 값만 수정해야 하며, 이 작업을 수행하려면 스레드로부터 안전한 코드를 고유하게 작성해야 합니다. <xref:System.Lazy%601> 개체에서 지원하는 읽기/쓰기 속성에 필요한 추가 초기화때문에 성능이 문제가 될 수 있습니다. 또한 특정 시나리오에 따라 setter와 getter 사이의 경합 상태를 방지하기 위해 추가 조정이 필요할 수 있습니다.  
  
## <a name="thread-local-lazy-initialization"></a>스레드 로컬 초기화 지연  
 일부 다중 스레드 시나리오에서는 각 스레드에 고유 개인 데이터를 제공할 수 있습니다. 이러한 데이터는 *스레드 로컬 데이터*라고 합니다. .NET Framework 버전 3.5 이하에서 `ThreadStatic` 특성을 정적 변수에 적용하여 스레드 로컬로 만들 수 있습니다. 그러나 `ThreadStatic` 특성을 사용하면 사소한 오류가 발생할 수 있습니다. 예를 들어 다음 예제에 표시된 대로 기본 초기화 명령문도 액세스하는 첫 번째 스레드에서만 변수가 초기화되게 합니다.  
  
 [!code-csharp[Lazy#6](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#6)]
 [!code-vb[Lazy#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#6)]  
  
 다른 모든 스레드에서는 변수가 기본값(0)을 사용하여 초기화됩니다. .NET Framework 버전 4의 대안으로 <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> 유형을 사용하여 인스턴스 기반의 스레드 지역 변수를 만들 수 있습니다. 이 변수는 사용자가 제공하는 <xref:System.Action%601> 대리자가 모든 스레드에서 초기화됩니다. 다음 예제에서 `counter`에 액세스하는 모든 스레드에는 시작 값이 1로 표시됩니다.  
  
 [!code-csharp[Lazy#7](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#7)]
 [!code-vb[Lazy#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#7)]  
  
 <xref:System.Threading.ThreadLocal%601>에서는 <xref:System.Lazy%601>와 거의 동일한 방식으로 개체를 래핑합니다. 단, 다음과 같은 중요한 차이점이 있습니다.  
  
- 각 스레드가 다른 스레드에서 액세스할 수 없는 고유한 개인 데이터를 사용하여 스레드 지역 변수를 초기화합니다.  
  
- <xref:System.Threading.ThreadLocal%601.Value%2A?displayProperty=nameWithType> 속성은 읽기-쓰기이고 여러 번 수정할 수 있습니다. 따라서 예외 전파에 영향을 미칠 수 있습니다. 예를 들어 하나의 `get` 작업에서는 예외가 throw될 수 있지만, 다른 작업에서는 성공적으로 값을 초기화할 수 있습니다.  
  
- 초기화 대리자가 제공되지 않으면 <xref:System.Threading.ThreadLocal%601>에서 형식의 기본값을 사용하여 래핑된 형식을 초기화합니다. 이런 점에서 <xref:System.Threading.ThreadLocal%601>은 <xref:System.ThreadStaticAttribute> 특성과 일치합니다.  
  
 다음 예제에서는 `ThreadLocal<int>` 인스턴스에 액세스하는 모든 스레드가 고유한 데이터 복사본을 가져옵니다.  
  
 [!code-csharp[Lazy#9](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#9)]
 [!code-vb[Lazy#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#9)]  
  
## <a name="thread-local-variables-in-parallelfor-and-foreach"></a>Parallel.For 및 ForEach의 스레드 지역 변수  
 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 메서드 또는 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 메서드를 사용하여 데이터 소스를 병렬로 반복할 때 스레드 로컬 데이터 지원을 기본으로 제공하는 오버로드를 사용할 수 있습니다. 이러한 메서드에서는 데이터를 만들고 액세스하며 정리하기 위해 로컬 대리자를 사용하여 스레드 국부성을 달성합니다. 자세한 내용은 [방법: 스레드 로컬 변수를 사용하는 Parallel.For 루프 작성](../../standard/parallel-programming/how-to-write-a-parallel-for-loop-with-thread-local-variables.md) 및 [방법: 파티션 로컬 변수를 사용하는 Parallel.ForEach 루프 작성](../../standard/parallel-programming/how-to-write-a-parallel-foreach-loop-with-partition-local-variables.md)을 참조하세요.  
  
## <a name="using-lazy-initialization-for-low-overhead-scenarios"></a>오버헤드가 적은 시나리오에 초기화 지연 사용  
 다수의 개체를 초기화 지연해야 하는 시나리오에서는 <xref:System.Lazy%601>의 각 개체를 래핑하는 데 너무 많은 메모리 또는 너무 많은 계산 리소스가 필요한지 판별할 수 있습니다. 또는 초기화 지연 노출 방법에 대한 엄격한 요구 사항이 있을 수 있습니다. 이 경우 <xref:System.Threading.LazyInitializer?displayProperty=nameWithType> 클래스의 `static`(Visual Basic에서 `Shared`) 메서드를 사용하여 <xref:System.Lazy%601> 인스턴스에 래핑하지 않고 각 개체의 초기화를 지연할 수 있습니다.  
  
 다음 예에서는 하나의 <xref:System.Lazy%601> 개체에 전체 `Orders` 개체를 래핑하지 않고 필요한 경우에만 개별 `Order` 개체의 초기화를 지연합니다.  
  
 [!code-csharp[Lazy#10](../../../samples/snippets/csharp/VS_Snippets_Misc/lazy/cs/cs_lazycodefile.cs#10)]
 [!code-vb[Lazy#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/lazy/vb/lazy_vb.vb#10)]  
  
 이 예에서는 루프를 반복할 때마다 초기화 프로시저가 호출됩니다. 다중 스레드 시나리오에서 초기화 프로시저를 호출하는 첫 번째 스레드는 모든 스레드에 해당 값이 표시되는 스레드입니다. 나중에 스레드에서 초기화 프로시저도 호출하지만 해당 결과는 사용하지 않습니다. 이 유형의 잠재적 경합 상태가 허용되지 않는 경우 부울 인수와 동기화 개체를 사용하는 <xref:System.Threading.LazyInitializer.EnsureInitialized%2A?displayProperty=nameWithType>의 오버로드를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [관리되는 스레딩 기본 사항](../../standard/threading/managed-threading-basics.md)
- [스레드 및 스레딩](../../standard/threading/threads-and-threading.md)
- [TPL(작업 병렬 라이브러리)](../../standard/parallel-programming/task-parallel-library-tpl.md)
- [방법: 개체의 초기화 지연 수행](how-to-perform-lazy-initialization-of-objects.md)
