---
title: '방법: 요소 변환'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], translations
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
ms.openlocfilehash: 04e1e8288bcccc4a310f05abff01fbdf160cdb11
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43505910"
---
# <a name="how-to-translate-an-element"></a>방법: 요소 변환
이 예제에서는 변환 (이동) 요소를 사용 하 여를 <xref:System.Windows.Media.TranslateTransform>입니다.  
  
 <xref:System.Windows.Media.TranslateTransform> 클래스는 절대 위치 지정을 지원 하지 않는 패널 내에서 요소를 이동 하는 데 특히 유용 합니다. 적용 하 여 예를 들어를 <xref:System.Windows.Media.TranslateTransform> 에 <xref:System.Windows.UIElement.RenderTransform%2A> 요소의 속성 내의 요소를 이동할 수 있습니다는 <xref:System.Windows.Controls.StackPanel> 또는 <xref:System.Windows.Controls.DockPanel>합니다.  
  
 사용 하 여는 <xref:System.Windows.Media.TranslateTransform.X%2A> 의 속성을 <xref:System.Windows.Media.TranslateTransform> 픽셀 x 축 따라 요소를 이동할 크기를 지정 하 합니다. 사용 된 <xref:System.Windows.Media.TranslateTransform.Y%2A> 픽셀은 y 축 따라 요소를 이동할 크기를 지정 하는 속성입니다. 마지막으로 적용 합니다 <xref:System.Windows.Media.TranslateTransform> 에 <xref:System.Windows.UIElement.RenderTransform%2A> 요소의 속성입니다.  
  
 다음 예제에서는 <xref:System.Windows.Media.TranslateTransform> 는 요소 50 픽셀을 오른쪽에서 50 픽셀을 아래로 이동 하려면.  
  
## <a name="example"></a>예제  
 [!code-xaml[transformsSample#53](../../../../samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 전체 샘플을 보려면 [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transform 개요](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)
