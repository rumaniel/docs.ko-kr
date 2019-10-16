---
title: Visual Basic에서 구성 요소 만들기 및 사용
ms.date: 07/20/2015
helpviewer_keywords:
- components [Visual Basic]
ms.assetid: ee6a4156-73f7-4e9b-8e01-c74c4798b65c
ms.openlocfilehash: 5f130c4de45f81dfb21c8c87c9e24d22cd4276ce
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65586731"
---
# <a name="creating-and-using-components-in-visual-basic"></a>Visual Basic에서 구성 요소 만들기 및 사용
*구성 요소*는 <xref:System.ComponentModel.IComponent?displayProperty=nameWithType> 인터페이스를 구현하는 클래스이거나 <xref:System.ComponentModel.IComponent>를 구현하는 클래스에서 직접 또는 간접적으로 파생되는 클래스입니다. .NET Framework 구성 요소는 재사용 가능한가, 다른 개체와 상호 작용할 수 및 외부 리소스 및 디자인 타임 지원에 대 한 제어를 제공 하는 개체입니다.  
  
 구성 요소의 중요한 기능은 디자인할 수 있다는 것입니다. 즉, Visual Studio 통합 개발 환경에서 구성 요소인 클래스를 사용할 수 있습니다. 구성 요소는 도구 상자에 추가하고, 양식에 끌어서 놓고, 디자인 화면에서 조작할 수 있습니다. 구성 요소에 대 한 기본 디자인 타임 지원을 않으며.NET Framework에 기본 제공 되는 구성 요소 개발자는 기본 디자인 타임 기능을 활용 하기 위해 추가 작업을 수행할 필요가 없습니다.  
  
 *컨트롤*과 구성 요소는 둘 다 디자인 가능하다는 점에서 비슷합니다. 그러나 컨트롤은 사용자 인터페이스를 제공하지만 구성 요소는 제공하지 않습니다. 컨트롤은 기본 컨트롤 클래스인 <xref:System.Windows.Forms.Control> 또는 <xref:System.Web.UI.Control> 중 하나에서 파생되어야 합니다.  
  
## <a name="when-to-create-a-component"></a>구성 요소를 만들어야 하는 경우  
 클래스가 Design Surface(예: Windows Forms 또는 Web Forms 디자이너)에서 사용되지만 사용자 인터페이스가 없는 경우 클래스는 구성 요소로서, <xref:System.ComponentModel.IComponent>를 구현하거나 <xref:System.ComponentModel.IComponent>를 직접 또는 간접적으로 구현하는 클래스에서 파생되어야 합니다.  
  
 <xref:System.ComponentModel.Component> 및 <xref:System.ComponentModel.MarshalByValueComponent> 클래스는 <xref:System.ComponentModel.IComponent> 인터페이스의 기본 구현입니다. 이러한 클래스 간의 기본 차이점은 <xref:System.ComponentModel.Component> 클래스는 참조에 의해 마샬링되지만 <xref:System.ComponentModel.IComponent>는 값에 의해 마샬링된다는 점입니다. 다음 목록에서는 구현에 대한 다양한 지침을 제공합니다.  
  
- 구성 요소가 참조에 의해 마샬링되어야 하는 경우 <xref:System.ComponentModel.Component>에서 파생합니다.  
  
- 구성 요소가 값에 의해 마샬링되어야 하는 경우 <xref:System.ComponentModel.MarshalByValueComponent>에서 파생합니다.  
  
- 단일 상속으로 인해 구성 요소가 기본 구현 중 하나에서 파생될 수 없는 경우 <xref:System.ComponentModel.IComponent>를 구현합니다.  
  
## <a name="component-classes"></a>구성 요소 클래스  
 <xref:System.ComponentModel> 네임스페이스는 구성 요소와 컨트롤의 런타임 및 디자인 타임 동작을 구현하는 데 사용되는 클래스를 제공합니다. 이 네임스페이스에는 특성 및 형식 변환기를 구현하고, 데이터 소스에 바인딩하고, 구성 요소 사용을 허가하기 위한 기본 클래스 및 인터페이스가 포함됩니다.  
  
 핵심 구성 요소 클래스는 다음과 같습니다.  
  
- <xref:System.ComponentModel.Component>. <xref:System.ComponentModel.IComponent> 인터페이스에 대한 기본 구현입니다. 이 클래스를 통해 애플리케이션 간에 개체를 공유할 수 있습니다.  
  
- <xref:System.ComponentModel.MarshalByValueComponent>. <xref:System.ComponentModel.IComponent> 인터페이스에 대한 기본 구현입니다.  
  
- <xref:System.ComponentModel.Container>. <xref:System.ComponentModel.IContainer> 인터페이스에 대한 기본 구현입니다. 이 클래스는 0 또는 추가 구성 요소를 캡슐화합니다.  
  
 구성 요소 라이선싱에 사용되는 일부 클래스는 다음과 같습니다.  
  
- <xref:System.ComponentModel.License>. 모든 라이선스에 대한 추상 기본 클래스입니다. 라이선스는 구성 요소의 특정 인스턴스에 부여됩니다.  
  
- <xref:System.ComponentModel.LicenseManager>. 라이선스를 구성 요소에 추가하고 <xref:System.ComponentModel.LicenseProvider>를 관리하기 위한 속성과 메서드를 제공합니다.  
  
- <xref:System.ComponentModel.LicenseProvider>. 라이선스 공급자를 구현하기 위한 추상 기본 클래스입니다.  
  
- <xref:System.ComponentModel.LicenseProviderAttribute>. 클래스와 함께 사용할 <xref:System.ComponentModel.LicenseProvider> 클래스를 지정합니다.  
  
 구성 요소를 설명 및 유지하는 데 일반적으로 사용되는 클래스입니다.  
  
- <xref:System.ComponentModel.TypeDescriptor>. 구성 요소의 특성, 속성 및 이벤트와 같이, 구성 요소의 특성에 대한 정보를 제공합니다.  
  
- <xref:System.ComponentModel.EventDescriptor>. 이벤트에 대한 정보를 제공합니다.  
  
- <xref:System.ComponentModel.PropertyDescriptor>. 속성에 대한 정보를 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [컨트롤 및 구성 요소 제작 문제 해결](../../framework/winforms/controls/troubleshooting-control-and-component-authoring.md)  
 일반적인 문제 해결 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: Windows Forms에서 디자인 타임 지원 액세스](../../framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)
