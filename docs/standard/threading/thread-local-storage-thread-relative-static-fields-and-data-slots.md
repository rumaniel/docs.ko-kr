---
title: '스레드 로컬 스토리지: 스레드 상대 정적 필드 및 데이터 슬롯'
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], local storage
- threading [.NET Framework], thread-relative static fields
- local thread storage
- TLS
ms.assetid: c633a4dc-a790-4ed1-96b5-f72bd968b284
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7beb22c68450d7ae4aeb6d0bcae45fafdfe78191
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490909"
---
# <a name="thread-local-storage-thread-relative-static-fields-and-data-slots"></a>스레드 로컬 스토리지: 스레드 상대 정적 필드 및 데이터 슬롯
관리되는 TLS(스레드 로컬 스토리지)를 사용하여 스레드 및 애플리케이션 도메인에 고유한 데이터를 저장할 수 있습니다. .NET Framework는 관리되는 TLS를 사용하는 두 가지 방법인 스레드 관련 정적 필드 및 데이터 슬롯을 제공합니다.  
  
- 컴파일 시간에 정확한 요구 사항을 예상할 수 있는 경우에는 스레드 관련 정적 필드(Visual Basic의 스레드 관련 `Shared` 필드)를 사용합니다. 스레드 관련 정적 필드는 최고의 성능을 제공합니다. 또한 컴파일 시간 형식 검사의 이점을 제공합니다.  
  
- 실제 요구 사항이 런타임에만 검색될 수 있는 경우에는 데이터 슬롯을 사용합니다. 데이터 슬롯은 스레드 관련 정적 필드보다 사용하기에 더 느리고 더 불편하고 데이터는 <xref:System.Object> 형식으로 저장되므로 사용하기 전에 올바른 형식으로 캐스트해야 합니다.  
  
 관리되지 않는 C++에서 `TlsAlloc`를 사용하여 슬롯을 동적으로 할당하고 `__declspec(thread)`를 사용하여 변수가 스레드 관련 스토리지에서 할당되어야 함을 선언합니다. 스레드 관련 정적 필드 및 데이터 슬롯은 이 동작의 관리되는 버전을 제공합니다.  
  
 .NET Framework 4에서 <xref:System.Threading.ThreadLocal%601?displayProperty=nameWithType> 클래스를 사용하여 개체가 처음 사용될 때 초기화가 지연되는 스레드 로컬 개체를 만들 수 있습니다. 자세한 내용은 [초기화 지연](../../../docs/framework/performance/lazy-initialization.md)을 참조하세요.  
  
## <a name="uniqueness-of-data-in-managed-tls"></a>관리되는 TLS의 데이터 고유성  
 스레드 관련 정적 필드 또는 데이터 슬롯을 사용할지 여부에 관계없이 관리되는 TLS의 데이터는 스레드 및 애플리케이션 도메인의 조합에 고유합니다.  
  
- 애플리케이션 도메인 내에서는 두 스레드가 동일한 필드 또는 슬롯을 사용하는 경우에도 한 스레드가 다른 스레드의 데이터를 수정할 수 없습니다.  
  
- 스레드가 여러 애플리케이션 도메인에서 동일한 필드나 슬롯에 액세스하는 경우 개별 값은 각 애플리케이션 도메인에서 유지 관리됩니다.  
  
 예를 들어 스레드가 스레드 관련 정적 필드의 값을 설정하고, 다른 애플리케이션 도메인에 들어간 다음, 필드 값을 검색할 경우 두 번째 애플리케이션 도메인에서 검색된 값은 첫 번째 애플리케이션 도메인의 값과 다릅니다. 두 번째 애플리케이션 도메인에서 필드에 대한 새 값을 설정해도 첫 번째 애플리케이션 도메인의 필드 값에 영향을 주지 않습니다.  
  
 마찬가지로 스레드가 두 개의 다른 애플리케이션 도메인에서 동일한 이름의 데이터 슬롯을 가져오는 경우 첫 번째 애플리케이션 도메인의 데이터는 두 번째 애플리케이션 도메인의 데이터와 독립적으로 유지됩니다.  
  
## <a name="thread-relative-static-fields"></a>스레드 관련 정적 필드  
 데이터 조각이 항상 스레드 및 애플리케이션 도메인 조합에 고유하다는 것을 알고 있다면 <xref:System.ThreadStaticAttribute> 특성을 정적 필드에 적용하세요. 다른 정적 필드를 사용하는 것처럼 필드를 사용하세요. 필드의 데이터는 이를 사용하는 각 스레드에 고유합니다.  
  
 스레드 관련 정적 필드는 데이터 슬롯보다 향상된 성능을 제공하며 컴파일 시간 형식 검사의 이점을 제공합니다.  
  
 모든 클래스 생성자 코드는 필드에 액세스하는 첫 번째 컨텍스트의 첫 번째 스레드에서 실행됩니다. 동일한 애플리케이션 도메인의 다른 모든 스레드 또는 컨텍스트에서 필드는 참조 형식인 경우 `null`(Visual Basic의 `Nothing`)로 초기화되고 값 형식인 경우 해당 기본값으로 초기화됩니다. 따라서 스레드 관련 정적 필드를 초기화할 때 클래스 생성자를 사용하면 안 됩니다. 대신 스레드 관련 정적 필드를 초기화하지 않고 해당 필드가 `null`(`Nothing`) 또는 기본값으로 초기화된다고 가정합니다.  
  
## <a name="data-slots"></a>데이터 슬롯  
 .NET Framework는 스레드 및 애플리케이션 도메인의 조합에 고유한 동적 데이터 슬롯을 제공합니다. 두 가지 형식의 데이터 슬롯인 명명된 슬롯 및 명명되지 않은 슬롯이 있습니다. 둘 다 <xref:System.LocalDataStoreSlot> 구조체를 사용하여 구현됩니다.  
  
- 명명된 데이터 슬롯을 만들려면 <xref:System.Threading.Thread.AllocateNamedDataSlot%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType> 메서드를 사용합니다. 기존 명명된 슬롯에 대한 참조를 가져오려면 해당 이름을 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 메서드에 전달합니다.  
  
- 명명되지 않은 데이터 슬롯을 만들려면 <xref:System.Threading.Thread.AllocateDataSlot%2A?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 명명된 슬롯과 명명되지 않은 슬롯 모두에 대해 <xref:System.Threading.Thread.SetData%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.GetData%2A?displayProperty=nameWithType> 메서드를 사용하여 슬롯에서 정보를 설정하고 검색합니다. 이러한 정적 메서드는 현재 메서드를 실행 중인 스레드에 대한 데이터에서 항상 작동합니다.  
  
 명명된 슬롯은 명명되지 않은 슬롯에 대한 참조를 유지하는 대신 <xref:System.Threading.Thread.GetNamedDataSlot%2A> 메서드에 이름을 전달하여 필요한 경우 슬롯을 검색할 수 있기 때문에 편리합니다. 그러나 또 다른 구성 요소가 스레드 관련 스토리지에 동일한 이름을 사용하고 스레드가 해당 구성 요소와 다른 구성 요소의 코드를 둘 다 실행하는 경우 두 구성 요소가 서로의 데이터를 손상시킬 수 있습니다. (이 시나리오는 두 구성 요소가 모두 동일한 애플리케이션 도메인에서 실행되고 있고 동일한 데이터를 공유하도록 설계되지 않았다고 가정합니다.)  
  
## <a name="see-also"></a>참고 항목

- <xref:System.ContextStaticAttribute>
- <xref:System.Threading.Thread.GetNamedDataSlot%2A?displayProperty=nameWithType>
- <xref:System.ThreadStaticAttribute>
- <xref:System.Runtime.Remoting.Messaging.CallContext>
- [스레딩](../../../docs/standard/threading/index.md)
