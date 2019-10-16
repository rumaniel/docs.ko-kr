---
title: Windows Forms 디자이너의 디자인 타임 오류
ms.date: 09/09/2019
f1_keywords:
- DTELErrorList
- WhyDTELPage
helpviewer_keywords:
- errors [Windows Forms Designer]
- design-time errors [Windows Forms Designer]
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3e2366513183337c3c5dd05ff45f8a6f724deaae
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988436"
---
# <a name="windows-forms-designer-error-page"></a>Windows Forms 디자이너 오류 페이지

코드, 타사 구성 요소 또는 다른 위치에 오류가 발생 하 여 Windows Forms 디자이너 로드 되지 않으면 디자이너 대신 오류 페이지가 표시 됩니다. 이 오류 페이지는 디자이너의 버그를 나타내지는 않습니다. 버그는 코드를 작성 하는 페이지의 어딘가에 있을 수 있습니다. \<이 페이지에는 이름이 >. Designer.cs. 오류는 축소 가능한 노란색 막대로 표시 되 고 코드 페이지에서 오류 위치로 이동할 수 있는 링크가 표시 됩니다.

![Windows Forms 디자이너 오류 페이지](media/windows-forms-designer-error-page-collapsed.png)

오류를 무시 하 고 **무시 및 계속**을 클릭 하 여 디자이너를 계속 로드 하도록 선택할 수 있습니다. 이 동작으로 인해 예기치 않은 동작이 발생할 수 있습니다. 예를 들어 컨트롤이 디자인 화면에 표시 되지 않을 수 있습니다.

## <a name="instances-of-this-error"></a>이 오류의 인스턴스

노란색 오차 막대가 확장 되 면 각 오류 인스턴스가 나열 됩니다. 많은 오류 유형에는 다음 형식의 정확한 위치가 포함 됩니다. *[프로젝트 이름]* *[양식 이름]* 줄: *[줄 번호]* 열: *[열 번호]* . 호출 스택이 오류와 연결 된 경우 **호출 스택 표시** 링크를 클릭 하 여 해당 오류를 볼 수 있습니다. 호출 스택을 검사 하면 오류를 해결 하는 데 도움이 될 수 있습니다.

![Windows Forms 디자이너 확장 된 오류](media/windows-forms-designer-error-page-expanded.png)

> [!NOTE]
>
> - Visual Basic 앱의 경우 디자인 타임 오류 페이지에는 두 개 이상의 오류가 표시 되지 않지만 동일한 오류의 여러 인스턴스가 표시 될 수 있습니다.
> - 앱 C++ 의 경우 오류에 코드 위치 링크가 없습니다.

## <a name="help-with-this-error"></a>이 오류에 대 한 도움말

오류에 대 한 도움말 항목을 사용할 수 있는 경우 **MSDN 도움말** 링크를 클릭 하 여 docs.microsoft.com의 도움말 페이지로 직접 이동 합니다.

## <a name="forum-posts-about-this-error"></a>이 오류에 대한 포럼 게시물

**MSDN 포럼에서이 오류와 관련 된 게시물 검색** 링크를 클릭 하 여 Microsoft Developer Network 포럼으로 이동 합니다. [Windows Forms 디자이너](https://social.msdn.microsoft.com/Forums/windows/home?forum=winformsdesigner) 또는 [Windows Forms](https://social.msdn.microsoft.com/Forums/windows/home?category=windowsforms) 포럼을 구체적으로 검색 하는 것이 좋습니다.

## <a name="design-time-errors"></a>디자인 타임 오류

이 섹션에는 발생할 수 있는 몇 가지 오류가 나열 되어 있습니다.

### <a name="identifier-name-is-not-a-valid-identifier"></a>'\<identifier name > '은 (는) 올바른 식별자가 아닙니다.

이 오류는 필드, 메서드, 이벤트 또는 개체의 이름이 잘못 되었음을 나타냅니다.

### <a name="name-already-exists-in-project-name"></a>' name > '이 (가)\<' project name > '에 이미 있습니다.\<

오류 메시지: "'\<name > '이 (가)\<' project name > '에 이미 있습니다. 고유한 이름을 입력 하십시오. "

프로젝트에 이미 존재 하는 상속 된 폼의 이름을 지정 했습니다. 이 오류를 해결 하려면 상속 된 폼에 고유한 이름을 지정 합니다.

### <a name="toolbox-tab-name-is-not-a-toolbox-category"></a>'\<도구 상자 탭 이름 > '은 (는) 도구 상자 범주가 아닙니다.

타사 디자이너가 존재 하지 않는 도구 상자의 탭에 액세스 하려고 했습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="a-requested-language-parser-is-not-installed"></a>요청한 언어 파서가 설치되어 있지 않습니다.

오류 메시지: "요청 된 언어 파서가 설치 되어 있지 않습니다. 언어 파서 이름은 '{0}'입니다. "

Visual Studio에서 파일 형식에 대해 등록 된 디자이너를 로드 하려고 했지만이를 수행할 수 없습니다. 이는 설치 중에 발생 한 오류 때문일 수 있습니다. 수정에 사용 중인 언어의 공급 업체에 문의 하세요.

### <a name="a-service-required-for-generating-and-parsing-source-code-is-missing"></a>소스 코드를 생성하고 구문 분석하는 데 필요한 서비스가 없습니다.

이는 타사 구성 요소에 대 한 문제입니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="an-exception-occurred-while-trying-to-create-an-instance-of-object-name"></a>'\<개체 이름 > '의 인스턴스를 만드는 동안 예외가 발생 했습니다.

오류 메시지: "'\<개체 이름 > '의 인스턴스를 만드는 동안 예외가 발생 했습니다. "\<Exception string\>" 예외가 발생 했습니다.

타사 디자이너에서 Visual Studio가 개체를 만들지만 오류가 발생 했습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="another-editor-has-document-name-open-in-an-incompatible-mode"></a>다른 편집기의 '\<문서 이름 > '이 (가) 호환 되지 않는 모드로 열려 있습니다.

오류 메시지: "다른 편집기에는\<호환 되지 않는 모드에서 ' 문서 이름 > '이 (가) 열려 있습니다. 편집기를 닫고이 작업을 다시 시도 하십시오. "

다른 편집기에서 이미 열려 있는 파일을 열려고 하는 경우이 오류가 발생 합니다. 파일이 이미 열려 있는 편집기가 표시 됩니다. 이 오류를 해결 하려면 파일이 열려 있는 편집기를 닫은 후 다시 시도 하십시오.

### <a name="another-editor-has-made-changes-to-document-name"></a>다른 편집기가 ' 문서 이름 >\<'을 (를) 변경 했습니다.

변경 내용을 적용 하려면 디자이너를 닫았다가 다시 엽니다. 일반적으로 Visual Studio는 변경을 수행한 후 디자이너를 자동으로 다시 로드 합니다. 그러나 타사 구성 요소 디자이너와 같은 다른 디자이너는 다시 로드 동작을 지원 하지 않을 수 있습니다. 이 경우 Visual Studio에서 디자이너를 닫았다가 다시 열어야 한다는 메시지가 표시 됩니다.

### <a name="another-editor-has-the-file-open-in-an-incompatible-mode"></a>다른 편집기에서 파일이 호환되지 않는 모드로 열려 있습니다.

오류 메시지: "다른 편집기에서 파일이 호환 되지 않는 모드로 열려 있습니다. 편집기를 닫고이 작업을 다시 시도 하십시오. "

이 메시지는 "다른 편집기에서 '\<문서 이름 > '이 (가) 호환 되지 않는 모드로 열려 있습니다."와 유사 하지만 Visual Studio에서 파일 이름을 확인할 수 없습니다. 이 오류를 해결 하려면 파일이 열려 있는 편집기를 닫은 후 다시 시도 하십시오.

### <a name="array-rank-rank-in-array-is-too-high"></a>배열 차수 '\<배열 > '의 차수가 너무 높습니다.

Visual Studio는 디자이너에서 구문 분석 되는 코드 블록에서 단일 차원 배열만 지원 합니다. 다차원 배열은이 영역 외부에서 유효 합니다.

### <a name="assembly-assembly-name-could-not-be-opened"></a>'\<어셈블리 이름 > ' 어셈블리를 열 수 없습니다.

오류 메시지: "어셈블리 '\<어셈블리 이름 > '을 (를) 열 수 없습니다. 파일이 있는지 확인 하십시오. "

이 오류 메시지는 열지 못한 파일을 열려고 할 때 발생 합니다. 파일이 있고 올바른 어셈블리 인지 확인 하십시오.

### <a name="bad-element-type-this-serializer-expects-an-element-of-type-type-name"></a>요소 형식이 잘못 되었습니다. 이 serializer에는 '\<type name > ' 형식의 요소가 필요 합니다.

이는 타사 구성 요소에 대 한 문제입니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="cannot-access-the-visual-studio-toolbox-at-this-time"></a>지금은 Visual Studio 도구 상자에 액세스할 수 없습니다.

Visual Studio에서 사용할 수 없는 도구 상자를 호출 했습니다. 이 오류가 표시 되는 경우이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="cannot-bind-an-event-handler-to-the-event-name-event-because-it-is-read-only"></a>'\<Event name > ' 이벤트는 읽기 전용 이므로이 이벤트에 이벤트 처리기를 바인딩할 수 없습니다.

이 오류는 주로 기본 클래스에서 상속 된 컨트롤에 이벤트를 연결 하려고 할 때 발생 합니다. 컨트롤의 멤버 변수가 private 이면 Visual Studio에서 이벤트를 메서드에 연결할 수 없습니다. 개인적으로 상속 된 컨트롤에는 추가 이벤트를 바인딩할 수 없습니다.

### <a name="cannot-create-a-method-name-for-the-requested-component-because-it-is-not-a-member-of-the-design-container"></a>디자인 컨테이너의 멤버가 아니므로 요청한 구성 요소에 대한 메서드 이름을 만들 수 없습니다.

Visual Studio가 디자이너에 멤버 변수가 없는 구성 요소에 이벤트 처리기를 추가 하려고 했습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="cannot-name-the-object-name-because-it-is-already-named-name"></a>' Name > ' 개체\<의 이름을 이미 ' name > ' (으\<)로 지정 했으므로 이름을 지정할 수 없습니다.

Visual Studio serializer에서 내부 오류가 발생 했습니다. Serializer가 개체의 이름을 두 번 (지원 되지 않음) 시도 했음을 나타냅니다. 이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="cannot-remove-or-destroy-inherited-component-component-name"></a>상속 된 구성 요소 '\<구성 요소 이름 > '을 (를) 제거 하거나 삭제할 수 없습니다.

상속 된 컨트롤은 상속 하는 클래스의 소유권이 있습니다. 상속 된 컨트롤에 대 한 변경 내용은 컨트롤이 시작 되는 클래스에서 이루어져야 합니다. 따라서 이름을 바꾸거나 제거할 수 없습니다.

### <a name="category-toolbox-tab-name-does-not-have-a-tool-for-class-class-name"></a>범주 '\<도구 상자 탭 이름 > '에 '\<클래스 이름 > ' 클래스에 대 한 도구가 없습니다.

디자이너가 특정 도구 상자 탭의 클래스를 참조 하려고 했지만 클래스가 존재 하지 않습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="class-class-name-has-no-matching-constructor"></a>'\<Class name > ' 클래스에 일치 하는 생성자가 없습니다.

타사 디자이너에서 Visual Studio가 존재 하지 않는 생성자의 특정 매개 변수를 사용 하 여 개체를 만들도록 요청 했습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="code-generation-for-property-property-name-failed"></a>'\<속성 이름 > ' 속성에 대 한 코드를 생성 하지 못했습니다.

이는 오류에 대 한 일반 래퍼입니다. 이 메시지와 함께 제공 되는 오류 문자열은 오류 메시지에 대 한 자세한 정보를 제공 하 고 더 구체적인 도움말 항목에 대 한 링크를 제공 합니다. 이 오류를 해결 하려면 오류 메시지에 지정 된 오류를이 오류에 추가 합니다.

### <a name="component-component-name-did-not-call-containeradd-in-its-constructor"></a>'\<Component name > ' 구성 요소가 생성자에서 Container. Add ()를 호출 하지 않았습니다.

이는 방금 로드 했거나 폼에 배치한 구성 요소에서 발생 하는 오류입니다. 이는 구성 요소가 다른 컨트롤 또는 폼 인지 여부와 관계 없이 해당 컨테이너 컨트롤에 구성 요소가 추가 되지 않았음을 나타냅니다. 디자이너는 계속 작동 하지만 런타임에 구성 요소에 문제가 있을 수 있습니다.

오류를 해결 하려면 구성 요소 공급 업체에 문의 하십시오. 또는 만든 구성 요소인 경우 구성 요소의 생성자에서 메서드를 `IContainer.Add` 호출 합니다.

### <a name="component-name-cannot-be-empty"></a>구성 요소 이름은 비워 둘 수 없습니다.

이 오류는 구성 요소를 빈 값으로 변경 하려고 할 때 발생 합니다.

### <a name="could-not-access-the-variable-variable-name-because-it-has-not-been-initialized-yet"></a>'\<Variable name > ' 변수는 아직 초기화 되지 않았으므로 액세스할 수 없습니다.

이 오류는 두 가지 시나리오로 인해 발생할 수 있습니다. 타사 구성 요소 공급 업체에서 배포한 컨트롤이 나 구성 요소에 문제가 있거나 사용자가 작성 한 코드에 구성 요소 간의 재귀 종속성이 있습니다.

이 오류를 해결 하려면 코드에 재귀 종속성이 없는지 확인 합니다. 이러한 문제가 없는 경우 오류 메시지의 정확한 텍스트를 확인 하 고 구성 요소 공급 업체에 문의 하십시오.

### <a name="could-not-find-type-type-name"></a>'\<Type name > ' 형식을 찾을 수 없습니다.

오류 메시지: "'\<Type name > ' 형식을 찾을 수 없습니다. 이 형식을 포함 하는 어셈블리가 참조 되는지 확인 하세요. 이 형식이 개발 프로젝트의 일부인 경우 프로젝트가 성공적으로 빌드 되었는지 확인 합니다. "

참조를 찾을 수 없기 때문에이 오류가 발생 했습니다. 오류 메시지에 지정 된 형식이 참조 되었는지, 그리고 형식에 필요한 모든 어셈블리도 참조 되는지 확인 합니다. 문제는 종종 솔루션의 컨트롤이 빌드되지 않았기 때문입니다. 빌드 하려면 **빌드** 메뉴에서 **솔루션 빌드** 를 선택 합니다. 그렇지 않고 컨트롤이 이미 빌드된 경우 솔루션 탐색기의 **참조** 또는 **종속성** 폴더의 오른쪽 클릭 메뉴에서 수동으로 참조를 추가 합니다.

### <a name="could-not-load-type-type-name"></a>'\<Type name > ' 형식을 로드할 수 없습니다.

오류 메시지: "유형 '\<유형 이름 > '을 (를) 로드할 수 없습니다. 이 형식을 포함 하는 어셈블리가 프로젝트 참조에 추가 되었는지 확인 하십시오. "

Visual Studio에서 이벤트 처리 메서드를 연결 하려고 했으나 해당 메서드에 대 한 매개 변수 형식을 하나 이상 찾을 수 없습니다. 이 문제는 일반적으로 참조 누락으로 인해 발생 합니다. 이 오류를 해결 하려면 형식이 포함 된 참조를 프로젝트에 추가한 후 다시 시도 하십시오.

### <a name="could-not-locate-the-project-item-templates-for-inherited-components"></a>상속된 구성 요소에 대한 프로젝트 항목 템플릿을 찾을 수 없습니다.

Visual Studio에서 상속 된 폼에 대 한 템플릿을 사용할 수 없습니다. 이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="delegate-class-class-name-has-no-invoke-method-is-this-class-a-delegate"></a>대리자 클래스 '\<class name > '에 invoke 메서드가 없습니다. 이 클래스가 대리자 입니까?

Visual Studio에서 이벤트 처리기를 만들려고 했지만 이벤트 형식에 문제가 있습니다. 이 문제는 이벤트가 CLS 규격이 아닌 언어로 생성 된 경우에 발생할 수 있습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="duplicate-declaration-of-member-member-name"></a>'\<Member name > ' 멤버의 선언이 중복 되었습니다.

이 오류는 멤버 변수가 두 번 선언 되었기 때문에 발생 합니다. 예를 들어 라는 `Button1` 두 개의 컨트롤이 코드에서 선언 됩니다. 이름은 상속 된 폼에서 고유 해야 합니다. 또한 이름은 대/소문자만 다를 수 있습니다.

### <a name="error-reading-resources-from-the-resource-file-for-the-culture-culture-name"></a>'\<Culture 이름 > ' 문화권에 대 한 리소스 파일에서 리소스를 읽는 동안 오류가 발생 했습니다.

이 오류는 프로젝트에 잘못 된 .resx 파일이 있는 경우에 발생할 수 있습니다.

이 오류를 해결하려면 다음 단계를 수행합니다.

1. 솔루션과 연결 된 .resx 파일을 보려면 솔루션 탐색기의 **모든 파일 표시** 단추를 클릭 합니다.
2. .Resx 파일을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 선택 하 여 .resx 파일을 XML 편집기에서 로드 합니다.
3. .Resx 파일을 수동으로 편집 하 여 오류를 해결 합니다.

### <a name="error-reading-resources-from-the-resource-file-for-the-default-culture-culture-name"></a>기본 문화권 '\<culture 이름 > '에 대 한 리소스 파일에서 리소스를 읽는 동안 오류가 발생 했습니다.

이 오류는 프로젝트에 기본 문화권에 대 한 잘못 된 .resx 파일이 있는 경우에 발생할 수 있습니다.

이 오류를 해결하려면 다음 단계를 수행합니다.

1. 솔루션과 연결 된 .resx 파일을 보려면 솔루션 탐색기의 **모든 파일 표시** 단추를 클릭 합니다.
2. .Resx 파일을 마우스 오른쪽 단추로 클릭 하 고 **열기**를 선택 하 여 .resx 파일을 XML 편집기에서 로드 합니다.
3. .Resx 파일을 수동으로 편집 하 여 오류를 해결 합니다.

### <a name="failed-to-parse-method-method-name"></a>'\<Method name > ' 메서드를 구문 분석 하지 못했습니다.

오류 메시지: "메서드\<이름 > '을 (를) 구문 분석 하지 못했습니다. 파서에서 다음 오류를 보고 했습니다. '\<오류 문자열 > '. 작업 목록에서 잠재적 오류를 확인 하십시오. "

이는 구문 분석 중에 발생 하는 문제에 대 한 일반적인 오류 메시지입니다. 이러한 오류는 종종 구문 오류로 인해 발생 합니다. 오류와 관련 된 특정 메시지는 작업 목록를 참조 하세요.

### <a name="invalid-component-name-component-name"></a>잘못 된 구성 요소 이름\<: ' 구성 요소 이름 > '

구성 요소의 이름을 해당 언어에 대해 잘못 된 값으로 바꾸려고 했습니다. 이 오류를 해결 하려면 해당 언어에 대 한 명명 규칙을 준수 하도록 구성 요소의 이름을 지정 합니다.

### <a name="the-type-class-name-is-made-of-several-partial-classes-in-the-same-file"></a>'\<Class name > ' 형식은 동일한 파일의 여러 partial 클래스로 구성 되어 있습니다.

[Partial](/dotnet/csharp/language-reference/keywords/partial-type) 키워드를 사용 하 여 여러 파일에 클래스를 정의 하는 경우 각 파일에 하나의 부분 정의만 있을 수 있습니다.

이 오류를 해결 하려면 파일에서 클래스의 부분 정의 중 하나를 제외 하 고 모두 제거 합니다.

### <a name="the-assembly-assembly-name-could-not-be-found"></a>'\<Assembly name > ' 어셈블리를 찾을 수 없습니다.

오류 메시지: "'\<어셈블리 이름 > ' 어셈블리를 찾을 수 없습니다. 어셈블리가 참조 되는지 확인 합니다. 어셈블리가 현재 개발 프로젝트의 일부인 경우 프로젝트가 빌드 되었는지 확인 합니다. "

이 오류는 "유형 '\<유형 이름 > '을 (를) 찾을 수 없습니다."와 유사 하지만이 오류는 일반적으로 메타 데이터 특성 때문에 발생 합니다. 이 오류를 해결 하려면 특성에서 사용 하는 모든 어셈블리가 참조 되는지 확인 합니다.

### <a name="the-assembly-name-assembly-name-is-invalid"></a>어셈블리 이름 '\<어셈블리 이름 > '이 (가) 잘못 되었습니다.

구성 요소가 특정 어셈블리를 요청 했지만 구성 요소에서 제공한 이름이 올바른 어셈블리 이름이 아닙니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-base-class-class-name-cannot-be-designed"></a>'\<Class name > ' 기본 클래스를 디자인할 수 없습니다.

Visual Studio에서 클래스를 로드 했지만 클래스의 구현 자가 디자이너를 제공 하지 않았으므로 클래스를 디자인할 수 없습니다. 클래스가 디자이너를 지 원하는 경우에는 컴파일러 오류와 같이 디자이너에 문제를 표시 하는 데 문제가 발생 하지 않도록 해야 합니다. 또한 클래스에 대 한 모든 참조가 올바르며 모든 클래스 이름의 철자가 올바른지 확인 합니다. 그렇지 않고 클래스를 디자인할 수 없는 경우 코드 뷰에서 편집 합니다.

### <a name="the-base-class-class-name-could-not-be-loaded"></a>기본 클래스 '\<클래스 이름 > '을 (를) 로드할 수 없습니다.

클래스는 프로젝트에서 참조 되지 않으므로 Visual Studio에서 로드할 수 없습니다. 이 오류를 해결 하려면 프로젝트에 클래스에 대 한 참조를 추가 하 고 Windows Forms 디자이너 창을 닫았다가 다시 엽니다.

### <a name="the-class-class-name-cannot-be-designed-in-this-version-of-visual-studio"></a>'\<Class name > ' 클래스는이 버전의 Visual Studio에서 디자인할 수 없습니다.

이 컨트롤 또는 구성 요소에 대 한 디자이너에서 Visual Studio와 동일한 형식을 지원 하지 않습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-class-name-is-not-a-valid-identifier-for-this-language"></a>클래스 이름이 이 언어에 대한 올바른 식별자가 아닙니다.

사용자가 만든 소스 코드의 클래스 이름이 사용 중인 언어에 적합 하지 않습니다. 이 오류를 해결 하려면 언어 요구 사항을 준수 하도록 클래스의 이름을로 합니다.

### <a name="the-component-cannot-be-added-because-it-contains-a-circular-reference-to-reference-name"></a>구성 요소에 '\<reference name > '에 대 한 순환 참조가 포함 되어 있으므로이 구성 요소를 추가할 수 없습니다.

컨트롤 또는 구성 요소를 자체에 추가할 수 없습니다. 이 문제가 발생할 수 있는 또 다른 경우는 Form1의 다른 인스턴스를 만드는 폼 (예: Form1)의 InitializeComponent 메서드에 코드가 있는 경우입니다.

### <a name="the-designer-cannot-be-modified-at-this-time"></a>지금은 디자이너를 수정할 수 없습니다.

편집기의 파일이 읽기 전용으로 표시 되 면이 오류가 발생 합니다. 파일이 읽기 전용으로 표시 되지 않고 응용 프로그램이 실행 되 고 있지 않은지 확인 합니다.

### <a name="the-designer-could-not-be-shown-for-this-file-because-none-of-the-classes-within-it-can-be-designed"></a>이 파일에 디자인할 수 있는 클래스가 없으므로 디자이너에서 이 파일을 표시할 수 없습니다.

이 오류는 Visual Studio에서 디자이너 요구 사항을 충족 하는 기본 클래스를 찾을 수 없을 때 발생 합니다. 폼과 컨트롤은 디자이너를 지 원하는 기본 클래스에서 파생 되어야 합니다. 상속 된 폼 이나 컨트롤에서 파생 하는 경우 프로젝트가 빌드 되었는지 확인 합니다.

### <a name="the-designer-for-base-class-class-name-is-not-installed"></a>기본 클래스 '\<클래스 이름 > '에 대 한 디자이너가 설치 되어 있지 않습니다.

Visual Studio가 클래스에 대 한 디자이너를 로드할 수 없습니다. 이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="the-designer-must-create-an-instance-of-type-type-name-but-it-cant-because-the-type-is-declared-as-abstract"></a>디자이너에서 '\<type name > ' 형식의 인스턴스를 만들어야 하지만 형식이 abstract로 선언 되었으므로 사용할 수 없습니다.

이 오류는 디자이너에 전달 되는 개체의 기본 클래스가 [abstract](/dotnet/csharp/language-reference/keywords/abstract)이므로 허용 되지 않기 때문에 발생 했습니다.

### <a name="the-file-could-not-be-loaded-in-the-designer"></a>파일을 디자이너에 로드할 수 없습니다.

이 파일의 기본 클래스는 디자이너를 지원 하지 않습니다. 해결 방법으로, 코드 뷰를 사용 하 여 파일에 대해 작업을 수행 합니다. 솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 **코드 보기**를 선택 합니다.

### <a name="the-language-for-this-file-does-not-support-the-necessary-code-parsing-and-generation-services"></a>이 파일의 언어는 필요한 코드 구문 분석 및 생성 서비스를 지원하지 않습니다.

오류 메시지: "이 파일의 언어는 필요한 코드 구문 분석 및 생성 서비스를 지원 하지 않습니다. 열려는 파일이 프로젝트의 멤버 인지 확인 한 후 파일을 다시 여십시오. "

이 오류는 대부분 디자이너를 지원 하지 않는 프로젝트에 있는 파일을 여는 경우에 발생할 수 있습니다.

### <a name="the-language-parser-class-class-name-is-not-implemented-properly"></a>'\<Class name > ' 언어 파서 클래스가 제대로 구현 되지 않았습니다.

오류 메시지: "언어 파서 클래스 '\<클래스 이름 > '이 (가) 제대로 구현 되지 않았습니다. 업데이트 된 파서 모듈의 공급 업체에 문의 하세요. "

사용 중인 언어가 올바른 기본 클래스에서 파생 되지 않은 디자이너 클래스를 등록 했습니다. 사용 중인 언어의 공급 업체에 문의 하세요.

### <a name="the-name-name-is-already-used-by-another-object"></a>이름 ' name\<> '은 (는) 다른 개체에서 이미 사용 중입니다.

Visual Studio serializer에서 내부 오류가 발생 했습니다. 이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="the-object-object-name-does-not-implement-the-icomponent-interface"></a>개체 ' 개체\<이름 > '이 (가) IComponent 인터페이스를 구현 하지 않습니다.

Visual Studio에서 구성 요소를 만들려고 했지만 만든 개체가 인터페이스를 <xref:System.ComponentModel.IComponent> 구현 하지 않습니다. 수정 사항은 구성 요소 공급 업체에 문의 하세요.

### <a name="the-object-object-name-returned-null-for-the-property-property-name-but-this-is-not-allowed"></a>'\<Object name > ' 개체는 '\<property name > ' 속성에 대해 null을 반환 했지만이는 허용 되지 않습니다.

항상 개체를 반환 해야 하는 일부 .NET 속성이 있습니다. 예를 들어 폼의 **controls** 컬렉션에는 컨트롤이 없더라도 항상 개체를 반환 해야 합니다.

이 오류를 해결 하려면 오류에 지정 된 속성이 null이 아닌지 확인 하십시오.

### <a name="the-serialization-data-object-is-not-of-the-proper-type"></a>serialization 데이터 개체는 올바른 형식이 아닙니다.

Serializer에서 제공 하는 데이터 개체가 현재 사용 중인 serializer와 일치 하는 형식의 인스턴스가 아닙니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-service-service-name-is-required-but-could-not-be-located"></a>서비스\<이름 > '이 (가) 필요한 데 찾을 수 없습니다.

오류 메시지: "서비스\<이름 > '이 (가) 필요한 데 찾을 수 없습니다. Visual Studio를 설치 하는 데 문제가 있을 수 있습니다. "

Visual Studio에 필요한 서비스를 사용할 수 없습니다. 해당 디자이너를 지원 하지 않는 프로젝트를 로드 하려는 경우 코드 편집기를 사용 하 여 필요한 대로 변경 합니다. 그렇지 않으면이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="the-service-instance-must-derive-from-or-implement-interface-name"></a>서비스 인스턴스는 '\<interface name > '에서 파생 되거나이를 구현 해야 합니다.

이 오류는 구성 요소 또는 구성 요소 디자이너에서 인터페이스와 개체가 필요한 **Addservice** 메서드를 호출 했지만 지정 된 개체가 지정 된 인터페이스를 구현 하지 않음을 나타냅니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-text-in-the-code-window-could-not-be-modified"></a>코드 창의 텍스트를 수정할 수 없습니다.

오류 메시지: "코드 창의 텍스트를 수정할 수 없습니다. 파일이 읽기 전용이 아니고 디스크 공간이 충분 한지 확인 하십시오. "

이 오류는 Visual Studio에서 디스크 공간 또는 메모리 문제로 인해 파일을 편집할 수 없거나 파일이 읽기 전용으로 표시 된 경우에 발생 합니다.

### <a name="the-toolbox-enumerator-object-only-supports-retrieving-one-item-at-a-time"></a>도구 상자 열거자 개체에서는 한 번에 하나의 항목만 검색할 수 있습니다.

이 오류가 표시 되는 경우이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="the-toolbox-item-for-component-name-could-not-be-retrieved-from-the-toolbox"></a>도구 상자에서 '\<component name > '에 대 한 도구 상자 항목을 검색할 수 없습니다.

오류 메시지: "'\<Component name > '에 대 한 도구 상자 항목을 도구 상자에서 검색할 수 없습니다. 도구 상자 항목이 포함 된 어셈블리가 제대로 설치 되었는지 확인 합니다. 도구 상자 항목에서 다음 오류가 \<발생 했습니다. 오류 문자열 >. "

해당 구성 요소에서 Visual Studio에 액세스할 때 예외를 throw 했습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-toolbox-item-for-toolbox-item-name-could-not-be-retrieved-from-the-toolbox"></a>도구 상자에서 '\<도구 상자 항목 이름 > '에 대 한 도구 상자 항목을 검색할 수 없습니다.

오류 메시지: "도구 상자에서 '\<도구 상자 항목 이름 > '에 대 한 도구 상자 항목을 검색할 수 없습니다. 도구 상자에서 항목을 제거 하 고 다시 추가 해 보세요. "

이 오류는 도구 상자 항목 내의 데이터가 손상 되거나 구성 요소의 버전이 변경 된 경우에 발생 합니다. 도구 상자에서 항목을 제거 하 고 다시 추가 해 보세요.

### <a name="the-type-type-name-could-not-be-found"></a>'\<Type name > ' 형식을 찾을 수 없습니다.

오류 메시지: "'\<Type name > ' 형식을 찾을 수 없습니다. 형식을 포함 하는 어셈블리가 참조 되는지 확인 합니다. 어셈블리가 현재 개발 프로젝트의 일부인 경우 프로젝트가 빌드 되었는지 확인 합니다. "

디자이너를 로드 하는 동안 Visual Studio에서 형식을 찾지 못했습니다. 형식을 포함 하는 어셈블리가 참조 되는지 확인 합니다. 어셈블리가 현재 개발 프로젝트의 일부인 경우 프로젝트가 빌드 되었는지 확인 합니다.

### <a name="the-type-resolution-service-may-only-be-called-from-the-main-application-thread"></a>형식 확인 서비스는 기본 응용 프로그램 스레드에서만 호출할 수 있습니다.

Visual Studio에서 잘못 된 스레드의 필요한 리소스에 액세스 하려고 했습니다. 이 오류는 디자이너를 만드는 데 사용 된 코드가 주 응용 프로그램 스레드가 아닌 다른 스레드에서 형식 확인 서비스를 호출한 경우에 표시 됩니다. 이 오류를 해결 하려면 올바른 스레드에서 서비스를 호출 하거나 구성 요소 공급 업체에 문의 하십시오.

### <a name="the-variable-variable-name-is-either-undeclared-or-was-never-assigned"></a>'\<Variable name > ' 변수의 선언 되지 않았거나 할당 되지 않았습니다.

소스 코드에는 선언 되거나 할당 되지 않은 **Button1**과 같은 변수에 대 한 참조가 있습니다. 변수가 할당 되지 않은 경우이 메시지는 오류가 아니라 경고로 표시 됩니다.

### <a name="there-is-already-a-command-handler-for-the-menu-command-menu-command-name"></a>메뉴 명령 '\<메뉴 명령 이름 > '에 대 한 명령 처리기가 이미 있습니다.

이 오류는 타사 디자이너가 이미 명령 테이블에 처리기가 있는 명령을 추가 하는 경우에 발생 합니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="there-is-already-a-component-named-component-name"></a>'\<Component name > ' (이) 라는 구성 요소가 이미 있습니다.

오류 메시지: "'\<Component name > ' (이) 라는 구성 요소가 이미 있습니다. 구성 요소에는 고유한 이름이 있어야 하 고 이름은 대/소문자를 구분 하지 않아야 합니다. 또한 이름은 상속 된 클래스의 구성 요소 이름과 충돌 하지 않습니다. "

이 오류 메시지는 속성 창 구성 요소의 이름이 변경 된 경우에 발생 합니다. 이 오류를 해결 하려면 모든 구성 요소 이름이 고유 하 고 대/소문자를 구분 하지 않으며 상속 된 클래스의 구성 요소 이름과 충돌 하지 않는지 확인 합니다.

### <a name="there-is-already-a-toolbox-item-creator-registered-for-the-format-format-name"></a>'\<Format name > ' 형식에 대 한 도구 상자 항목 작성자가 이미 등록 되어 있습니다.

타사 구성 요소에서 도구 상자 탭의 항목에 대해 콜백을 수행 했지만 항목에 이미 콜백이 포함 되어 있습니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="this-language-engine-does-not-support-a-codemodel-with-which-to-load-a-designer"></a>이 언어 엔진에서 디자이너를 로드할 수 있는 CodeModel을 지원하지 않습니다.

이 메시지는 "이 파일의 언어는 필요한 코드 구문 분석 및 생성 서비스를 지원 하지 않습니다."와 유사 하지만이 메시지는 내부 등록 문제를 포함 합니다. 이 오류가 표시 되는 경우이 오류가 표시 되 면 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)를 사용 하 여 문제를 기록 하세요.

### <a name="type-type-name-does-not-have-a-constructor-with-parameters-of-types-parameter-type-names"></a>' Type name\>' 형식에 '\<매개 변수 형식 이름 > ' 형식의 매개 변수를 사용 하는 생성자가 없습니다.\<

Visual Studio에서 일치 하는 매개 변수가 있는 [생성자](/dotnet/csharp/programming-guide/classes-and-structs/constructors) 를 찾을 수 없습니다. 이는 필요한 것 이외의 형식으로 생성자를 제공한 결과일 수 있습니다. 예를 들어 **Point** 생성자는 두 개의 정수를 사용할 수 있습니다. Float를 제공한 경우이 오류가 발생 합니다.

이 오류를 해결 하려면 다른 생성자를 사용 하거나 생성자가 제공 하는 것과 일치 하도록 매개 변수 형식을 명시적으로 캐스팅 합니다.

### <a name="unable-to-add-reference-reference-name-to-the-current-application"></a>현재 응용 프로그램에 참조\<' 참조 이름 > '을 (를) 추가할 수 없습니다.

오류 메시지: "참조 '\<참조 이름 > '을 현재 응용 프로그램에 추가할 수 없습니다. 다른 버전의 '\<참조 이름 > '이 (가) 이미 참조 되지 않았는지 확인 하십시오. "

Visual Studio에서 참조를 추가할 수 없습니다. 이 오류를 해결 하려면 다른 버전의 참조가 이미 참조 되지 않았는지 확인 합니다.

### <a name="unable-to-check-out-the-current-file"></a>현재 파일을 체크 아웃할 수 없습니다.

오류 메시지: "현재 파일을 체크 아웃할 수 없습니다. 파일이 잠겨 있거나 파일을 수동으로 체크 아웃 해야 할 수 있습니다. "

이 오류는 현재 소스 코드 제어에 체크 인 된 파일을 변경할 때 발생 합니다. 일반적으로 Visual Studio는 사용자가 파일을 체크 아웃할 수 있도록 파일 체크 아웃 대화 상자를 표시 합니다. 이번에는 체크 아웃 중 병합 충돌 때문에 파일이 체크 아웃 되지 않았습니다. 이 오류를 해결 하려면 파일이 잠겨 있지 않은지 확인 한 후 파일을 수동으로 체크 아웃 하십시오.

### <a name="unable-to-find-page-named-options-dialog-box-tab-name"></a>'\<Options 대화 상자 탭 이름 > ' 페이지를 찾을 수 없습니다.

이 오류는 존재 하지 않는 이름을 사용 하 여 구성 요소 디자이너에서 옵션 대화 상자에 있는 페이지에 대 한 액세스를 요청할 때 발생 합니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="unable-to-find-property-property-name-on-page-options-dialog-box-tab-name"></a>페이지의\<옵션대화상자 탭 이름 > '에서 속성 ' 속성 이름 > '을 (를) 찾을 수 없음\<

이 오류는 구성 요소 디자이너에서 옵션 대화 상자에 있는 페이지의 특정 값에 대 한 액세스를 요청 하지만 해당 값이 존재 하지 않을 때 발생 합니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="visual-studio-cannot-open-a-designer-for-the-file-because-the-class-within-it-does-not-inherit-from-a-class-that-can-be-visually-designed"></a>파일 내부에 있는 클래스가 시각적으로 디자인할 수 있는 클래스에서 상속되지 않으므로 Visual Studio에서 해당 파일에 대한 디자이너를 열 수 없습니다.

Visual Studio에서 클래스를 로드했는데 해당 클래스의 디자이너는 로드할 수 없습니다. Visual Studio를 사용 하려면 디자이너에서 파일의 첫 번째 클래스를 사용 해야 합니다. 이 오류를 해결 하려면 클래스 코드를 파일의 첫 번째 클래스로 이동한 후 디자이너를 다시 로드 합니다.

### <a name="visual-studio-cannot-save-or-load-instances-of-the-type-type-name"></a>Visual Studio에서 '\<type name > ' 형식의 인스턴스를 저장 하거나 로드할 수 없습니다.

이는 타사 구성 요소에 대 한 문제입니다. 구성 요소 공급 업체에 문의 하십시오.

### <a name="visual-studio-is-unable-to-open-document-name-in-design-view"></a>Visual Studio가 디자인 뷰에서 '\<문서 이름 > '을 (를) 열 수 없습니다.

오류 메시지: "디자인 뷰에서 Visual Studio가 '\<문서 이름 > '을 (를) 열 수 없습니다. 파일 형식에 대 한 파서가 설치 되어 있지 않습니다. "

이 오류는 프로젝트의 언어가 디자이너를 지원 하지 않고 파일 열기 대화 상자에서 또는 솔루션 탐색기에서 파일을 열려고 할 때 발생 함을 나타냅니다. 대신 코드 보기에서 파일을 편집 합니다.

### <a name="visual-studio-was-unable-to-find-a-designer-for-classes-of-type-type-name"></a>Visual Studio에서 '\<type name > ' 형식의 클래스에 대 한 디자이너를 찾을 수 없습니다.

Visual Studio에서 클래스를 로드 했지만 클래스를 디자인할 수 없습니다. 대신 클래스를 마우스 오른쪽 단추로 클릭 하 고 **코드 보기**를 선택 하 여 코드 뷰에서 클래스를 편집 합니다.

## <a name="see-also"></a>참고자료

- [디자이너를 사용 하 여 Windows Forms 컨트롤 개발](developing-windows-forms-controls-at-design-time.md)
- [Windows Forms 디자이너 포럼](https://social.msdn.microsoft.com/Forums/windows/home?forum=winformsdesigner)
