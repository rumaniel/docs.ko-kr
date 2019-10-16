---
title: 컨트롤 형식 권장 사항
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- user controls [Windows Forms], when to use
- custom controls [Windows Forms], types
- controls [Windows Forms], creating
ms.assetid: 5235fe9d-c36a-4c08-ae76-6cb90b50085e
ms.openlocfilehash: fba10de27f7ba6f4c799d2110acd87394b7dbc95
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015994"
---
# <a name="control-type-recommendations"></a>컨트롤 형식 권장 사항

.NET Framework는 새 컨트롤을 개발 및 구현하는 기능을 제공합니다. 익숙한 사용자 정의 컨트롤뿐 아니라 이제 고유한 그리기를 수행하는 사용자 지정 컨트롤을 작성할 수 있으며 상속을 통해 기존 컨트롤의 기능을 확장할 수도 있습니다. 만들 컨트롤 형식을 결정하기 어려울 수 있습니다. 이 섹션에서는 상속할 수 있는 다양한 컨트롤 형식 간의 차이점을 요약하고 프로젝트에 대해 선택할 형식과 관련된 고려 사항을 제공합니다.

> [!NOTE]
> Web Forms에서 사용할 컨트롤을 작성하려는 경우 [사용자 지정 ASP.NET 서버 컨트롤 개발](https://docs.microsoft.com/previous-versions/aspnet/zt27tfhy(v=vs.100))을 참조하세요.

## <a name="inheriting-from-a-windows-forms-control"></a>Windows Forms 컨트롤에서 상속

기존 Windows Forms 컨트롤에서 상속된 컨트롤을 파생시킬 수 있습니다. 이 접근 방식을 통해 Windows Forms 컨트롤의 고유 기능을 모두 유지하는 동시에 사용자 지정 속성, 메서드 또는 다른 기능을 추가하여 해당 기능을 확장할 수 있습니다. 예를 들어 숫자만 입력할 수 있고 자동으로 입력을 값으로 변환하는 <xref:System.Windows.Forms.TextBox>에서 파생된 컨트롤을 만들 수 있습니다. 이러한 컨트롤에는 텍스트 상자의 텍스트가 변경될 때마다 호출된 유효성 검사 코드가 포함될 수 있으며 추가 속성인 값이 있을 수 있습니다. 일부 컨트롤에서는 기본 클래스의 <xref:System.Windows.Forms.Control.OnPaint%2A> 메서드를 재정의하여 컨트롤의 그래픽 인터페이스에 사용자 지정 모양을 추가할 수도 있습니다.

 다음과 같은 경우 Windows Forms 컨트롤에서 상속합니다.

- 필요한 기능이 대부분 기존 Windows Forms 컨트롤에 이미 있는 것과 동일한 경우

- 사용자 지정 그래픽 인터페이스가 필요하지 않거나 기존 컨트롤에 대한 새 그래픽 프런트 엔드를 디자인하려는 경우

## <a name="inheriting-from-the-usercontrol-class"></a>UserControl 클래스에서 상속

사용자 정의 컨트롤은 공용 컨테이너로 캡슐화된 Windows Forms 컨트롤 컬렉션입니다. 컨테이너는 각 Windows Forms 컨트롤과 연결된 고유 기능을 모두 포함하며 해당 속성을 선택적으로 노출하고 바인딩할 수 있게 해줍니다. 사용자 정의 컨트롤의 예로 데이터베이스의 고객 주소 데이터를 표시하기 위해 빌드된 컨트롤을 들 수 있습니다. 이 컨트롤은 각 필드를 표시할 여러 개의 텍스트 상자와 레코드를 탐색하는 단추 컨트롤을 포함합니다. 데이터 바인딩 속성을 선택적으로 노출할 수 있으며, 전체 컨트롤을 패키징하고 애플리케이션 간에 다시 사용할 수 있습니다.

다음과 같은 경우 <xref:System.Windows.Forms.UserControl> 클래스에서 상속합니다.

- 여러 Windows Forms 컨트롤의 기능을 다시 사용 가능한 단일 단위로 결합하려는 경우

## <a name="inheriting-from-the-control-class"></a>Control 클래스에서 상속

컨트롤을 만드는 또 다른 방법은 <xref:System.Windows.Forms.Control>에서 상속하여 처음부터 새로 만드는 것입니다. <xref:System.Windows.Forms.Control> 클래스는 컨트롤에 필요한 기본 기능(예: 이벤트)을 모두 제공하지만 컨트롤별 기능이나 그래픽 인터페이스는 제공하지 않습니다. <xref:System.Windows.Forms.Control> 클래스에서 상속하여 컨트롤을 만들려면 사용자 정의 컨트롤 또는 기존 Windows Forms 컨트롤에서 상속하는 것보다 훨씬 더 많은 노력과 사고가 필요합니다. 작성자는 컨트롤의 <xref:System.Windows.Forms.Control.OnPaint%2A> 이벤트에 대한 코드 및 필요한 기능별 코드를 작성해야 합니다. 그러나 허용되는 유연성이 더 크며, 정확한 요구에 맞게 컨트롤을 사용자 지정할 수 있습니다. 사용자 지정 컨트롤의 예로 아날로그 시계의 모양과 동작을 복제하는 시계 컨트롤이 있습니다. 사용자 지정 그리기를 호출하면 시계 바늘이 내부 타이머 구성 요소의 <xref:System.Windows.Forms.Timer.Tick> 이벤트에 대한 응답으로 움직입니다.

다음과 같은 경우 <xref:System.Windows.Forms.Control> 클래스에서 상속합니다.

- 컨트롤의 사용자 지정 그래픽 표현을 제공하려는 경우

- 표준 컨트롤을 통해 사용할 수 없는 사용자 지정 기능을 구현해야 하는 경우

## <a name="related-articles"></a>관련 문서

- [방법: 도구 상자 항목 선택 대화 상자에 컨트롤 표시](how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)

- [연습: DesignerSerializationVisibilityAttribute를 사용 하 여 표준 형식의 컬렉션 serialize](serializing-collections-designerserializationvisibilityattribute.md)

- [연습: Windows Forms 컨트롤에서 상속](walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)

- [방법: 컨트롤에 대 한 도구 상자 비트맵 제공](how-to-provide-a-toolbox-bitmap-for-a-control.md)

- [방법: 기존 Windows Forms 컨트롤에서 상속](how-to-inherit-from-existing-windows-forms-controls.md)

- [연습: 디자인 타임에 사용자 지정 Windows Forms 컨트롤 디버그](walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)

- [방법: Control 클래스에서 상속](how-to-inherit-from-the-control-class.md)

- [방법: UserControl의 런타임 동작 테스트](how-to-test-the-run-time-behavior-of-a-usercontrol.md)

- [방법: 디자인 타임에 컨트롤을 폼의 가장자리에 맞춤](how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)

- [방법: UserControl 클래스에서 상속](how-to-inherit-from-the-usercontrol-class.md)

- [방법: Windows Forms에 대 한 Author 컨트롤](how-to-author-controls-for-windows-forms.md)

- [방법: 복합 컨트롤 작성](how-to-author-composite-controls.md)

- [연습: 복합 컨트롤 작성](walkthrough-authoring-a-composite-control-with-visual-csharp.md)

- [연습: Visual Studio 디자인 타임 기능을 활용 하는 Windows Forms 컨트롤 만들기](creating-a-wf-control-design-time-features.md)

- [방법: 디자인 타임 기능을 활용 하는 Windows Forms 컨트롤 만들기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))

## <a name="see-also"></a>참고자료

- [방법: 간단한 Windows Forms 컨트롤 개발](how-to-develop-a-simple-windows-forms-control.md)
- [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)
