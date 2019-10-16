---
title: '방법: Panel의 OnRender 메서드 재정의'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- overriding OnRender method
- Panel control, overriding OnRender method
- OnRender method
- controls, Panel, overriding OnRender method
helpviewer_keywords:
- overriding OnRender method of Panel control [WPF]
- OnRender method [WPF], overriding
- Panel control [WPF], overriding OnRender method
ms.assetid: 57397834-a085-4e36-90ab-416fad98f341
ms.openlocfilehash: 23c3353e130585ed83726816a467ca73f6aa9152
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666710"
---
# <a name="how-to-override-the-panel-onrender-method"></a>방법: Panel의 OnRender 메서드 재정의
이 예제에서는 레이아웃 요소에 사용자 <xref:System.Windows.Controls.Panel.OnRender%2A> 지정 그래픽 <xref:System.Windows.Controls.Panel> 효과를 추가 하기 위해의 메서드를 재정의 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 렌더링 된 <xref:System.Windows.Controls.Panel.OnRender%2A> 패널 요소에 그래픽 효과를 추가 하려면 메서드를 사용 합니다. 예를 들어이 메서드를 사용 하 여 사용자 지정 테두리나 배경 효과를 추가할 수 있습니다. <xref:System.Windows.Media.DrawingContext> 개체는 도형, 텍스트, 이미지 또는 비디오를 그리기 위한 메서드를 제공 하는 인수로 전달 됩니다. 따라서이 메서드는 panel 개체의 사용자 지정에 유용 합니다.  
  
 [!code-csharp[LightWeightCustomPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LightWeightCustomPanel/CSharp/OffsetPanel.cs#1)]
 [!code-vb[LightWeightCustomPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/LightWeightCustomPanel/visualbasic/offsetpanel.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Panel>
- [패널 개요](panels-overview.md)
- [방법 항목](panel-how-to-topics.md)
