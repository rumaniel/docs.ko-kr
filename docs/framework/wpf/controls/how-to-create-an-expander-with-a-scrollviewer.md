---
title: '방법: ScrollViewer를 사용하여 Expander 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Expander
- ScrollViewer control [WPF], with Expander control
- Expander control [WPF], creating
- controls [WPF], ScrollViewer
ms.assetid: 2ad124d2-2406-4157-aaf2-64e067298f01
ms.openlocfilehash: ef0bc5d344f7d465de9209708430d3e61d40d4f7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910795"
---
# <a name="how-to-create-an-expander-with-a-scrollviewer"></a>방법: ScrollViewer를 사용하여 Expander 만들기
만드는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Expander> 이미지 및 텍스트와 같은 복잡 한 콘텐츠를 포함 하는 컨트롤입니다. 예제의 콘텐츠도 포함 합니다 <xref:System.Windows.Controls.Expander> 에 <xref:System.Windows.Controls.ScrollViewer> 제어 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 만드는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Expander>합니다. 이 예제에서는 사용을 <xref:System.Windows.Controls.Primitives.BulletDecorator> 정의 하기 위해 이미지 및 텍스트를 포함 하는 컨트롤은 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A>합니다. <xref:System.Windows.Controls.ScrollViewer> 컨트롤은 확장 된 콘텐츠를 스크롤 하는 방법을 제공 합니다.  
  
 설정 하는 예제는 합니다 <xref:System.Windows.FrameworkElement.Height%2A> 속성에는 <xref:System.Windows.Controls.ScrollViewer> 대신 콘텐츠. 경우는 <xref:System.Windows.FrameworkElement.Height%2A> 콘텐츠를 설정 합니다 <xref:System.Windows.Controls.ScrollViewer> 내용을 스크롤 하는 사용자를 허용 하지 않습니다. <xref:System.Windows.FrameworkElement.Width%2A> 속성이 설정 되어 합니다 <xref:System.Windows.Controls.Expander> 컨트롤과이 설정을 적용할를 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 및 확장 된 콘텐츠입니다.  
  
 [!code-xaml[ExpanderRichContent#CreateExpander](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml#createexpander)]  
  
 [!code-csharp[ExpanderRichContent#CreateExpanderCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ExpanderRichContent/CSharp/Window1.xaml.cs#createexpandercode)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Expander>
- [Expander 개요](expander-overview.md)
- [방법 항목](expander-how-to-topics.md)
