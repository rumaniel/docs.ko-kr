---
title: '방법: 패널의 자식 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], binding to children of Panels
- Panel control [WPF], binding adorners to children
ms.assetid: 4cc9b972-b472-4e5c-bdf3-3702d7fbb1f5
ms.openlocfilehash: 739ccaa0273e66c4650c35217a1156d64336dbbb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923522"
---
# <a name="how-to-adorn-the-children-of-a-panel"></a>방법: 패널의 자식 표시
이 예제에서는 지정 <xref:System.Windows.Controls.Panel>된의 자식에 표시기를 프로그래밍 방식으로 바인딩하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 표시기를의 <xref:System.Windows.Controls.Panel>자식에 바인딩하려면 다음 단계를 수행 합니다.  
  
1. 새 <xref:System.Windows.Documents.AdornerLayer> 개체를 선언 하 고 메서드 `static` 를 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 호출 하 여 자식을 표시할 요소의 표시기 계층을 찾습니다.  
  
2. 부모 요소의 자식을 열거 하 고 메서드를 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 호출 하 여 각 자식 요소에 표시기를 바인딩합니다.  
  
 다음 예제에서는 SimpleCircleAdorner (위에 표시 됨)를 <xref:System.Windows.Controls.StackPanel> *mystackpanel*이라는의 자식에 바인딩합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 사용하여 표시기를 다른 요소에 바인딩하는 것은 현재 지원되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [표시기 개요](adorners-overview.md)
