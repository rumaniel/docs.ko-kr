---
title: '방법: 자동 레이아웃을 사용하여 단추 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- Button controls [WPF], creating with automatic layout
- automatic layout [WPF], creating buttons
ms.assetid: 96c206d0-9e77-4784-9d2d-5045aed2021c
ms.openlocfilehash: 8eb1e93dd87c210812c9b7758c744a616ef2d862
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62052393"
---
# <a name="how-to-use-automatic-layout-to-create-a-button"></a>방법: 자동 레이아웃을 사용하여 단추 만들기
이 예제는 자동 레이아웃 방식을 사용하여 지역화 가능한 애플리케이션에 단추를 만드는 방법을 설명합니다.  
  
 지역화는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 시간이 소요 될 수 있습니다. 종종 지역화 담당자는 텍스트 번역 외에도 요소 크기를 조정하고 위치를 재조정해야 합니다. 과거에 각 언어는는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 된 조정 작업이 필요 합니다. 기능을 사용 하 여 이제 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 조정의 필요성이 감소 하는 요소를 디자인할 수 있습니다. 보다 쉽게 크기 및 위치가 변경 될 수 있는 응용 프로그램을 작성 하는 방법을 라고 `automatic layout`합니다.  
  
## <a name="example"></a>예제  

다음 두 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제에서는 단추; 하나는 영어 텍스트를 스페인어 텍스트를 사용 하 여 하나를 인스턴스화하는 응용 프로그램을 만듭니다. 코드는 텍스트를 제외하고 동일합니다. 단추는 텍스트에 맞게 조정됩니다.

[!code-xaml[LocalizationBtn_snip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]  
  
[!code-xaml[LocalizationBtn#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]  
  
 다음 그림에서는 자동 크기 조정이 불가능 단추를 사용 하 여 코드 샘플의 출력을 보여 줍니다.
  
 ![텍스트가 여러 언어로 표시되는 동일한 단추](./media/use-automatic-layout-overview/auto-resizable-button.png)  
  
## <a name="see-also"></a>참고자료

- [자동 레이아웃 사용 개요](use-automatic-layout-overview.md)
- [자동 레이아웃에 그리드 사용](how-to-use-a-grid-for-automatic-layout.md)
