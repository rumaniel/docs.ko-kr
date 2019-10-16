---
title: '방법: Office 프로그래밍에서 명명된 인수 및 선택적 인수 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- named and optional arguments [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
ms.assetid: 65b8a222-bcd8-454c-845f-84adff5a356f
ms.openlocfilehash: 90b60a6410ffbe7f9802b01bf3303b6e842a1424
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002795"
---
# <a name="how-to-use-named-and-optional-arguments-in-office-programming-c-programming-guide"></a>방법: Office 프로그래밍에서 명명된 인수 및 선택적 인수 사용(C# 프로그래밍 가이드)

C# 4에서 도입된 명명된 인수와 선택적 인수는 C# 프로그래밍의 편의성, 유연성 및 가독성을 향상합니다. 또한 이러한 기능은 Microsoft Office 자동화 API와 같은 COM 인터페이스에 대한 액세스에 큰 도움이 됩니다.

다음 예제의 [ConvertToTable](<xref:Microsoft.Office.Interop.Word.Range.ConvertToTable%2A>) 메서드에는 열과 행 수, 서식, 테두리, 글꼴, 색 등의 테이블 특성을 나타내는 매개 변수 16개가 있습니다. 대부분의 경우 모든 매개 변수에 대해 특정 값을 지정하지는 않으므로 16개 매개 변수는 모두 선택 사항입니다. 그러나 명명된 인수와 선택적 인수를 사용하지 않을 경우 각 매개 변수에 대해 값 또는 자리 표시자 값을 제공해야 합니다. 명명된 인수와 선택적 인수를 사용할 경우 프로젝트에 필요한 매개 변수의 값만 지정합니다.

이 절차를 완료하려면 컴퓨터에 Microsoft Office Word가 설치되어 있어야 합니다.

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-new-console-application"></a>새 콘솔 애플리케이션을 만들려면

1. Visual Studio를 시작합니다.

2. **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.

3. **템플릿 범주** 창에서 **Visual C#** 을 확장한 다음 **Windows**를 클릭합니다.

4. **템플릿** 창의 맨 위에서 **.NET Framework 4**가 **대상 프레임워크** 상자에 표시되는지 확인합니다.

5. **템플릿** 창에서 **콘솔 애플리케이션**을 클릭합니다.

6. **이름** 필드에 프로젝트의 이름을 입력합니다.

7. **확인**을 클릭합니다.

     **솔루션 탐색기**에 새 프로젝트가 표시됩니다.

## <a name="to-add-a-reference"></a>참조를 추가하려면

1. **솔루션 탐색기**에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다. **참조 추가** 대화 상자가 나타납니다.

2. **.NET** 페이지의 **구성 요소 이름** 목록에서 **Microsoft.Office.Interop.Word**를 선택합니다.

3. **확인**을 클릭합니다.

## <a name="to-add-necessary-using-directives"></a>필요한 using 지시문을 추가하려면

1. **솔루션 탐색기**에서 *Program.cs* 파일을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 클릭합니다.

2. 다음 `using` 지시문을 코드 파일의 맨 위에 추가합니다.

     [!code-csharp[csProgGuideNamedAndOptional#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#4)]

## <a name="to-display-text-in-a-word-document"></a>Word 문서에 텍스트를 표시하려면

1. *Program.cs*의 `Program` 클래스에서 다음 메서드를 추가하여 Word 애플리케이션과 Word 문서를 만듭니다. [Add](<xref:Microsoft.Office.Interop.Word.Documents.Add%2A>) 메서드에는 선택적 매개 변수 4개가 있습니다. 이 예제에서는 해당 기본값을 사용합니다. 따라서 호출하는 문에 인수가 필요하지 않습니다.

     [!code-csharp[csProgGuideNamedAndOptional#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#6)]

2. 메서드의 끝에 다음 코드를 추가하여 문서에서 텍스트를 표시할 위치 및 표시할 텍스트를 정의합니다.

     [!code-csharp[csProgGuideNamedAndOptional#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#7)]

## <a name="to-run-the-application"></a>애플리케이션을 실행하려면

1. 다음 문을 Main에 추가합니다.

     [!code-csharp[csProgGuideNamedAndOptional#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#8)]

2. <kbd>Ctrl</kbd>+<kbd>F5</kbd>를 눌러 프로젝트를 실행합니다. 지정된 텍스트를 포함하는 Word 문서가 나타납니다.

## <a name="to-change-the-text-to-a-table"></a>텍스트를 표로 변경하려면
  
1. `ConvertToTable` 메서드를 사용하여 텍스트를 표로 묶습니다. 이 메서드에는 선택적 매개 변수 16개가 있습니다. IntelliSense는 다음 그림과 같이 선택적 매개 변수를 중괄호로 묶습니다.

     ![ConvertToTable 메서드의 매개 변수 목록](./media/how-to-use-named-and-optional-arguments-in-office-programming/convert-table-parameters.png)

     명명된 인수 및 선택적 인수를 사용하면 변경하려는 매개 변수의 값만 지정할 수 있습니다. `DisplayInWord` 메서드의 끝에 다음 코드를 추가하여 간단한 표를 만듭니다. 인수는 `range`의 텍스트 문자열에 있는 쉼표가 표의 셀을 구분하도록 지정합니다.

     [!code-csharp[csProgGuideNamedAndOptional#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#9)]

     이전 버전의 C#에서 `ConvertToTable`을 호출하려면 다음 코드와 같이 각 매개 변수에 대한 참조 인수가 필요합니다.
  
     [!code-csharp[csProgGuideNamedAndOptional#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#14)]

2. <kbd>Ctrl</kbd>+<kbd>F5</kbd>를 눌러 프로젝트를 실행합니다.

## <a name="to-experiment-with-other-parameters"></a>다른 매개 변수로 실험하려면

1. 열 1개와 행 3개가 포함되도록 표를 변경하려면 `DisplayInWord`의 마지막 줄을 다음 문으로 바꾼 다음 <kbd>Ctrl</kbd>+<kbd>F5</kbd>를 입력합니다.  

     [!code-csharp[csProgGuideNamedAndOptional#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#10)]

2. 미리 정의된 표 형식을 지정하려면 `DisplayInWord`의 마지막 줄을 다음 문으로 바꾼 다음 <kbd>Ctrl</kbd>+<kbd>F5</kbd>를 입력합니다. 형식은 [WdTableFormat](<xref:Microsoft.Office.Interop.Word.WdTableFormat>) 상수 중 하나일 수 있습니다.

     [!code-csharp[csProgGuideNamedAndOptional#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#11)]

## <a name="example"></a>예

다음 코드에는 전체 예제가 포함되어 있습니다.

 [!code-csharp[csProgGuideNamedAndOptional#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguidenamedandoptional/cs/wordprogram.cs#12)]

## <a name="see-also"></a>참고 항목

- [명명된 인수 및 선택적 인수](./named-and-optional-arguments.md)
