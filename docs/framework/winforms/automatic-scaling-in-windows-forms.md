---
title: Windows Forms의 자동 크기 조정
ms.date: 06/15/2017
helpviewer_keywords:
- scalability [Windows Forms], automatic in Windows Forms
- Windows Forms, automatic scaling
ms.assetid: 68fad25b-afbc-44bd-8e1b-966fc43507a4
ms.openlocfilehash: f8afece073076b9ae94faaba8477f2a13e11b295
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268092"
---
# <a name="automatic-scaling-in-windows-forms"></a>Windows Forms의 자동 크기 조정

자동 크기 조정은 한 컴퓨터에서 특정 디스플레이 해상도 또는 시스템 글꼴로 디자인된 폼과 해당 컨트롤이 다른 디스플레이 해상도 또는 시스템 글꼴을 사용하는 다른 컴퓨터에서 제대로 표시될 수 있게 합니다. 이 기능은 사용자 및 다른 개발자 컴퓨터 둘 다의 네이티브 Windows 및 기타 애플리케이션과 일치하도록 폼과 해당 컨트롤의 크기가 지능적으로 조정되도록 합니다. 자동 크기 조정 및 비주얼 스타일에 대 한.NET Framework의 지원을 통해 일관 된 모양과 느낌을 각 사용자의 컴퓨터에서 네이티브 Windows 응용 프로그램에 비해 유지 하기 위해.NET Framework 응용 프로그램을 수 있습니다.

대부분의 경우 2.0 이상으로 자동 크기 조정 작동 하는.NET Framework 버전에 필요합니다. 그러나 글꼴 구성표 변경은 문제가 될 수 있습니다. 이 문제를 해결 하는 방법의 예제를 참조 하세요. [방법: Windows Forms 응용 프로그램에서 글꼴 구성표 변경에 응답](how-to-respond-to-font-scheme-changes-in-a-windows-forms-application.md)합니다.

## <a name="need-for-automatic-scaling"></a>자동 크기 조정 요구

자동 크기 조정이 없으면 특정 디스플레이 해상도 또는 글꼴로 디자인된 애플리케이션이 해당 해상도나 글꼴이 변경될 경우 너무 작거나 너무 크게 나타납니다. 예를 들어 애플리케이션이 Tahoma 9 포인트를 기준으로 디자인된 경우 조정하지 않으면 시스템 글꼴이 Tahoma 12 포인트인 컴퓨터에서 실행할 경우 너무 작게 나타납니다. 제목, 메뉴, 텍스트 상자 내용 등의 텍스트 요소가 다른 애플리케이션보다 작게 렌더링됩니다. 또한 제목 표시줄, 메뉴, 많은 컨트롤 등 텍스트가 포함된 UI(사용자 인터페이스) 요소의 크기는 사용하는 글꼴에 따라 달라집니다. 이 예제에서는 이러한 요소도 상대적으로 더 작게 나타납니다.

애플리케이션이 특정 디스플레이 해상도로 디자인된 경우 비슷한 상황이 발생합니다. 가장 일반적인 디스플레이 해상도 96dpi DPI (인치당), 100%는 디스플레이 배율을 같음는 있지만 125%, 150%, 200%를 지 원하는 더 높은 해상도 표시 (각각 같으면는 120, 144 및 192DPI) 위에 더욱 더 보편화 되 고 합니다. 조정하지 않으면 특정 해상도로 디자인된 애플리케이션, 특히 그래픽 기반 애플리케이션은 다른 해상도로 실행할 경우 너무 크거나 너무 작게 나타납니다.

자동 크기 조정은 상대 글꼴 크기나 디스플레이 해상도에 따라 폼과 해당 자식 컨트롤의 크기를 자동으로 조정하여 이러한 문제를 개선하려고 합니다. Windows 운영 체제는 대화 상자 단위라는 상대 측정 단위를 사용하여 대화 상자의 자동 크기 조정을 지원합니다. 대화 상자 단위는 시스템 글꼴을 기반으로 하며, Win32 SDK 함수 `GetDialogBaseUnits`를 통해 픽셀과의 해당 관계를 확인할 수 있습니다. 사용자가 Windows에서 사용되는 테마를 변경하면 모든 대화 상자가 자동으로 적절하게 조정됩니다. 또한.NET Framework 기본 시스템 글꼴 또는 디스플레이 해상도 따라 자동 크기 조정을 지원 합니다. 필요에 따라 애플리케이션에서 자동 크기 조정을 사용하지 않도록 설정할 수 있습니다.

## <a name="original-support-for-automatic-scaling"></a>자동 크기 조정에 대 한 원래 지원

버전 1.0 및 1.1 지원 되는.NET Framework 자동 크기 조정 Win32 SDK 값으로 표시 되는 UI에 사용 된 Windows 기본 글꼴에 종속 된 어렵지는 **DEFAULT_GUI_FONT**합니다. 이 글꼴은 일반적으로 디스플레이 해상도가 변경되는 경우에만 변경됩니다. 자동 크기 조정을 구현하기 위해 다음 메커니즘이 사용되었습니다.

1. 디자인 타임에 <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> 속성(이제 사용 되지 않음)이 개발자 컴퓨터의 기본 시스템 글꼴 높이와 너비로 설정되었습니다.

2. 런타임에 사용자 컴퓨터의 기본 시스템 글꼴이 <xref:System.Windows.Forms.Form> 클래스의 <xref:System.Windows.Forms.Control.Font%2A> 속성을 초기화하는 데 사용되었습니다.

3. 폼을 표시하기 전에 <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> 메서드가 폼의 크기 조정을 위해 호출되었습니다. 이 메서드는 <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> 및 <xref:System.Windows.Forms.Control.Font%2A>에서 상대 크기를 계산한 다음 <xref:System.Windows.Forms.Control.Scale%2A> 메서드를 호출하여 실제로 폼과 자식의 크기를 조정했습니다.

4. 후속 <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A> 호출에서 점진적으로 폼의 크기를 조정하지 않도록 <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> 값이 업데이트되었습니다.

이 메커니즘은 대부분의 용도에 충분했지만 다음과 같은 제한 사항이 있었습니다.

- 이후를 <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> 속성 정수 값으로 기준 글꼴 크기를 나타내며, 반올림 오류가 분명 하 게 여러 해상도 양식을 차례로 사용할 때 발생 합니다.

- 자동 크기 조정이 <xref:System.Windows.Forms.Form> 클래스에서만 구현되고 <xref:System.Windows.Forms.ContainerControl> 클래스에서는 구현되지 않았습니다. 따라서 사용자 정의 컨트롤이 폼과 동일한 해상도로 디자인되고 디자인 타임에 폼에 배치된 경우에만 제대로 크기가 조정되었습니다.

- 컴퓨터 해상도가 동일한 경우에만 여러 개발자가 동시에 폼과 해당 자식 컨트롤을 디자인할 수 있었습니다. 마찬가지로, 폼의 상속이 부모 폼과 연결된 해상도에 따라 달라지도록 했습니다.

- 와 같은.NET Framework 버전 2.0에 도입 된 최신 레이아웃 관리자와 호환 되지 않습니다 <xref:System.Windows.Forms.FlowLayoutPanel> 고 <xref:System.Windows.Forms.TableLayoutPanel>입니다.

- .NET Compact Framework에 대 한 호환성에 필요한 디스플레이 해상도 직접 기반 크기 조정을 지원 하지 않았습니다.

이 메커니즘은 이전 버전과 호환성을 유지 하기 위해.NET Framework 버전 2.0 유지 하지만 다음에 설명 하는 보다 강력한 크기 조정 메커니즘으로 대체 되었습니다. 따라서 <xref:System.Windows.Forms.Form.AutoScale%2A>, <xref:System.Windows.Forms.Form.ApplyAutoScaling%2A>, <xref:System.Windows.Forms.Form.AutoScaleBaseSize%2A> 및 특정 <xref:System.Windows.Forms.Control.Scale%2A> 오버로드는 사용되지 않는 것으로 표시됩니다.

> [!NOTE]
> 레거시 코드는.NET Framework 버전 2.0으로 업그레이드할 때 이러한 멤버에 대 한 참조를 안전 하 게 삭제할 수 있습니다.

## <a name="current-support-for-automatic-scaling"></a>자동 크기 조정에 대 한 현재 지원

.NET Framework 버전 2.0은 Windows Forms의 자동 크기 조정에 다음과 같이 변경을 도입 하 여 이전 제한 surmounts:

- 폼, 네이티브 복합 컨트롤 및 사용자 정의 컨트롤이 모두 균일한 크기 조정 지원을 받을 수 있도록 크기 조정에 대한 기본 지원이 <xref:System.Windows.Forms.ContainerControl> 클래스로 이동되었습니다. 새 멤버 <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>, <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 및 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>이 추가되었습니다.

- <xref:System.Windows.Forms.Control> 클래스에는 크기 조정에 참여하고 동일한 폼에서 혼합된 크기 조정을 지원할 수 있게 해주는 여러 개의 새 멤버도 있습니다. 구체적으로 <xref:System.Windows.Forms.Control.Scale%2A>, <xref:System.Windows.Forms.Control.ScaleChildren%2A> 및 <xref:System.Windows.Forms.Control.GetScaledBounds%2A> 멤버가 크기 조정을 지원합니다.

- <xref:System.Windows.Forms.AutoScaleMode> 열거형에서 정의된 시스템 글꼴 지원을 보완하기 위해 화면 해상도를 기반으로 하는 크기 조정 지원이 추가되었습니다. 이 모드는 응용 프로그램을 쉽게 마이그레이션할을 사용 하도록 설정 하는.NET Compact Framework에서 지 원하는 자동 크기 조정과 호환입니다.

- <xref:System.Windows.Forms.FlowLayoutPanel> 및 <xref:System.Windows.Forms.TableLayoutPanel>과 같은 레이아웃 관리자와의 호환성이 자동 크기 조정 구현에 추가되었습니다.

- 이제 배율 인수가 일반적으로 <xref:System.Drawing.SizeF> 구조체를 사용하여 부동 소수점 값으로 표시되므로 반올림 오류가 거의 제거되었습니다.

> [!CAUTION]
> DPI 및 글꼴 크기 조정 모드의 임의 혼합은 지원되지 않습니다. 특정 모드(예: DPI)를 사용하여 사용자 정의 컨트롤의 크기를 조정하고 다른 모드(글꼴)를 사용하여 폼에 배치하는 것은 아무 문제가 없지만 특정 모드의 기본 폼과 다른 모드의 파생 폼을 혼합하면 예기치 않은 결과가 발생할 수 있습니다.

### <a name="automatic-scaling-in-action"></a>작업의 자동 크기 조정

이제 Windows Forms에서 다음 논리를 사용하여 폼과 해당 내용의 크기를 자동으로 조정합니다.

1. 디자인 타임에 각 <xref:System.Windows.Forms.ContainerControl>이 크기 조정 모드와 현재 해상도를 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 및 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>에 각각 기록합니다.

2. 런타임에 실제 해상도가 <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A> 속성에 저장됩니다. <xref:System.Windows.Forms.ContainerControl.AutoScaleFactor%2A> 속성이 런타임 및 디자인 타임 크기 조정 해상도 간의 비율을 동적으로 계산합니다.

3. 폼이 로드될 때 <xref:System.Windows.Forms.ContainerControl.CurrentAutoScaleDimensions%2A> 및 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>의 값이 서로 다르면 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A> 메서드가 호출되어 컨트롤 및 해당 자식의 크기를 조정합니다. 이 메서드는 레이아웃을 일시 중단하고 <xref:System.Windows.Forms.Control.Scale%2A> 메서드를 호출하여 실제 크기 조정을 수행합니다. 그 후에 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> 값이 업데이트되어 점진적 크기 조정을 방지합니다.

4. 다음 상황에서는 <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>도 자동으로 호출됩니다.

    - 크기 조정 모드가 <xref:System.Windows.Forms.AutoScaleMode.Font>인 경우 <xref:System.Windows.Forms.Control.OnFontChanged%2A> 이벤트에 대한 응답으로

    - 컨테이너 컨트롤의 레이아웃이 다시 시작되고 <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A> 또는 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 속성에서 변경 내용이 검색되는 경우

    - 위에서 암시한 대로 부모 <xref:System.Windows.Forms.ContainerControl>의 크기가 조정되는 경우 각 컨테이너 컨트롤은 부모 컨테이너의 배율 인수가 아니라 고유한 배율 인수를 사용하여 자식의 크기를 조정해야 합니다.

5. 자식 컨트롤은 다음과 같은 여러 수단을 통해 해당 크기 조정 동작을 수정할 수 있습니다.

    - <xref:System.Windows.Forms.Control.ScaleChildren%2A> 속성을 재정의하여 해당 자식 컨트롤의 크기를 조정할지 여부를 결정할 수 있습니다.

    - <xref:System.Windows.Forms.Control.GetScaledBounds%2A> 메서드를 재정의하여 컨트롤의 크기가 조정되는 범위를 조정할 수 있지만 크기 조정 논리는 조정할 수 없습니다.

    - <xref:System.Windows.Forms.Control.ScaleControl%2A> 메서드를 재정의하여 현재 컨트롤에 대한 크기 조정 논리를 변경할 수 있습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A>
- <xref:System.Windows.Forms.Control.Scale%2A>
- <xref:System.Windows.Forms.ContainerControl.PerformAutoScale%2A>
- <xref:System.Windows.Forms.ContainerControl.AutoScaleDimensions%2A>
- [비주얼 스타일을 사용하여 컨트롤 렌더링](./controls/rendering-controls-with-visual-styles.md)
- [방법: 자동 크기 조정 없이 성능 향상](./advanced/how-to-improve-performance-by-avoiding-automatic-scaling.md)
