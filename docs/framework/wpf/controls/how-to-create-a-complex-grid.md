---
title: 복잡 한 모눈을 만드는 방법
description: 표 형태 컨트롤을 사용 하 여 월별 달력 처럼 보이는 레이아웃을 만드는 방법의 예입니다.
ms.date: 03/30/2017
helpviewer_keywords:
- calendar [WPF], creating
- monthly calendar [WPF], creating
- Grid control [WPF], creating [WPF], complex grid
ms.assetid: 4ce3040a-a156-4364-9596-98ca1eca5550
ms.openlocfilehash: e2356113457e8c9a6737132e9779e49c05a23d77
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199983"
---
# <a name="how-to-create-a-complex-grid"></a>복잡 한 모눈을 만드는 방법

사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Grid> 월별 달력 처럼 보이는 레이아웃을 만들 컨트롤입니다.

## <a name="example"></a>예제

다음 예제에서는 8 개 행과 8 개의 열을 사용 하 여 정의 된 <xref:System.Windows.Controls.RowDefinition> 고 <xref:System.Windows.Controls.ColumnDefinition> 클래스입니다. 사용 하 여는 <xref:System.Windows.Controls.Grid.ColumnSpan%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Controls.Grid.RowSpan%2A?displayProperty=nameWithType> 와 함께 연결 된 속성으로 <xref:System.Windows.Shapes.Rectangle> 요소에는 다양 한 열과 행의 배경을 채웁니다. 각 셀에 요소가 둘 이상 있을 수 있으므로이 디자인은 가능한 한 <xref:System.Windows.Controls.Grid>, 원칙 차이점 <xref:System.Windows.Controls.Grid> 및 <xref:System.Windows.Documents.Table>합니다.

이 예제에서는 세로 그라데이션을 사용 <xref:System.Windows.Shapes.Shape.Fill%2A> 열 및 시각적 표시 및 달력의 가독성을 개선 하는 행입니다. 스타일 <xref:System.Windows.Controls.TextBlock> 요소는 날짜 및 요일을 나타냅니다. <xref:System.Windows.Controls.TextBlock> 사용 하 여 해당 셀 내의 요소는 절대적으로 배치를 <xref:System.Windows.FrameworkElement.Margin%2A> 속성 및 응용 프로그램에 대 한 스타일 내에 정의 된 맞춤 속성입니다.

[!code-xaml[GridComplex#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridComplex/CS/default.xaml#1)]

다음 이미지에는 결과 컨트롤을 사용자 지정할 수 있는 달력을 보여 줍니다.

![결과 컨트롤의 스크린샷](./media/how-to-create-a-complex-grid/wpf-manual-calendar.png)

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Grid?displayProperty=nameWithType>
- <xref:System.Windows.Documents.TableCell?displayProperty=nameWithType>
- [단색 및 그라데이션을 사용한 그리기 개요](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [패널 개요](panels-overview.md)
- [테이블 개요](../advanced/table-overview.md)