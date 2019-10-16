---
title: '성능 최적화: 응용 프로그램 리소스'
ms.date: 03/30/2017
helpviewer_keywords:
- application resources [WPF], performance
- resources [WPF], performance
- static resources [WPF]
- sharing resources [WPF]
- brushes [WPF], performance
- sharing brushes without copying [WPF]
ms.assetid: 62b88488-c08e-4804-b7de-a1c34fbe929c
ms.openlocfilehash: 759d02afe1934d2ace4ed226d5d911db2d676d98
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005046"
---
# <a name="optimizing-performance-application-resources"></a>성능 최적화: 응용 프로그램 리소스
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]을 사용 하면 유사한 형식의 요소에서 일관 된 모양과 동작을 지원할 수 있도록 응용 프로그램 리소스를 공유할 수 있습니다. 이 항목에서는 응용 프로그램의 성능을 향상 시키는 데 도움이 되는이 영역에 대 한 몇 가지 권장 사항을 제공 합니다.  
  
 리소스에 대한 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조하세요.  
  
## <a name="sharing-resources"></a>리소스 공유  
 응용 프로그램에서 사용자 지정 컨트롤을 사용 하 고 <xref:System.Windows.ResourceDictionary> (또는 XAML 리소스 노드)에서 리소스를 정의 하는 경우 <xref:System.Windows.Application> 또는 <xref:System.Windows.Window> 개체 수준에서 리소스를 정의 하거나 사용자 지정 컨트롤에 대 한 기본 테마에서 정의 하는 것이 좋습니다. 사용자 지정 컨트롤의 <xref:System.Windows.ResourceDictionary>에서 리소스를 정의 하면 해당 컨트롤의 모든 인스턴스에 대 한 성능에 영향을 줍니다. 예를 들어, 사용자 지정 컨트롤의 리소스 정의와 사용자 지정 컨트롤의 여러 인스턴스에 대 한 리소스 정의의 일부로 정의 된 성능 집약적인 브러시 작업을 사용 하는 경우 응용 프로그램의 작업 집합이 현저 하 게 증가 합니다.  
  
 이 점을 설명 하려면 다음 사항을 고려 하세요. @No__t-0을 사용 하 여 카드 게임을 개발 하는 경우를 가정해 보겠습니다. 대부분의 카드 게임의 경우 52 다른 얼굴의 52 카드가 필요 합니다. 카드 사용자 지정 컨트롤을 구현 하 고 카드 사용자 지정 컨트롤의 리소스에서 52 브러시 (카드 얼굴을 나타냄)를 정의 합니다. 주 응용 프로그램에서 처음에이 카드 사용자 지정 컨트롤의 52 인스턴스를 만듭니다. 카드 사용자 지정 컨트롤의 각 인스턴스는 <xref:System.Windows.Media.Brush> 개체의 52 인스턴스를 생성 하 여 응용 프로그램에 총 52 * 52 <xref:System.Windows.Media.Brush> 개체를 제공 합니다. 카드 사용자 지정 컨트롤 리소스에서 브러시를 <xref:System.Windows.Application> 또는 <xref:System.Windows.Window> 개체 수준으로 이동 하거나 사용자 지정 컨트롤에 대 한 기본 테마에 정의 하 여 이제 52에서 52 브러시를 공유 하므로 응용 프로그램의 작업 집합을 줄일 수 있습니다. card 컨트롤의 인스턴스입니다.  
  
## <a name="sharing-a-brush-without-copying"></a>복사 하지 않고 브러시 공유  
 동일한 <xref:System.Windows.Media.Brush> 개체를 사용 하는 요소가 여러 개 있는 경우 브러시를 리소스로 정의 하 고 XAML에서 브러시 인라인을 정의 하는 대신이를 참조 합니다. 이 메서드는 하나의 인스턴스를 만들고 다시 사용 하는 반면, XAML에서 인라인으로 인라인을 정의 하면 각 요소에 대 한 새 인스턴스가 생성 됩니다.  
  
 다음 태그 샘플은이 점을 보여 줍니다.  
  
 [!code-xaml[Performance#PerformanceSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/BrushResource.xaml#performancesnippet7)]  
  
## <a name="use-static-resources-when-possible"></a>가능 하면 정적 리소스 사용  
 정적 리소스는 이미 정의 된 리소스에 대 한 참조를 조회 하 여 모든 XAML 속성 특성에 대 한 값을 제공 합니다. 해당 리소스에 대 한 조회 동작은 컴파일 시간 조회와 유사 합니다.  
  
 반면에 동적 리소스는 초기 컴파일 중에 임시 식을 만들며 요청 된 리소스 값이 실제로 개체를 생성 하는 데 필요할 때까지 리소스 조회를 지연 합니다. 해당 리소스에 대 한 조회 동작은 런타임 조회와 비슷하며 성능에 영향을 줍니다. 필요한 경우에만 동적 리소스를 사용 하 여 응용 프로그램에서 가능 하면 항상 정적 리소스를 사용 합니다.  
  
 다음 태그 예제에서는 두 가지 유형의 리소스를 사용 하는 방법을 보여 줍니다.  
  
 [!code-xaml[Performance#PerformanceSnippet8](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/DynamicResource.xaml#performancesnippet8)]  
  
## <a name="see-also"></a>참조

- [WPF 애플리케이션 성능 최적화](optimizing-wpf-application-performance.md)
- [애플리케이션 성능 계획](planning-for-application-performance.md)
- [하드웨어 이용](optimizing-performance-taking-advantage-of-hardware.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [개체 동작](optimizing-performance-object-behavior.md)
- [텍스트 모드](optimizing-performance-text.md)
- [데이터 바인딩](optimizing-performance-data-binding.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
