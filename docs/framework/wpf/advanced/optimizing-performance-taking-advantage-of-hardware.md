---
title: '성능 최적화: 하드웨어 활용'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], performance
- hardware rendering pipeline [WPF]
- rendering tiers [WPF]
- graphics rendering tiers [WPF]
- graphics [WPF], rendering tiers
- software rendering pipeline [WPF]
ms.assetid: bfb89bae-7aab-4cac-a26c-a956eda8fce2
ms.openlocfilehash: a47a4aae785d817904c30fe7c865a1c033eb3cca
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709220"
---
# <a name="optimizing-performance-taking-advantage-of-hardware"></a>성능 최적화: 하드웨어 활용
의 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 내부 아키텍처에는 두 개의 렌더링 파이프라인 인 하드웨어와 소프트웨어가 있습니다. 이 항목에서는 응용 프로그램의 성능 최적화에 대 한 결정을 내리는 데 도움이 되는 이러한 렌더링 파이프라인에 대 한 정보를 제공 합니다.  
  
## <a name="hardware-rendering-pipeline"></a>하드웨어 렌더링 파이프라인  
 성능을 결정 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 하는 데 가장 중요 한 요소 중 하나는 렌더링 바인딩되어 있음을 의미 합니다. 렌더링 해야 하는 픽셀 수가 많을 수록 성능 비용은 높아집니다. 그러나 GPU (그래픽 처리 장치)로 오프 로드할 수 있는 더 많은 렌더링으로 얻을 수 있는 성능상의 이점이 증가 합니다. 응용 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 프로그램 하드웨어 렌더링 파이프라인은 최소 microsoft directx 버전 7.0을 지 원하는 하드웨어에서 microsoft directx 기능을 최대한 활용 합니다. Microsoft DirectX 버전 7.0 및 Shadereffect 2.0 이상 기능을 지 원하는 하드웨어에서 추가 최적화를 얻을 수 있습니다.  
  
## <a name="software-rendering-pipeline"></a>소프트웨어 렌더링 파이프라인  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 소프트웨어 렌더링 파이프라인은 완전히 CPU에 바인딩되어 있습니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 CPU의 SSE 및 SSE2 명령 집합을 활용 하 여 최적화 되 고 완전 한 기능을 갖춘 소프트웨어 래스터 라이저를 구현 합니다. 소프트웨어에 대 한 대체는 하드웨어 렌더링 파이프라인을 사용 하 여 응용 프로그램 기능을 렌더링할 수 없을 때마다 원활 하 게 진행 됩니다.  
  
 소프트웨어 모드에서 렌더링할 때 발생 하는 가장 큰 성능 문제는 렌더링 하려는 픽셀 수로 정의 되는 채우기 속도와 관련이 있습니다. 소프트웨어 렌더링 모드의 성능에 대해 염려 하는 경우 픽셀을 다시 그려지는 횟수를 최소화 합니다. 예를 들어 파란색 배경의 응용 프로그램이 있는 경우이를 통해 약간 투명 한 이미지를 렌더링 하면 응용 프로그램의 모든 픽셀이 두 번 렌더링 됩니다. 결과적으로 파란색 배경만 있는 경우를 제외 하 고는 이미지를 사용 하 여 응용 프로그램을 렌더링 하는 데 시간이 2 배가 됩니다.  
  
### <a name="graphics-rendering-tiers"></a>그래픽 렌더링 계층  
 응용 프로그램이 실행 되는 하드웨어 구성을 예측 하는 것은 매우 어려울 수 있습니다. 그러나 다른 하드웨어에서 실행 하는 경우 응용 프로그램에서 기능을 원활 하 게 전환할 수 있도록 하는 디자인을 고려해 볼 수 있습니다. 그러면 각 하드웨어 구성을 최대한 활용할 수 있습니다.  
  
 이를 위해에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 런타임에 시스템의 그래픽 기능을 결정 하는 기능을 제공 합니다. 비디오 카드를 세 가지 렌더링 기능 계층 중 하나로 분류 하 여 그래픽 기능을 결정 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]응용 프로그램에서 렌더링 기능 계층을 쿼리할 수 있도록 하는 API를 노출 합니다. 그러면 응용 프로그램은 하드웨어에서 지 원하는 렌더링 계층에 따라 런타임에 다른 코드 경로를 사용할 수 있습니다.  
  
 렌더링 계층 수준에 가장 큰 영향을 미치는 그래픽 하드웨어 기능은 다음과 같습니다.  
  
- **비디오 RAM** 그래픽 하드웨어의 비디오 메모리 양에 따라 그래픽을 합성하는 데 사용할 수 있는 버퍼의 크기와 수를 결정합니다.  
  
- **픽셀 셰이더** 픽셀 셰이더는 픽셀별 미치는 영향을 계산하는 그래픽 처리 함수입니다. 표시된 그래픽의 해상도에 따라 표시 프레임별로 수백만 픽셀을 처리해야 할 수도 있습니다.  
  
- **꼭짓점 셰이더** 꼭짓점 셰이더는 개체의 꼭짓점 데이터에서 수학 연산을 수행하는 그래픽 처리 함수입니다.  
  
- **여러 질감 지원** 여러 질감 지원은 3D 그래픽 개체에서 혼합 작업 중에 두 개 이상의 개별 질감을 적용할 수 있는 기능을 나타냅니다. 여러 질감 지원 정도는 그래픽 하드웨어의 여러 질감 단위 수에 따라 결정됩니다.  
  
 픽셀 셰이더, 꼭 짓 점 셰이더 및 다중 질감 기능은 특정 DirectX 버전 수준을 정의 하는 데 사용 되며,이를 통해에서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]다른 렌더링 계층을 정의 하는 데 사용 됩니다.  
  
 그래픽 하드웨어 기능에 따라 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션의 렌더링 기능이 결정됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 시스템에서는 다음 세 개의 렌더링 계층을 정의합니다.  
  
- **렌더링 계층 0** 그래픽 하드웨어 가속이 없습니다. DirectX 버전 수준이 버전 7.0 보다 낮습니다.  
  
- **렌더링 계층 1** 부분 그래픽 하드웨어 가속. DirectX 버전 수준은 버전 7.0 보다 크거나 같고 9.0 버전 보다 **낮습니다** .  
  
- **렌더링 계층 2** 대부분의 그래픽 기능에서는 그래픽 하드웨어 가속을 사용합니다. DirectX 버전 수준이 버전 9.0 보다 크거나 같습니다.  
  
 렌더링 계층에 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 대 한 자세한 내용은 [그래픽 렌더링 계층](graphics-rendering-tiers.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 성능 최적화](optimizing-wpf-application-performance.md)
- [응용 프로그램 성능 계획](planning-for-application-performance.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [개체 동작](optimizing-performance-object-behavior.md)
- [애플리케이션 리소스](optimizing-performance-application-resources.md)
- [텍스트](optimizing-performance-text.md)
- [데이터 바인딩](optimizing-performance-data-binding.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
