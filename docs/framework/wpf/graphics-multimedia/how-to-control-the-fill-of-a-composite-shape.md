---
title: '방법: 복합 도형의 채우기 제어'
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], composite [WPF], controlling fill
- composite shapes [WPF], controlling fill
- graphics [WPF], composite shapes
- fill [WPF], controlling
ms.assetid: c1c94575-9eca-48a5-a49a-2ec65259f229
ms.openlocfilehash: 89f69d392e8838af99538c759a2f06453e1bcd60
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855905"
---
# <a name="how-to-control-the-fill-of-a-composite-shape"></a>방법: 복합 도형의 채우기 제어

또는<xref:System.Windows.Media.GeometryGroup> 의속성<xref:System.Windows.Media.GeometryGroup.FillRule%2A> 은 복합 셰이프가 지정 된 점이 기 하 도형의 일부 인지 여부를 확인 하는 데 사용 하는 "규칙"을 지정 합니다. <xref:System.Windows.Media.PathGeometry> 에는 <xref:System.Windows.Media.FillRule> <xref:System.Windows.Media.FillRule.EvenOdd> 및 의두가지값을사용할수있습니다.<xref:System.Windows.Media.FillRule.Nonzero> 다음 섹션에서는 이러한 두 가지 규칙을 사용하는 방법을 설명합니다.

**EvenOdd:** 이 규칙은 해당 점에서 모든 방향으로 무한대로 광선을 그리고 광선이 교차 하는 지정 된 도형 내에서 경로 세그먼트 수를 계산 하 여 채우기 영역에 점이 있는지 여부를 결정 합니다. 이 숫자가 홀수이면 점이 안에 있고, 짝수이면 밖에 있습니다.

예를 들어 아래 XAML은가 <xref:System.Windows.Media.GeometryGroup.FillRule%2A> 로 <xref:System.Windows.Media.FillRule.EvenOdd>설정 된 일련의 동심 링 (대상)으로 구성 된 복합 셰이프를 만듭니다.

[!code-xaml[GeometriesMiscSnippets_snip#FillRuleEvenOddValue](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillruleevenoddvalue)]

다음 그림은 이전 예제에서 만든 도형을 보여 줍니다.

![교대로 반복 되는 색을 사용 하는 계열 동심 링으로 구성 된 원입니다.](./media/how-to-control-the-fill-of-a-composite-shape/fillrule-evenodd-property.png)

위의 그림에서 중심과 세 번째 링은 채워지지 않습니다. 두 링 중 하나에 있는 점에서 그린 광선이 짝수의 세그먼트를 통과하기 때문입니다. 다음 그림을 참조 하세요.

![원에 그려진 EvenOdd 광선을 보여 주는 다이어그램입니다.](./media/how-to-control-the-fill-of-a-composite-shape/fillrule-evenodd-rays.png)

**0이 아닌** 이 규칙은 해당 점에서 모든 방향으로 무한대로 광선을 그린 다음 도형의 세그먼트가 광선과 교차 하는 위치를 검사 하 여 경로의 채우기 영역에 점이 있는지 여부를 확인 합니다. 0부터 시작하여 세그먼트가 왼쪽에서 오른쪽으로 광선과 교차할 때마다 1을 추가하고 경로 세그먼트가 오른쪽에서 왼쪽으로 광선과 교차할 때마다 1을 뺍니다. 교차 수를 계산한 후 결과가 0이면 점이 경로의 밖에 있습니다. 그렇지 않으면 점이 내부에 있습니다.

[!code-xaml[GeometriesMiscSnippets_snip#FillRuleNonZeroValueEllipseGeometry](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillrulenonzerovalueellipsegeometry)]

이전 예제를 사용 하는 경우 <xref:System.Windows.Media.FillRule.Nonzero> 에 대 한 <xref:System.Windows.Media.GeometryGroup.FillRule%2A> 값은 다음 그림을 보여 줍니다.

![계열 동심 링으로 구성 된 원은 모두 동일한 색으로 채워집니다.](./media/how-to-control-the-fill-of-a-composite-shape/fillrule-value-nonzero.png)

여기에서 볼 수 있듯이 모든 링이 채워집니다. 모든 세그먼트가 같은 방향으로 실행되므로 임의 점에서 그린 광선이 하나 이상의 세그먼트와 교차하고 교차의 합계가 0이 아니기 때문입니다. 예를 들어 다음 그림에서 빨간색 화살표는 세그먼트가 그려지는 방향을 나타내고 흰색 화살표는 가장 안쪽 링의 지점에서 실행 되는 임의의 광선을 나타냅니다. 광선이 교차하는 각 세그먼트에 대해 0 값부터 시작할 경우 세그먼트가 왼쪽에서 오른쪽으로 광선과 교차하므로 1이 추가됩니다.

![0이 아닌 값과 같은 FillRule 속성 값을 보여 주는 다이어그램입니다.](./media/how-to-control-the-fill-of-a-composite-shape/fillrule-value-equal-nonzero.png)

규칙의 <xref:System.Windows.Media.FillRule.Nonzero> 동작을 더 잘 보여 주기 위해 다른 방향으로 실행 되는 세그먼트가 있는 보다 복잡 한 모양이 필요 합니다. 아래 XAML 코드는 앞의 예제와 비슷한 모양의 도형을 만듭니다. 단,이는를 사용 <xref:System.Windows.Media.PathGeometry> 하 여 만든 <xref:System.Windows.Media.EllipseGeometry> 다음이를 사용 하 여 네 개의 동심 원호를 만든 다음이를 사용 하 여 완전히 폐쇄형 동심 원을 만듭니다.

[!code-xaml[GeometriesMiscSnippets_snip#FillRuleNonZeroValuePathGeometry](~/samples/snippets/xaml/VS_Snippets_Wpf/GeometriesMiscSnippets_snip/XAML/FillRuleExample.xaml#fillrulenonzerovaluepathgeometry)]

다음 그림은 이전 예제에서 만든 도형을 보여 줍니다.

![세 번째 호를 채우지 않고 교대로 반복 되는 색을 사용 하는 계열 동심 링으로 구성 된 원입니다.](./media/how-to-control-the-fill-of-a-composite-shape/pathgeometry-concentric-arcs.png)

중심에서 세 번째 호까지는 채워지지 않습니다. 다음 그림에서는이를 보여 줍니다. 이 그림에서 빨간색 화살표는 세그먼트가 그려진 방향을 나타냅니다. 두 개의 흰색 화살표는 “채워지지 않은” 영역의 점에서 외부로 이동되는 2개의 임의 광선을 나타냅니다. 이 그림에서 볼 수 있듯이 해당 경로에서 세그먼트를 교차하는 지정된 광선의 값 합계는 0입니다. 앞에서 정의한 대로 합계가 0이 *아닌* 경우는 해당 점이 형상에 속하는 것을 의미하지만 합계가 0이라는 사실은 해당 점이 형상에 속하지 않음을 의미합니다(채우기의 일부가 아님).

![세그먼트를 교차 하는 임의의 광선을 보여 주는 다이어그램](./media/how-to-control-the-fill-of-a-composite-shape/arbitrary-ray-cross-segment.png)

> [!NOTE]
> 의 <xref:System.Windows.Media.FillRule>목적을 위해 모든 셰이프는 닫힌 것으로 간주 됩니다. 세그먼트에 틈이 있으면 가상선을 그려 닫습니다. 위의 예제에서는 링에 작은 틈이 있습니다. 이점을 고려할 때 이러한 틈을 지나가는 광선이 다른 결과를 가져와 광선이 다른 방향으로 진행될 것으로 예상할 수 있습니다. 다음은 이러한 간격과 "허수 세그먼트" (를 <xref:System.Windows.Media.FillRule>적용 하기 위해 그려진 세그먼트) 중 하나를 닫는 확대 된 그림입니다.

![항상 닫혀 있는 FillRule 세그먼트를 보여 주는 다이어그램](./media/how-to-control-the-fill-of-a-composite-shape/fillrule-closed-segments.png)

## <a name="example"></a>예제

## <a name="see-also"></a>참고자료

- [복합 도형 만들기](how-to-create-a-composite-shape.md)
- [Geometry 개요](geometry-overview.md)
