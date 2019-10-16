---
title: 마이그레이션 지침
ms.date: 03/30/2017
ms.assetid: cb65c132-58c9-4028-b3d4-1efc71d5e60e
ms.openlocfilehash: 45f81b29f63701f690e396de2e9834f9933fd775
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796808"
---
# <a name="migration-guidance"></a>마이그레이션 지침
[!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에서 Microsoft는 두 번째 주요 버전의 WF (Windows Workflow Foundation)를 출시 하 고 있습니다. [!INCLUDE[wf1](../../../includes/wf1-md.md)]은 (는\* ) WinFX에서 릴리스 되었으며 (이제 WF3 이라고 함)에서 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]향상 되었습니다. WF3도의 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]일부 이지만 새 워크플로 기술 (w f 4의\* 형식, 이라고 함)과 함께 존재 합니다. WF4 사용을 고려하는 경우 타이밍을 제어한다는 점을 먼저 인식해야 합니다.  
  
- WF3은 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에서 완전히 지원되는 부분입니다.  
  
- WF3 애플리케이션은 수정 없이 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]에서 실행되며 계속해서 완전히 지원됩니다.  
  
- 새 WF3 응용 프로그램을 만들 수 있으며 Visual Studio 2012에서 기존 응용 프로그램을 편집할 수 있으며 완전히 지원 됩니다.  
  
 따라서 .NET Framework 4를 채택 하는 결정은 WF3 (\*\*)에서 w f 4 ()로 이동 하는 결정에서 분리 됩니다. 이 항목에서는 WF3 및 WF4 작업에 대한 정보를 담은 WF 마이그레이션 지침의 링크를 제공합니다.  
  
## <a name="wf-migration-whitepapers-and-cookbooks"></a>WF 마이그레이션 백서 및 설명서  
 [WF 마이그레이션 개요](https://go.microsoft.com/fwlink/?LinkId=153873) 항목에서는 WF3와 w f 4 및 마이그레이션 전략 간의 관계에 대 한 광범위 한 개요를 제공 합니다. 관련 항목에서는 특정 항목을 자세히 다룹니다.  
  
 [WF 마이그레이션 개요](https://go.microsoft.com/fwlink/?LinkId=153873)  
 WF3과 WF4 간의 관계를 설명하고 .NET 4에서 워크플로 기술의 사용자 또는 잠재 사용자가 선택할 수 있는 사항을 설명합니다.  
  
 [WF 마이그레이션: WF3 개발에 대 한 모범 사례](https://go.microsoft.com/fwlink/?LinkId=153852)  
 WF4로 쉽게 마이그레이션할 수 있도록 WF3 아티팩트를 디자인하는 방법을 설명합니다.  
  
 [WF 지침: 역할](https://go.microsoft.com/fwlink/?LinkId=153854)  
 규칙 관련 투자를 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 솔루션에 적용하는 방법을 설명합니다.  
  
 [WF 지침: 상태 시스템](https://go.microsoft.com/fwlink/?LinkId=153855)  
 상태 시스템 활동이 없는 경우의 WF4 흐름 제어 모델링을 설명합니다.  
  
 이 지침은 .NET Framework 4를 대상으로 하는 워크플로 프로젝트에만 적용됩니다. 상태 시스템 워크플로는 .NET 4.0.1 플랫폼 업데이트 1 릴리스에서 추가되었으며 .NET Framework 4.5의 일부로 포함되었습니다. .NET 4.0.1-4.0.3 및 .NET Framework 4.5의 상태 시스템 워크플로에 대 한 자세한 내용은 [Update 4.0.1 for Microsoft .NET Framework 4 Features](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hh290669(v=vs.100)) And [state machine 워크플로만](state-machine-workflows.md)항목을 참조 하세요.  
  
 [WF 마이그레이션 Cookbook: 사용자 지정 작업](https://go.microsoft.com/fwlink/?LinkId=153856)  
 WF4에서 WF3 사용자 지정 활동을 다시 디자인하기 위한 지침과 예를 제공합니다.  
  
 [WF 마이그레이션 Cookbook: 고급 사용자 지정 작업](https://go.microsoft.com/fwlink/?LinkId=275560)  
 WF3 큐를 사용하고 자식 활동을 WF4 사용자 지정 활동으로 예약하는 고급 WF3 사용자 지정 활동을 다시 디자인하기 위한 지침을 제공합니다.  
  
 [WF 마이그레이션 Cookbook: 워크플로도](https://go.microsoft.com/fwlink/?LinkId=153858)  
 WF4에서 WF3 워크플로를 다시 디자인하기 위한 지침과 예를 제공합니다.  
  
 [WF 마이그레이션 Cookbook: 워크플로 호스팅](https://go.microsoft.com/fwlink/?LinkId=275561)  
 WF3 호스팅 코드를 WF4 호스팅 코드로 다시 디자인하기 위한 지침을 제공합니다. 이 설명서의 목적은 WF3과 WF4 간의 주요 워크플로 호스팅 차이점을 설명하는 것입니다.  
  
 [WF 마이그레이션 Cookbook: 워크플로 추적](https://go.microsoft.com/fwlink/?LinkId=275562)  
 WF3 추적 코드 및 구성을 해당하는 WF4 추적 코드 및 구성을 사용하여 다시 디자인하기 위한 지침을 제공합니다.  
  
 [WF 지침: 워크플로 서비스](https://go.microsoft.com/fwlink/?LinkId=275564)  
 일반적인 기본 제공 활동의 시나리오에서 WF3으로 만들어진 WCF(Windows Communication Foundation) 웹 서비스(일반적으로 워크플로 서비스라고 함)를 구현하는 워크플로를 WF4를 사용하도록 다시 디자인하기 위한 단계별 지침을 예제 중심으로 제공합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.Interop>
