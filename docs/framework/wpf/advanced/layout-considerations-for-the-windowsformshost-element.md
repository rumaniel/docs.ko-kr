---
title: WindowsFormsHost 요소에 대한 레이아웃 고려 사항
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- WindowsFormsHost element layout considerations [WPF]
- dynamic layout [WPF interoperability]
- device-independent pixels
ms.assetid: 3c574597-bbde-440f-95cc-01371f1a5d9d
ms.openlocfilehash: 67698a0a45bdf84d36603cd1309a8dd5bce2f895
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64598840"
---
# <a name="layout-considerations-for-the-windowsformshost-element"></a>WindowsFormsHost 요소에 대한 레이아웃 고려 사항
이 항목에 설명 하는 방법을 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소와 상호 작용 하는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 시스템입니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 폼 또는 페이지에 요소 배치 및 크기 조정에 대 한 다르지만, 비슷한 논리를 지원 합니다. 하이브리드 사용자 인터페이스 (UI)를 만들 때 해당 호스트 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 두 레이아웃 스키마를 통합 하는 요소입니다.  
  
## <a name="differences-in-layout-between-wpf-and-windows-forms"></a>WPF 및 Windows Forms 간의 레이아웃 차이점  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 해상도 레이아웃이 사용 됩니다. 모든 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 크기를 사용 하 여 지정 된 *장치 독립적 픽셀*합니다. 장치 독립적 픽셀 1/96 인치 크기 및 해상도 독립적인 이므로 72 dpi 모니터 또는 19200 dpi 프린터를 렌더링 하는 여부에 관계 없이 비슷한 결과 표시 합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기준으로 *동적 레이아웃*합니다. 이 UI 요소를 폼 이나 내용을, 해당 부모 레이아웃 컨테이너 및 사용 가능한 화면 크기에 따라 페이지에서 자체 정렬를 의미 합니다. 동적 레이아웃 자동으로 포함 된 문자열 길이 변경 하는 경우 UI 요소의 위치와 크기를 조정 하 여 지역화를 용이해 집니다.  
  
 레이아웃에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 이며 장치 종속적 정적일 가능성이 있습니다. 일반적으로 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 하드웨어 픽셀 단위로 지정 된 차원을 사용 하 여 폼에 컨트롤 절대적으로 배치 됩니다. 그러나 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 다음 표에 요약 된 것 처럼 일부 동적 레이아웃 기능을 지 원하는지 않습니다.  
  
|레이아웃 기능|설명|  
|--------------------|-----------------|  
|자동 크기 조정|일부 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤의 콘텐츠를 올바르게 표시 하는 자체 크기를 조정 합니다. 자세한 내용은 [AutoSize 속성 개요](../../winforms/controls/autosize-property-overview.md)합니다.|  
|고정 및 도킹|[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 위치 및 크기 조정 기준으로 부모 컨테이너를 지원 합니다. 자세한 내용은 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=nameWithType>를 참조하세요.|  
|자동 크기 조정|컨테이너 컨트롤의 자체 및 출력 장치 또는 기본 컨테이너 글꼴의 픽셀에서 크기, 해상도에 따라 해당 자식 항목 크기를 조정 합니다. 자세한 내용은 [Windows Forms의 자동 크기 조정을](../../winforms/automatic-scaling-in-windows-forms.md)합니다.|  
|레이아웃 컨테이너|합니다 <xref:System.Windows.Forms.FlowLayoutPanel> 고 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤 해당 자식 컨트롤을 정렬 하 고 해당 내용에 따라 자체 크기입니다.|  
  
## <a name="layout-limitations"></a>레이아웃 제한 사항  
 일반적으로 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 없으며 확장에서 가능한 범위까지 변환 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다. 다음과 같은 알려진된 제한 사항을 설명 할 때 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 호스 티 드 통합 하려고 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 시스템.  
  
- 경우에 따라 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 크기를 조정할 수 없거나 특정 차원으로만 크기를 조정할 수 있습니다. 예를 들어, 한 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.ComboBox> 컨트롤은 컨트롤의 글꼴 크기에 의해 정의 된 단일 높이 지원 합니다. 에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 여기서 요소가 세로로 확장 될 수, 호스트 된 동적 레이아웃 <xref:System.Windows.Forms.ComboBox> 예상 대로 컨트롤이 늘어나지 것입니다.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤을 회전하거나 기울일 수 없습니다. 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소를 발생 시킵니다는 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> 기울이기, 회전 변환을 적용 하는 경우에 이벤트입니다. 처리 하지 않는 경우는 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> 이벤트는 <xref:System.InvalidOperationException> 발생 합니다.  
  
- 대부분의 경우 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 서는 비례하여 크기 조정을 지원하지 않습니다. 컨트롤의 전체 크기는 조정할 수 있지만, 컨트롤의 구성 요소와 자식 컨트롤의 크기가 예상대로 조정되지 않을 수 있습니다. 이 제한 사항은 각 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에서 얼마나 효과적으로 크기 조정을 지원하는지에 따라 달라집니다. 또한 확장할 수 없으며 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 0 픽셀의 크기로 컨트롤입니다.  
  
- [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 나타나는 양식을 자동으로 조정할지 자체 및 해당 컨트롤의 글꼴 크기에 따라 자동 크기 조정을 지원 합니다. 개별 요소의 크기는 동적으로 조정할 수 있지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자 인터페이스에서 글꼴 크기를 변경해도 전체 레이아웃의 크기는 조정되지 않습니다.  
  
### <a name="z-order"></a>Z 순서  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 사용자 인터페이스에서 겹치는 동작을 제어하기 위해 요소의 z 순서를 변경할 수 있습니다. 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤은 개별 HWND에서 그려지므로 항상 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소 위에 그려집니다.  
  
 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 하나를 기반으로 컨트롤을 그리면도 <xref:System.Windows.Documents.Adorner> 요소입니다.  
  
## <a name="layout-behavior"></a>레이아웃 동작  
 다음 섹션을 호스팅할 때 레이아웃 동작의 특정 측면을 설명 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]합니다.  
  
### <a name="scaling-unit-conversion-and-device-independence"></a>크기 조정, 단위 변환 및 장치 독립성  
 때마다를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 관련 된 작업을 수행 하는 요소 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 차원 좌표 두 개가 포함 된:에 대 한 장치 독립적 픽셀 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에 대 한 하드웨어 픽셀 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]합니다. 따라서 일관 된 레이아웃을 달성 하기 위해 적절 한 단위 및 배율 변환을 적용 해야 합니다.  
  
 현재 장치 해상도 및 모든 레이아웃에 따라 좌표 시스템 간의 변환 또는 적용할 렌더링 변환은 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 해당 상위 항목입니다.  
  
 출력 장치는 96dpi 및에 없는 확장을 적용 하는 경우는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 하드웨어 픽 요소를 하나의 장치 독립적 픽셀은입니다.  
  
 다른 모든 경우 좌표 시스템 크기 조정이 필요 합니다. 호스팅된 컨트롤 조정 되지 않습니다. 대신는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소에서 호스트 된 컨트롤 및 모든 자식 컨트롤의 크기를 조정 하려고 합니다. 때문에 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 크기 조정, 완벽 하 게 지원 하지 않습니다는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 특정 컨트롤에서 지원 되는 정도를 확장 합니다.  
  
 재정의 <xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A> 호스팅된 Windows Forms 컨트롤에 대 한 사용자 지정 크기 조정 동작을 제공 하는 방법입니다.  
  
 크기 조정 하는 것 외에도 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 다음 표에 설명 된 대로 반올림 하 고 오버플로 경우를 처리 합니다.  
  
|변환 문제|설명|  
|----------------------|-----------------|  
|반올림|[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 장치 독립적 픽셀 크기와 지정 된 `double`, 및 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 으로 지정 된 하드웨어 픽셀 크기 `int`합니다. 경우에서 여기서 `double`-기반된 크기로 변환할 `int`-차원 기반는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 표준 반올림 되므로 0.5 보다 작은 소수 값 0으로 반올림 됩니다.|  
|오버플로|경우는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소에서 변환 `double` 값을 `int` 값 오버플로가 발생 가능성이 있습니다. 합니다. 보다 큰 값은 <xref:System.Int32.MaxValue> 로 설정 되어 <xref:System.Int32.MaxValue>입니다.|  
  
### <a name="layout-related-properties"></a>레이아웃 관련 속성  
 레이아웃 동작을 제어 하는 속성 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤 및 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소에서 적절 하 게 매핑되는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소입니다. 자세한 내용은 [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)을 참조하세요.  
  
### <a name="layout-changes-in-the-hosted-control"></a>호스팅된 컨트롤에서 레이아웃 변경  
 레이아웃 변경에서 호스팅된 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤에 전파 됩니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 업데이트를 트리거합니다. <xref:System.Windows.UIElement.InvalidateMeasure%2A> 메서드를 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 호스팅된 컨트롤에서 레이아웃 변경으로 인해 하면는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 엔진이 실행 되도록 합니다.  
  
### <a name="continuously-sized-windows-forms-controls"></a>지속적으로 Windows Forms 컨트롤 크기 조정  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 연속 확장을 완전히 지 원하는 컨트롤 상호 작용을 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 시스템입니다. <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소를 사용 합니다 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 및 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 일반적으로 정렬 하 고 크기 호스팅된 메서드 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 컨트롤.  
  
### <a name="sizing-algorithm"></a>크기 조정 알고리즘  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소 다음 절차를 사용 하 여 호스트 된 컨트롤의 크기:  
  
1. 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소를 재정의 합니다 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 및 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 메서드.  
  
2. 호스팅된 컨트롤의 크기를 결정 하는 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 호스팅된 컨트롤의 메서드를 호출 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 제약 조건이 있는 메서드에 전달할 제약 조건에서 변환의 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> 메서드.  
  
3. <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 메서드는 지정 된 크기 제약 조건에 호스트 된 컨트롤을 설정 하려고 시도 합니다.  
  
4. 경우 호스팅된 컨트롤의 <xref:System.Windows.Forms.Control.Size%2A> 속성에 지정 된 제약 조건과 일치, 제약 조건에 호스트 된 컨트롤 크기가 조정 됩니다.  
  
 경우는 <xref:System.Windows.Forms.Control.Size%2A> 속성이 지정된 된 제약 일치 하지 않습니다, 호스트 된 컨트롤에 연속 크기 조정을 지원 하지 않습니다. 예를 들어를 <xref:System.Windows.Forms.MonthCalendar> 컨트롤 불연속 크기만 허용 합니다. 이 컨트롤에 대 한 허용 되는 크기 높이 너비에 대 한 정수 (개월 수를 나타냄)으로 구성 됩니다. 이 같은 경우에는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 다음과 같이 동작 합니다.  
  
- 경우는 <xref:System.Windows.Forms.Control.Size%2A> 속성에 지정한 제약 조건이 보다 더 큰 크기를 반환 합니다.는 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 요소는 호스트 된 컨트롤을 자릅니다. 호스팅된 컨트롤 어느 방향으로든에서 잘릴 수도 있습니다 있도록 높이 너비를 별도로 처리 됩니다.  
  
- 경우는 <xref:System.Windows.Forms.Control.Size%2A> 속성에 지정된 된 제약 보다 작은 크기를 반환 합니다 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 크기 값이 허용 하 고 값을 반환 합니다는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 레이아웃 시스템입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [연습: WPF에서 정렬 Windows Forms 컨트롤](walkthrough-arranging-windows-forms-controls-in-wpf.md)
- [WPF 샘플에서 정렬 Windows Forms 컨트롤](https://go.microsoft.com/fwlink/?LinkID=159971)
- [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)
- [마이그레이션 및 상호 운용성](migration-and-interoperability.md)
