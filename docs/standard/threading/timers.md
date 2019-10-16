---
title: 타이머
description: 다중 스레드 환경에서 사용할 .NET 타이머에 대해 알아봅니다.
ms.date: 07/03/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [.NET Framework], timers
- timers, about timers
ms.assetid: 7091500d-be18-499b-a942-95366ce185e5
author: pkulikov
ms.author: ronpet
ms.openlocfilehash: 644ccf5951e9d2556fc697d2fd763f026fd0ebdb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54617228"
---
# <a name="timers"></a>타이머

.NET은 다중 스레드 환경에서 사용할 다음 두 개의 타이머를 제공합니다.

- <xref:System.Threading.Timer?displayProperty=nameWithType> - <xref:System.Threading.ThreadPool> 스레드에서 단일 콜백 메서드를 정기적으로 실행합니다.
- <xref:System.Timers.Timer?displayProperty=nameWithType> - 기본적으로 <xref:System.Threading.ThreadPool> 스레드에서 이벤트를 정기적으로 발생시킵니다.

> [!NOTE]
> 일부 .NET 구현에는 다음과 같은 추가 타이머가 포함될 수 있습니다.
>
> - <xref:System.Windows.Forms.Timer?displayProperty=nameWithType>: 이벤트를 정기적으로 발생시키는 Windows Forms 구성 요소입니다. 이 구성 요소에는 사용자 인터페이스가 없으며, 단일 스레드 환경에서 사용하도록 설계되었습니다.  
> - <xref:System.Web.UI.Timer?displayProperty=nameWithType>: 비동기 또는 동기 웹 페이지 포스트백을 정기적으로 수행하는 ASP.NET 구성 요소입니다.
> - <xref:System.Windows.Threading.DispatcherTimer?displayProperty=nameWithType>: 지정된 시간 간격 및 지정된 우선 순위로 처리되는 <xref:System.Windows.Threading.Dispatcher> 큐에 통합된 타이머입니다.

## <a name="the-systemthreadingtimer-class"></a>System.Threading.Timer 클래스

<xref:System.Threading.Timer?displayProperty=nameWithType> 클래스를 사용하면 대리자를 지정된 시간 간격으로 계속 호출할 수 있습니다. 또한 이 클래스를 사용하여 지정된 시간 간격으로 대리자에 대한 단일 호출을 예약할 수 있습니다. 대리자는 <xref:System.Threading.ThreadPool> 스레드에서 실행됩니다.

<xref:System.Threading.Timer?displayProperty=nameWithType> 개체를 만들 때 콜백 메서드를 정의하는 <xref:System.Threading.TimerCallback> 대리자, 콜백에 전달되는 선택적 상태 개체, 콜백의 첫 번째 호출까지 지연되는 시간 및 콜백 호출 간의 시간 간격을 지정합니다. 보류 중인 타이머를 취소하려면 <xref:System.Threading.Timer.Dispose%2A?displayProperty=nameWithType> 메서드를 호출합니다.

다음 예제에서는 제공된 대리자를 1초(1,000밀리초) 후에 처음 호출한 다음, 2초마다 호출하는 타이머를 만듭니다. 이 예제의 상태 개체는 대리자를 호출한 횟수를 계산하는 데 사용됩니다. 대리자가 10회 이상 호출되면 타이머가 중지됩니다.

[!code-cpp[System.Threading.Timer#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.Timer/CPP/source2.cpp#2)]
[!code-csharp[System.Threading.Timer#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.Timer/CS/source2.cs#2)]
[!code-vb[System.Threading.Timer#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.Timer/VB/source2.vb#2)]

자세한 내용과 예제를 보려면 <xref:System.Threading.Timer?displayProperty=nameWithType>을 참조하세요.

## <a name="the-systemtimerstimer-class"></a>System.Timers.Timer 클래스

다중 스레드 환경에서 사용할 수 있는 또 다른 타이머는 <xref:System.Timers.Timer?displayProperty=nameWithType>이며, 기본적으로 <xref:System.Threading.ThreadPool> 스레드에서 이벤트를 발생시킵니다.

<xref:System.Timers.Timer?displayProperty=nameWithType> 개체를 만들 때 <xref:System.Timers.Timer.Elapsed> 이벤트가 발생되는 시간 간격을 지정할 수 있습니다. <xref:System.Timers.Timer.Enabled%2A> 속성을 사용하여 타이머에서 <xref:System.Timers.Timer.Elapsed> 이벤트가 발생되어야 하는지 여부를 나타냅니다. 지정된 간격이 지난 후에 <xref:System.Timers.Timer.Elapsed> 이벤트가 한 번만 발생해야 하는 경우 <xref:System.Timers.Timer.AutoReset%2A>을 `false`로 설정합니다. <xref:System.Timers.Timer.AutoReset%2A> 속성의 기본값은 `true`이며, 이는 즉 <xref:System.Timers.Timer.Elapsed> 이벤트가 <xref:System.Timers.Timer.Interval%2A> 속성에 정의된 간격으로 정기적으로 발생하는 것을 의미합니다.

자세한 내용과 예제를 보려면 <xref:System.Timers.Timer?displayProperty=nameWithType>을 참조하세요.
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Timer?displayProperty=nameWithType>
- <xref:System.Timers.Timer?displayProperty=nameWithType>
- [스레딩 개체 및 기능](threading-objects-and-features.md)
