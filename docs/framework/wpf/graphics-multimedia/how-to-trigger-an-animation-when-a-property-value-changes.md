---
title: '방법: 속성 값 변경 시 애니메이션 트리거'
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], starting when property values change
- triggering animation [WPF]
- Storyboards [WPF], starting when property values change
ms.assetid: 12399c21-0300-4f4f-9e3a-d92d9907e5f5
ms.openlocfilehash: 7e3eecedf7d464eeb8e4f60f2f05fa06d2e23e09
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61769306"
---
# <a name="how-to-trigger-an-animation-when-a-property-value-changes"></a>방법: 속성 값 변경 시 애니메이션 트리거
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Trigger> 시작 하는 <xref:System.Windows.Media.Animation.Storyboard> 속성 값을 변경 하는 경우. 사용할 수는 <xref:System.Windows.Trigger> 내부를 <xref:System.Windows.Style>, <xref:System.Windows.Controls.ControlTemplate>, 또는 <xref:System.Windows.DataTemplate>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Trigger> 애니메이션 효과를 주는 합니다 <xref:System.Windows.UIElement.Opacity%2A> 의 <xref:System.Windows.Controls.Button> 때 해당 <xref:System.Windows.UIElement.IsMouseOver%2A> 속성이 됩니다 `true`.  
  
 [!code-xaml[AnimatePropertyStoryboards#PropertyTriggerExample](~/samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/PropertyTriggerExample.xaml#propertytriggerexample)]  
  
 속성에 의해 적용 된 애니메이션 <xref:System.Windows.Trigger> 개체 보다 더 복잡 한 방식으로 동작 <xref:System.Windows.EventTrigger> 애니메이션이 나 애니메이션 사용을 시작 <xref:System.Windows.Media.Animation.Storyboard> 메서드.  이러한 "전달" 애니메이션을 사용 하 여 다른 정의한 <xref:System.Windows.Trigger> 개체를 사용 하 여 하지만 구성 <xref:System.Windows.EventTrigger> 및 메서드 트리거 애니메이션 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Trigger>
- [속성 애니메이션 기술 개요](property-animation-techniques-overview.md)
- [Storyboard 개요](storyboards-overview.md)
