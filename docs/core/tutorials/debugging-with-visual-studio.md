---
title: Visual Studio 2017을 사용하여 Hello World .NET Core 애플리케이션 디버그
description: Visual Studio 2017에서 C# 또는 Visual Basic으로 작성된 Hello World 앱을 디버그하는 방법을 알아봅니다.
ms.date: 12/15/2017
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: 7239ca52c0b90c4cfacd68581f569b9ac7d70eae
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70969386"
---
# <a name="debug-your-c-or-visual-basic-net-core-hello-world-application-using-visual-studio-2017"></a>Visual Studio 2017을 사용하여 C# 또는 Visual Basic .NET Core Hello World 애플리케이션 디버그

지금까지 [Visual Studio 2017에서 .NET Core를 사용하여 C# Hello World 애플리케이션 빌드](with-visual-studio.md) 또는 [Visual Studio 2017에서 .NET Core를 사용하여 Visual Basic Hello World 애플리케이션 빌드](vb-with-visual-studio.md)의 단계에 따라 간단한 콘솔 애플리케이션을 만들고 실행했습니다. 애플리케이션을 작성하고 컴파일했으면 테스트를 시작할 수 있습니다. Visual Studio에는 애플리케이션을 테스트하고 문제를 해결하는 데 사용할 수 있는 포괄적인 디버깅 도구 집합이 포함되어 있습니다. 

## <a name="debugging-in-debug-mode"></a>디버그 모드에서 디버깅

*디버그* 및 *릴리스*는 Visual Studio의 기본 빌드 구성 중 두 개입니다. 현재 빌드 구성은 도구 모음에 표시됩니다. 다음 도구 모음 그림은 Visual Studio가 **디버그** 모드로 애플리케이션을 컴파일하도록 구성되어 있음을 보여 줍니다.

   ![디버그가 강조 표시된 기본 Visual Studio 도구 모음](./media/debugging-with-visual-studio/visual-studio-toolbar-debug.png)

항상 디버그 모드에서 프로그램을 테스트하면서 시작해야 합니다. 디버그 모드는 대부분의 컴파일러 최적화를 끄고 빌드 프로세스 중 보다 다양한 정보를 제공합니다.

## <a name="setting-a-breakpoint"></a>중단점 설정

디버그 모드에서 프로그램을 실행하고 몇 가지 디버깅 기능을 수행합니다.

<!-- markdownlint-disable MD025 -->

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. *중단점*은 중단점이 설정된 줄이 실행되기 *전에* 애플리케이션 실행을 일시적으로 중단합니다. 

   코드 창의 왼쪽 여백에서 `Console.WriteLine($"\nHello, {name}, on {date:d} at {date:t}!");` 줄을 클릭하거나 해당 줄을 선택하고 **디버그** > **중단점 설정/해제** 메뉴 항목을 선택하여 줄에 중단점을 설정합니다. 다음 그림에서 볼 수 있듯이 Visual Studio에서는 중단점이 설정된 줄을 강조 표시하고 왼쪽 여백에 빨간색 원을 표시합니다.

   ![중단점이 설정된 Visual Studio 프로그램 창](./media/debugging-with-visual-studio/set-breakpoint-in-editor.png)

1. 도구 모음에서 녹색 화살표가 있는 **HelloWorld** 단추를 선택하거나 F5 키를 누르거나 **디버그** > **디버깅 시작**을 선택하여 프로그램을 디버그 모드에서 실행합니다.

1. 프로그램 이름을 입력하라는 메시지가 표시되면 콘솔 창에 문자열을 입력하고 Enter 키를 누릅니다.

1. 중단점에 도달할 때와 `Console.WriteLine` 메서드가 실행되기 전에 프로그램 실행이 중지됩니다. **자동** 창에는 현재 줄 주위에서 사용되는 변수 값이 표시됩니다. **지역** 창(**지역** 탭을 클릭하여 볼 수 있음)에는 현재 실행 중인 메서드에 정의된 변수 값이 표시됩니다.

   ![Visual Studio의 중단점 스크린샷](./media/debugging-with-visual-studio/breakpoint-console-window.png)

1. 변수 값을 변경하여 프로그램에 미치는 영향을 확인할 수 있습니다. **직접 실행 창**이 표시되지 않는 경우 **디버그** > **창** > **직접 실행** 메뉴 항목을 선택하여 표시합니다. **직접 실행 창**에서는 디버그하는 애플리케이션을 조작할 수 있습니다.

1. 변수 값을 대화형으로 변경할 수 있습니다. **직접 실행 창**에 `name = "Gracie"`를 입력하고 Enter 키를 누릅니다.

1. **직접 실행 창**에 `date = new DateTime(2016,11,01,11,59,00)`을 입력하고 Enter 키를 누릅니다.

   **직접 실행 창**에는 문자열 변수의 값과 <xref:System.DateTime> 값의 속성이 표시됩니다. 또한 변수 값이 **자동** 및 **지역** 창에서 업데이트됩니다.

   ![자동 창 및 직접 실행 창](./media/debugging-with-visual-studio/autos-immediate-window.png)

1. 도구 모음에서 **계속** 단추를 선택하거나 **디버그** > **계속** 메뉴 항목을 선택하여 프로그램을 계속 실행합니다. 콘솔 창에 표시되는 값은 **직접 실행 창**에서 변경한 값과 일치합니다.

   ![What is your name? 프롬프트에 값 Jack과 Hello Gracie를 차례로 표시하는 콘솔 창](./media/debugging-with-visual-studio/debug-changed-value.png)

1. 아무 키나 눌러 애플리케이션을 끝내고 디버그 모드를 종료합니다.

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. *중단점*은 중단점이 설정된 줄이 실행되기 *전에* 애플리케이션 실행을 일시적으로 중단합니다. 

   코드 창의 왼쪽 여백에서 `Console.WriteLine(vbCrLf + $"Hello, {name}, on {currentDate:d} at {currentDate:t}!")` 줄을 클릭하거나 해당 줄을 선택하고 **디버그** > **중단점 설정/해제** 메뉴 항목을 선택하여 줄에 중단점을 설정합니다. 다음 그림에서 볼 수 있듯이 Visual Studio에서는 중단점이 설정된 줄을 강조 표시하고 왼쪽 여백에 빨간색 원을 표시합니다.

   ![중단점이 설정된 Visual Studio 프로그램 창](./media/debugging-with-visual-studio/vb-set-breakpoint-in-editor.png)

1. 도구 모음에서 녹색 화살표가 있는 **HelloWorld** 단추를 선택하거나 F5 키를 누르거나 **디버그** > **디버깅 시작**을 선택하여 프로그램을 디버그 모드에서 실행합니다.

1. 프로그램 이름을 입력하라는 메시지가 표시되면 콘솔 창에 문자열을 입력하고 Enter 키를 누릅니다.

1. 중단점에 도달할 때와 `Console.WriteLine` 메서드가 실행되기 전에 프로그램 실행이 중지됩니다. **자동** 창에는 현재 줄 주위에서 사용되는 변수 값이 표시됩니다. **지역** 창(**지역** 탭을 클릭하여 볼 수 있음)에는 현재 실행 중인 메서드에 정의된 변수 값이 표시됩니다.

   ![중단점에서 Visual Studio 애플리케이션 창](./media/debugging-with-visual-studio/vb-stop-at-breakpoint.png)

1. 변수 값을 변경하여 프로그램에 미치는 영향을 확인할 수 있습니다. **직접 실행 창**이 표시되지 않는 경우 **디버그** > **창** > **직접 실행** 메뉴 항목을 선택하여 표시합니다. **직접 실행 창**에서는 디버그하는 애플리케이션을 조작할 수 있습니다.

1. 변수 값을 대화형으로 변경할 수 있습니다. **직접 실행 창**에 `name = "Gracie"`를 입력하고 Enter 키를 누릅니다.

1. **직접 실행 창**에 `currentDate = new DateTime(2016,11,01,11,59,00)`를 입력하고 Enter 키를 누릅니다.

1. 도구 모음에서 **계속** 단추를 선택하거나 **디버그** > **계속** 메뉴 항목을 선택하여 프로그램을 계속 실행합니다. 콘솔 창에 표시되는 값은 **직접 실행 창**에서 변경한 값과 일치합니다.

   ![직접 실행 창에 입력된, 변경된 값을 보여 주는 콘솔 창](./media/debugging-with-visual-studio/debug-changed-value.png)

1. 아무 키나 눌러 애플리케이션을 끝내고 디버그 모드를 종료합니다.

---

## <a name="setting-a-conditional-breakpoint"></a>조건부 중단점 설정

프로그램은 사용자가 입력하는 문자열을 표시합니다. 사용자가 아무 값도 입력하지 않으면 어떻게 되나요? 하나 이상의 조건이 충족될 경우 프로그램 실행을 중단하는 유용한 디버깅 기능인 *조건부 중단점*을 사용하여 테스트할 수 있습니다.

조건부 중단점을 설정하고 사용자가 문자열을 입력하지 못한 경우에 발생하는 상황을 테스트하려면 다음을 수행합니다.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. 중단점을 나타내는 빨간색 점을 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **조건**을 선택하여 **중단점 설정** 대화 상자를 엽니다. **조건** 확인란을 선택합니다.

   ![중단점 설정 패널을 보여 주는 편집기 - C#](./media/debugging-with-visual-studio/breakpoint-settings.png)

1. **조건식**에서 "e.g. x == 5"를 다음 코드로 바꿉니다.

   ```csharp
   String.IsNullOrEmpty(name)
   ```

   *name*에 값이 할당되지 않았거나 해당 값이 빈 문자열("")이기 때문에 `String.IsNullOrEmpty(name)` 메서드 호출이 `true`인 코드 조건을 테스트하고 있습니다. 문이 실행되기 전에 프로그램 실행을 중단하는 *적중 횟수* 또는 스레드 식별자, 프로세스 이름 또는 스레드 이름과 같은 특성을 기준으로 프로그램 실행을 중단하는 *필터 조건*을 지정할 수도 있습니다.

1. **닫기** 단추를 선택하여 대화 상자를 닫습니다.

1. 디버그 모드에서 프로그램을 실행합니다.

1. 콘솔 창에 이름을 입력하라는 메시지가 나타나면 Enter 키를 누릅니다.

1. `name`이 `null` 또는 <xref:System.String.Empty?displayProperty=nameWithType>이라는 지정한 조건이 충족되었으므로 중단점에 도달한 후 `Console.WriteLine` 메서드가 실행되기 전에 프로그램 실행이 중지됩니다.

1. **지역** 창을 선택합니다. 이 창에는 현재 실행 중인 메서드(프로그램의 `Main` 메서드)에 로컬인 변수 값이 표시됩니다. `name` 변수의 값은 `""` 또는 <xref:System.String.Empty?displayProperty=nameWithType>입니다.

1. **직접 실행 창**에 다음 문을 입력하여 값이 빈 문자열인지 확인합니다. 결과는 `true`입니다.

   ```csharp
   ? name == String.Empty
   ```

   ![문이 실행된 후 true 값을 반환하는 직접 실행 창 - C#](./media/debugging-with-visual-studio/immediate-window-output.png)

1. 도구 모음에서 **계속** 단추를 선택하여 프로그램 실행을 계속합니다.

1. 아무 키나 눌러 콘솔 창을 닫고 디버그 모드를 끝냅니다.

1. 코드 창 왼쪽 여백에 있는 점을 클릭하거나 행을 선택하고 **디버그 > 중단점 설정/해제** 메뉴 항목을 선택하여 중단점을 지웁니다.

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. 중단점을 나타내는 빨간색 점을 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **조건**을 선택하여 **중단점 설정** 대화 상자를 엽니다. **조건** 확인란을 선택합니다.

   ![중단점 설정 패널을 보여 주는 편집기 - Visual Basic](./media/debugging-with-visual-studio/vb-breakpointsettings.png)

1. **조건식**에서 “e.g. x = 5”를 다음 코드로 바꿉니다.

   ```vb
   String.IsNullOrEmpty(name)
   ```

   *name*에 값이 할당되지 않았거나 해당 값이 빈 문자열("")이기 때문에 `String.IsNullOrEmpty(name)` 메서드 호출이 `True`인 코드 조건을 테스트하고 있습니다. 문이 실행되기 전에 프로그램 실행을 중단하는 *적중 횟수* 또는 스레드 식별자, 프로세스 이름 또는 스레드 이름과 같은 특성을 기준으로 프로그램 실행을 중단하는 *필터 조건*을 지정할 수도 있습니다.

1. **닫기** 단추를 선택하여 대화 상자를 닫습니다.

1. 디버그 모드에서 프로그램을 실행합니다.

1. 콘솔 창에 이름을 입력하라는 메시지가 나타나면 Enter 키를 누릅니다.

1. `name`이 `null` 또는 <xref:System.String.Empty?displayProperty=nameWithType>이라는 지정한 조건이 충족되었으므로 중단점에 도달한 후 `Console.WriteLine` 메서드가 실행되기 전에 프로그램 실행이 중지됩니다.

1. **지역** 창을 선택합니다. 이 창에는 현재 실행 중인 메서드(프로그램의 `Main` 메서드)에 로컬인 변수 값이 표시됩니다. `name` 변수의 값은 `""` 또는 <xref:System.String.Empty?displayProperty=nameWithType>입니다.

1. **직접 실행 창**에 다음 문을 입력하여 값이 빈 문자열인지 확인합니다. 결과는 `true`입니다.

   ```vb
   ? String.IsNullOrEmpty(name)
   ```

  ![문이 실행된 후 true 값을 반환하는 직접 실행 창 - Visual Basic](./media/debugging-with-visual-studio/vb-immediate-window-output.png)

1. 도구 모음에서 **계속** 단추를 선택하여 프로그램 실행을 계속합니다.

1. 아무 키나 눌러 콘솔 창을 닫고 디버그 모드를 끝냅니다.

1. 코드 창 왼쪽 여백에 있는 점을 클릭하거나 행을 선택하고 **디버그 > 중단점 설정/해제** 메뉴 항목을 선택하여 중단점을 지웁니다.

---
## <a name="stepping-through-a-program"></a>단계별 프로그램 실행

Visual Studio에서 프로그램을 한 줄씩 단계별로 실행하고 해당 실행을 모니터링할 수도 있습니다. 일반적으로 중단점을 설정하고 이 기능을 사용하여 프로그램 코드 일부의 프로그램 흐름을 따라가면서 확인할 수 있습니다. 여기서는 프로그램이 작으므로 다음을 수행하여 전체 프로그램을 단계별로 실행할 수 있습니다.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

1. 메뉴 모음에서 **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio에서 다음에 실행될 줄을 강조 표시하고 옆에 화살표를 표시합니다.

   ![Visual Studio 한 단계씩 코드 실행 메서드 - C#](./media/debugging-with-visual-studio/step-into-method.png)

   이때 **자동** 창에는 현재 프로그램에서 단일 변수인 `args`만 정의되었다고 표시됩니다. 프로그램에 명령줄 인수를 전달하지 않았으므로 해당 값은 빈 문자열 배열입니다. 또한 Visual Studio에서는 빈 콘솔 창이 열려 있습니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. 이제 Visual Studio에서 다음에 실행될 줄을 강조 표시합니다. 그림에서 볼 수 있듯이 마지막 문과 이 문 사이의 코드를 실행하는 데는 1밀리초 미만이 소요되었습니다. `args`가 선언된 유일한 변수이며 콘솔 창은 여전히 비어 있습니다.

   ![Visual Studio 한 단계씩 코드 실행 메서드 소스 - C#](./media/debugging-with-visual-studio/step-into-source-method.png)

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio는 `name` 변수 할당을 포함하는 문을 강조 표시합니다. **자동** 창에서는 `name`이 `null`로 표시되고 콘솔 창에서는 문자열 "What is your name?"이 표시됩니다.

1. 콘솔 창에 문자열을 입력하고 Enter 키를 눌러 프롬프트에 응답합니다. 콘솔은 응답하지 않게 되고 입력한 문자열이 콘솔 창에 표시되지 않지만 <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> 메서드는 사용자의 입력을 캡처합니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio는 `date`(C#) 또는 `currentDate`(Visual Basic) 변수 할당을 포함하는 문을 강조 표시합니다. **자동** 창에는 <xref:System.DateTime.Now?displayProperty=nameWithType> 속성 값과 <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> 메서드 호출에 의해 반환된 값이 표시됩니다. 콘솔 창에는 콘솔이 입력을 요구할 때 입력된 문자열도 표시됩니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. **자동** 창에는 <xref:System.DateTime.Now?displayProperty=nameWithType> 속성에 따라 할당된 이후의 `date` 변수 값이 표시됩니다. 콘솔 창은 변경되지 않습니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio에서 <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> 메서드를 호출합니다. `date`(또는 `currentDate`) 및 `name` 변수 값이 **자동** 창에 표시되고 콘솔 창에는 서식 문자열이 표시됩니다.

1. **디버그** > **프로시저 나가기**를 선택하거나 Shift+F11을 누릅니다. 이렇게 하면 단계별 실행이 중지됩니다. 콘솔 창은 메시지를 표시하고 사용자가 키를 누르기를 기다립니다.

1. 아무 키나 눌러 콘솔 창을 닫고 디버그 모드를 끝냅니다.

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

1. 메뉴 모음에서 **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio에서 다음에 실행될 줄을 강조 표시하고 옆에 화살표를 표시합니다.

   ![Visual Studio 한 단계씩 코드 실행 메서드 - Visual Basic](./media/debugging-with-visual-studio/vb-step-into-method.png)

   현재 프로그램에 명령줄 인수를 전달하지 않았으므로 **자동** 창에는 `args` 변수의 값이 빈 문자열 배열로 표시됩니다. 또한 Visual Studio에서는 빈 콘솔 창이 열려 있습니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. 이제 Visual Studio에서 다음에 실행될 줄을 강조 표시합니다. 그림에서 볼 수 있듯이 마지막 문과 이 문 사이의 코드를 실행하는 데는 1밀리초 미만이 소요되었습니다. `args`가 선언된 유일한 변수이며 콘솔 창은 여전히 비어 있습니다.

   ![Visual Studio 한 단계씩 코드 실행 메서드 소스 - Visual Basic](./media/debugging-with-visual-studio/vb-step-into-source-method.png)

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio는 `name` 변수 할당을 포함하는 문을 강조 표시합니다. **자동** 창에서는 `name`이 `Nothing`로 표시되고 콘솔 창에서는 문자열 "What is your name?"이 표시됩니다.

1. 콘솔 창에 문자열을 입력하고 Enter 키를 눌러 프롬프트에 응답합니다. 콘솔은 응답하지 않게 되고 입력한 문자열이 콘솔 창에 표시되지 않지만 <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> 메서드는 사용자의 입력을 캡처합니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio는 `date`(C#) 또는 `currentDate`(Visual Basic) 변수 할당을 포함하는 문을 강조 표시합니다. **자동** 창에는 <xref:System.DateTime.Now?displayProperty=nameWithType> 속성 값과 <xref:System.Console.ReadLine%2A?displayProperty=nameWithType> 메서드 호출에 의해 반환된 값이 표시됩니다. 콘솔 창에는 콘솔이 입력을 요구할 때 입력된 문자열도 표시됩니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. **자동** 창에는 <xref:System.DateTime.Now?displayProperty=nameWithType> 속성에 따라 할당된 이후의 `date` 변수 값이 표시됩니다. 콘솔 창은 변경되지 않습니다.

1. **디버그** > **한 단계씩 코드 실행**을 선택하거나 F11 키를 누릅니다. Visual Studio에서 <xref:System.Console.WriteLine(System.String,System.Object,System.Object)?displayProperty=nameWithType> 메서드를 호출합니다. `date`(또는 `currentDate`) 및 `name` 변수 값이 **자동** 창에 표시되고 콘솔 창에는 서식 문자열이 표시됩니다.

1. **디버그** > **프로시저 나가기**를 선택하거나 Shift+F11을 누릅니다. 이렇게 하면 단계별 실행이 중지됩니다. 콘솔 창은 메시지를 표시하고 사용자가 키를 누르기를 기다립니다.

1. 아무 키나 눌러 콘솔 창을 닫고 디버그 모드를 끝냅니다.

---

## <a name="building-a-release-version"></a>릴리스 버전 빌드

애플리케이션의 디버그 빌드를 테스트한 후에는 릴리스 버전을 컴파일하고 테스트해야 합니다. 릴리스 버전에는 애플리케이션의 동작에 부정적인 영향을 줄 수 있는 컴파일러 최적화가 통합됩니다. 예를 들어 성능 향상을 위해 설계된 컴파일러 최적화는 비동기 또는 다중 스레드 애플리케이션에서 경합 상태를 만들 수 있습니다.

콘솔 애플리케이션의 릴리스 버전을 빌드하고 테스트하려면 도구 모음에서 빌드 구성을 **디버그**에서 **릴리스**로 변경합니다.

![디버그가 강조 표시된 기본 Visual Studio 도구 모음](./media/debugging-with-visual-studio/visual-studio-toolbar-release.png)

F5 키를 누르거나 **빌드** 메뉴에서 **솔루션 빌드**를 선택하면 Visual Studio에서 콘솔 애플리케이션의 릴리스 버전을 컴파일합니다. 애플리케이션의 디버그 버전처럼 릴리스 버전을 테스트할 수 있습니다.

애플리케이션 디버그를 마친 후의 다음 단계는 배포 가능한 애플리케이션 버전을 게시하는 것입니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [Visual Studio 2017을 사용하여 Hello World 애플리케이션 게시](publishing-with-visual-studio.md)를 참조하세요.
