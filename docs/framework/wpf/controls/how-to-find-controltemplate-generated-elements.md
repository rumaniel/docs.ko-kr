---
title: '방법: ControlTemplate에서 생성된 요소 찾기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ControlTemplates [WPF], finding elements
- finding ControlTemplate elements [WPF]
ms.assetid: d7b25447-ceff-4bb4-9be5-fd7c40ef00af
ms.openlocfilehash: 426f6c93433711ac72fe67eff2ee3006aa4d9166
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62037144"
---
# <a name="how-to-find-controltemplate-generated-elements"></a>방법: ControlTemplate에서 생성된 요소 찾기
이 예제에 의해 생성 된 요소를 찾는 방법을 보여 줍니다는 <xref:System.Windows.Controls.ControlTemplate>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 간단한 만드는 스타일을 보여 줍니다 <xref:System.Windows.Controls.ControlTemplate> 에 대 한는 <xref:System.Windows.Controls.Button> 클래스:  
  
 [!code-xaml[FindGeneratedItems#CT](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#ct)]  
  
 템플릿 내에서 요소를 찾으려면 템플릿을 적용 된 후 호출할 수 있습니다 합니다 <xref:System.Windows.FrameworkTemplate.FindName%2A> 메서드는 <xref:System.Windows.Controls.Control.Template%2A>합니다. 다음 예제에서는 실제 너비 값을 표시 하는 메시지 상자는 <xref:System.Windows.Controls.Grid> 컨트롤 템플릿에서:  
  
 [!code-csharp[FindGeneratedItems#CTFindElement](~/samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#ctfindelement)]
 [!code-vb[FindGeneratedItems#CTFindElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#ctfindelement)]  
  
## <a name="see-also"></a>참고자료

- [DataTemplate에서 생성된 요소 찾기](../data/how-to-find-datatemplate-generated-elements.md)
- [스타일 지정 및 템플릿](styling-and-templating.md)
- [WPF XAML 이름 범위](../advanced/wpf-xaml-namescopes.md)
- [WPF의 트리](../advanced/trees-in-wpf.md)
