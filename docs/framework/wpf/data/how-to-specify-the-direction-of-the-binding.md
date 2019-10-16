---
title: '방법: 바인딩 방향 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- direction of binding [WPF]
- binding direction [WPF]
- data binding [WPF], direction of binding
ms.assetid: 37334478-028b-4514-86c9-1420709f4818
ms.openlocfilehash: 023cd42ad5fb321e7ffa65f08673cb4145f49af4
ms.sourcegitcommit: 10736f243dd2296212e677e207102c463e5f143e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817914"
---
# <a name="how-to-specify-the-direction-of-the-binding"></a>방법: 바인딩 방향 지정

이 예제에서는 바인딩으로 바인딩 대상(대상) 속성만 업데이트되는지, 바인딩 소스(소스) 속성만 업데이트되는지 아니면 대상 속성과 소스 속성이 모두 업데이트되는지 여부를 지정하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Data.Binding.Mode%2A?displayProperty=nameWithType> 속성을 사용 하 여 바인딩의 방향을 지정 합니다. 바인딩 업데이트에 사용할 수 있는 옵션은 다음과 같습니다.  
  
- <xref:System.Windows.Data.BindingMode.TwoWay?displayProperty=nameWithType>대상 속성이 나 원본 속성이 변경 될 때마다 대상 속성 또는 속성을 업데이트 합니다.  
  
- <xref:System.Windows.Data.BindingMode.OneWay?displayProperty=nameWithType>원본 속성이 변경 될 때만 대상 속성을 업데이트 합니다.  
  
- <xref:System.Windows.Data.BindingMode.OneTime?displayProperty=nameWithType>응용 프로그램이 시작 되거나가 변경 되는 경우에 <xref:System.Windows.FrameworkElement.DataContext%2A> 만 대상 속성을 업데이트 합니다.  
  
- <xref:System.Windows.Data.BindingMode.OneWayToSource?displayProperty=nameWithType>대상 속성이 변경 될 때 소스 속성을 업데이트 합니다.  
  
- <xref:System.Windows.Data.BindingMode.Default?displayProperty=nameWithType>target 속성의 <xref:System.Windows.Data.Binding.Mode%2A> 기본값을 사용 합니다.  
  
 자세한 내용은 <xref:System.Windows.Data.BindingMode> 열거형을 참조하세요.  
  
 다음 예제에서는 <xref:System.Windows.Data.Binding.Mode%2A> 속성을 설정하는 방법을 보여 줍니다.  
  
 [!code-xaml[DirectionalBinding#4](~/samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#4)]  
  
 원본 변경 내용 ( <xref:System.Windows.Data.BindingMode.OneWay> 및 <xref:System.Windows.Data.BindingMode.TwoWay> 바인딩에 적용 됨)을 검색 하려면 소스가와 <xref:System.ComponentModel.INotifyPropertyChanged>같은 적절 한 속성 변경 알림 메커니즘을 구현 해야 합니다. <xref:System.ComponentModel.INotifyPropertyChanged> 구현에 대 한 예제는 [속성 변경 알림 구현](how-to-implement-property-change-notification.md) 을 참조 하세요.  
  
 또는 바인딩의 경우 속성을 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 설정 하 여 원본 업데이트의 타이밍을 제어할 수 있습니다. <xref:System.Windows.Data.BindingMode.OneWayToSource> <xref:System.Windows.Data.BindingMode.TwoWay> 자세한 내용은 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Data.Binding>
- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
