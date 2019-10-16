---
title: '연습: ElementHost 컨트롤을 사용하여 속성 매핑'
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- mapping properties [WPF]
- ElementHost control [WPF], mapping properties
ms.assetid: bccd6e0d-2272-4924-9107-ff8ed58b88aa
ms.openlocfilehash: 3c74878a91f89e14837b42a45a35ab35bcd5cf68
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64650822"
---
# <a name="walkthrough-mapping-properties-using-the-elementhost-control"></a>연습: ElementHost 컨트롤을 사용하여 속성 매핑

이 연습에서는 사용 하는 방법을 보여 줍니다.는 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A> 매핑할 속성을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 속성을 해당 속성에 호스트 된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소입니다.

이 연습에서 설명하는 작업은 다음과 같습니다.

- 프로젝트 만들기.

- 새 속성 매핑 정의.

- 기본 속성 매핑 제거.

- 기본 속성 매핑 확장.

이 연습에 설명 된 작업의 전체 코드 목록은 참조 하세요 [ElementHost 컨트롤 샘플을 사용 하 여 속성 매핑](https://go.microsoft.com/fwlink/?LinkID=160018)합니다.

에 매핑할 수 있게 됩니다 완료 했으면 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 속성을 해당 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 호스팅된 요소 속성입니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- Visual Studio 2017

## <a name="creating-the-project"></a>프로젝트 만들기

### <a name="to-create-the-project"></a>프로젝트를 만들려면

1. 만들기는 **Windows Forms 앱** 라는 프로젝트 `PropertyMappingWithElementHost`합니다.

2. **솔루션 탐색기**, 다음에 대 한 참조를 추가 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 어셈블리입니다.

    - PresentationCore

    - PresentationFramework

    - WindowsBase

    - WindowsFormsIntegration

3. 맨 위에 다음 코드를 복사 합니다 `Form1` 코드 파일.

     [!code-csharp[PropertyMappingWithElementHost#10](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#10)]
     [!code-vb[PropertyMappingWithElementHost#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#10)]

4. Windows Forms 디자이너에서 `Form1`을 엽니다. 에 대 한 이벤트 처리기를 추가 하려면 폼을 두 번 클릭 합니다 <xref:System.Windows.Forms.Form.Load> 이벤트입니다.

5. Windows Forms 디자이너로 돌아가서 폼에 대 한 이벤트 처리기를 추가 <xref:System.Windows.Forms.Control.Resize> 이벤트입니다. 자세한 내용은 [방법: 디자이너를 사용 하 여 이벤트 처리기를 만들](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))합니다.

6. 선언를 <xref:System.Windows.Forms.Integration.ElementHost> 필드에 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#16](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#16)]
     [!code-vb[PropertyMappingWithElementHost#16](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#16)]

## <a name="defining-new-property-mappings"></a>새 속성 매핑 정의

<xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 몇 가지 기본 속성 매핑의 제공 합니다. 호출 하 여 새 속성 매핑을 추가 합니다 <xref:System.Windows.Forms.Integration.PropertyMap.Add%2A> 메서드를 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤의 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A>합니다.

### <a name="to-define-new-property-mappings"></a>새 속성 매핑을 정의 하려면

1. 다음 코드에 대 한 정의를 복사 합니다 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#12](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#12)]
     [!code-vb[PropertyMappingWithElementHost#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#12)]

     합니다 `AddMarginMapping` 에 대 한 새 매핑을 추가 하는 메서드는 <xref:System.Windows.Forms.Control.Margin%2A> 속성입니다.

     `OnMarginChange` 메서드 변환 하는 <xref:System.Windows.Forms.Control.Margin%2A> 속성을 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.FrameworkElement.Margin%2A> 속성.

2. 다음 코드에 대 한 정의를 복사 합니다 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#14](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#14)]
     [!code-vb[PropertyMappingWithElementHost#14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#14)]

     합니다 `AddRegionMapping` 에 대 한 새 매핑을 추가 하는 메서드는 <xref:System.Windows.Forms.Control.Region%2A> 속성입니다.

     `OnRegionChange` 메서드 변환 하는 <xref:System.Windows.Forms.Control.Region%2A> 속성을 합니다 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.UIElement.Clip%2A> 속성.

     합니다 `Form1_Resize` 양식의 처리 <xref:System.Windows.Forms.Control.Resize> 이벤트 호스 티 드 요소에 맞게 클리핑 영역의 크기입니다.

## <a name="removing-a-default-property-mapping"></a>기본 속성 매핑 제거

호출 하 여 기본 속성 매핑을 제거 합니다 <xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A> 메서드를 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤의 <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A>합니다.

### <a name="to-remove-a-default-property-mapping"></a>기본 속성 매핑을 제거하려면

- 다음 코드에 대 한 정의를 복사 합니다 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#13](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#13)]
     [!code-vb[PropertyMappingWithElementHost#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#13)]

     합니다 `RemoveCursorMapping` 에 대 한 기본 매핑을 삭제 하는 메서드를 <xref:System.Windows.Forms.Control.Cursor%2A> 속성입니다.

## <a name="extending-a-default-property-mapping"></a>기본 속성 매핑 확장

기본 속성 매핑을 사용하고 고유 매핑으로 확장할 수도 있습니다.

### <a name="to-extend-a-default-property-mapping"></a>기본 속성 매핑을 확장하려면

- 다음 코드에 대 한 정의를 복사 합니다 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#15](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#15)]
     [!code-vb[PropertyMappingWithElementHost#15](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#15)]

     합니다 `ExtendBackColorMapping` 메서드를 기존 사용자 지정 속성 변환기를 추가 <xref:System.Windows.Forms.Control.BackColor%2A> 속성 매핑.

     합니다 `OnBackColorChange` 메서드를 호스팅된 컨트롤의 이미지를 할당 <xref:System.Windows.Controls.Control.Background%2A> 속성입니다. `OnBackColorChange` 기본 속성 매핑을 적용 된 후 호출 됩니다.

## <a name="initialize-your-property-mappings"></a>속성 매핑을 초기화합니다

1. 다음 코드에 대 한 정의를 복사 합니다 `Form1` 클래스입니다.

     [!code-csharp[PropertyMappingWithElementHost#11](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithElementHost/CSharp/PropertyMappingWithElementHost/Form1.cs#11)]
     [!code-vb[PropertyMappingWithElementHost#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithElementHost/VisualBasic/PropertyMappingWithElementHost/Form1.vb#11)]

     `Form1_Load` 메서드 핸들을 <xref:System.Windows.Forms.Form.Load> 이벤트 하 고 다음과 같은 초기화를 수행 합니다.

    - 만듭니다는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> 요소입니다.

    - 연습에서 이전에 정의한 메서드를 호출하여 속성 매핑을 설정합니다.

    - 매핑된 속성에 초기 값을 할당합니다.

2. F5 키를 눌러 애플리케이션을 빌드하고 실행합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Windows Forms 및 WPF 속성 매핑](windows-forms-and-wpf-property-mapping.md)
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
- [연습: Windows Forms에서 WPF 복합 컨트롤 호스팅](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)