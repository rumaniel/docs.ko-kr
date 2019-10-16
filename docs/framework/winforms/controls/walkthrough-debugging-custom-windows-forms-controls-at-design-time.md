---
title: '연습: 디자인 타임에 사용자 지정 Windows Forms 컨트롤 디버깅'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- custom controls [Windows Forms], walkthroughs
- visual editors
- debugging [Visual Studio], Windows Forms
- custom controls [Windows Forms], debugging
- designers
- controls [Windows Forms], debugging
- walkthroughs [Windows Forms], debugging
- design-time debugging
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 824d8a7de8e9e37899cb84d6cee9621f84a5bc65
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015692"
---
# <a name="walkthrough-debug-custom-windows-forms-controls-at-design-time"></a>연습: 디자인 타임에 사용자 지정 Windows Forms 컨트롤 디버그

사용자 지정 컨트롤을 만들 때 디자인 타임 동작을 디버깅 해야 하는 경우가 종종 있습니다. 이는 사용자 지정 컨트롤에 대 한 사용자 지정 디자이너를 제작 하는 경우 특히 그렇습니다. 자세한 [내용은 연습: Visual Studio 디자인 타임 기능](creating-a-wf-control-design-time-features.md)을 활용 하는 Windows Forms 컨트롤 만들기

다른 .NET Framework 클래스를 디버그 하는 것 처럼 Visual Studio를 사용 하 여 사용자 지정 컨트롤을 디버그할 수 있습니다. 차이점은 사용자 지정 컨트롤의 코드를 실행 하는 Visual Studio의 개별 인스턴스를 디버깅할 것입니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

첫 번째 단계에서는 애플리케이션 프로젝트를 만듭니다. 이 프로젝트를 사용 하 여 사용자 지정 컨트롤을 호스트 하는 응용 프로그램을 빌드합니다.

Visual Studio에서 Windows 응용 프로그램 프로젝트를 만들고 이름을 **DebuggingExample**로 표시 합니다.

## <a name="create-the-control-library-project"></a>컨트롤 라이브러리 프로젝트 만들기

1. **Windows 컨트롤 라이브러리** 프로젝트를 솔루션에 추가 합니다.

2. DebugControlLibrary 프로젝트에 새 **UserControl** 항목을 추가 합니다. **Debugcontrol**로 이름을로 합니다.

3. **솔루션 탐색기**에서 기본 이름이 UserControl1 인 코드 파일을 삭제 하 여 프로젝트의 기본 컨트롤을 삭제 합니다.

4. 솔루션을 빌드합니다.

## <a name="checkpoint"></a>검사점

이 시점에서 **도구 상자**에 사용자 지정 컨트롤을 볼 수 있습니다.

진행 상황을 확인 하려면 **Debugcontrollibrary 구성 요소** 라는 새 탭을 찾고 클릭 하 여 선택 합니다. 열리면 컨트롤이 표시 되 고 기본 아이콘 옆에는 **Debugcontrol** 이 표시 됩니다.

## <a name="add-a-property-to-your-custom-control"></a>사용자 지정 컨트롤에 속성 추가

디자인 타임에 사용자 지정 컨트롤의 코드가 실행 되 고 있음을 보여 주기 위해 속성을 추가 하 고 속성을 구현 하는 코드에서 중단점을 설정 합니다.

1. **코드 편집기**에서 **debugcontrol** 을 엽니다. 클래스 정의에 다음 코드를 추가 합니다.

    ```vb
    Private demoStringValue As String = Nothing
    <BrowsableAttribute(true)>
    Public Property DemoString() As String

        Get
            Return Me.demoStringValue
        End Get

        Set(ByVal value As String)
            Me.demoStringValue = value
        End Set

    End Property
    ```

    ```csharp
    private string demoStringValue = null;
    [Browsable(true)]
    public string DemoString
    {
        get
        {
            return this.demoStringValue;
        }
        set
        {
            demoStringValue = value;
        }
    }
    ```

2. 솔루션을 빌드합니다.

## <a name="add-your-custom-control-to-the-host-form"></a>호스트 폼에 사용자 지정 컨트롤 추가

사용자 지정 컨트롤의 디자인 타임 동작을 디버깅 하려면 호스트 폼에 사용자 지정 컨트롤 클래스의 인스턴스를 추가 합니다.

1. "DebuggingExample" 프로젝트의 **Windows Forms 디자이너**에서 Form1을 엽니다.

2. **도구 상자**에서 **Debugcontrollibrary 구성 요소** 탭을 열고 **debugcontrol** 인스턴스를 폼으로 끌어다 놓습니다.

3. 속성 창 `DemoString` 에서 사용자 지정 속성 을 찾습니다. 다른 속성과 같이 값을 변경할 수 있습니다. 또한 `DemoString` 속성을 선택 하면 속성의 설명 문자열이 **속성** 창의 맨 아래에 나타납니다.

## <a name="set-up-the-project-for-design-time-debugging"></a>디자인 타임 디버깅을 위한 프로젝트 설정

사용자 지정 컨트롤의 디자인 타임 동작을 디버깅 하려면 사용자 지정 컨트롤의 코드를 실행 하는 Visual Studio의 개별 인스턴스를 디버깅 합니다.

1. **솔루션 탐색기** 에서 **debugcontrollibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

2. **Debugcontrollibrary** 속성 시트에서 **디버그** 탭을 선택 합니다.

     **시작 작업** 섹션에서 **시작 외부 프로그램**을 선택 합니다. Visual studio의 개별 인스턴스를 디버깅 하 게 되므로 visual studio IDE를 찾아보려면 줄임표![(visual studio](./media/visual-studio-ellipsis-button.png)속성 창의 줄임표 단추 (...)) 단추를 클릭 합니다. 실행 파일의 이름은 **devenv.exe입니다.** 를 기본 위치에 설치한 경우 해당 경로는 *% ProgramFiles (x86)% \ Microsoft Visual Studio\2019\\\<edition > \Common7\IDE*입니다.

3. **확인**을 선택하여 대화 상자를 닫습니다.

4. **Debugcontrollibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **시작 프로젝트로 설정** 을 선택 하 여이 디버깅 구성을 사용 하도록 설정 합니다.

## <a name="debug-your-custom-control-at-design-time"></a>디자인 타임에 사용자 지정 컨트롤 디버그

이제 디자인 모드에서 실행 되는 사용자 지정 컨트롤을 디버그할 준비가 되었습니다. 디버깅 세션을 시작 하면 Visual Studio의 새 인스턴스가 생성 되 고이를 사용 하 여 "DebuggingExample" 솔루션을 로드 합니다. **폼 디자이너**에서 Form1을 열면 사용자 지정 컨트롤의 인스턴스가 만들어지고 실행이 시작 됩니다.

1. **코드 편집기** 에서 `Set` **debugcontrol** 원본 파일을 열고 `DemoString` 속성의 접근자에 중단점을 추가 합니다.

2. **F5** 키를 눌러 디버깅 세션을 시작 합니다. Visual Studio의 새 인스턴스가 만들어집니다. 두 가지 방법으로 인스턴스를 구분할 수 있습니다.

    - 디버깅 인스턴스의 제목 표시줄에는 **실행 중인** 단어가 있습니다.

    - 디버깅 인스턴스의 **디버그** 도구 모음에 있는 **시작** 단추를 사용할 수 없습니다.

   중단점은 디버깅 인스턴스에 설정 됩니다.

3. Visual Studio의 새 인스턴스에서 "DebuggingExample" 솔루션을 엽니다. **파일** 메뉴에서 **최근 프로젝트** 를 선택 하 여 솔루션을 쉽게 찾을 수 있습니다. "DebuggingExample" 솔루션 파일이 가장 최근에 사용 된 파일로 나열 됩니다.

4. **폼 디자이너** 에서 Form1을 열고 **debugcontrol** 컨트롤을 선택 합니다.

5. `DemoString` 속성 값을 변경합니다. 변경 내용을 커밋하는 경우 Visual Studio의 디버깅 인스턴스는 포커스를 획득 하 고 중단점에서 실행을 중지 합니다. 다른 코드와 마찬가지로 속성 접근자를 한 단계씩 실행 할 수 있습니다.

6. 디버깅을 중지 하려면 Visual Studio의 호스팅된 인스턴스를 종료 하거나 디버깅 인스턴스에서 **디버깅 중지** 단추를 선택 합니다.

## <a name="next-steps"></a>다음 단계

이제 디자인 타임에 사용자 지정 컨트롤을 디버그할 수 있으므로 Visual Studio IDE와의 상호 작용을 확장 하는 여러 가지 가능성이 있습니다.

- 클래스의 속성<xref:System.ComponentModel.Component.DesignMode%2A> 을 사용 하 여 디자인 타임에만 실행 되는 코드를 작성할 수 있습니다. <xref:System.ComponentModel.Component> 자세한 내용은 <xref:System.ComponentModel.Component.DesignMode%2A>를 참조하세요.

- 사용자 지정 컨트롤의 속성에 적용 하 여 디자이너와의 사용자 지정 컨트롤의 상호 작용을 조작할 수 있는 몇 가지 특성이 있습니다. 이러한 특성은 <xref:System.ComponentModel?displayProperty=nameWithType> 네임 스페이스에서 찾을 수 있습니다.

- 사용자 지정 컨트롤에 대 한 사용자 지정 디자이너를 작성할 수 있습니다. 이를 통해 Visual Studio에서 제공 하는 확장 가능한 디자이너 인프라를 사용 하 여 디자인 환경을 완벽 하 게 제어할 수 있습니다. 자세한 [내용은 연습: Visual Studio 디자인 타임 기능](creating-a-wf-control-design-time-features.md)을 활용 하는 Windows Forms 컨트롤 만들기

## <a name="see-also"></a>참고자료

- [연습: Visual Studio 디자인 타임 기능을 활용 하는 Windows Forms 컨트롤 만들기](creating-a-wf-control-design-time-features.md)
