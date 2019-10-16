---
title: '방법: PriorityBinding 구현'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], PriorityBinding class
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
ms.openlocfilehash: 4be1ce434eb1e169e8a19b56c92ca1efb48773d2
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169080"
---
# <a name="how-to-implement-prioritybinding"></a>방법: PriorityBinding 구현
<xref:System.Windows.Data.PriorityBinding>의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 경우 바인딩 목록을 지정 합니다. 바인딩 목록은 우선 순위가 가장 높은 우선 순위로 정렬 됩니다. 우선 순위가 가장 높은 바인딩이 처리 될 때 값을 성공적으로 반환 하는 경우 목록에서 다른 바인딩을 처리할 필요가 없습니다. 우선 순위가 가장 높은 바인딩이 계산 되는 데 시간이 오래 걸릴 수 있습니다. 값을 반환 하는 다음으로 높은 우선 순위는 더 높은 우선 순위의 바인딩이 성공적으로 값을 반환할 때까지 사용 됩니다.  
  
## <a name="example"></a>예제  
 `FastDP`가 작동 <xref:System.Windows.Data.PriorityBinding> `SlowerDP` `SlowestDP`하는 방법을 시연 하기 위해, 및의 세 가지 속성을 사용 하 여 개체를만들었습니다.`AsyncDataSource`  
  
 의 `FastDP` get 접근자는 `_fastDP` 데이터 멤버의 값을 반환 합니다.  
  
 의 `SlowerDP` get 접근자는 `_slowerDP` 데이터 멤버의 값을 반환 하기 전에 3 초간 대기 합니다.  
  
 의 `SlowestDP` get 접근자는 `_slowestDP` 데이터 멤버의 값을 반환 하기 전에 5 초 동안 대기 합니다.  
  
> [!NOTE]
> 이 예제는 데모용으로만 제공됩니다. .NET 지침은 필드 집합 보다 느린 크기의 속성을 정의 하는 것에 대해 권장 됩니다. 자세한 내용은 [속성 및 메서드 중에서 선택](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229054(v=vs.100))을 참조 하세요.  
  
 [!code-csharp[PriorityBinding#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 속성 <xref:System.Windows.Controls.TextBlock.Text%2A> 은 다음을 사용 하 `AsyncDS` 여 <xref:System.Windows.Data.PriorityBinding>위의에 바인딩합니다.  
  
 [!code-xaml[PriorityBinding#2](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 바인딩 엔진은 <xref:System.Windows.Data.Binding> 개체를 처리할 때 `SlowestDP` 속성에 바인딩된 첫 번째 <xref:System.Windows.Data.Binding>로 시작 합니다. 이 <xref:System.Windows.Data.Binding> 를 처리 하면 5 초 동안 절전 모드로 전환 되므로 값을 반환 하지 않으므로 다음 <xref:System.Windows.Data.Binding> 요소가 처리 됩니다. 다음 <xref:System.Windows.Data.Binding> 은 3 초 동안 중지 되기 때문에 성공적으로 값을 반환 하지 않습니다. 그러면 바인딩 엔진이 <xref:System.Windows.Data.Binding> `FastDP` 속성에 바인딩된 다음 요소로 이동 합니다. 그러면 <xref:System.Windows.Data.Binding> "Fast value" 값이 반환 됩니다. 이제 <xref:System.Windows.Controls.TextBlock> 에 "Fast value" 값이 표시 됩니다.  
  
 3 초가 경과 하면 속성은 `SlowerDP` "느린 값" 값을 반환 합니다. 그런 <xref:System.Windows.Controls.TextBlock> 다음에 "느린 값" 값을 표시 합니다.  
  
 5 초가 경과 하면 속성은 `SlowestDP` "가장 느린 값" 값을 반환 합니다. 이 바인딩은 먼저 나열 되기 때문에 가장 높은 우선 순위를 갖습니다. 이제 <xref:System.Windows.Controls.TextBlock> 에 "가장 느린 값" 값이 표시 됩니다.  
  
 바인딩에서 <xref:System.Windows.Data.PriorityBinding> 성공한 반환 값으로 간주 되는 항목에 대 한 자세한 내용은를 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=nameWithType>
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
