---
title: '방법: 슬라이더의 틱 사용자 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- TickBar [WPF]
- Slider control [WPF], creating with TickBar
ms.assetid: 4fa694f2-a620-4b15-be78-5f4286f89361
ms.openlocfilehash: 3b32bbedb5f654ce75e90a827eb0c4dba1d4d345
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910691"
---
# <a name="how-to-customize-the-ticks-on-a-slider"></a>방법: 슬라이더의 틱 사용자 지정
만드는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Slider> 눈금이 있는 컨트롤입니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Controls.Primitives.TickBar> 설정 하는 경우 표시는 <xref:System.Windows.Controls.Slider.TickPlacement%2A> 이외의 값으로 속성을 <xref:System.Windows.Controls.Primitives.TickPlacement.None>, 기본 값입니다.  
  
 다음 예제에서는 만드는 방법을 보여 줍니다.는 <xref:System.Windows.Controls.Slider> 사용 하 여는 <xref:System.Windows.Controls.Primitives.TickBar> 는 눈금을 표시 합니다. 합니다 <xref:System.Windows.Controls.Slider.TickPlacement%2A> 고 <xref:System.Windows.Controls.Slider.TickFrequency%2A> 속성 눈금 표시 및 간격의 위치를 정의 합니다. 이동 하는 경우는 <xref:System.Windows.Controls.Primitives.Thumb>, 도구 설명의 값을 표시 합니다 <xref:System.Windows.Controls.Slider>합니다. <xref:System.Windows.Controls.Slider.AutoToolTipPlacement%2A> 속성은 도구 설명이 발생할 위치를 정의 합니다. 합니다 <xref:System.Windows.Controls.Primitives.Thumb> 있기 때문에 눈금의 위치로 이동 일치 <xref:System.Windows.Controls.Slider.IsSnapToTickEnabled%2A> 로 설정 된 `true`합니다.  
  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다 <xref:System.Windows.Controls.Slider.Ticks%2A> 속성을 따라 눈금을 만드는 <xref:System.Windows.Controls.Slider> 불규칙 한 간격입니다.  
  
 [!code-xaml[Slider#4](~/samples/snippets/xaml/VS_Snippets_Wpf/Slider/xaml/window1.xaml#4)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Slider>
- <xref:System.Windows.Controls.Primitives.TickBar>
- <xref:System.Windows.Controls.Slider.TickPlacement%2A>
- [방법: 속성 값을 슬라이더 바인딩합니다](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms788716(v=vs.90))
