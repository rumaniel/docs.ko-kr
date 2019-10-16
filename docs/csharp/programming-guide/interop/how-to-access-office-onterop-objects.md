---
title: '방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- optional parameters [C#], Office programming
- named and optional arguments [C#], Office programming
- dynamic [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
- Office programming [C#]
ms.assetid: 041b25c2-3512-4e0f-a4ea-ceb2999e4d5e
ms.openlocfilehash: 3399d1aad8a2118775f7779727d4d03ee2002547
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834203"
---
# <a name="how-to-access-office-interop-objects-by-using-visual-c-features-c-programming-guide"></a>방법: Visual C# 기능을 사용하여 Office Interop 개체에 액세스(C# 프로그래밍 가이드)

Visual C#에는 Office API 개체에 간편하게 액세스할 수 있는 기능이 있습니다. 새로운 기능에는 명명된 인수와 선택적 인수, `dynamic`이라는 새 형식 그리고 인수를 값 매개 변수처럼 COM 메서드의 참조 매개 변수로 전달하는 기능이 포함됩니다.

이 항목에서는 새 기능을 사용하여 Microsoft Office Excel 워크시트를 만들고 표시하는 코드를 작성합니다. 그런 다음 Excel 워크시트에 연결된 아이콘이 들어 있는 Office Word 문서를 추가하는 코드를 작성합니다.

이 연습을 완료하려면 Microsoft Office Excel 2007 및 Microsoft Office Word 2007 이상 버전이 컴퓨터에 설치되어 있어야 합니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-new-console-application"></a>새 콘솔 애플리케이션을 만들려면

1. Visual Studio를 시작합니다.

2. **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자가 나타납니다.

3. **설치된 템플릿** 창에서 **Visual C#** 을 확장한 다음 **Windows**를 클릭합니다.

4. **새 프로젝트** 대화 상자 위쪽에서 **.NET Framework 4** 이상 버전이 대상 프레임워크로 선택되어 있는지 확인합니다.

5. **템플릿** 창에서 **콘솔 애플리케이션**을 클릭합니다.

6. **이름** 필드에 프로젝트의 이름을 입력합니다.

7. **확인**을 클릭합니다.

     **솔루션 탐색기**에 새 프로젝트가 표시됩니다.

## <a name="to-add-references"></a>참조를 추가하려면

1. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다. **참조 추가** 대화 상자가 나타납니다.

2. **어셈블리** 페이지의 **구성 요소 이름** 목록에서 **Microsoft.Office.Interop.Word**를 선택하고 Ctrl 키를 누른 상태로 **Microsoft.Office.Interop.Excel**을 선택합니다.  이러한 어셈블리가 보이지 않으면 어셈블리가 설치되어 있으며 표시되는지를 확인해야 할 수 있습니다. [방법: Office Primary Interop Assemblies](/visualstudio/vsto/how-to-install-office-primary-interop-assemblies)를 설치합니다.

3. **확인**을 클릭합니다.

## <a name="to-add-necessary-using-directives"></a>필요한 using 지시문을 추가하려면

1. **솔루션 탐색기**에서 *Program.cs* 파일을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.

2. 다음 `using` 지시문을 코드 파일의 맨 위에 추가합니다.

     [!code-csharp[csProgGuideOfficeHowTo#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#1)]

## <a name="to-create-a-list-of-bank-accounts"></a>은행 계좌 목록을 만들려면

1. 다음 클래스 정의를 **Program.cs**의 `Program` 클래스 아래에 붙여 넣습니다.

     [!code-csharp[csProgGuideOfficeHowTo#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#2)]

2. 다음 코드를 `Main` 메서드에 추가하여 계좌 두 개가 포함된 `bankAccounts` 목록을 만듭니다.

     [!code-csharp[csProgGuideOfficeHowTo#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#3)]

## <a name="to-declare-a-method-that-exports-account-information-to-excel"></a>계좌 정보를 Excel로 내보내는 메서드를 선언하려면

1. 다음 메서드를 `Program` 클래스에 추가하여 Excel 워크시트를 설정합니다.

     <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 메서드에는 특정 템플릿을 지정하기 위한 선택적 매개 변수가 있습니다. C# 4에서 도입된 선택적 매개 변수를 사용하면 매개 변수의 기본값을 사용하려는 경우 해당 매개 변수의 인수를 생략할 수 있습니다. 다음 코드에서는 인수가 전송되지 않으므로 `Add`는 기본 템플릿을 사용하며 새 통합 문서를 만듭니다. 이전 버전의 C#에서 이와 동일한 문을 사용하려면 자리 표시자 인수인 `ExcelApp.Workbooks.Add(Type.Missing)`를 사용해야 했습니다.

     [!code-csharp[csProgGuideOfficeHowTo#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#4)]

2. `DisplayInExcel` 끝에 다음 코드를 추가합니다. 이 코드는 워크시트 첫 번째 행의 처음 두 열에 값을 삽입합니다.

     [!code-csharp[csProgGuideOfficeHowTo#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#5)]

3. `DisplayInExcel` 끝에 다음 코드를 추가합니다. `foreach` 루프는 계좌 목록의 정보를 워크시트에서 연속 행의 처음 두 열에 삽입합니다.

     [!code-csharp[csProgGuideOfficeHowTo#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#7)]

4. 열 너비를 콘텐츠에 맞게 조정하려면 `DisplayInExcel` 끝에 다음 코드를 추가합니다.

     [!code-csharp[csProgGuideOfficeHowTo#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#13)]

     이전 버전의 C#에서는 이러한 작업을 명시적으로 캐스트해야 했습니다. `ExcelApp.Columns[1]`은 `Object`를 반환하며 `AutoFit`은 Excel <xref:Microsoft.Office.Interop.Excel.Range> 메서드이기 때문입니다. 다음 줄에는 캐스팅이 나와 있습니다.

     [!code-csharp[csProgGuideOfficeHowTo#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#14)]

     C# 4 이상 버전에서는 [/link](../../language-reference/compiler-options/link-compiler-option.md) 컴파일러 옵션이 어셈블리를 참조한 경우 또는 이와 동등하게 Excel의 **Interop 형식 포함** 속성이 true로 설정되어 있는 경우, 반환된 `Object`를 `dynamic`으로 자동 변환합니다. 이 속성의 기본값은 true입니다.

## <a name="to-run-the-project"></a>프로젝트를 실행하려면

1. `Main` 끝에 다음 줄을 추가합니다.

     [!code-csharp[csProgGuideOfficeHowTo#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#8)]

2. Ctrl+F5를 누릅니다.

     두 계좌의 데이터가 포함된 Excel 워크시트가 표시됩니다.

## <a name="to-add-a-word-document"></a>Word 문서를 추가하려면

1. C# 4 이상 버전에서 Office 프로그래밍을 향상하는 추가 방법을 설명하기 위해, 다음 코드에서는 Word 애플리케이션을 열고 Excel 워크시트에 연결되는 아이콘을 만듭니다.

     이 단계의 뒷부분에서 제공되는 `CreateIconInWordDoc` 메서드를 `Program` 클래스에 붙여 넣습니다. `CreateIconInWordDoc`는 명명된 인수와 선택적 인수를 사용하여 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 및 <xref:Microsoft.Office.Interop.Word.Selection.PasteSpecial%2A>에 대한 메서드 호출의 복잡성을 줄입니다. 이러한 호출에는 C# 4에 도입된 다른 두 가지 새 기능이 통합됩니다. 이러한 기능은 참조 매개 변수가 포함된 COM 메서드 호출을 간소화합니다. 그 중 첫 번째 기능은 인수를 값 매개 변수처럼 참조 매개 변수로 전달하는 것입니다. 즉, 각 참조 매개 변수에 대한 변수를 만들지 않고 직접 값을 보낼 수 있습니다. 컴파일러는 인수 값을 저장하기 위한 임시 변수를 생성하고 호출에서 값이 반환되면 해당 변수를 삭제합니다. 두 번째 기능은 인수 목록의 `ref` 키워드를 생략하는 것입니다.

     `Add` 메서드에는 참조 매개 변수 4개가 있습니다(모두 선택적 매개 변수임). C# 4.0 이상 버전에서는 기본값을 사용하려는 경우 모든 매개 변수 또는 원하는 매개 변수의 인수를 생략할 수 있습니다. C# 3.0 이하 버전에서는 각 매개 변수에 대해 인수를 제공해야 하며 매개 변수가 참조 매개 변수이므로 인수는 변수여야 합니다.

     `PasteSpecial` 메서드는 클립보드의 내용을 삽입합니다. 이 메서드에는 참조 매개 변수 7개가 있습니다(모두 선택적 매개 변수임). 다음 코드는 이러한 매개 변수 중 두 개에 대해 인수를 지정합니다. 그 중 하나는 클립보드 내용의 소스에 대한 링크를 만드는 `Link`이고 다른 하나는 링크를 아이콘으로 표시하는 `DisplayAsIcon`입니다. C# 4.0 이상 버전에서는 이 두 매개 변수에 대해 명명된 인수를 사용하고 나머지 인수는 생략할 수 있습니다. 이러한 매개 변수는 참조 매개 변수이지만 `ref` 키워드를 사용하거나 인수로 보낼 변수를 만들 필요가 없으며, 값을 직접 보낼 수 있습니다. C# 3.0 이하 버전에서는 각 참조 매개 변수에 대해 가변 인수를 공급해야 합니다.

     [!code-csharp[csProgGuideOfficeHowTo#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#9)]

     C# 3.0 이하 버전의 언어에서는 다음과 같은 더 복잡한 코드를 사용해야 합니다.

     [!code-csharp[csProgGuideOfficeHowTo#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#10)]

2. `Main` 끝에 다음 문을 추가합니다.

     [!code-csharp[csProgGuideOfficeHowTo#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#11)]

3. `DisplayInExcel` 끝에 다음 문을 추가합니다. `Copy` 메서드는 클립보드에 워크시트를 추가합니다.

     [!code-csharp[csProgGuideOfficeHowTo#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#12)]

4. Ctrl+F5를 누릅니다.

     아이콘이 포함된 Word 문서가 나타납니다. 아이콘을 두 번 클릭하여 워크시트를 포그라운드로 가져옵니다.

## <a name="to-set-the-embed-interop-types-property"></a>Interop 형식 포함 속성을 설정하려면

1. 런타임에 PIA(주 interop 어셈블리)를 사용하지 않아도 되는 COM 형식을 호출할 때는 코드를 추가로 개선할 수 있습니다. PIA에 대한 종속성을 제거하면 버전을 독립적으로 실행할 수 있으며 보다 쉽게 배포할 수 있습니다. PIA를 사용하지 않는 프로그래밍의 장점에 대한 자세한 내용은 [연습: 관리되는 어셈블리의 형식 포함](../../../standard/assembly/embed-types-visual-studio.md)을 참조하세요.

     또한 COM 메서드에서 사용해야 하며 반환되는 형식은 `dynamic`가 아닌 `Object` 형식을 사용하여 표시할 수 있으므로 프로그램이 더욱 쉬워집니다. `dynamic` 형식이 포함된 변수는 런타임까지 평가되지 않으므로 명시적 캐스팅을 수행할 필요가 없습니다. 자세한 내용은 [dynamic 형식 사용](../types/using-type-dynamic.md)을 참조하세요.

     C# 4에서는 PIA를 사용하는 대신 형식 정보를 포함하는 것이 기본 동작입니다. 이러한 기본 동작으로 인해 명시적 캐스팅이 필요하지 않으므로 위의 여러 예제가 간소화됩니다. 예를 들어 `worksheet`의 `DisplayInExcel` 선언은 `Excel._Worksheet workSheet = excelApp.ActiveSheet`가 아닌 `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet`로 작성됩니다. 마찬가지로 기본 동작이 없으면 같은 메서드의 `AutoFit`에 대한 호출에서도 명시적 캐스팅을 수행해야 합니다. `ExcelApp.Columns[1]`는 `Object`를 반환하며 `AutoFit`은 Excel 메서드이기 때문입니다. 다음 코드에서는 캐스팅을 보여 줍니다.

     [!code-csharp[csProgGuideOfficeHowTo#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#14)]

2. 형식 정보를 포함하는 대신 기본값을 변경하여 PIA를 사용하려면 **솔루션 탐색기**에서 **참조** 노드를 확장하고 **Microsoft.Office.Interop.Excel** 또는 **Microsoft.Office.Interop.Word**를 선택합니다.

3. **속성** 창이 보이지 않으면 **F4**키를 누릅니다.

4. 속성 목록에서 **Interop 형식 포함**을 찾은 다음 해당 값을 **False**로 변경합니다. 마찬가지로 명령 프롬프트에서 [/link](../../language-reference/compiler-options/link-compiler-option.md) 대신 [/reference](../../language-reference/compiler-options/reference-compiler-option.md) 컴파일러 옵션을 사용하여 컴파일할 수 있습니다.

## <a name="to-add-additional-formatting-to-the-table"></a>표에 서식을 더 추가하려면

1. `AutoFit`에서 `DisplayInExcel`에 대한 두 호출을 다음 문으로 바꿉니다.

     [!code-csharp[csProgGuideOfficeHowTo#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#15)]

     <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> 메서드에는 모두 선택적 매개 변수인 값 매개 변수 7개가 있습니다. 명명된 인수와 선택적 인수를 사용하여 이러한 매개 변수 중 일부 또는 모두에 대해 인수를 제공할 수도 있고 모든 매개 변수에 인수를 제공하지 않을 수도 있습니다. 위의 문에서는 `Format` 매개 변수 하나에만 인수가 제공됩니다. `Format`은 매개 변수 목록의 첫 번째 매개 변수이므로 매개 변수 이름은 지정하지 않아도 됩니다. 그러나 다음 코드에 나와 있는 것처럼 매개 변수 이름을 포함하면 문을 더 쉽게 이해할 수 있습니다.

     [!code-csharp[csProgGuideOfficeHowTo#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#16)]

2. 결과를 보려면 CTRL+F5를 누릅니다. 기타 서식은 <xref:Microsoft.Office.Interop.Excel.XlRangeAutoFormat> 열거형에 나열됩니다.

3. 1단계의 문을 다음 코드와 비교합니다. 이 코드는 C# 3.0 이하 버전에 필요한 인수를 보여 줍니다.

     [!code-csharp[csProgGuideOfficeHowTo#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#17)]

## <a name="example"></a>예

다음 코드에서는 전체 예제를 보여 줍니다.

[!code-csharp[csProgGuideOfficeHowTo#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/walkthrough.cs#18)]

## <a name="see-also"></a>참고 항목

- <xref:System.Type.Missing?displayProperty=nameWithType>
- [dynamic](../../language-reference/keywords/dynamic.md)
- [dynamic 형식 사용](../types/using-type-dynamic.md)
- [명명된 인수 및 선택적 인수](../classes-and-structs/named-and-optional-arguments.md)
- [방법: Office 프로그래밍에서 명명된 인수 및 선택적 인수 사용](../classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
