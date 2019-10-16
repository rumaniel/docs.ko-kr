---
title: Windows Forms DataGridView 컨트롤에서 데이터 형식 지정
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], formatting data
- data [Windows Forms], formatting in grids
- data grids [Windows Forms], formatting data
ms.assetid: 07bf558d-3748-42ba-8ba0-37fdef924081
ms.openlocfilehash: 5966f16238999655d6072c1127e5bf16aefde5e4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969182"
---
# <a name="data-formatting-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤에서 데이터 형식 지정
컨트롤 <xref:System.Windows.Forms.DataGridView> 은 셀 값과 부모 열에 표시 되는 데이터 형식 간에 자동 변환을 제공 합니다. 텍스트 상자 열 (예: 날짜, 시간, 숫자 및 열거형 값의 문자열 표현을 표시 하 고 사용자가 입력 한 문자열 값을 데이터 저장소에 필요한 형식으로 변환)  
  
## <a name="formatting-with-the-datagridviewcellstyle-class"></a>DataGridViewCellStyle 클래스를 사용 하 여 서식 지정  
 컨트롤 <xref:System.Windows.Forms.DataGridView> 은 클래스를 <xref:System.Windows.Forms.DataGridViewCellStyle> 통해 셀 값의 기본 데이터 서식을 제공 합니다. <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 속성을 사용 하 여 형식 [지정](../../../standard/base-types/formatting-types.md)형식에 설명 된 형식 지정자를 사용 하 여 현재 기본 문화권의 날짜, 시간, 숫자 및 열거형 값에 서식을 지정할 수 있습니다. 또한 속성을 <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A> 사용 하 여 특정 문화권에 대 한 이러한 값의 형식을 지정할 수 있습니다. 지정 된 형식은 데이터를 표시 하 고 사용자가 지정 된 형식으로 입력 한 데이터를 구문 분석 하는 데 사용 됩니다.  
  
 클래스 <xref:System.Windows.Forms.DataGridViewCellStyle> 는 wordwrap, 텍스트 맞춤 및 null 데이터베이스 값의 사용자 지정 표시에 대 한 추가 서식 속성을 제공 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤](how-to-format-data-in-the-windows-forms-datagridview-control.md)의 데이터에 서식을 지정 합니다.  
  
## <a name="formatting-with-the-cellformatting-event"></a>셀 서식 지정 이벤트로 서식 지정  
 기본 형식이 요구 사항에 맞지 않는 경우 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> 이벤트 처리기에서 사용자 지정 데이터 형식을 제공할 수 있습니다. <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> 처리기<xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 에 전달 된에는 처음에 셀 값을 포함 하는 속성이 있습니다. 일반적으로이 값은 자동으로 표시 형식으로 변환 됩니다. 값을 직접 변환 하려면 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 속성을 표시 형식 값으로 설정 합니다.  
  
> [!NOTE]
> 셀에 서식 문자열이 적용 되는 경우 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.FormattingApplied%2A> 속성을로 `true`설정 하지 않으면 속성 값의 변경 내용이 재정의 됩니다.  
  
 이벤트 <xref:System.Windows.Forms.DataGridView.CellFormatting> 는 값을 기준으로 개별 셀의 속성 <xref:System.Windows.Forms.DataGridViewCellStyle> 을 설정 하려는 경우에도 유용 합니다. 자세한 내용은 [방법: DataGridView 컨트롤](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)Windows Forms에서 데이터 서식을 사용자 지정 합니다.  
  
 사용자 지정 값의 기본 구문 분석이 사용자의 요구에 맞지 않는 경우 <xref:System.Windows.Forms.DataGridView.CellParsing> <xref:System.Windows.Forms.DataGridView> 컨트롤의 이벤트를 처리 하 여 사용자 지정 구문 분석을 제공할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤의 데이터 서식 지정](how-to-format-data-in-the-windows-forms-datagridview-control.md)
- [방법: DataGridView 컨트롤 Windows Forms에서 데이터 서식 지정](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)
