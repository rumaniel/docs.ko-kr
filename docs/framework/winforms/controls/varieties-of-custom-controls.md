---
title: 사용자 지정 컨트롤의 종류
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], user controls
- controls [Windows Forms], types of
- composite controls [Windows Forms]
- extended controls [Windows Forms]
- controls [Windows Forms], extended
- user controls [Windows Forms]
- custom controls [Windows Forms]
- controls [Windows Forms], composite
ms.assetid: 3cea09e5-4344-4ccb-9858-b66ccac210ff
ms.openlocfilehash: 106da550fc6e6c50bc40e103e1f855059a9ffa9c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950099"
---
# <a name="varieties-of-custom-controls"></a>사용자 지정 컨트롤의 종류
.NET Framework를 사용하여 새 컨트롤을 개발 및 구현할 수 있습니다. 상속을 통해서 기존 컨트롤 및 친숙한 사용자 정의 컨트롤의 기능을 확장할 수 있습니다. 또한 고유한 그리기를 수행하는 사용자 지정 컨트롤을 작성할 수도 있습니다.  
  
 만들 컨트롤 종류를 결정하기 어려울 수 있습니다. 이 항목에서는 상속할 수 있는 다양한 종류의 컨트롤 간의 차이점을 강조하고 프로젝트에 대한 특정 종류의 컨트롤을 선택하는 방법에 대한 정보를 제공합니다.  
  
> [!NOTE]
> Web Forms에서 사용할 컨트롤 작성에 대한 자세한 내용은 [사용자 지정 ASP.NET 서버 컨트롤 개발](https://docs.microsoft.com/previous-versions/aspnet/zt27tfhy(v=vs.100))을 참조하세요.  
  
## <a name="base-control-class"></a>기본 컨트롤 클래스  
 <xref:System.Windows.Forms.Control> 클래스는 Windows Forms 컨트롤의 기본 클래스입니다. Windows Forms 애플리케이션에서 시각적 개체 표시에 필요한 인프라를 제공합니다.  
  
 클래스 <xref:System.Windows.Forms.Control> 는 다음 작업을 수행 하 여 Windows Forms 응용 프로그램에서 시각적 표시를 제공 합니다.  
  
- 창 핸들을 노출합니다.  
  
- 메시지 라우팅을 관리합니다.  
  
- 마우스 및 키보드 이벤트 및 다른 많은 사용자 인터페이스 이벤트를 제공합니다.  
  
- 고급 레이아웃 기능을 제공합니다.  
  
- <xref:System.Windows.Forms.Control.ForeColor%2A>에는 <xref:System.Windows.Forms.Control.BackColor%2A> ,,<xref:System.Windows.Forms.Control.Width%2A>, 등의 시각적 표시와 관련 된 많은 속성이 있습니다. <xref:System.Windows.Forms.Control.Height%2A>  
  
- Microsoft® ActiveX® 컨트롤 역할을 하는 Windows Forms 컨트롤에 필요한 보안 및 스레딩 지원을 제공합니다.  
  
 인프라의 상당 부분이 기본 클래스에서 제공되므로 비교적 쉽게 사용자 고유의 Windows Forms 컨트롤을 개발할 수 있습니다.  
  
## <a name="kinds-of-controls"></a>컨트롤의 종류  
 Windows Forms에서는 *복합*, *확장된* 및 *사용자 지정*으로 세 가지 종류의 사용자 정의 컨트롤을 지원합니다. 다음 섹션에서는 각 종류의 컨트롤을 설명하고 프로젝트에서 사용할 종류를 선택하기 위한 권장 사항을 제공합니다.  
  
### <a name="composite-controls"></a>복합 컨트롤  
 복합 컨트롤은 공용 컨테이너로 캡슐화된 Windows Forms 컨트롤의 컬렉션입니다. 이러한 종류의 컨트롤은 *사용자 정의 컨트롤*이라고도 합니다. 포함된 컨트롤은 *구성 요소 컨트롤*이라고 합니다.  
  
 복합 컨트롤은 포함된 각 Windows Forms 컨트롤과 연결된 고유 기능을 모두 포함하며 해당 속성을 선택적으로 노출하고 바인딩할 수 있게 해줍니다. 또한 복합 컨트롤은 사용자의 추가 개발 작업 없이 기능을 처리하는 다량의 기본 키보드를 제공합니다.  
  
 예를 들어 데이터베이스의 고객 주소 데이터를 표시하기 위해 복합 컨트롤을 빌드할 수 있습니다. 이 컨트롤에는 데이터베이스 <xref:System.Windows.Forms.DataGridView> 필드 <xref:System.Windows.Forms.BindingSource> 를 표시 하는 컨트롤, <xref:System.Windows.Forms.BindingNavigator> 데이터 소스에 대 한 바인딩을 처리 하기 위한 컨트롤 및 레코드 간을 이동 하는 컨트롤이 포함 될 수 있습니다. 데이터 바인딩 속성을 선택적으로 노출할 수 있으며, 애플리케이션 간에 전체 컨트롤을 패키징하고 다시 사용할 수 있습니다. 이러한 종류의 복합 컨트롤에 대 한 예제를 보려면 [방법: Windows Forms 컨트롤](how-to-apply-attributes-in-windows-forms-controls.md)에 특성을 적용 합니다.  
  
 복합 컨트롤을 작성 하려면 <xref:System.Windows.Forms.UserControl> 클래스에서 파생 합니다. 기본 <xref:System.Windows.Forms.UserControl> 클래스는 자식 컨트롤에 대 한 키보드 라우팅을 제공 하 고 자식 컨트롤이 그룹으로 작동할 수 있도록 합니다. 자세한 내용은 [Windows Forms 복합 컨트롤 개발](developing-a-composite-windows-forms-control.md)을 참조하세요.  
  
 **권장 사항**  
  
 다음과 같은 경우 <xref:System.Windows.Forms.UserControl> 클래스에서 상속합니다.  
  
- 여러 Windows Forms 컨트롤의 기능을 다시 사용 가능한 단일 단위로 결합하려는 경우  
  
### <a name="extended-controls"></a>확장된 컨트롤  
 기존 Windows Forms 컨트롤에서 상속된 컨트롤을 파생시킬 수 있습니다. 이 접근 방식을 통해 Windows Forms 컨트롤의 고유 기능을 모두 유지한 다음 사용자 지정 속성, 메서드 또는 다른 기능을 추가하여 해당 기능을 확장할 수 있습니다. 이 옵션을 사용하여 기본 컨트롤의 그리기 논리를 재정의한 다음 모양을 변경하여 해당 사용자 인터페이스를 확장할 수 있습니다.  
  
 예를 들어 사용자가 클릭 한 횟수를 추적 하 <xref:System.Windows.Forms.Button> 는 컨트롤에서 파생 된 컨트롤을 만들 수 있습니다.  
  
 일부 컨트롤에서는 기본 클래스의 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 재정의 하 여 컨트롤의 그래픽 사용자 인터페이스에 사용자 지정 모양을 추가할 수도 있습니다. 클릭을 추적 하는 확장 된 단추의 경우 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 재정의 하 여의 <xref:System.Windows.Forms.Control.OnPaint%2A>기본 구현을 호출한 다음 <xref:System.Windows.Forms.Button> 컨트롤의 클라이언트 영역 한쪽 모퉁이에 클릭 횟수를 그릴 수 있습니다.  
  
 **권장 사항**  
  
 다음과 같은 경우 Windows Forms 컨트롤에서 상속합니다.  
  
- 필요한 기능이 대부분 기존 Windows Forms 컨트롤에 이미 있는 것과 동일한 경우  
  
- 사용자 지정 그래픽 사용자 인터페이스가 필요하지 않거나 기존 컨트롤에 대한 새 그래픽 사용자 인터페이스를 디자인하려는 경우  
  
### <a name="custom-controls"></a>사용자 지정 컨트롤  
 컨트롤을 만드는 또 다른 방법은에서를 <xref:System.Windows.Forms.Control>상속 하 여 처음부터 크게 만드는 것입니다. 클래스 <xref:System.Windows.Forms.Control> 는 마우스 및 키보드 처리 이벤트를 비롯 하 여 컨트롤에 필요한 모든 기본 기능을 제공 하지만 컨트롤별 기능이 나 그래픽 인터페이스는 제공 하지 않습니다.  
  
 <xref:System.Windows.Forms.Control> 클래스에서 상속 하 여 컨트롤을 만들려면 또는 기존 Windows Forms 컨트롤에서 <xref:System.Windows.Forms.UserControl> 상속 하는 것 보다 훨씬 더 많은 생각과 노력이 필요 합니다. 많은 구현이 남아 있으므로 사용자의 컨트롤은 복합 또는 확장된 컨트롤보다 더 큰 유연성을 가질 수 있으며 정확한 요구에 맞게 컨트롤을 만들 수 있습니다.  
  
 사용자 지정 컨트롤을 구현 하려면 필요한 기능별 코드 뿐만 아니라 컨트롤 <xref:System.Windows.Forms.Control.OnPaint%2A> 의 이벤트에 대 한 코드를 작성 해야 합니다. 메서드를 <xref:System.Windows.Forms.Control.WndProc%2A> 재정의 하 고 windows 메시지를 직접 처리할 수도 있습니다. 이는 컨트롤을 만드는 가장 강력한 방법이지만 이 기술을 효과적으로 사용하려면 Microsoft Win32® API에 대해 잘 알고 있어야 합니다.  
  
 사용자 지정 컨트롤의 예로 아날로그 시계의 모양과 동작을 복제하는 시계 컨트롤이 있습니다. 사용자 지정 그리기를 호출 하면 시계 바늘이 내부 <xref:System.Windows.Forms.Timer.Tick> <xref:System.Windows.Forms.Timer> 구성 요소의 이벤트에 대 한 응답으로 이동 합니다. 자세한 내용은 [방법: 간단한 Windows Forms 컨트롤](how-to-develop-a-simple-windows-forms-control.md)을 개발 합니다.  
  
 **권장 사항**  
  
 다음과 같은 경우 <xref:System.Windows.Forms.Control> 클래스에서 상속합니다.  
  
- 컨트롤의 사용자 지정 그래픽 표현을 제공하려는 경우  
  
- 표준 컨트롤을 통해 사용할 수 없는 사용자 지정 기능을 구현해야 하는 경우  
  
### <a name="activex-controls"></a>ActiveX 컨트롤  
 Windows Forms 인프라는 Windows Forms 컨트롤을 호스팅하도록 최적화되어 있지만 ActiveX 컨트롤을 사용할 수도 있습니다. Visual Studio에서는 이 작업이 지원됩니다. 자세한 내용은 [방법: ActiveX 컨트롤을 Windows Forms](how-to-add-activex-controls-to-windows-forms.md)에 추가 합니다.  
  
### <a name="windowless-controls"></a>창 없는 컨트롤  
 Microsoft Visual Basic® 6.0 및 ActiveX 기술은 *창 없는* 컨트롤을 지원합니다. 창 없는 컨트롤은 Windows Forms에서 지원되지 않습니다.  
  
## <a name="custom-design-experience"></a>사용자 지정 디자인 환경  
 사용자 지정 디자인 타임 환경을 구현해야 할 경우 디자이너를 직접 작성할 수 있습니다. 복합 컨트롤의 경우 <xref:System.Windows.Forms.Design.ParentControlDesigner> <xref:System.Windows.Forms.Design.DocumentDesigner> 또는 클래스에서 사용자 지정 디자이너 클래스를 파생 시킵니다. 확장 및 사용자 지정 컨트롤의 경우 <xref:System.Windows.Forms.Design.ControlDesigner> 클래스에서 사용자 지정 디자이너 클래스를 파생 시킵니다.  
  
 를 <xref:System.ComponentModel.DesignerAttribute> 사용 하 여 디자이너와 컨트롤을 연결 합니다. 자세한 내용은 [디자인 타임 지원 확장](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120)) 및 [방법: 디자인 타임 기능](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))을 활용 하는 Windows Forms 컨트롤을 만듭니다.  
  
## <a name="see-also"></a>참고자료

- [.NET Framework에서 사용자 지정 Windows Forms 컨트롤 개발](developing-custom-windows-forms-controls.md)
- [방법: 간단한 Windows Forms 컨트롤 개발](how-to-develop-a-simple-windows-forms-control.md)
- [합성 Windows Forms 컨트롤 개발](developing-a-composite-windows-forms-control.md)
- [디자인 타임 지원 확장](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [방법: 디자인 타임 기능을 활용 하는 Windows Forms 컨트롤 만들기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))
