---
title: 기술 영역 개요
ms.date: 03/30/2017
helpviewer_keywords:
- window regions [WPF]
- Win32 code [WPF], WPF interoperation
- Win32 code [WPF], airspace
- airspace [WPF]
- interoperability [WPF], airspace
- Win32 code [WPF], window regions
ms.assetid: b7cc350f-b9e2-48b1-be14-60f3d853222e
ms.openlocfilehash: 4f1489065a70065700d2f8ceb974e66ecceeebd0
ms.sourcegitcommit: 77e33b682db39955e331b8e8eda4ef1925a24e78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70133808"
---
# <a name="technology-regions-overview"></a>기술 영역 개요
애플리케이션에 WPF, Win32 또는 DirectX와 같은 여러 프레젠테이션 기술이 사용되는 경우 이러한 기술은 공통 최상위 창에서 렌더링 영역을 공유해야 합니다. 이 항목에서는 WPF 상호 운용 애플리케이션에 대한 프레젠테이션과 입력에 영향을 미칠 수 있는 문제를 설명합니다.  
  
## <a name="regions"></a>영역  
 최상위 창에서 상호 운용 애플리케이션의 기술 중 하나로 구성되는 각 HWND에 자체 영역("에어스페이스"라고도 함)이 포함되도록 개념화할 수 있습니다. 창 내의 각 픽셀은 해당 HWND의 영역을 형성하는 정확히 하나의 HWND에 속합니다. 엄격히 말하면 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] HWND가 두 개 이상 있는 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 영역도 두 개 이상 있지만 이 설명을 위해 하나만 있다고 가정할 수 있습니다. 영역은 애플리케이션 수명 중에 해당 픽셀 위에 렌더링되는 모든 계층 또는 기타 창이 같은 렌더링 수준 기술에 포함되어야 함을 의미합니다. 에 대해 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 픽셀을 렌더링 하려고 하면 원하지 않는 결과가 발생 하며 상호 운용 api를 통해 가능한 한 많이 허용 되지 않습니다.  
  
### <a name="region-examples"></a>영역 예제  
 다음 그림에서는, DirectX 및 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]를 혼합 하는 응용 프로그램을 보여 줍니다. 각 기술은 자체적인 별도의 겹치지 않는 픽셀 집합을 사용하고 영역 문제가 없습니다.  
  
 ![Win32, DirectX 및 WPF를 혼합 하는 응용 프로그램의 예입니다.](./media/technology-regions-overview/win32-directx-windows-presentation-foundation-application.png)  
  
 이 애플리케이션이 마우스 포인터 위치를 사용하여 이러한 세 개의 영역 위에 렌더링할 애니메이션을 만든다고 가정해 봅니다. 애니메이션 자체에 응답 가능한 기술이 무엇이든 관계없이 해당 기술은 다른 두 기술의 영역을 침해합니다. 다음 그림에서는 Win32 영역 위에 WPF 원을 렌더링하는 시도를 보여 줍니다.  
  
 ![Win32 영역에 WPF 원을 렌더링 하려고 합니다.](./media/technology-regions-overview/render-windows-presentation-foundation-circle-over-win32-region.png)  
  
 또 다른 침해는 서로 다른 기술 사이에 투명도/알파 블렌딩을 사용하려는 경우입니다.  다음 그림에서 상자는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 및 DirectX 지역을 위반 합니다. 해당 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 상자의 픽셀은 반투명 하므로 DirectX와 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 모두 공동 소유 해야 합니다 .이는 가능 하지 않습니다.  따라서 이는 또 다른 침해이며 빌드될 수 없습니다.  
  
 ![Win32 및 DirectX 지역을 위반 하는 WPF 상자를 보여 주는 다이어그램입니다.](./media/technology-regions-overview/windows-foundation-presentation-box-violate-win32-directx-region.png)  
  
 이전 세 개의 예제에서는 사각형 영역을 사용했으나 다른 모양이 가능합니다.  예를 들어 영역에 구멍이 있을 수 있습니다. 다음 그림에서는 사각형 구멍이 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 있는 영역을 보여 줍니다 .이는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 및 DirectX 영역의 크기입니다.  
  
 ![사각형 구멍이 있는 Win32 영역을 보여 주는 다이어그램입니다.](./media/technology-regions-overview/win32-region-rectangular-hole.png)  
  
 영역은 완전히 사각형이 아니거나 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] HRGN(영역)으로 설명 가능한 모양일 수도 있습니다.  
  
 ![사각형이 아닌 영역을 표시 하는 다이어그램입니다.](./media/technology-regions-overview/nonrectangular-win32-region.png)  
  
## <a name="transparency-and-top-level-windows"></a>투명도 및 최상위 창  
 Windows의 창 관리자는 실제로 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] HWND만 처리합니다. 따라서 모든 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> 는 HWND입니다. Hwnd <xref:System.Windows.Window> 는 모든 hwnd에 대 한 일반 규칙을 따라야 합니다. 해당 HWND 내에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 코드는 전체 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] api가 지 원하는 모든 작업을 수행할 수 있습니다. 하지만 데스크톱에 있는 다른 HWND에 대한 상호 작용의 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 처리 및 렌더링 규칙을 따라야 합니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 api를 사용 하 여 사각형이 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 아닌 창을 지원 합니다. 비 사각형 창에는 hrgns를 사용 하 고 픽셀 별 알파에는 계층화 된 창을 지원 합니다.  
  
 상수 알파 및 색 키는 지원되지 않습니다.  [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 창 겹침 기능은 플랫폼에 따라 달라집니다.  
  
 창 겹침의 경우 창의 모든 픽셀에 적용할 알파 값을 지정하여 전체 창을 반투명하게 만들 수 있습니다.  실제로 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]는 픽셀별 알파를 지원하지만, 이 모드에서는 대화 상자, 드롭다운을 포함된 모든 자식 HWND를 직접 그려야 하므로 이 기술은 실제 프로그램에서 사용하기 매우 어렵습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]HRGNs; 지원 그러나이 기능에 대 한 관리 되는 Api는 없습니다. 플랫폼 호출 <xref:System.Windows.Interop.HwndSource> 을 사용 하 여 관련 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] api를 호출할 수 있습니다. 자세한 내용은 [관리 코드에서 네이티브 함수 호출](/cpp/dotnet/calling-native-functions-from-managed-code)을 참조하세요.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 창 겹침에는 다양한 운영 체제에 대한 여러 가지 기능이 포함됩니다. 이는 directx [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 를 사용 하 여 렌더링 하 고 계층화 된 창은 주로 directx 렌더링이 아닌 GDI 렌더링 용으로 설계 되었기 때문입니다.  
  
- WPF는 하드웨어 가속 계층화 된 창을 지원 합니다.  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 투명색 키를 지원하지 않습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 특히 렌더링이 하드웨어 가속될 경우 요청한 정확한 색을 렌더링하도록 보장할 수 없기 때문입니다.  
  
## <a name="see-also"></a>참고자료

- [WPF 및 Win32 상호 운용성](wpf-and-win32-interoperation.md)
- [연습: Win32에서 WPF 시계 호스팅](walkthrough-hosting-a-wpf-clock-in-win32.md)
- [WPF에서 Win32 콘텐츠 호스트](hosting-win32-content-in-wpf.md)
