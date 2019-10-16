---
title: 이벤트 기반 비동기 패턴(EAP)
ms.date: 07/23/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- asynchronous calls
- asynchronous programming, design patterns
- asynchronous programming
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 052773c615bcc4ddb5b735ae8164d44ed70bd935
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54513492"
---
# <a name="event-based-asynchronous-pattern-eap"></a>이벤트 기반 비동기 패턴(EAP)

비동기 기능을 클라이언트 코드에 노출하는 방법은 여러 가지가 있습니다. 이벤트 기반 비동기 패턴은 클래스에 비동기 동작을 표시하는 한 가지 방법을 규정합니다.  
  
> [!NOTE]
> .NET Framework 4부터는 작업 병렬 라이브러리에서 비동기 및 병렬 프로그래밍을 위한 새로운 모델을 제공합니다. 자세한 내용은 [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md) 및 [TAP(작업 기반 비동기 패턴)](task-based-asynchronous-pattern-tap.md)을 참조하세요.
  
## <a name="in-this-section"></a>섹션 내용

 [이벤트 기반 비동기 패턴 개요](event-based-asynchronous-pattern-overview.md)  
 이벤트 기반 비동기 패턴이 다중 스레드 디자인에 본질적으로 존재하는 복잡한 여러 가지 문제를 숨기면서 다중 스레드 애플리케이션의 장점을 이용할 수 있게 해주는 방법을 설명합니다.  
  
 [이벤트 기반 비동기 패턴 구현](implementing-the-event-based-asynchronous-pattern.md)  
 비동기 기능을 포함하는 클래스를 패키징하는 표준화된 방법을 설명합니다.  
  
 [최선의 이벤트 기반 비동기 패턴 구현 방법](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 이벤트 기반 비동기 패턴에 따라 비동기 기능을 노출하기 위한 요구 사항을 설명합니다.  
  
 [이벤트 기반 비동기 패턴 구현 시기 결정](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 [APM(비동기 프로그래밍 모델)](asynchronous-programming-model-apm.md)에서 나타내는 <xref:System.IAsyncResult> 패턴 대신 이벤트 기반 비동기 패턴을 구현하도록 선택해야 하는 경우를 결정하는 방법을 설명합니다.
  
 [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 구현](component-that-supports-the-event-based-asynchronous-pattern.md)  
 이벤트 기반 비동기 패턴을 구현하는 구성 요소를 만드는 방법을 설명합니다. 구성 요소가 모든 애플리케이션 모델에서 올바르게 작동하도록 하는 <xref:System.ComponentModel?displayProperty=nameWithType> 네임스페이스의 도우미 클래스를 사용하는 것이 좋습니다.  

 [방법: 이벤트 기반 비동기 패턴의 클라이언트 구현](how-to-implement-a-client-of-the-event-based-asynchronous-pattern.md)  
 이벤트 기반 비동기 패턴을 구현하는 구성 요소를 사용하는 클라이언트를 만드는 방법을 설명합니다.
  
 [방법: 이벤트 기반 비동기 패턴을 지원하는 구성 요소 사용](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 이벤트 기반 비동기 패턴을 지원하는 구성 요소를 사용하는 방법을 설명합니다.  
  
## <a name="reference"></a>참조

 <xref:System.ComponentModel.AsyncOperation>  
 <xref:System.ComponentModel.AsyncOperation> 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 <xref:System.ComponentModel.AsyncOperationManager> 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 <xref:System.ComponentModel.BackgroundWorker> 구성 요소를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
## <a name="related-sections"></a>관련 단원

 [TPL(작업 병렬 라이브러리)](../parallel-programming/task-parallel-library-tpl.md)  
 비동기 및 병렬 작업용 프로그래밍 모델에 대해 설명합니다.  
  
 [스레딩](../../../docs/standard/threading/index.md)  
 .NET의 다중 스레딩 기능에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목

- [관리되는 스레딩을 구현하는 최선의 방법](../threading/managed-threading-best-practices.md)
- [이벤트](../events/index.md)
- [비동기 프로그래밍 패턴](index.md)
