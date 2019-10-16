---
title: '방법: BetweenShowDelay 속성 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- ToolTip control [WPF], BetweenShowDelay time property
- BetweenShowDelay time property [WPF]
ms.assetid: 984ea76d-f2a2-4326-a02e-f97ec3d036d6
ms.openlocfilehash: 9b63675ec21294496117860aa5b58af132c4284a
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614523"
---
# <a name="how-to-use-the-betweenshowdelay-property"></a>방법: BetweenShowDelay 속성 사용
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 도구 설명 신속 하 게 표시 되도록 속성을 시간-지연 시간을 거의 또는 전혀-사용자 이동 하면 포인터가 하나의 도구 설명에서 간 직접.  
  
## <a name="example"></a>예제  
 다음 예에서 <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> 속성을 1 초 (1000 밀리초)로 설정 하며 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 모두의 도구 설명에 2 초 (2000 밀리초)로 설정 되어 <xref:System.Windows.Shapes.Ellipse> 컨트롤입니다. 타원 중 하나에 대 한 도구 설명을 표시 하 고 다음 마우스 포인터를 이동 다른 타원 일시 중지 하 고 2 초 내에 두 번째 타원의 도구 설명 바로 표시 합니다.  
  
 다음 시나리오 중 하나에 <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> 적용, 1 초 표시 되기 전에 두 번째 타원에 대 한 도구 설명 하면:  
  
- 두 번째 단추를 이동 하는 데 걸리는 시간 이면 2 초 이상.  
  
- 도구 설명은 첫 번째 타원은 시간 간격의 시작 부분에 표시 되지 않습니다.  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
[!code-xaml[ToolTipService#NoToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#notooltip)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipService>
- [방법 항목](tooltip-how-to-topics.md)
- [도구 설명 개요](tooltip-overview.md)
