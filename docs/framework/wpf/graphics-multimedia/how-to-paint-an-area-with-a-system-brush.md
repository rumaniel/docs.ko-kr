---
title: '방법: 시스템 브러시로 영역 칠하기'
ms.date: 03/30/2017
helpviewer_keywords:
- system brushes [WPF], painting with
- painting [WPF], with system brushes
- brushes [WPF], painting with system brushes [WPF]
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
ms.openlocfilehash: 26511c577bf06b016dfc69cedc7fce2bafb35f32
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645372"
---
# <a name="how-to-paint-an-area-with-a-system-brush"></a>방법: 시스템 브러시로 영역 칠하기
합니다 <xref:System.Windows.SystemColors> 클래스와 같은 시스템 브러시 및 색에 대 한 액세스를 제공 합니다 <xref:System.Windows.SystemColors.ControlBrush%2A>를 <xref:System.Windows.SystemColors.ControlBrushKey%2A>, 및 <xref:System.Windows.SystemColors.DesktopBrush%2A>합니다. 시스템 브러시는는 <xref:System.Windows.Media.SolidColorBrush> 개체는 지정된 된 시스템 색으로 영역을 그립니다. 시스템 브러시는 항상 단색을 생성하므로 그라데이션을 만드는 데는 사용할 수 없습니다.  
  
 시스템 브러시는 정적 또는 동적 리소스로 사용할 수 있습니다. 사용자 애플리케이션이 실행될 때 사용자가 시스템 브러시를 변경하는 경우 브러시가 자동으로 업데이트되게 하려면 동적 리소스를 사용하고, 그렇지 않으면 정적 리소스를 사용합니다. SystemColors 클래스는 엄격한 명명 규칙을 따르는 다양한 정적 속성을 포함합니다.  
  
- *\<SystemColor>* Brush  
  
     정적 참조를 가져옵니다는 <xref:System.Windows.Media.SolidColorBrush> 지정된 된 시스템 색입니다.  
  
- *\<SystemColor>* BrushKey  
  
     동적 참조를 가져옵니다는 <xref:System.Windows.Media.SolidColorBrush> 지정된 된 시스템 색입니다.  
  
- *\<SystemColor>* Color  
  
     정적 참조를 가져옵니다는 <xref:System.Windows.Media.Color> 지정된 된 시스템 색의 구조입니다.  
  
- *\<SystemColor>* ColorKey  
  
     동적 참조를 가져옵니다는 <xref:System.Windows.Media.Color> 지정된 된 시스템 색의 구조입니다.  
  
 시스템 색은을 <xref:System.Windows.Media.Color> 브러시를 구성 하는 데 사용할 수 있는 구조입니다. 예를 들어, 설정 하 여 시스템 색을 사용 하는 그라데이션을 만들 수 있습니다 합니다 <xref:System.Windows.Media.GradientStop.Color%2A> 의 속성을 <xref:System.Windows.Media.LinearGradientBrush> 시스템 색을 사용 하 여 개체의 그라데이션 중지점입니다. 예를 들어 참조 [그라데이션에 시스템 색을 사용 하 여](how-to-use-system-colors-in-a-gradient.md)입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 동적 시스템 브러시 참조를 사용하여 단추의 배경색을 설정합니다.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 다음 예제에서는 정적 시스템 브러시 참조를 사용하여 단추의 배경색을 설정합니다.  
  
 [!code-xaml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 그라데이션에 시스템 색을 사용 하는 방법을 보여 주는 예제를 보려면 [그라데이션에 시스템 색 사용](how-to-use-system-colors-in-a-gradient.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [그라데이션에 시스템 색 사용](how-to-use-system-colors-in-a-gradient.md)
- [단색 및 그라데이션을 사용한 그리기 개요](painting-with-solid-colors-and-gradients-overview.md)
