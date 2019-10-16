---
title: '방법: 자동 레이아웃에 눈금 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- grids [WPF], automatic layout
- automatic layout [WPF], grid use
ms.assetid: ab9de407-e0c1-4047-bdf0-24951bf73879
ms.openlocfilehash: 590ad7292fea572b20ccaa09ce2886724e004a6a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052406"
---
# <a name="how-to-use-a-grid-for-automatic-layout"></a>방법: 자동 레이아웃에 눈금 사용
이 예제에서는 지역화할 수 있는 애플리케이션을 만드는 자동 레이아웃 방법에서 그리드를 사용하는 방법을 설명합니다.  
  
 지역화는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 시간이 소요 될 수 있습니다. 지역화 담당자는 텍스트를 번역하는 작업 외에도 요소의 크기를 조정하고 위치를 변경해야 하는 경우가 많습니다. 과거에 각 언어는는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 된 조정 작업이 필요 합니다. 기능을 사용 하 여 이제 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 조정의 필요성이 감소 하는 요소를 디자인할 수 있습니다. 응용 프로그램을 보다 쉽게 크기 조정 및 위치를 작성 하는 방법을 라고 `auto layout`합니다.  
  
 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제에서는 그리드를 사용 하 여 일부 단추 및 텍스트 위치를 보여 줍니다. 셀의 너비와 높이가 설정 된 알림 `Auto`; 있으므로 이미지가 있는 단추가 포함 된 셀을 이미지에 맞게 조정 합니다. 때문에 <xref:System.Windows.Controls.Grid> 요소 지역화할 수 있는 응용 프로그램을 디자인 하는 자동 레이아웃 방법을 사용할 경우에 유용할 수 있습니다 콘텐츠에 맞게 조정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 그리드를 사용하는 방법을 보여 줍니다.  
  
 [!code-xaml[LocalizationGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]  
  
 다음 그래픽에서는 코드 샘플의 출력을 보여 줍니다.  
  
 ![그리드 예제](./media/glob-grid.png "glob_grid")  
표  
  
## <a name="see-also"></a>참고자료

- [자동 레이아웃 사용 개요](use-automatic-layout-overview.md)
- [자동 레이아웃을 사용하여 단추 만들기](how-to-use-automatic-layout-to-create-a-button.md)
