---
title: '연습: 동적 개체 만들기 및 사용(C# 및 Visual Basic)'
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dynamic objects [Visual Basic]
- dynamic objects
- dynamic objects [C#]
ms.assetid: 568f1645-1305-4906-8625-5d77af81e04f
ms.openlocfilehash: 8134a7c7c1f2c4e6432dd19889faf796a9284553
ms.sourcegitcommit: fd8d4587cc26e53f0e27e230d6e27d828ef4306b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49347970"
---
# <a name="walkthrough-creating-and-using-dynamic-objects-c-and-visual-basic"></a>연습: 동적 개체 만들기 및 사용(C# 및 Visual Basic)

동적 개체는 컴파일 시간이 아닌 런타임에 속성 및 메서드 같은 멤버를 노출합니다. 이를 통해 형식 또는 정적 형식과 일치하지 않는 구조와 작동할 개체를 만들 수 있습니다. 예를 들어 동적 개체를 사용하여 DOM(문서 개체 모델)을 참조할 수 있습니다. DOM에는 유효한 HTML 마크업 요소 및 특성의 조합을 포함할 수 있습니다. 각 HTML 문서는 고유하므로, 특정 HTML 문서에 대한 멤버는 런타임에 의해 결정됩니다. HTML 요소의 특성을 참조하는 일반적인 방법은 요소의 `GetProperty` 메서드에 특성의 이름을 전달하는 것입니다. HTML 요소 `<div id="Div1">`의 `id` 특성을 참조하려면 먼저 `<div>` 요소에 대한 참조를 가져온 다음 `divElement.GetProperty("id")`를 사용합니다. 동적 개체를 사용하는 경우 `id` 특성을 `divElement.id`로서 참조할 수 있습니다.  
  
 동적 개체를 사용하면 IronPython 및 IronRuby와 같은 동적 언어에 편리하게 액세스할 수 있습니다. 동적 개체를 사용하면 런타임에 해석되는 동적 스크립트를 참조할 수 있습니다.  
  
 런타임에 바인딩을 사용하여 동적 개체를 참조합니다. C#에서는 런타임에 바인딩된 개체의 형식을 `dynamic`으로 지정합니다. Visual Basic에서는 런타임에 바인딩된 개체의 형식을 `Object`으로 지정합니다. 자세한 내용은 [dynamic](../../../csharp/language-reference/keywords/dynamic.md) 및 [초기 바인딩 및 런타임에 바인딩](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)을 참조하세요.  
  
 <xref:System.Dynamic?displayProperty=nameWithType> 네임스페이스의 클래스를 사용하여 사용자 지정 동적 개체를 만들 수 있습니다. 예를 들어 <xref:System.Dynamic.ExpandoObject>를 만들고 해당 개체의 멤버를 런타임에 지정할 수 있습니다. <xref:System.Dynamic.DynamicObject> 클래스를 상속하는 고유한 형식을 만들 수도 있습니다. 그런 다음 런타임 동적 기능을 제공하도록 <xref:System.Dynamic.DynamicObject> 클래스의 멤버를 재정의할 수 있습니다.  
  
 이 연습에서는 다음 작업을 수행합니다.  
  
-   텍스트 파일의 내용을 개체의 속성으로서 동적으로 노출하는 사용자 지정 개체를 만듭니다.  
  
-   `IronPython` 라이브러리를 사용하는 프로젝트를 만듭니다.  
  
## <a name="prerequisites"></a>전제 조건  
이 연습을 완료하려면 .NET용 [IronPython](http://ironpython.net/)이 필요합니다. [다운로드 페이지](http://ironpython.net/download/)로 이동하여 최신 버전을 다운로드하세요.
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-a-custom-dynamic-object"></a>사용자 지정 동적 개체 만들기

이 연습에서 만드는 첫 번째 프로젝트는 텍스트 파일의 내용을 검색하는 사용자 지정 동적 개체를 정의합니다. 검색할 텍스트는 동적 속성의 이름으로 지정됩니다. 예를 들어, 호출 코드가 `dynamicFile.Sample`을 지정하면 동적 클래스는 "Sample"로 시작하는 파일의 모든 줄을 포함하는 문자열의 제네릭 목록을 반환합니다. 검색은 대/소문자를 구분합니다. 동적 클래스는 또한 두 개의 선택적 인수를 지원합니다. 첫 번째 인수는 동적 클래스가 행의 시작, 행의 끝 또는 행의 어디에서나 일치를 검색하도록 지정하는 검색 옵션 열거형 값입니다. 두 번째 인수는 동적 클래스가 검색 전에 각 행의 선행 및 후행 공백을 잘라내야 함을 지정합니다. 예를 들어 호출 코드가 `dynamicFile.Sample(StringSearchOption.Contains)`을 지정하면 동적 클래스는 한 줄의 어디에서나 "Sample"을 검색합니다. 호출 코드가 `dynamicFile.Sample(StringSearchOption.StartsWith, false)`을 지정하면 동적 클래스는 각 줄의 시작 부분에서 "Sample"을 검색하고, 선행 및 후행 공백을 제거하지 않습니다. 동적 클래스의 기본 동작은 각 줄의 시작 부분에서 일치를 검색하고 선행 및 후행 공백을 제거하는 것입니다.  
  
### <a name="to-create-a-custom-dynamic-class"></a>사용자 지정 동적 클래스를 만들려면  
  
1.  Visual Studio를 시작합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기** 를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
3.  **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Windows**가 선택되었는지 확인합니다. **템플릿** 창에서 **콘솔 응용 프로그램**을 선택합니다. **이름** 상자에 `DynamicSample`를 입력한 다음 **확인**을 클릭합니다. 새 프로젝트가 만들어집니다.  
  
4.  DynamicSample 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **클래스**를 클릭합니다. **이름** 상자에 `ReadOnlyFile`을 입력한 다음 **확인**을 클릭합니다. ReadOnlyFile 클래스가 포함된 새 파일이 추가됩니다.  
  
5.  ReadOnlyFile.cs 또는 ReadOnlyFile.vb 파일 맨 위에 다음 코드를 추가하여 <xref:System.IO?displayProperty=nameWithType> 및 <xref:System.Dynamic?displayProperty=nameWithType> 네임스페이스를 가져옵니다.  

    [!code-csharp[VbDynamicWalkthrough#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#1)]
    [!code-vb[VbDynamicWalkthrough#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#1)]  

6.  사용자 지정 동적 개체는 열거형을 사용하여 검색 기준을 결정합니다. Class 문 앞에 다음 열거형 정의를 추가합니다.  
  
    [!code-csharp[VbDynamicWalkthrough#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#2)]
    [!code-vb[VbDynamicWalkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#2)]
  
7.  다음 코드 예제와 같이, `DynamicObject` 클래스를 상속하도록 class 문을 업데이트합니다.  
  
    [!code-csharp[VbDynamicWalkthrough#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#3)]
    [!code-vb[VbDynamicWalkthrough#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#3)]

8.  다음 코드를 `ReadOnlyFile` 클래스에 추가하여 파일 경로의 전용 필드 및 `ReadOnlyFile` 클래스의 생성자를 정의합니다.  
  
    [!code-csharp[VbDynamicWalkthrough#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#4)]
    [!code-vb[VbDynamicWalkthrough#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#4)]
  
9. 다음 `GetPropertyValue` 메서드를 `ReadOnlyFile` 클래스에 추가합니다. `GetPropertyValue` 메서드는 검색 기준을 입력으로 가져오고 해당 검색 기준과 일치하는 텍스트 파일로부터 줄을 반환합니다. `ReadOnlyFile` 클래스가 제공하는 동적 메서드는 `GetPropertyValue` 메서드를 호출하여 각 결과를 검색합니다.  
  
    [!code-csharp[VbDynamicWalkthrough#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#5)]
    [!code-vb[VbDynamicWalkthrough#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#5)]  
  
10. `GetPropertyValue` 메서드 뒤에 다음 코드를 추가하여 <xref:System.Dynamic.DynamicObject> 클래스의 <xref:System.Dynamic.DynamicObject.TryGetMember%2A> 메서드를 재정의합니다. 동적 클래스의 멤버를 요청했는데 지정된 인수가 없는 경우 <xref:System.Dynamic.DynamicObject.TryGetMember%2A> 메서드가 호출됩니다. `binder` 인수는 참조된 멤버에 대한 정보를 포함하며, `result` 인수는 지정된 멤버에 대해 반환된 결과를 참조합니다. <xref:System.Dynamic.DynamicObject.TryGetMember%2A> 메서드는 요청한 멤버가 있는 경우 `true`, 없는 경우 `false`를 반환하는 부울 값을 반환합니다.  
  
    [!code-csharp[VbDynamicWalkthrough#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#6)]
    [!code-vb[VbDynamicWalkthrough#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#6)]
  
11. `TryGetMember` 메서드 뒤에 다음 코드를 추가하여 <xref:System.Dynamic.DynamicObject> 클래스의 <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> 메서드를 재정의합니다. 인수를 사용하여 동적 클래스의 멤버를 요청하면 <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> 메서드가 호출됩니다. `binder` 인수는 참조된 멤버에 대한 정보를 포함하며, `result` 인수는 지정된 멤버에 대해 반환된 결과를 참조합니다. `args` 인수는 멤버에 전달되는 인수의 배열을 포함합니다. <xref:System.Dynamic.DynamicObject.TryInvokeMember%2A> 메서드는 요청한 멤버가 있는 경우 `true`, 없는 경우 `false`를 반환하는 부울 값을 반환합니다.  
  
    `TryInvokeMember` 메서드의 사용자 지정 버전은 첫 번째 인수로 이전 단계에서 정의한 `StringSearchOption` 열거형의 값을 예상합니다. `TryInvokeMember` 메서드는 두 번째 인수로 부울 값을 예상합니다. 하나 또는 두 인수가 유효한 값인 경우 결과를 검색할 수 있도록 `GetPropertyValue` 메서드로 전달됩니다.  
  
    [!code-csharp[VbDynamicWalkthrough#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/readonlyfile.cs#7)]
    [!code-vb[VbDynamicWalkthrough#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/readonlyfile.vb#7)]
  
12. 파일을 저장한 후 닫습니다.  
  
#### <a name="to-create-a-sample-text-file"></a>샘플 텍스트 파일을 만들려면  
  
1.  DynamicSample 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다. **설치된 템플릿** 창에서 **일반**을 선택한 다음 **텍스트 파일** 템플릿을 선택합니다. **이름** 상자에 있는 기본 이름 TextFile1.txt를 그대로 두고 **추가**를 클릭합니다. 새 텍스트 파일이 프로젝트에 추가됩니다.  
  
2.  TextFile1.txt 파일에 다음 텍스트를 복사합니다.  
  
    ```  
    List of customers and suppliers  
  
    Supplier: Lucerne Publishing (https://www.lucernepublishing.com/)  
    Customer: Preston, Chris  
    Customer: Hines, Patrick  
    Customer: Cameron, Maria  
    Supplier: Graphic Design Institute (https://www.graphicdesigninstitute.com/)   
    Supplier: Fabrikam, Inc. (https://www.fabrikam.com/)   
    Customer: Seubert, Roxanne  
    Supplier: Proseware, Inc. (http://www.proseware.com/)   
    Customer: Adolphi, Stephan  
    Customer: Koch, Paul  
    ```  
  
3.  파일을 저장한 후 닫습니다.  
  
#### <a name="to-create-a-sample-application-that-uses-the-custom-dynamic-object"></a>사용자 지정 동적 개체를 사용하는 샘플 응용 프로그램을 만들려면  
  
1.  **솔루션 탐색기**에서, Visual Basic을 사용 중인 경우 Module1.vb 파일, Visual C#을 사용 중인 경우 Program.cs 파일을 두 번 클릭합니다.  
  
2.  Main 프로시저에 다음 코드를 추가하여 TextFile1.txt 파일에 대한 `ReadOnlyFile` 클래스의 인스턴스를 만듭니다. 코드는 런타임에 바인딩을 사용하여 동적 멤버를 호출하고 "Customer" 문자열이 포함된 텍스트의 줄을 검색합니다.  
  
     [!code-csharp[VbDynamicWalkthrough#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthrough/cs/program.cs#8)]
     [!code-vb[VbDynamicWalkthrough#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthrough/vb/module1.vb#8)]
  
3.  파일을 저장한 다음 Ctrl+F5를 눌러 응용 프로그램을 빌드하고 실행합니다.  
  
## <a name="calling-a-dynamic-language-library"></a>동적 언어 라이브러리 호출  

이 연습에서 만드는 새 프로젝트는 동적 언어 IronPython에서 작성된 라이브러리에 액세스합니다.
  
### <a name="to-create-a-custom-dynamic-class"></a>사용자 지정 동적 클래스를 만들려면
  
1.  Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.  
  
2.  **새 프로젝트** 대화 상자의 **프로젝트 형식** 창에서 **Windows**가 선택되었는지 확인합니다. **템플릿** 창에서 **콘솔 응용 프로그램**을 선택합니다. **이름** 상자에 `DynamicIronPythonSample`를 입력한 다음 **확인**을 클릭합니다. 새 프로젝트가 만들어집니다.  
  
3.  Visual Basic을 사용 중인 경우 DynamicIronPythonSample 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. **참조** 탭을 클릭합니다. **추가** 단추를 클릭합니다. Visual C#을 사용 중인 경우 **솔루션 탐색기**에서 **References** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **참조 추가**를 클릭합니다.  
  
4.  **찾아보기** 탭에서 IronPython 라이브러리가 설치된 폴더로 이동합니다. 예를 들어 .NET 4.0의 경우 C:\Program Files\IronPython 2.6입니다. **IronPython.dll**, **IronPython.Modules.dll**, **Microsoft.Scripting.dll** 및 **Microsoft.Dynamic.dll** 라이브러리를 선택합니다. **확인**을 클릭합니다.  
  
5.  Visual Basic을 사용 중인 경우 Module1.vb 파일을 편집합니다. Visual C#을 사용 중인 경우 Program.cs 파일을 편집합니다.  
  
6.  파일 맨 위에 다음 코드를 추가하여 IronPython 라이브러리에서 `Microsoft.Scripting.Hosting` 및 `IronPython.Hosting` 네임스페이스를 가져옵니다.  
  
    [!code-csharp[VbDynamicWalkthroughIronPython#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/cs/program.cs#1)]
    [!code-vb[VbDynamicWalkthroughIronPython#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/vb/module1.vb#1)]
  
7.  Main 메서드에서 다음 코드를 추가하여 IronPython 라이브러리를 호스트하기 위한 새 `Microsoft.Scripting.Hosting.ScriptRuntime` 개체를 만듭니다. `ScriptRuntime` 개체는 IronPython 라이브러리 모듈 random.py를 로드합니다.  
  
     [!code-csharp[VbDynamicWalkthroughIronPython#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/cs/program.cs#2)]
     [!code-vb[VbDynamicWalkthroughIronPython#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/vb/module1.vb#2)]
  
8.  random.py 모듈을 로드할 코드 뒤에 다음 코드를 추가하여 정수 배열을 만듭니다. 배열은 random.py 모듈의 `shuffle` 메서드로 전달되며, 이 모듈은 배열의 값을 임의로 정렬합니다.  
  
     [!code-csharp[VbDynamicWalkthroughIronPython#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/cs/program.cs#3)]
     [!code-vb[VbDynamicWalkthroughIronPython#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbdynamicwalkthroughironpython/vb/module1.vb#3)]
  
9. 파일을 저장한 다음 Ctrl+F5를 눌러 응용 프로그램을 빌드하고 실행합니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Dynamic?displayProperty=nameWithType>  
- <xref:System.Dynamic.DynamicObject?displayProperty=nameWithType>  
- [dynamic 형식 사용](../../../csharp/programming-guide/types/using-type-dynamic.md)  
- [초기 바인딩 및 런타임에 바인딩](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)  
- [dynamic](../../../csharp/language-reference/keywords/dynamic.md)  
- [동적 인터페이스 구현(Microsoft TechNet에서 다운로드 가능한 PDF)](https://download.microsoft.com/download/5/4/B/54B83DFE-D7AA-4155-9687-B0CF58FF65D7/implementing-dynamic-interfaces.pdf)
