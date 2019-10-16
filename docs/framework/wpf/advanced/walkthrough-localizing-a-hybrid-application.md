---
title: '연습: 하이브리드 애플리케이션 지역화'
ms.date: 08/18/2018
helpviewer_keywords:
- localization [WPF interoperability]
- hybrid applications [WPF interoperability]
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
ms.openlocfilehash: b98bf7b3f0aa4e7698a5c0ca7c8ae16051ce6300
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991772"
---
# <a name="walkthrough-localizing-a-hybrid-application"></a>연습: 하이브리드 애플리케이션 지역화

이 연습에서는 기반 하이브리드 응용 프로그램 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]에서 요소를 지역화 하는 방법을 보여 줍니다.

이 연습에서 설명하는 작업은 다음과 같습니다.

- 호스트 프로젝트 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 를 만듭니다.

- 지역화 가능한 콘텐츠 추가.

- 지역화 사용.

- 리소스 식별자 할당.

- LocBaml 도구를 사용하여 위성 어셈블리 생성.

이 연습에서 설명 하는 작업의 전체 코드 목록은 [하이브리드 응용 프로그램 지역화 샘플](https://go.microsoft.com/fwlink/?LinkID=160015)을 참조 하세요.

위의 작업을 완료하면 지역화된 하이브리드 애플리케이션이 구현됩니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 다음 구성 요소가 필요합니다.

- Visual Studio 2017

## <a name="creating-the-windows-forms-host-project"></a>Windows Forms 호스트 프로젝트 만들기

첫 번째 단계는 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 응용 프로그램 프로젝트를 만들고 지역화할 내용이 포함 된 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 요소를 추가 하는 것입니다.

### <a name="to-create-the-host-project"></a>호스트 프로젝트 만들기

1. 이라는`LocalizingWpfInWf` **WPF 앱** 프로젝트를 만듭니다.  (**파일** > **새로 만들기** **프로젝트 C# 시각적 개체** 또는 Visual Basic클래식데스크톱 > **WPF 응용 프로그램**). >  >  > 

2. 이라는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> 요소를 프로젝트에 추가 합니다. `SimpleControl`

3. 컨트롤을 사용 하 여 폼 `SimpleControl` 에 요소를 넣습니다. <xref:System.Windows.Forms.Integration.ElementHost> 자세한 내용은 [연습: Windows Forms](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)에서 3 차원 WPF 복합 컨트롤을 호스팅합니다.

## <a name="adding-localizable-content"></a>지역화 가능한 콘텐츠 추가

다음 단원에서는 레이블 컨트롤을 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 추가 하 고 지역화 가능한 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 문자열에 요소 콘텐츠를 설정 합니다.

### <a name="to-add-localizable-content"></a>지역화 가능한 콘텐츠를 추가하려면

1. **솔루션 탐색기**에서 **simplecontrol .xaml** 을 두 번 클릭 하 여에서 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]엽니다.

2. 다음 코드를 사용 하 <xref:System.Windows.Controls.Button> 여 컨트롤의 내용을 설정 합니다.

     [!code-xaml[LocalizingWpfInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]

3. **솔루션 탐색기**에서 **Form1** 을 두 번 클릭 하 여 Windows Forms 디자이너에서 엽니다.

4. **도구 상자** 를 열고 **레이블** 을 두 번 클릭 하 여 레이블 컨트롤을 폼에 추가 합니다. <xref:System.Windows.Forms.Control.Text%2A> 속성의 값을 `"Hello"`로 설정합니다.

5. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다.

     요소와 레이블 컨트롤 모두 텍스트 **"Hello"** 를 표시 합니다. `SimpleControl`

## <a name="enabling-localization"></a>지역화 사용

Windows Forms 디자이너에서는 위성 어셈블리에서 지역화를 사용하도록 설정하기 위한 설정을 제공합니다.

### <a name="to-enable-localization"></a>지역화를 사용하려면

1. **솔루션 탐색기**에서 **Form1.cs** 를 두 번 클릭 하 여 Windows Forms 디자이너에서 엽니다.

2. **속성** 창에서 폼의 **지역화할** 수 있는 속성 값을로 `true`설정 합니다.

3. **속성** 창에서 **Language** 속성의 값을 **스페인어 (스페인)** 로 설정 합니다.

4. Windows Forms 디자이너에서 레이블 컨트롤을 선택합니다.

5. **속성** 창에서 <xref:System.Windows.Forms.Control.Text%2A> 속성의 값을로 `"Hola"`설정 합니다.

     Form1.es-ES.resx라는 새 리소스 파일이 프로젝트에 추가됩니다.

6. **솔루션 탐색기**에서 **Form1.cs** 을 마우스 오른쪽 단추로 클릭 하 고 **코드 보기** 를 클릭 하 여 코드 편집기에서 엽니다.

7. 에 대 `Form1` `InitializeComponent`한 호출 앞에 다음 코드를 생성자에 복사 합니다.

     [!code-csharp[LocalizingWpfInWf#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]

8. **솔루션 탐색기**에서 **LocalizingWpfInWf** 을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 언로드**를 클릭 합니다.

     프로젝트 이름에는 **(사용할 수 없음)** 이라는 레이블이 지정 됩니다.

9. **LocalizingWpfInWf**를 마우스 오른쪽 단추로 클릭 하 고 **LocalizingWpfInWf 편집**을 클릭 합니다.

     프로젝트 파일이 코드 편집기에서 열립니다.

10. 다음 줄을 프로젝트 파일의 첫 `PropertyGroup` 번째에 복사 합니다.

    ```xml
    <UICulture>en-US</UICulture>
    ```

11. 프로젝트 파일을 저장하고 닫습니다.

12. **솔루션 탐색기**에서 **LocalizingWpfInWf** 을 마우스 오른쪽 단추로 클릭 하 고 **프로젝트 다시 로드**를 클릭 합니다.

## <a name="assigning-resource-identifiers"></a>리소스 식별자 할당

리소스 식별자를 사용하여 리소스 어셈블리에 지역화 가능한 콘텐츠를 매핑할 수 있습니다. 옵션을 `updateuid` 지정 하면 msbuild.exe 응용 프로그램에서 리소스 식별자를 자동으로 할당 합니다.

### <a name="to-assign-resource-identifiers"></a>리소스 식별자를 할당하려면

1. 시작 메뉴에서 Visual Studio에 대 한 개발자 명령 프롬프트를 엽니다.

2. 다음 명령을 사용하여 지역화 가능한 콘텐츠에 리소스 식별자를 할당합니다.

    ```console
    msbuild -t:updateuid LocalizingWpfInWf.csproj
    ```

3. **솔루션 탐색기**에서 **simplecontrol .xaml** 을 두 번 클릭 하 여 코드 편집기에서 엽니다. 명령에서 `msbuild` 모든 요소에 `Uid` 특성을 추가 하는 것을 볼 수 있습니다. 따라서 리소스 식별자 할당을 통해 지역화가 용이해집니다.

     [!code-xaml[LocalizingWpfInWf#20](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]

4. **F6** 키를 눌러 솔루션을 빌드합니다.

## <a name="using-locbaml-to-produce-a-satellite-assembly"></a>LocBaml을 사용하여 위성 어셈블리 생성

지역화 된 콘텐츠는 리소스 전용 *위성 어셈블리*에 저장 됩니다. 명령줄 도구인 LocBaml을 사용 하 여 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 콘텐츠에 대 한 지역화 된 어셈블리를 만듭니다.

### <a name="to-produce-a-satellite-assembly"></a>위성 어셈블리를 생성하려면

1. LocBaml.exe를 프로젝트의 obj\Debug 폴더에 복사합니다. 자세한 내용은 [응용 프로그램 지역화](how-to-localize-an-application.md)를 참조 하세요.

2. [명령 프롬프트] 창에서 다음 명령을 사용하여 리소스 문자열을 임시 파일로 추출합니다.

    ```console
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv
    ```

3. Visual Studio 또는 다른 텍스트 편집기를 사용 하 여 임시 .csv 파일을 엽니다. 문자열 `"Hello"` 을 스페인어 `"Hola"`변환으로 바꿉니다.

4. temp.csv 파일을 저장합니다.

5. 다음 명령을 사용하여 지역화된 리소스 파일을 생성합니다.

    ```console
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES
    ```

     LocalizingWpfInWf.g.es-ES.resources 파일이 obj\Debug 폴더에 만들어집니다.

6. 다음 명령을 사용하여 지역화된 위성 어셈블리를 빌드합니다.

    ```console
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources
    ```

     LocalizingWpfInWf.resources.dll 파일이 obj\Debug 폴더에 만들어집니다.

7. LocalizingWpfInWf.resources.dll 파일을 프로젝트의 bin\Debug\es-ES 폴더에 복사합니다. 기존 파일을 바꿉니다.

8. 프로젝트의 bin\Debug 폴더에 있는 LocalizingWpfInWf.exe를 실행합니다. 애플리케이션을 다시 빌드하지 마세요. 다시 빌드하면 위성 어셈블리가 덮어 쓰입니다.

     애플리케이션에서 영어 문자열 대신 지역화된 문자열을 표시합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [응용 프로그램 지역화](how-to-localize-an-application.md)
- [연습: Windows Forms 지역화](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/y99d1cd3(v=vs.100))
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
