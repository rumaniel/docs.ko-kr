---
ms.openlocfilehash: 0825233c0dae131fa9d00565348fac6fdf0be063
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67857474"
---
### <a name="horizontal-scrolling-and-virtualization"></a>가로 스크롤 및 가상화

|   |   |
|---|---|
|세부 정보|이 변경 내용은 주 스크롤 방향의 직각 방향으로 자체 가상화를 수행하는 <xref:System.Windows.Controls.ItemsControl?displayProperty=name>에 적용됩니다(주요 예제는 EnableColumnVirtualization=&quot;True&quot;를 사용하는 <xref:System.Windows.Controls.DataGrid?displayProperty=name>임).  특정 가로 스크롤 작업의 결과는 보다 직관적이고 비교 가능한 세로 작업의 결과와 좀 더 유사한 결과를 생성하도록 변경되었습니다.<p/>작업으로는 가로 스크롤 막대를 마우스 오른쪽 단추로 클릭할 때 표시되는 메뉴의 이름을 사용하기 위한 &quot;여기로 스크롤&quot; 및 &quot;오른쪽 가장자리&quot;가 있습니다.  이 두 작업 모두에서는 후보 오프셋을 컴퓨팅하고 <xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset(System.Double)>을 호출합니다.<p/>새롭게 가상화가 취소된 콘텐츠에서는 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=name>의 값이 변경되었으므로 새 오프셋으로 스크롤한 후에 &quot;여기&quot; 또는 &quot;오른쪽 가장자리&quot;의 개념이 변경되었을 수 있습니다.<p/>.NET Framework 4.6.2 이전에는 &quot;여기&quot; 또는 &quot;오른쪽 가장자리&quot;는 더 이상 아닐 수 있지만 스크롤 작업을 수행하면 후보 오프셋이 사용됩니다.  결과적으로 그림과 같은 스크롤 상자 &quot;바운스&quot;와 같은 결과가 나타납니다. <xref:System.Windows.Controls.DataGrid?displayProperty=name>에서 ExtentWidth=1000 및 Width=200이라고 가정합니다.  &quot;오른쪽 가장자리&quot;로 스크롤하면 후보 오프셋 1000 - 200 = 800이 사용됩니다.  해당 오프셋으로 스크롤하는 동안 새 열의 가상화가 취소됩니다. 열이 매우 넓어서 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=name>가 2000으로 변경된다고 가정하겠습니다.  스크롤은 HorizontalOffset=800에서 종료되며 엄지는 스크롤 막대 가운데 근처로 다시 &quot;바운스&quot;됩니다. 이 위치에 해당하는 값은 800/2000=40%입니다.<p/>이 변경으로 이 상황이 발생할 경우 새 후보 오프셋을 다시 계산하고 다시 시도하게 됩니다. (세로 스크롤도 이미 이와 같이 작동합니다.) <p/>이 변경으로 인해 최종 사용자가 오프셋을 더욱 쉽게 예측할 수 있는 직관적인 환경이 생성됩니다. 하지만 가로 스크롤 이후 <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset?displayProperty=name>(최종 사용자가 호출하거나 명시적 <xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset(System.Double)> 호출을 통해 호출됨)의 정확한 값에 따라 동작이 달라지는 앱에도 영향을 줄 수 있습니다.|
|제안|<xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset?displayProperty=name>의 예측 값을 사용하는 앱의 경우 가상화 취소로 인해 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=name>가 변경될 수 있는 가로 스크롤 이후 실제 값과 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth?displayProperty=name>의 값을 페치하도록 변경해야 합니다.|
|범위|부|
|버전|4.6.2|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.Primitives.IScrollInfo?displayProperty=nameWithType></li></ul>|

