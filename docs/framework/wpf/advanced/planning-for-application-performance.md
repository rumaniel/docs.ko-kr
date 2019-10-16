---
title: 애플리케이션 성능 계획
ms.date: 03/30/2017
helpviewer_keywords:
- applications [WPF], optimizing
- WPF application [WPF], optimizing
ms.assetid: c91bd0c5-a193-46ff-9da1-eb7a3a76a3b3
ms.openlocfilehash: 70dda68112d47d3e5a0609a5df7696920477c698
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62032866"
---
# <a name="planning-for-application-performance"></a>애플리케이션 성능 계획
성능 목표를 달성 하는 성공 성능 전략을 개발 하는 정도에 따라 달라 집니다. 계획은 모든 제품 개발의 첫 번째 단계입니다. 이 항목에서는 적절 한 성능을 전략을 개발 하기 위한 몇 가지 간단한 규칙을 설명 합니다.  
  
## <a name="think-in-terms-of-scenarios"></a>시나리오 측면에서 생각 합니다.  
 시나리오 도움이 응용 프로그램의 중요 한 구성 요소에 집중 합니다. 시나리오는 경쟁 제품 뿐 아니라 고객에 게 프로그램에서 일반적으로 파생 됩니다. 항상 고객에 게 연구 하 고 확인 하는 진짜 이유, 제품 및 경쟁 업체의 제품에 대 한 기대 합니다. 고객의 의견 응용 프로그램의 기본 시나리오 결정에 도움이 됩니다. 예를 들어 시작 시 사용 될 구성 요소를 디자인할 경우 것 응용 프로그램을 시작 하는 경우 구성 요소를 한 번만 호출할으로입니다. 시작 시간에는 주요 시나리오가 됩니다. 주요 시나리오의 다른 예에는 애니메이션 시퀀스의 경우 원하는 프레임 속도 수 또는 최대 응용 프로그램에 대 한 허용 집합을 작업 수 없습니다.  
  
## <a name="define-goals"></a>목표 정의  
 목표에는 더 빠르거나 응용 프로그램은 수행 여부를 확인할 수 있습니다. 모든 시나리오에 대 한 목표를 정의 해야 합니다. 정의 하는 모든 성능 목표는 고객의 기대를 기반으로 해야 합니다. 집합 성능 문제가 여전히 많은 확인 되지 않은 경우 응용 프로그램 개발 초기에 목표로 순환 하기 어려울 수 있습니다. 그러나 초기 목표를 설정 하 고 이상 없는 목표를 전혀 수정 하는 것이 좋습니다.  
  
## <a name="understand-your-platform"></a>플랫폼 이해  
 측정, 조사, 응용 프로그램 개발 주기 동안 구체화/수정 주기를 항상 유지 합니다. 개발 주기의 끝부터 안정적이 고 안정적인 환경에서 응용 프로그램의 성능을 측정 해야 합니다. 외부 요인에 의해 발생 한 가변성을 피해 야 합니다. 예를 들어, 성능 테스트, 바이러스 백신 또는 SMS와 같은 자동 업데이트를 사용 하지 않도록 설정, 성능에 영향을 필요가 있는 순서로 테스트 결과 해야 있습니다. 응용 프로그램의 성능을 측정 했을 가장 크게 개선할에서를 일으키는 변경 내용을 식별 해야 합니다. 응용 프로그램을 수정한 후에 주기를 다시 시작 합니다.  
  
## <a name="make-performance-tuning-an-iterative-process"></a>성능 튜닝을 반복 처리  
 사용 하 여 각 기능의 상대적 비용을 알고 있어야 합니다. 예를 들어, Microsoft.NET Framework의 리플렉션 사용 되므로 일반적으로 성능에 컴퓨팅 리소스를 기준으로 신중 하 게 사용 하려는. 그렇다고 리플렉션 사용 하지 않으려면 사용 하는 기능의 성능 요구를 사용 하 여 응용 프로그램의 성능 요구 사항을 균형을 유지 하도록 주의 해야 하에 합니다.  
  
## <a name="build-towards-graphical-richness"></a>그래픽 다양성 빌드  
 달성 하기 위해 확장 가능한 접근 방법을 위한 핵심 기술은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램의 성능을 그래픽 다양성 및 복잡성에 대해 작성 하는 것입니다. 항상 시나리오 목표를 달성 하는 최소 성능 집약적인 리소스를 사용 하 여 시작 합니다. 이러한 목표를 달성 되 면 더 많은 성능 집약적인 기능과 항상 염두 시나리오 목표를 사용 하 여 그래픽 다양성 빌드하십시오. 말하지만 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 는 매우 다양 한 플랫폼 및 강력한 그래픽 기능을 제공 합니다. 걱정 없이 성능 집약적인 기능을 사용 하 여 전체 응용 프로그램의 성능에 부정적인 영향을 줄 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤은 광범위 한 사용자 지정 컨트롤 동작을 변경 하지 않고도 모양의 있으므로 기본적으로 확장할 수 있습니다. 스타일, 데이터 템플릿 및 컨트롤 템플릿을 활용 하 여 만들기를 점차적으로 사용자 지정 가능한를 개선할 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 는 성능 요구 사항에 맞게 조정 합니다.  
  
## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 성능 최적화](optimizing-wpf-application-performance.md)
- [하드웨어 이용](optimizing-performance-taking-advantage-of-hardware.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [개체 동작](optimizing-performance-object-behavior.md)
- [애플리케이션 리소스](optimizing-performance-application-resources.md)
- [텍스트](optimizing-performance-text.md)
- [데이터 바인딩](optimizing-performance-data-binding.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
