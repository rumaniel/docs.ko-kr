---
title: 약한 참조
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- weak references, short
- weak references, using
- weak references, long
- garbage collection, weak references
ms.assetid: 6a600fe5-3af3-4c64-82da-10a0a8e2d79b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 65492beb888da1986f456d3fd000fc02f340f3c4
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121105"
---
# <a name="weak-references"></a>약한 참조
응용 프로그램의 코드가 해당 개체에 연결될 수 있는 반면 가비지 수집기는 응용 프로그램에서 사용 중인 개체를 수집할 수 없습니다. 응용 프로그램은 개체에 대한 강력한 참조를 가진다고 합니다.  
  
 Weak references는 응용 프로그램에서 개체에 계속 액세스할 수 있는 동안 가비지 수집기에서 해당 개체를 수집할 수 있도록 합니다. 강한 참조가 없을 경우 Weak references는 개체가 수집되기 전까지 임의의 시간 동안에만 유효합니다. Weak references를 사용하면 응용 프로그램은 여전히 개체에 대한 강한 참조를 유지할 수 있으며 이로 인해 개체가 수집되지 않도록 방지합니다. 그러나 강력한 참조를 다시 설정하기 전에 가비지 수집기가 먼저 개체에 연결될 위험이 항상 존재합니다.  
  
 Weak references는 많은 메모리를 사용하는 개체에 유용하지만 가비지 수집에서 회수될 경우 쉽게 다시 만들 수 있습니다.  
  
 Windows Forms 응용 프로그램의 트리 뷰에서는 사용자에게 복잡한 계층적 선택 옵션을 표시한다고 가정합니다. 기본 데이터가 크다면 사용자가 응용 프로그램에서 다른 작업을 수행하는 경우 트리를 메모리에 유지하는 것은 비효율적입니다.  
  
 사용자가 응용 프로그램의 다른 부분으로 전환할 때 <xref:System.WeakReference> 클래스를 사용하여 트리에 대한 약한 참조를 만들고 모든 강력한 참조를 삭제할 수 있습니다. 사용자가 트리로 다시 전환할 때 응용 프로그램은 트리에 대한 강한 참조를 가지려고 하며 이 시도가 성공할 경우 트리를 다시 생성하지 않도록 방지합니다.  
  
 개체를 사용하여 약한 참조를 설정하려면 추적할 개체의 인스턴스를 사용하여 <xref:System.WeakReference>를 만듭니다. 그런 다음 <xref:System.WeakReference.Target%2A> 속성을 해당 개체로 설정하고 해당 개체에 대한 원래 참조를 `null`로 설정합니다. 코드 예제는 클래스 라이브러리의 <xref:System.WeakReference>를 참조하세요.  
  
## <a name="short-and-long-weak-references"></a>Short 및 Long Weak References  
 Short Weak Reference 또는 Long Weak References를 만들 수 있습니다.  
  
-   Short  
  
     가비지 수집에서 개체를 회수하는 경우 Short Weak Reference의 대상은 `null`이 됩니다. Weak Reference는 자체 관리되는 개체이며 다른 관리되는 개체와 마찬가지로 가비지 수집의 대상입니다.  짧은 약한 참조는 <xref:System.WeakReference>의 기본 생성자입니다.  
  
-   Long  
  
     개체의 <xref:System.Object.Finalize%2A> 메서드가 호출된 후에 긴 약한 참조는 유지됩니다. 이렇게 하면 개체를 다시 만들 수 있지만 개체의 상태는 예측할 수 없게 됩니다. 긴 참조를 사용하려면 <xref:System.WeakReference> 생성자에서 `true`를 지정합니다.  
  
     개체의 형식에 <xref:System.Object.Finalize%2A> 메서드가 없는 경우 짧은 약한 참조 기능이 적용되며 약한 참조는 대상이 수집될 때까지만 유효합니다. 이는 종료자가 실행된 후에 언제든지 발생할 수 있습니다.  
  
 강한 참조를 설정하고 개체를 다시 사용하려면 <xref:System.WeakReference>의 <xref:System.WeakReference.Target%2A> 속성을 개체의 형식에 캐스트합니다. <xref:System.WeakReference.Target%2A> 속성이 `null`을 반환하는 경우 개체가 수집되었습니다. 그러지 않으면, 응용 프로그램이 해당 개체에 대한 강한 참조를 회복하기 때문에 개체를 계속 사용할 수 있습니다.  
  
## <a name="guidelines-for-using-weak-references"></a>Weak References를 사용하기 위한 지침  
 종료된 후에 개체의 상태를 예측할 수 없기 때문에 필요한 경우에만 Long Weak Referencs를 사용합니다.  
  
 포인터 자체는 이상일 수 있기 때문에 작은 개체에 Weak Referencs를 사용하지 않습니다.  
  
 메모리 관리 문제에 대한 자동 솔루션으로 Weak Referencs를 사용하지 않습니다. 대신, 응용 프로그램의 개체를 처리하기 위한 효과적인 캐싱 정책을 개발합니다.  
  
## <a name="see-also"></a>참고 항목

- [가비지 수집](../../../docs/standard/garbage-collection/index.md)
