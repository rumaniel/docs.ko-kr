---
title: UI 자동화 컨트롤 형식 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, control types
- control types, UI Automation
ms.assetid: 75159ef8-bd43-4d13-acb7-1f1fe9253160
ms.openlocfilehash: 3c53d07cc6ebbd5259a4bfb5224c486481167c10
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042240"
---
# <a name="ui-automation-control-types-overview"></a>UI 자동화 컨트롤 형식 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 컨트롤 형식은 콤보 상자나 단추와 같은 특정 요소가 구현하는 컨트롤의 종류를 나타내기 위해 사용할 수 있는 알려진 식별자입니다.  
  
 알려진 식별자를 사용하면 보조 기술 디바이스가 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 에서 사용 가능한 컨트롤의 형식 및 이 컨트롤을 조작하는 방식을 더 쉽게 확인할 수 있습니다.  
  
<a name="UI_Automation_Control_Type_Requisites"></a>   
## <a name="ui-automation-control-type-requisites"></a>UI 자동화 컨트롤 형식 필수 요소  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 컨트롤 형식은 공급자가 충족해야 하는 일련의 조건을 제공합니다. 이러한 조건이 충족되는 경우 컨트롤은 특정 컨트롤 형식 이름을 사용할 수 있습니다. 각 컨트롤 형식에는 다음에 대한 조건이 있습니다.  
  
- [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 컨트롤 패턴 - 지원해야 하는 컨트롤 패턴, 선택 사항인 컨트롤 패턴, 컨트롤에서 지원해서는 안 되는 컨트롤 패턴  
  
- [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 속성 값 - 지원되는 속성 값  
  
- [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조 - 컨트롤에 필요한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리 구조  
  
 컨트롤이 특정 컨트롤 형식에 대한 조건을 충족한다면 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A> 속성 값이 해당 컨트롤 형식을 나타내는 것입니다.  
  
<a name="Current_UI_Automation_Control_Types"></a>   
## <a name="current-ui-automation-control-types"></a>현재 UI 자동화 컨트롤 형식  
 다음 목록에는 현재 제공되는 일련의 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 컨트롤 형식이 나옵니다.  
  
- [Button 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-button-control-type.md)  
  
- [Calendar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-calendar-control-type.md)  
  
- [CheckBox 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-checkbox-control-type.md)  
  
- [ComboBox 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-combobox-control-type.md)  
  
- [DataGrid 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-datagrid-control-type.md)  
  
- [DataItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-dataitem-control-type.md)  
  
- [Document 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-document-control-type.md)  
  
- [Edit 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-edit-control-type.md)  
  
- [Group 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-group-control-type.md)  
  
- [Header 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-header-control-type.md)  
  
- [HeaderItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-headeritem-control-type.md)  
  
- [Hyperlink 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-hyperlink-control-type.md)  
  
- [Image 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-image-control-type.md)  
  
- [List 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-list-control-type.md)  
  
- [ListItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-listitem-control-type.md)  
  
- [Menu 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-menu-control-type.md)  
  
- [MenuBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-menubar-control-type.md)  
  
- [MenuItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-menuitem-control-type.md)  
  
- [Pane 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-pane-control-type.md)  
  
- [ProgressBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-progressbar-control-type.md)  
  
- [RadioButton 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-radiobutton-control-type.md)  
  
- [ScrollBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-scrollbar-control-type.md)  
  
- [Separator 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-separator-control-type.md)  
  
- [Slider 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-slider-control-type.md)  
  
- [Spinner 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-spinner-control-type.md)  
  
- [SplitButton 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-splitbutton-control-type.md)  
  
- [StatusBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-statusbar-control-type.md)  
  
- [Tab 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-tab-control-type.md)  
  
- [TabItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-tabitem-control-type.md)  
  
- [Table 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-table-control-type.md)  
  
- [Text 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-text-control-type.md)  
  
- [Thumb 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-thumb-control-type.md)  
  
- [TitleBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-titlebar-control-type.md)  
  
- [ToolBar 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-toolbar-control-type.md)  
  
- [ToolTip 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-tooltip-control-type.md)  
  
- [Tree 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-tree-control-type.md)  
  
- [TreeItem 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-treeitem-control-type.md)  
  
- [Window 컨트롤 형식에 대한 UI 자동화 지원](ui-automation-support-for-the-window-control-type.md)  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.ControlType>
