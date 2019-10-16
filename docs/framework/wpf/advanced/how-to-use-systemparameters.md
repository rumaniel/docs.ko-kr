---
title: '방법: SystemParameters 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- classes [WPF], SystemParameters
ms.assetid: 02e7a5de-94eb-4953-b91c-52e6c872ad5b
ms.openlocfilehash: 344fb54b48bcbf188b36a29d8205c21deff713c4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001457"
---
# <a name="how-to-use-systemparameters"></a>방법: SystemParameters 사용
액세스 속성을 사용 하는 방법을 보여주는이 예제 <xref:System.Windows.SystemParameters> 스타일을 지정 하거나 단추를 사용자 지정 합니다.  
  
## <a name="example"></a>예제  
 시스템 리소스는 시스템 설정과 일관된 시각적 효과를 만들 수 있도록 몇 가지 시스템 기반 설정을 리소스로 노출합니다. <xref:System.Windows.SystemParameters> 시스템 매개 변수 값 속성 및 값에 바인딩되는 리소스 키를 모두 포함 하는 클래스입니다. 예를 들어 <xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> 되는 <xref:System.Windows.SystemParameters> 속성 값 및 <xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> 해당 리소스 키입니다.  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에서의 멤버를 사용할 수 있습니다 <xref:System.Windows.SystemParameters> 는 정적 속성 사용 또는 동적 리소스 참조 (정적 속성 값을 키로). 애플리케이션이 실행되는 동안 시스템 기반 값을 자동으로 업데이트하려면 동적 리소스 참조를 사용하고 자동으로 업데이트하지 않으려면 정적 참조를 사용합니다. 리소스 키 접미사가 `Key` 속성 이름에 추가 합니다.  
  
 다음 예제에서는 액세스 하 고 정적 값을 사용 하는 방법을 보여 줍니다 <xref:System.Windows.SystemParameters> 스타일을 지정 하거나 단추를 사용자 지정 합니다. 이 태그 예제에서는 단추의 크기를 조정 적용 하 여 <xref:System.Windows.SystemParameters> 단추에는 값입니다.  
  
 [!code-xaml[SystemRes_snip#ParameterStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#parameterstaticresources)]  
  
 값을 사용 하도록 <xref:System.Windows.SystemParameters> 코드에서 필요가 없습니다 정적 참조 또는 동적 리소스 참조를 사용 합니다. 대신 값을 사용 합니다 <xref:System.Windows.SystemParameters> 클래스입니다. 키가 아닌 속성이 정적 속성의 런타임 동작으로 정의 된 것 이지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시스템에서 호스트 속성에서 실시간으로 다시 계산 하 고 적절 하 게 시스템 값을 사용자가 수행한 변경 작업에 대 한 고려 됩니다. 다음 예제를 사용 하 여 단추의 높이 너비를 설정 하는 방법을 보여 줍니다 <xref:System.Windows.SystemParameters> 값입니다.  
  
 [!code-csharp[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#parameterresourcescode)]
 [!code-vb[SystemRes_snip#ParameterResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#parameterresourcescode)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.SystemParameters>
- [시스템 브러시로 영역 그리기](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemFonts 사용](how-to-use-systemfonts.md)
- [시스템 매개 변수 키 사용](how-to-use-system-parameters-keys.md)
- [방법 항목](resources-how-to-topics.md)
