---
title: 컨트롤 및 구성 요소 제작 문제 해결
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- troubleshooting components
- troubleshooting controls [Windows Forms]
- controls [Windows Forms], troubleshooting
- components [Windows Forms], troubleshooting
- Windows Forms controls, debugging
ms.assetid: e9c8c099-2271-4737-882f-50f336c7a55e
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2e0b98107ac5f43c80aad6cb5ea61e6f4e1e28d3
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015708"
---
# <a name="troubleshoot-control-and-component-authoring"></a>컨트롤 및 구성 요소 제작 문제 해결

이 항목에서는 구성 요소 및 컨트롤을 개발할 때 발생 하는 다음과 같은 일반적인 문제를 나열 합니다.

- 도구 상자에 컨트롤을 추가할 수 없습니다.

- Windows Forms 사용자 정의 컨트롤 또는 구성 요소를 디버깅할 수 없습니다.

- 상속된 컨트롤 또는 구성 요소에서 이벤트가 두 번 발생합니다.

- 디자인 타임 오류: "구성 요소 '*구성 요소 이름*'을 만들지 못했습니다."

- STAThreadAttribute

- 도구 상자에 구성 요소 아이콘이 표시되지 않습니다.

## <a name="cannot-add-control-to-toolbox"></a>도구 상자에 컨트롤을 추가할 수 없습니다.

다른 프로젝트에서 만든 사용자 지정 컨트롤 또는 타사 컨트롤을 **도구 상자**에 추가하려는 경우 수동으로 수행해야 합니다. 현재 프로젝트가 컨트롤 또는 구성 요소를 포함하는 경우 **도구 상자**에 자동으로 표시되어야 합니다. 자세한 내용은 [연습: 도구 상자에 사용자 지정 구성 요소](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)를 자동으로 채웁니다.

### <a name="to-add-a-control-to-the-toolbox"></a>도구 상자에 컨트롤을 추가하려면

1. 바로 가기 메뉴에서 **도구 상자**를 마우스 오른쪽 단추로 클릭하고 **항목 선택**을 선택합니다.

2. **도구 상자 항목 선택** 대화 상자에서 구성 요소를 추가합니다.

    - .NET Framework 구성 요소 또는 컨트롤을 추가하려면 **.NET Framework 구성 요소** 탭을 클릭합니다.

         -또는-

    - COM 구성 요소 또는 ActiveX 컨트롤을 추가하려면 **COM 구성 요소** 탭을 클릭합니다.

3. 컨트롤이 대화 상자에 표시되면 선택되었는지 확인한 다음 **확인**을 클릭합니다.

     컨트롤이 **도구 상자**에 추가됩니다.

4. 컨트롤이 대화 상자에 나열되지 않는 경우 다음을 수행합니다.

    1. **찾아보기** 단추를 클릭합니다.

    2. 컨트롤을 포함하는 .dll 파일이 포함된 폴더로 이동합니다.

    3. .dll 파일을 선택하고 **열기**를 클릭합니다.

         컨트롤이 대화 상자에 나타납니다.

    4. 컨트롤이 선택되었는지 확인한 다음 **확인**을 클릭합니다.

         컨트롤이 **도구 상자**에 추가됩니다.

## <a name="cannot-debug-the-windows-forms-user-control-or-component"></a>Windows Forms 사용자 정의 컨트롤 또는 구성 요소를 디버깅할 수 없습니다.

컨트롤이 <xref:System.Windows.Forms.UserControl> 클래스에서 파생 되는 경우 테스트 컨테이너를 사용 하 여 런타임 동작을 디버그할 수 있습니다. 자세한 내용은 [방법: UserControl](how-to-test-the-run-time-behavior-of-a-usercontrol.md)의 런타임 동작을 테스트 합니다.

다른 사용자 지정 컨트롤 및 구성 요소는 독립 실행형 프로젝트가 아닙니다. Windows Forms 프로젝트와 같은 애플리케이션에 의해 호스팅되어야 합니다. 컨트롤 또는 구성 요소를 디버깅하려면 Windows Forms 프로젝트에 추가해야 합니다.

### <a name="to-debug-a-control-or-component"></a>컨트롤 또는 구성 요소를 디버깅하려면

1. **빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 솔루션을 빌드합니다.

2. **파일** 메뉴에서 **추가**, **새 프로젝트**를 차례로 선택하여 응용 프로그램에 테스트 프로젝트를 추가합니다.

3. **새 프로젝트 추가** 대화 상자에서 프로젝트 형식에 **Windows 응용 프로그램**을 선택합니다.

4. **솔루션 탐색기**에서 새 프로젝트에 대한 **참조** 노드를 마우스 오른쪽 단추로 클릭합니다. 바로 가기 메뉴에서 **참조 추가**를 클릭하여 컨트롤 또는 구성 요소를 포함하는 프로젝트에 참조를 추가합니다.

5. 테스트 프로젝트에서 컨트롤 또는 구성 요소의 인스턴스를 만듭니다. 구성 요소가 **도구 상자**에 있는 경우 디자이너 화면으로 끌어 오거나 다음 코드 예제와 같이 프로그래밍 방식으로 인스턴스를 만들 수 있습니다.

    ```vb
    Dim Component1 As New MyNeatComponent()
    ```

    ```csharp
    MyNeatComponent Component1 = new MyNeatComponent();
    ```

   이제 컨트롤 또는 구성 요소를 정상적으로 디버깅할 수 있습니다.

디버깅 하는 방법에 대 한 자세한 내용은 [Visual Studio의 디버깅](/visualstudio/debugger/debugging-in-visual-studio) 및 [연습: 디자인 타임](walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)에 사용자 지정 Windows Forms 컨트롤 디버깅

## <a name="event-is-raised-twice-in-inherited-control-or-component"></a>상속된 컨트롤 또는 구성 요소에서 이벤트가 두 번 발생합니다.

중복된 `Handles` 절 때문일 수 있습니다. 자세한 내용은 [Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)을 참조하세요.

## <a name="design-time-error-failed-to-create-component-component-name"></a>디자인 타임 오류: "구성 요소 ' 구성 요소 이름 '을 만들지 못했습니다."

구성 요소나 컨트롤은 매개 변수가 없는 매개 변수가 없는 생성자를 제공 해야 합니다. 디자인 환경에서 구성 요소 또는 컨트롤의 인스턴스를 만드는 경우 매개 변수를 사용하는 생성자 오버로드에 매개 변수를 제공하려고 하지 않습니다.

## <a name="stathreadattribute"></a>STAThreadAttribute

는 <xref:System.STAThreadAttribute> Windows Forms 단일 스레드 아파트 모델을 사용 하는 CLR (공용 언어 런타임)에 알립니다. Windows Forms 애플리케이션의 `Main` 메서드에 이 특성을 적용하지 않는 경우 의도하지 않은 동작이 발생할 수 있습니다. 예를 들어와 같은 <xref:System.Windows.Forms.ListView>컨트롤에는 배경 이미지가 표시 되지 않을 수 있습니다. 일부 컨트롤은 올바른 자동 완성 및 끌어서 놓기 동작에 대해 이 특성을 요구할 수도 있습니다.

## <a name="component-icon-does-not-appear-in-toolbox"></a>도구 상자에 구성 요소 아이콘이 표시되지 않습니다.

를 사용 <xref:System.Drawing.ToolboxBitmapAttribute> 하 여 사용자 지정 구성 요소와 아이콘을 연결 하는 경우 자동 생성 된 구성 요소에 대 한 도구 상자에 비트맵이 나타나지 않습니다. 비트맵을 보려면 **도구 상자 항목 선택** 대화 상자를 사용하여 컨트롤을 다시 로드합니다. 자세한 내용은 [방법: 컨트롤](how-to-provide-a-toolbox-bitmap-for-a-control.md)에 대 한 도구 상자 비트맵을 제공 합니다.

## <a name="see-also"></a>참고자료

- [디자인 타임에 Windows Forms 컨트롤 개발](developing-windows-forms-controls-at-design-time.md)
- [연습: 사용자 지정 구성 요소를 사용 하 여 도구 상자 자동 채우기](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
- [방법: UserControl의 런타임 동작 테스트](how-to-test-the-run-time-behavior-of-a-usercontrol.md)
- [연습: 디자인 타임에 사용자 지정 Windows Forms 컨트롤 디버그](walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)
