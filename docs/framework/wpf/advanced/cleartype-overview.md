---
title: ClearType 개요
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], ClearType technology
- ClearType [WPF], technology
ms.assetid: 7e2392e0-75dc-463d-a716-908772782431
ms.openlocfilehash: dbef816a995d9f4909a887f017da29bab6fc3702
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015646"
---
# <a name="cleartype-overview"></a>ClearType 개요
이 항목에서는에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]확인할 수 있는 Microsoft ClearType 기술에 대해 간략하게 설명 합니다.  

<a name="overview"></a>   
## <a name="technology-overview"></a>기술 개요  
 ClearType은 랩톱 화면, Pocket PC 화면, 평면 패널 모니터 등 기존 Lcd (액체 크리스탈 디스플레이)의 텍스트 가독성을 향상 시키는 Microsoft에서 개발한 소프트웨어 기술입니다.  ClearType은 LCD 화면의 모든 픽셀에서 개별 세로 색 줄무늬 요소에 액세스 하는 방식으로 작동 합니다. ClearType 이전에는 컴퓨터에 표시 될 수 있는 가장 낮은 수준의 세부 정보는 단일 픽셀 이지만 ClearType을 LCD 모니터에서 실행 하면 이제 텍스트의 기능을 픽셀의 픽셀 분수로 표시할 수 있습니다. 해상도를 더 세밀하게 지원할수록 텍스트의 미세한 부분까지 더 선명하게 표시되므로 오랫동안 더 쉽게 읽을 수 있습니다.  
  
 에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 제공 되는 cleartype은 Microsoft Windows 그래픽 장치 인터페이스 (GDI)에서 제공 하는 버전에 비해 몇 가지 개선 된 cleartype의 최신 세대입니다.  
  
<a name="sub-pixel_positioning"></a>   
## <a name="sub-pixel-positioning"></a>하위 픽셀 위치 지정  
 이전 버전의 ClearType에 비해 크게 향상 된 기능은 하위 픽셀 위치 지정을 사용 하는 것입니다. GDI에 있는 cleartype 구현과 달리에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 발견 된 cleartype은 픽셀의 시작 경계가 아니라 픽셀 내에서 문자를 시작할 수 있도록 허용 합니다. 문자 모양의 위치 지정에 적용되는 이처럼 세밀한 추가 해상도로 인해 문자 모양의 간격과 비율이 더욱 정확하고 일관성 있게 유지됩니다.  
  
 다음 두 예에서는 하위 픽셀 위치 지정을 사용할 때 문자 모양이 모든 하위 픽셀 경계에서 시작할 수 있는 방법을 보여 줍니다. 왼쪽의 예제는 하위 픽셀 위치 지정을 사용 하지 않은 이전 버전의 ClearType 렌더러를 사용 하 여 렌더링 됩니다. 오른쪽의 예제는 하위 픽셀 위치 지정을 사용 하 여 새 버전의 ClearType 렌더러를 사용 하 여 렌더링 됩니다. 오른쪽 이미지의 **e**와 **l**은 각각 서로 다른 하위 픽셀에서 시작하기 때문에 약간 다르게 렌더링됩니다. 화면에서 텍스트를 정상 크기로 볼 때는 문자 모양 이미지의 고대비로 인해 이 차이가 눈에 띄지 않습니다. 이는 ClearType에 통합 된 정교한 색 필터링 때문에 가능 합니다.  
  
 ![두 가지 버전의 ClearType으로 표시 된 텍스트](./media/wcpsdk-mmgraphics-text-cleartype-overview-01.png "wcpsdk_mmgraphics_text_cleartype_overview_01")  
이전 버전 및 최신 버전의 ClearType으로 표시된 텍스트  
  
 다음 두 예제에서는 이전 ClearType 렌더러의 출력과 새 버전의 ClearType 렌더러를 비교 합니다. 오른쪽의 하위 픽셀 위치 지정은 화면의 글자 간격 조정을 크게 향상시키며, 특히 하위 픽셀과 전체 픽셀 사이의 차이가 문자 모양 너비의 많은 부분을 차지하는 작은 크기의 경우에는 더욱 그렇습니다. 두 번째 이미지에서는 글자 사이의 간격 조정이 더 균일합니다. 텍스트 화면의 전반적인 모양에 대 한 하위 픽셀 위치 지정의 누적 혜택은 상당히 늘어나고 ClearType 기술의 상당한 발전을 나타냅니다.  
  
 ![이전 버전의 ClearType으로 표시 된 텍스트](./media/wcpsdk-mmgraphics-text-cleartype-overview-02.png "wcpsdk_mmgraphics_text_cleartype_overview_02")  
이전 버전 및 이후 버전의 ClearType을 통한 텍스트  
  
<a name="y-direction_antialiasing"></a>   
## <a name="y-direction-antialiasing"></a>y 방향 앤티 앨리어싱  
 에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ClearType의 또 다른 향상 된 기능은 y 방향 앤티앨리어싱입니다. Y 방향 앤티앨리어싱을 사용 하지 않는 GDI의 ClearType은 x 축에서 해상도를 향상 하지만 y 축은 제공 하지 않습니다. 얇은 곡선의 위쪽과 아래쪽에서 들쭉날쭉한 가장자리는 가독성을 떨어뜨립니다.  
  
 다음 예는 y 방향 앤티 앨리어싱을 사용하지 않는 경우의 효과를 보여 줍니다. 이 경우 글자의 위쪽과 아래쪽의 들쭉날쭉한 가장자리가 분명하게 눈에 띕니다.  
  
 ![얕은 곡선에서 가장자리가 들쭉날쭉한 텍스트](./media/wcpsdk-mmgraphics-text-cleartype-overview-03.png "wcpsdk_mmgraphics_text_cleartype_overview_03")  
얇은 곡선의 가장자리가 들쭉날쭉한 텍스트  
  
 의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ClearType은 y 방향 수준에 앤티 앨리어싱을 제공 하 여 들쭉날쭉한 가장자리를 부드럽게 합니다. 이는 얇은 곡선의 가로와 세로 양이 거의 같은 표의 문자를 사용하는 동아시아 언어의 가독성을 향상시키는 데 특히 중요합니다.  
  
 다음 예는 y 방향 앤티 앨리어싱을 사용하는 경우의 효과를 보여 줍니다. 이 경우 글자의 위쪽과 아래쪽이 매끄러운 곡선을 나타냅니다.  
  
 ![ClearType&#45;y 방향 앤티&#45;앨리어싱를 사용 하는 텍스트](./media/wcpsdk-mmgraphics-text-cleartype-overview-04.png "wcpsdk_mmgraphics_text_cleartype_overview_04")  
ClearType y 방향 앤티앨리어싱으로 표시된 텍스트  
  
<a name="hardware_acceleration"></a>   
## <a name="hardware-acceleration"></a>하드웨어 가속  
 의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ClearType은 성능 향상을 위해 하드웨어 가속 기능을 활용 하 고 CPU 부하 및 시스템 메모리 요구 사항을 줄일 수 있습니다. ClearType은 그래픽 카드의 픽셀 셰이더 및 비디오 메모리를 사용 하 여 특히 애니메이션을 사용 하는 경우 텍스트의 렌더링 속도를 향상 합니다.  
  
 의 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] cleartype은 시스템 차원의 cleartype 설정을 수정 하지 않습니다. Windows에서 ClearType을 사용 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 하지 않도록 설정 하면 앤티 앨리어싱 모드로 앤티 앨리어싱 됩니다. 또한 cleartype [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 은 [cleartype 튜너 PowerToy](https://www.microsoft.com/typography/ClearTypePowerToy.mspx)의 설정을 수정 하지 않습니다.  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 아키텍처 디자인과 관련된 결정 중 하나는 더 광범위하게 보급되고 있는 고해상도 DPI 모니터를 더 효과적으로 지원하기 위해 해상도의 영향을 받지 않는 레이아웃이 있어야 한다는 것입니다. 이에 따라 일부 동아시아 글꼴의 앨리어싱된 텍스트 렌더링과 비트맵이 모두 해상도의 영향을 받기 때문에 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서는 이러한 렌더링과 비트맵을 지원하지 않습니다.  
  
<a name="further_information"></a>   
## <a name="further-information"></a>추가 정보  
 [ClearType 정보](https://www.microsoft.com/typography/ClearTypeInfo.mspx)  
  
 [ClearType Tuner PowerToy](https://www.microsoft.com/typography/ClearTypePowerToy.mspx)  
  
## <a name="see-also"></a>참고자료

- [ClearType 레지스트리 설정](cleartype-registry-settings.md)
