---
title: UI 자동화 공급자 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, providers
- providers, UI Automation
ms.assetid: 859557b8-51e1-4d15-92e8-318d2dcdb2f7
ms.openlocfilehash: c8db2e6cbd1f0c0dd61ecb8e147133b8c608ea8f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042037"
---
# <a name="ui-automation-providers-overview"></a>UI 자동화 공급자 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 UI 자동화 공급자를 통해 컨트롤이 UI 자동화 클라이언트 애플리케이션과 통신할 수 있습니다. 일반적으로 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 의 각 컨트롤 또는 기타 고유한 요소는 공급자가 나타냅니다. 공급자는 요소에 대한 정보를 노출하고 클라이언트 애플리케이션이 컨트롤과 상호 작용하도록 하는 컨트롤 패턴을 구현합니다(선택적).  
  
 클라이언트 애플리케이션은 일반적으로 공급자와 직접 작동될 필요가 없습니다. [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)], [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)]또는 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 프레임워크를 사용하는 응용 프로그램에서 대부분의 컨트롤은 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 시스템에 자동으로 노출됩니다. 또한 사용자 지정 컨트롤을 구현하는 애플리케이션은 이러한 컨트롤에 대해 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 공급자를 구현할 수도 있으며, 공급자에 액세스하기 위해 클라이언트 애플리케이션이 수행해야 할 특별한 단계는 없습니다.  
  
 컨트롤 개발자가 특히 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 및 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 창의 컨트롤에 대한 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 공급자를 구현하는 방법에 대한 개요를 제공합니다.  
  
<a name="Types_of_Providers"></a>   
## <a name="types-of-providers"></a>공급자 형식입니다.  
 UI 자동화 공급자는 클라이언트 쪽 공급자와 서버 쪽 공급자 두 범주로 나누어집니다.  
  
### <a name="client-side-providers"></a>클라이언트 쪽 공급자  
 클라이언트 쪽 공급자는 UI 자동화 클라이언트가 구현하여 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]을 지원하지 않거나 완전하게 지원되지 않는 애플리케이션과 통신합니다. 클라이언트 쪽 공급자는 일반적으로 Windows 메시지를 보내고 받아 프로세스 경계를 넘어 서버와 통신 합니다.  
  
 , Windows Forms 또는 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램의 컨트롤에 대 한 UI 자동화 공급자는 운영 체제의 일부로 제공 되므로 클라이언트 응용 프로그램은 자체 공급자를 구현할 필요가 거의 없으며이 개요에서는 다루지 않습니다. 추가.  
  
### <a name="server-side-providers"></a>서버 쪽 공급자  
 서버 쪽 공급자는, Windows Forms 또는 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]이외의 UI 프레임 워크를 기반으로 하는 응용 프로그램 또는 사용자 지정 컨트롤을 통해 구현 됩니다.  
  
 서버 쪽 공급자는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 핵심 시스템에 인터페이스를 노출하여 프로세스 경계를 넘어 클라이언트 애플리케이션과 통신하고, 클라이언트의 요청을 처리합니다.  
  
<a name="AutomationProviderConcepts"></a>   
## <a name="ui-automation-provider-concepts"></a>UI 자동화 공급자 개념  
 이 섹션에서는 UI 자동화 공급자를 구현하기 위해 이해해야 할 주요 개념 중 일부에 대해 간략하게 설명합니다.  
  
### <a name="elements"></a>요소  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소는 UI 자동화 클라이언트에 표시되는 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 항목입니다. 애플리케이션 창, 창, 단추, 도구 설명, 목록 상자 및 목록 항목을 예로 들 수 있습니다.  
  
### <a name="navigation"></a>탐색  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소는 클라이언트에 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리로 노출됩니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 은 요소를 탐색하여 트리를 생성합니다. 탐색은 부모, 형제, 자식을 나타낼 수 있는 각 요소의 공급자를 통해 사용할 수 있습니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 클라이언트 뷰에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.  
  
### <a name="views"></a>보기  
 다음 표에서와 같이 클라이언트에서는 3개의 주요 뷰로 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리가 표시됩니다.  
  
|||  
|-|-|  
|Raw 뷰|모든 요소를 포함합니다.|  
|컨트롤 뷰|컨트롤인 요소를 포함합니다.|  
|콘텐츠 뷰|콘텐츠가 있는 요소를 포함합니다.|  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 클라이언트 뷰에 대 한 자세한 내용은 [UI 자동화 트리 개요](ui-automation-tree-overview.md)를 참조 하세요.  
  
 콘텐츠 요소 또는 컨트롤 요소로 요소를 정의하는 것은 공급자 구현에서 담당합니다. 컨트롤 요소가 콘텐츠 요소일 수도 있고 그렇지 않을 수도 있지만, 모든 콘텐츠 요소는 컨트롤 요소입니다.  
  
### <a name="frameworks"></a>프레임워크  
 프레임워크는 화면 영역에서 하위 컨트롤, 적중 테스트, 렌더링을 관리하는 구성 요소입니다. 예를 들어, HWND라고도 하는 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 창은  메뉴 모음, 상태 표시줄 및 단추와 같은 여러 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 요소가 포함되는 프레임워크 역할을 할 수 있습니다.  
  
 목록 상자 및 트리 뷰와 같은[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 컨테이너 컨트롤은 하위 항목 렌더링 및 적중 테스트 수행을 위한 고유한 코드가 포함되어 있기 때문에 프레임워크로 간주됩니다. 한편, [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 목록 상자는 렌더링 및 적중 테스트가 포함된 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 창에서 처리되기 때문에 프레임워크가 아닙니다.  
  
 애플리케이션에서 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 는 다양한 프레임워크로 구성될 수 있습니다. 예를 들어, HWND 응용 프로그램 창에는 DHTML의 콤보 상자와 같은 구성 요소를 포함 하는 DHTML (동적 HTML)이 포함 될 수 있습니다.  
  
### <a name="fragments"></a>조각  
 조각은 특정 프레임워크에서 요소의 전체 하위 트리입니다. 하위 트리의 루트 노드에 있는 요소를 조각 루트라고 합니다. 조각 루트에는 부모는 없지만 다른 프레임워크, 일반적으로 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 창(HWND) 내에서 호스트됩니다.  
  
### <a name="hosts"></a>호스트  
 모든 조각의 루트 노드는 요소, 일반적으로 [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] 창(HWND)에서 호스트되어야 합니다. 다른 요소에서 호스트되지 않는 데스크톱은 예외입니다. 사용자 지정의 호스트는 애플리케이션 창 또는 최상위 컨트롤 그룹이 있을 수 있는 다른 창이 아닌 컨트롤 자체의 HWND입니다.  
  
 조각의 호스트는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 서비스를 제공하는 중요한 역할을 합니다. 이 호스트를 통해 조각 루트를 탐색할 수 있으며, 몇 가지 기본 속성을 제공하므로 사용자 지정 공급자가 속성을 구현할 필요가 없습니다.  
  
## <a name="see-also"></a>참고자료

- [서버 쪽 UI 자동화 공급자 구현](server-side-ui-automation-provider-implementation.md)
