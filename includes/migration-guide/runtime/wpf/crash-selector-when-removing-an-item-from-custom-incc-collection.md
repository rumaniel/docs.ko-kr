---
ms.openlocfilehash: 8f4ee44e8432bae3537c6f064f564b9f044a7c33
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802534"
---
### <a name="crash-in-selector-when-removing-an-item-from-a-custom-incc-collection"></a>사용자 지정 INCC 컬렉션에서 항목을 제거할 때 선택기에서 크래시가 발생합니다.

|   |   |
|---|---|
|세부 정보|<code>T:System.InvalidOperationException</code>는 다음과 같은 시나리오에서 발생할 수 있습니다.<ul><li><code>T:System.Windows.Controls.Primitives.Selector</code>의 ItemsSource는 <code>T:System.Collections.Specialized.INotifyCollectionChanged</code>의 사용자 지정 구현이 있는 컬렉션입니다.</li><li>선택한 항목이 컬렉션에서 제거됩니다.</li><li><code>T:System.Collections.Specialized.NotifyCollectionChangedEventArgs</code>에는 <code>P:System.Collections.Specialized.NotifyCollectionChangedEventArgs.OldStartingIndex</code> = -1(알 수 없는 위치를 나타냄)이 있습니다.</li></ul>예외의 호출 스택은 System.Windows.Threading.Dispatcher.VerifyAccess() System.Windows.DependencyObject.GetValue(DependencyProperty dp) System.Windows.Controls.Primitives.Selector.GetIsSelected(DependencyObject 요소)에서 시작합니다. 애플리케이션에 1 초과 디스패처 스레드가 있는 경우 이 예외는 .NET Framework 4.5에서 발생할 수 있습니다. .NET Framework 4.7의 경우 단일 디스패처 스레드가 있는 애플리케이션에서도 예외가 발생할 수 있습니다. 이 문제는 .NET Framework 4.7.1에서 해결됩니다.|
|제안|.NET Framework 4.7.1로 업그레이드합니다.|
|범위|부|
|버전|4.7|
|Type|런타임|

