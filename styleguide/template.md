---
title:
- 문서 제목
description: ''
author:
- GITHUB USERNAME
ms.author:
- MICROSOFT ALIAS OF INTERNAL OWNER
ms.date:
- CREATION/UPDATE DATE - MM/dd/yyyy
ms.topic:
- TOPIC TYPE
ms.prod:
- PRODUCT VALUE
helpviewer_keywords:
- OFFLINE BOOK INDEX ENTRIES
ms.openlocfilehash: 3674508c25e9a4b166f994e7ca16df04e484956b
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306357"
---
# <a name="metadata-and-markdown-template"></a>메타데이터 및 Markdown 템플릿

이 dotnet/docs 템플릿에는 Markdown 구문의 예제와 메타데이터 설정 지침이 포함되어 있습니다. 이 템플릿을 최대한 활용하려면 [원시 Markdown](https://raw.githubusercontent.com/dotnet/docs/master/styleguide/template.md) 및 [렌더링된 보기](https://github.com/dotnet/docs/blob/master/styleguide/template.md)를 모두 확인해야 합니다. 예를 들어 원시 Markdown에는 메타데이터 블록이 표시되는 반면 렌더링된 보기에는 표시되지 않습니다.

Markdown 파일을 만들 때는 이 템플릿을 새 파일로 복사하고, 아래에 지정되어 있는 것처럼 메타데이터를 입력하고, 위의 H1 제목을 문서 제목으로 설정한 다음 내용을 삭제해야 합니다.

## <a name="metadata"></a>Metadata

위의 [원시 Markdown](https://raw.githubusercontent.com/dotnet/docs/master/styleguide/template.md)에는 전체 메타데이터 블록이 필수 필드와 선택적 필드로 구분되어 나와 있습니다. 몇 가지 주요 참고 사항은 다음과 같습니다.

- 메타데이터 요소의 값과 콜론(:) 사이에는 공백이 **있어야 합니다**.
- 선택적 메타데이터 요소에 값이 없으면 #으로 요소를 주석으로 처리하거나 제거합니다(공백으로 두거나 “na”를 사용하지 않음). 주석 처리된 요소에 값을 추가하는 경우 #을 제거해야 합니다.
- 제목 등의 값에 콜론이 포함되어 있으면 메타데이터 파서가 중단됩니다. 이 경우 `title: "Writing .NET Core console apps: An advanced step-by-step guide"`와 같이 큰따옴표를 사용하여 제목을 묶습니다.
- **title**: 검색 엔진 결과에 표시됩니다. 제목(title)은 H1 제목(heading)의 제목(title)과 같을 필요는 없으며 60자 이내로 작성해야 합니다.
- **설명**: 문서의 내용을 요약합니다. 일반적으로 검색 결과 페이지에 표시되지만 검색 순위에는 사용되지 않습니다. 길이는 공백을 포함하여 115~145자여야 합니다.
- **author** 및 **ms.author**: author 필드는 작성자의 별칭이 아닌 **GitHub 사용자 이름**을 포함해야 합니다.  반면 **ms.author** 필드에서는 Microsoft 별칭을 포함해야 하며, 문서 유지 관리를 담당하는 개인을 표시합니다.
- **ms.topic**: 토픽 유형입니다. 가장 일반적인 값은 `conceptual`이고 전역 수준에서 설정됩니다. 기타 일반적으로 사용되는 값은 `tutorial`, `overview` 및 `reference`입니다.
- **ms.devlang**에서는 토픽에 대해 표시된 언어 필터를 정의합니다. 지원되는 값 목록은 [지원되는 언어](#supported-languages) 섹션에서 확인할 수 있습니다. 토픽에 포함된 프로그래밍 언어가 둘 이상 있는 경우에만 설정해야 합니다. 일반적으로 당사의 콘텐츠에서는 이 값으로 `csharp`, `vb`, `fsharp` 및 `cpp`만 사용합니다.
- **ms.prod**: BI 용도로 사용되는 제품 ID입니다. 이 ID는 일반적으로 전역 수준에서 설정되므로 대개 각 문서의 메타데이터 블록에 표시되지 않습니다.
- **ms.technology**: 추가 BI 분류. 지원되는 일부 값은 C# 토픽의 경우 `devlang-csharp`이고, F# 토픽의 경우 `devlang-fsharp`이며, VB 토픽의 경우 `devlang-visual-basic`입니다. 다른 가이드의 경우 값이 다를 수 있으므로 팀 멤버에게 문의하여 지침을 확인하세요.
- **ms.date**: YYYY/MM/DD 형식의 날짜입니다. 게시된 페이지에 표시되어 마지막으로 문서가 대폭 편집되었거나 확실히 “새로 고침”(즉, 문서가 검토되었고 최신 상태라고 간주됨)된 시간을 나타냅니다.
- **helpviewer_keywords**: 항목은 오프라인 서적 색인(Visual Studio의 기능)에 사용됩니다.
- **f1_keywords**: 문서를 F1 키(Visual Studio의 기능)에 연결합니다.

## <a name="basic-markdown-gfm-and-special-characters"></a>기본 Markdown, GFM 및 특수 문자

모든 기본 및 GFM(GitHub Flavored Markdown)이 지원되는 것은 아닙니다. 여기에 대한 자세한 내용은 다음 항목을 참조하세요.

- [기준 Markdown 구문](https://daringfireball.net/projects/markdown/syntax)
- [GFM 설명서](https://guides.github.com/features/mastering-markdown)

Markdown은 서식 지정을 위해 \*, \`, \# 등의 특수 문자를 사용합니다. 이러한 문자 중 하나를 내용에 포함하려는 경우에는 다음 두 작업 중 하나를 수행해야 합니다.

- 특수 문자 앞에 백슬래시를 넣어 특수 문자를 "이스케이프"합니다(예: \*의 경우 `\*`)
- 문자의 [HTML 엔터티 코드](https://www.ascii.cl/htmlcodes.htm)를 사용합니다(예: &#42;의 경우 `&#42;`).

## <a name="file-name"></a>파일 이름

파일 이름은 다음 규칙을 사용합니다.

- 소문자, 숫자 및 하이픈만 포함할 수 있습니다.
- 공백 또는 문장 부호 문자는 포함할 수 없습니다. 하이픈을 사용하여 파일 이름의 단어와 숫자를 구분합니다.
- 개발, 구매, 빌드, 문제 해결 등의 구체적인 작업 동사를 사용합니다. 현재 진행형 단어는 사용하지 않습니다.
- 한, 및, 그, 내, 또는 등의 군더더기로 간주되는 단어는 가급적 사용하지 않습니다.
- Markdown 파일 및 .md 파일 확장명을 사용해야 합니다.
- 파일 이름은 비교적 짧게 유지합니다. 문서의 URL에 파일 이름이 포함되기 때문입니다.

## <a name="headings"></a>제목

문장 스타일 대/소문자를 사용합니다. 항상 제목의 첫 번째 단어를 대문자로 표시하고, 제목에서 콜론 뒤에 오는 단어(예: "방법: 배열 정렬")는 대문자로 표시하지 않습니다.

제목은 atx 스타일로 작성해야 합니다. 즉, 줄 시작 부분에서 HTML 제목 수준 H1~H6에 해당하는 1~6개의 해시 문자(#)를 사용하여 제목을 나타냅니다. 위에서는 수준 1/수준 2 헤더의 예가 사용되었습니다.

항목에는 수준 1 제목(H1)이 **하나만** 있어야 합니다. 이 제목이 페이지의 제목으로 표시됩니다.

제목이 `#` 문자로 끝나는 경우에는 제목이 올바르게 렌더링되도록 끝에 여분의 `#` 문자를 추가해야 합니다. 예: `# Async Programming in F# #`.

수준 2 제목은 페이지 제목 아래의 "문서 내용" 섹션에 표시되는 페이지 TOC를 생성합니다.

### <a name="third-level-heading"></a>수준 3 제목
#### <a name="fourth-level-heading"></a>수준 4 제목
##### <a name="fifth-level-heading"></a>수준 5 제목
###### <a name="sixth-level-heading"></a>수준 6 제목

## <a name="text-styling"></a>텍스트 스타일 지정

*기울임꼴* 파일, 폴더, 경로(긴 항목의 경우 자체 줄로 분할), 새 용어에 사용됩니다.

**굵은 글씨체** UI 요소에 사용됩니다.

`Code` 인라인 코드, 언어 키워드, NuGet 패키지 이름, 명령줄 명령, 데이터베이스 테이블 및 열 이름, 클릭할 수 없게 하려는 URL 등에 사용합니다.

## <a name="links"></a>링크

### <a name="internal-links"></a>내부 링크

같은 Markdown 파일의 헤더(앵커 링크라고도 함)에 연결하려면 연결할 헤더의 ID를 확인해야 합니다. ID를 확인하려면 렌더링된 문서의 소스를 확인하여 헤더의 ID(예: `id="blockquote"`)를 찾은 다음 `#blockquote`와 같이 # + ID를 사용하여 연결합니다.
ID는 헤더 텍스트에 따라 자동 생성됩니다. 예를 들어 이름이 `## Step 2`인 고유 섹션의 경우 ID는 `id="step-2"`입니다.

- 예: `[Declare inline blocks with a language identifier](#inline-code-blocks-with-language-identifier)`에서 [언어 식별자를 사용하여 인라인 블록 선언](#inline-code-blocks-with-language-identifier)을 생성합니다.

같은 리포지토리의 Markdown 파일에 연결하려면 파일 이름 끝의 ".md"를 포함한 [상대 링크](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)를 사용합니다.

- 예: `[Readme file](../README.md)`에서 [Readme 파일](../README.md)을 생성합니다. (링크는 대/소문자를 구분합니다.)
- 예: `[Welcome to .NET](../docs/welcome.md)`에서 [.NET 시작](../docs/welcome.md)을 생성합니다.

같은 리포지토리에 있는 Markdown 파일의 헤더에 연결하려면 상대 링크 + 해시 태그 링크를 사용합니다.

- 예: `[.NET Community](../docs/welcome.md#open-source)`에서 [.NET Community](../docs/welcome.md#open-source)를 생성합니다.

대부분의 경우에는 상대 링크가 GitHub의 소스에서 확인되므로 상대 링크를 사용하고 링크에서 `~/` 사용을 억제합니다. 그러나 종속 리포지토리의 파일에 연결할 때마다 `~/` 문자를 사용하여 경로를 제공합니다. 종속 리포지토리의 파일은 GitHub에서 다른 위치에 있으므로 링크 작성 방법과 관계없이 상대 링크를 사용하여 링크가 제대로 확인되지 않습니다.

C# 언어 사양 및 Visual Basic 언어 사양은 언어 리포지토리의 소스를 포함하여 . NET 문서에 포함되어 있습니다. Markdown 소스는 [csharplang](https://github.com/dotnet/csharplang) 및 [visual basic](https://github.com/dotnet/vblang) 리포지토리에서 관리합니다.

사양에 대한 링크는 해당 사양이 포함된 소스 디렉터리를 가리켜야 합니다. C#의 경우 **~/_csharplang/spec**이고 VB의 경우 **~/_vblang/spec**입니다.

- 예: `[C# Query Expressions](~/_csharplang/spec/expressions.md#query-expressions)`에서는 [C# 쿼리 식](~/_csharplang/spec/expressions.md#query-expressions)을 생성합니다.

### <a name="external-links"></a>외부 링크

외부 파일에 연결하려면 링크로 전체 URL을 사용합니다.

- 예: `[GitHub](https://www.github.com)`에서는 [GitHub](https://www.github.com)를 생성합니다.

URL은 Markdown 파일에 표시되는 경우 클릭 가능한 링크로 변환됩니다.

- 예: `<https://www.github.com>`에서는 <https://www.github.com>을 생성합니다.

외부 링크의 경우 `https` 프로토콜을 사용하는 것이 좋습니다. `https`를 지원하지 않는 사이트에만 `http` 링크를 사용합니다.

### <a name="links-to-apis"></a>API에 대한 링크

빌드 시스템에는 외부 링크를 사용하지 않고도 .NET API에 연결할 수 있는 몇 가지 확장이 포함되어 있습니다.
API에 연결할 때는 소스 코드에서 자동 생성되는 해당 UID(고유 식별자)를 사용할 수 있습니다.

UID는 정규화된 형식 및 멤버 이름과 동일합니다.

UID 뒤에 \*(또는 %2A)를 추가하는 경우 링크는 특정 API가 아니라 오버로드 페이지를 나타냅니다. 예를 들어 [List\<T>.BinarySearch(T, IComparer\<T>)](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1.binarysearch#System_Collections_Generic_List_1_BinarySearch__0_)와 같은 특정 오버로드 대신 일반적인 방식으로 [List\<T>.BinarySearch Method](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1.binarysearch) 페이지를 연결하려고 할 때 사용할 수 있습니다. 멤버가 오버로드되지 않은 경우 멤버 페이지에 연결하는 데 \*도 사용할 수 있습니다. 그러면 UID에 매개 변수 목록을 포함할 필요가 없습니다.

특정 메서드 오버로드에 연결하려면 메서드의 매개 변수마다 정규화된 형식 이름을 포함해야 합니다. 예를 들어, \<xref:System.DateTime.ToString>을 통해서는 매개 변수가 없는 [DateTime.ToString](https://docs.microsoft.com/dotnet/api/system.datetime.tostring#System_DateTime_ToString) 메서드에 연결하는 반면, \<xref:System.DateTime.ToString(System.String,System.IFormatProvider)>를 통해서는 [DateTime.ToString(String,IFormatProvider)](https://docs.microsoft.com/dotnet/api/system.datetime.tostring#System_DateTime_ToString_System_String_System_IFormatProvider_) 메서드에 연결합니다. `https://xref.docs.microsoft.com/autocomplete`에서 오버로드된 특정 멤버의 UID를 찾을 수 있습니다. 쿼리 문자열 “?text= *\<type-member-name>* ”을 통해서는 확인할 UID가 있는 멤버 또는 형식을 식별합니다. 예를 들어, `https://xref.docs.microsoft.com/autocomplete?text=string.format`에서는 [String.Format](https://docs.microsoft.com/dotnet/api/system.string.format) 오버로드를 검색합니다.

[System.Collections.Generic.List\<T>](https://docs.microsoft.com/dotnet/api/system.collections.generic.list-1)와 같은 제네릭 형식에 연결하려면 ` (%60) 문자 다음에 제네릭 형식 매개 변수의 수를 사용합니다. 예를 들어, \<xref:System.Nullable%601>에서는 [System.Nullable\<T>](https://docs.microsoft.com/dotnet/api/system.nullable-1) 형식에 연결하는 반면 \<xref:System.Func%602>에서는 [System.Func\<T,TResult>](https://docs.microsoft.com/dotnet/api/system.func-2) 대리자에 연결합니다.

다음 구문 중 하나를 사용할 수 있습니다.

1. 자동 연결: `<xref:UID>` 또는 `<xref:UID?displayProperty=nameWithType>`

   `displayProperty` 쿼리 매개 변수를 통해서는 정규화된 링크 텍스트를 생성합니다. 기본적으로 링크 텍스트는 멤버 또는 형식 이름만 표시합니다.

2. Markdown 링크: `[link text](xref:UID)`

   표시되는 링크 텍스트를 사용자 지정하려는 경우에 사용합니다.

예:

- `<xref:System.String>`은 [문자열](https://docs.microsoft.com/dotnet/api/system.string)로 렌더링
- `<xref:System.String?displayProperty=nameWithType>`은 [System.String](https://docs.microsoft.com/dotnet/api/system.string)으로 렌더링
- `[String class](xref:System.String)`은 [문자열 클래스](https://docs.microsoft.com/dotnet/api/system.string)로 렌더링

이 표기법을 사용하는 방법에 대한 자세한 내용은 [상호 참조 사용](https://dotnet.github.io/docfx/tutorial/links_and_cross_references.html#using-cross-reference)을 참조하세요.

UID를 찾는 방법에는 두 가지가 있습니다.

- 연결하려는 API 페이지의 소스를 확인하고 assetid 값을 찾습니다. 개별 오버로드 값은 소스에 표시되지 않습니다.
- 다음 도구를 사용하여 UID 검색 https://xref.docs.microsoft.com/autocomplete?text=tostring (tostring을 사용자가 찾으려는 API 이름의 일부로 대체). 이 도구를 통해서는 UID 부분에서 제공된 `text` 쿼리 매개 변수를 검색합니다. 예를 들어, 멤버 이름(ToString), 부분 멤버 이름(ToStri), 형식 및 멤버 이름(Double.ToString) 등을 검색할 수 있습니다.

UID에 특수 문자 \`, \# 또는 \*가 포함된 경우 UID 값은 각각 `%60`, `%23` 및 `%2A`로 인코딩된 HTML이어야 합니다. 때때로 괄호가 인코딩된 것을 볼 수 있지만, 요구 사항은 아닙니다.

예:

- System.Threading.Tasks.Task\`1은 `System.Threading.Tasks.Task%601`이 됨
- System.Exception.\#ctor은 `System.Exception.%23ctor`이 됨
- System.Lazy\`1.\#ctor(System.Threading.LazyThreadSafetyMode)은 `System.Lazy%601.%23ctor%28System.Threading.LazyThreadSafetyMode%29`가 됨

## <a name="lists"></a>목록

### <a name="ordered-lists"></a>순서가 지정된 목록

1. This
1. 예
1. 입니다.
1. Ordered
1. 목록

#### <a name="ordered-list-with-an-embedded-list"></a>포함된 목록이 있는 순서가 지정된 목록

1. 여기
1. 에
1. an
1. 포함된
    1. Miss Scarlett
    1. Professor Plum
1. ordered
1. list

### <a name="unordered-lists"></a>순서가 지정되지 않은 목록

- This
- is
- a
- 글머리 기호
- list

#### <a name="unordered-list-with-an-embedded-list"></a>포함된 목록이 있는 순서가 지정되지 않은 목록

- This
- 글머리 기호
- list
  - 유유진
  - 주준서
- 포함
- 기타
  1. 유현기 대령
  1. 안예은
- 목록

## <a name="horizontal-rule"></a>가로줄

---

## <a name="tables"></a>Tables

| Tables        | 멋진           | 표  |
| ------------- |:-------------:| -----:|
| 3열은      | 오른쪽 맞춤 | $1600 |
| 2열은      | 가운데 맞춤      |   $12 |
| 1열은 기본값 | 왼쪽 맞춤     |    $1 |

[Markdown 테이블 생성기 도구](https://www.tablesgenerator.com/markdown_tables)를 사용하면 테이블을 보다 쉽게 만들 수 있습니다.

## <a name="code"></a>코드

코드를 포함하는 가장 효율적인 방법은 작동하는 샘플의 조각을 포함하는 것입니다. [지원 가이드](../CONTRIBUTING.md#contributing-to-samples)의 지침에 따라 샘플을 만들 수 있습니다.

다음 구문을 사용하여 코드를 포함할 수 있습니다.

```markdown
[!code-<language>[<name>](<pathToFile><queryoption><queryoptionvalue>)]
```

- `-<language>`(*선택 사항*이지만 *권장됨*)
  - 참조되는 코드 조각의 언어입니다. 지원되는 값 목록은 [지원되는 언어](#supported-languages)를 참조하세요.

- `<name>`(*선택 사항*)
  - 코드 조각의 이름입니다. 출력 HTML에는 영향을 주지 않지만 이를 사용하여 Markdown 소스에 대한 가독성을 높일 수 있습니다.

- `<pathToFile>`(*필수*)
  - 참조할 코드 조각 파일을 나타내는 파일 시스템의 상대 경로입니다.

- `<queryoption>` 및 `<queryoptionvalue>`(*선택 사항*)
  - 파일에서 코드를 검색하는 방법을 지정하는 데 함께 사용됩니다.
    - `#`:  `#L{startlinenumber}-L{endlinenumber}`(줄 범위) *또는* `#{tagname}`(태그 이름).
    하지만 줄 번호는 변경되기 쉬우므로 사용하지 않는 것이 좋습니다. 태그 이름은 코드 조각을 참조하는 기본 방법입니다.
    - `range`: `?range=1,3-5` 줄의 범위입니다. 이 예에는 줄 1, 3, 4 및 5가 포함됩니다.
    - `dedent`: `?dedent=8` 공백 수(이 경우 8)만큼 줄 들여쓰기를 취소합니다. 이는 `range` 및 파일 줄의 하위 집합을 선택하는 기타 쿼리 옵션과 결합할 수 있습니다.
    - `outdent`: `?outdent=8` 공백 수(이 경우 8)만큼 줄 들여쓰기를 뒤바꿉니다. 이는 `range` 및 파일 줄의 하위 집합을 선택하는 기타 쿼리 옵션과 결합할 수 있습니다.

가능하면 태그 이름 옵션을 사용하는 것이 좋습니다. 태그 이름은 소스 코드에 있는 `Snippettagname` 형식의 코드 주석 또는 지역 이름입니다. 다음 예제에서는 태그 이름 `1`을 참조하는 방법을 보여줍니다.

```markdown
[!code-csharp[csrefKeyword#1](../../../../samples/snippets/csharp/language-reference/keywords/throw/throw-1.cs#1)]
```

[이 소스 파일](https://github.com/dotnet/samples/blob/master/snippets/csharp/language-reference/keywords/throw/throw-1.cs)에서 코드 조각 태그가 구성된 방식을 확인할 수 있습니다. 언어별 코드 조각 소스 파일의 태그 이름 표현에 관한 자세한 내용은 [DocFX 지침](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html#tag-name-representation-in-code-snippet-source-file)을 참조하세요.

전체 프로그램의 조각을 포함하면 모든 코드가 Microsoft CI(연속 통합) 시스템을 통해 실행됩니다. 그러나 컴파일 시간 또는 런타임 오류를 발생시키는 항목을 표시해야 하는 경우 인라인 코드 블록을 사용할 수 있습니다.

### <a name="inline-code-blocks-with-language-identifier"></a>언어 식별자가 포함된 인라인 코드 블록

3개의 backtick(\`\`\`) + 언어 ID를 사용항여 코드 블록에 언어별 색 코딩을 적용합니다. 다음은 지원되는 언어 목록으로, 각 언어 ID의 markdown 레이블을 표시합니다.

#### <a name="supported-languages"></a>지원되는 언어

|name|Markdown 레이블|
|-----|-------|
|.NET 콘솔|dotnetcli|
|ASP.NET(C#)|aspx-csharp|
|ASP.NET(VB)|aspx-vb|
|Azure CLI|azurecli|
|AzCopy|azcopy|
|Azure PowerShell|azurepowershell|
|Bash|bash|
|C++|cpp|
|C++/CX|cppcx|
|C++/WinRT|cppwinrt|
|C#|c샵|
|브라우저의 C#|csharp-interactive|
|Console|콘솔|
|CSHTML|cshtml|
|DAX|dax|
|Dockerfile|dockerfile|
|F#|fsharp|
|이동|이동|
|HTML|html|
|HTTP|http|
|Java|java|
|JavaScript|javascript|
|JSON|json :|
|Kusto 쿼리 언어|kusto|
|Markdown|md|
|NodeJS|nodejs|
|Objective-C|objc|
|OData|odata|
|PHP|php|
|PowerApps(점 소수 구분 기호)|powerapps-dot|
|PowerApps(쉼표 소수 구분 기호)|powerapps-comma|
|PowerShell|powershell|
|Python|python|
|Q#|qsharp|
|R|r|
|Ruby|ruby|
|SQL|sql|
|Swift|swift|
|TypeScript|typescript|
|Visual Basic|vb|
|VBScript|vbscript|
|XAML|xaml|
|XML|Xml|

`csharp-interactive` 이름은 C# 언어를 지정하고 브라우저에서 샘플을 실행하는 기능을 지정합니다. 해당 코드 조각은 Docker 컨테이너에서 컴파일되고 실행되며, 해당 프로그램의 실행 결과는 사용자의 브라우저 창에 표시됩니다.

다음은 C#(\`\`\`csharp), Python(\`\`\`python) 및 PowerShell(\`\`\`powershell)의 언어 ID를 사용하는 코드 블록의 예입니다.

##### <a name="c9839"></a>C&#9839;

```csharp
using System;
namespace HelloWorld
{
    class Hello
    {
        static void Main()
        {
            Console.WriteLine("Hello World!");

            // Keep the console window open in debug mode.
            Console.WriteLine("Press any key to exit.");
            Console.ReadKey();
        }
    }
}
```

#### <a name="python"></a>Python

```python
friends = ['john', 'pat', 'gary', 'michael']
for i, name in enumerate(friends):
    print "iteration {iteration} is {name}".format(iteration=i, name=name)
```

#### <a name="powershell"></a>PowerShell

```powershell
Clear-Host
$Directory = "C:\Windows\"
$Files = Get-Childitem $Directory -recurse -Include *.log `
-ErrorAction SilentlyContinue
```

### <a name="generic-code-block"></a>제네릭 코드 블록

제네릭 코드 블록 코딩에는 3개의 backtick(&#96;&#96;&#96;)을 사용합니다.

> 이 경우 설명서 사이트에서 적절한 구문이 강조 표시되도록 이전 섹션에서 설명한 것처럼 언어 식별자가 포함된 코드 블록을 사용하는 것이 좋습니다. 제네릭 코드 블록은 필요할 때만 사용하세요.

```
function fancyAlert(arg) {
    if(arg) {
        $.docs({div:'#foo'})
    }
}
```

## <a name="blockquotes"></a>blockquote

> 가뭄이 천만 년이나 계속되어 끔찍한 도마뱀이 다스리던 시대도 끝이 났습니다. 후세에는 아프리카라고 불릴 대륙인 이곳 적도에서는 생존을 위한 싸움이 극에 달했으며 아직은 누구도 승리하지 못했습니다. 이 황량하고 말라빠진 땅에서는 작고 날쌔며 사나운 생명체만이 살아남거나, 살아남을 수 있다는 희망이라도 품을 수 있습니다.

## <a name="images"></a>이미지

### <a name="static-image-or-animated-gif"></a>정적 이미지 또는 애니메이션 gif

```markdown
![this is the alt text](../images/Logo_DotNet.png)
```

![대체 텍스트입니다.](../images/Logo_DotNet.png)

### <a name="linked-image"></a>연결된 이미지

```markdown
[![alt text for linked image](../images/Logo_DotNet.png)](https://dot.net)
```

[![연결된 이미지의 대체 텍스트](../images/Logo_DotNet.png)](https://dot.net)

## <a name="videos"></a>비디오

현재, 다음 구문을 사용하여 Channel 9 및 YouTube 동영상을 모두 포함할 수 있습니다.

### <a name="channel-9"></a>Channel 9

```markdown
> [!VIDEO <channel9_video_link>]
```

동영상의 올바른 URL을 가져오려면 동영상 프레임 아래의 **포함** 탭을 선택하고 `<iframe>` 요소에서 URL을 복사합니다. 예:

```markdown
> [!VIDEO https://channel9.msdn.com/Blogs/dotnet/NET-Core-20-Released/player]
```

### <a name="youtube"></a>YouTube

동영상의 올바른 URL을 가져오려면 동영상을 마우스 오른쪽 단추로 클릭하고 **Embed 태그 복사**를 선택한 다음, `<iframe>` 요소에서 URL을 복사합니다.

```markdown
> [!VIDEO <youtube_video_link>]
```

예:

```markdown
> [!VIDEO https://www.youtube.com/embed/Q2mMbjw6cLA]
```

## <a name="docsmicrosoft-extensions"></a>docs.microsoft 확장

docs.microsoft는 GitHub Flavored Markdown에 대해 몇 가지 추가 확장을 제공합니다.

### <a name="alerts"></a>경고

설명서 사이트에서 적절한 스타일로 렌더링되도록 다음 경고 스타일을 사용해야 합니다. 그러나 GitHub의 렌더링 엔진은 스타일을 구분하지 않습니다.

```markdown
> [!NOTE]
> Information the user should notice even if skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]
> Essential information required for user success.

> [!CAUTION]
> Negative potential consequences of an action.

> [!WARNING]
> Dangerous certain consequences of an action.
```

그러면 이러한 항목은 다음과 같이 렌더링됩니다. ![경고 스타일](../images/alerts.png)

### <a name="includes"></a>포함되는 내용

Include를 사용하여 한 파일의 Markdown을 다른 파일에 포함할 수 있습니다.

[!INCLUDE[sample include file](../includes/sampleinclude.md)]

### <a name="checked-lists"></a>선택된 목록

목록의 경우 사용자 지정 스타일을 사용할 수 있습니다. 녹색 확인 표시가 있는 목록을 렌더링할 수 있습니다.

> [!div class="checklist"]
>
> - .NET Core 앱을 만드는 방법
> - Microsoft.XmlSerializer.Generator 패키지에 대한 참조를 추가하는 방법
> - MyApp.csproj를 편집하여 종속성을 추가하는 방법
> - 클래스 및 XmlSerializer를 추가하는 방법
> - 애플리케이션을 빌드하고 실행하는 방법

[.NET Core 문서](https://docs.microsoft.com/dotnet/core/additional-tools/xml-serializer-generator)에서 작동 중인 선택된 목록의 예를 확인할 수 있습니다.

### <a name="buttons"></a>단추

> [!div class="button"]
> [단추 링크](../docs/core/index.md)

[Visual Studio 문서](https://docs.microsoft.com/visualstudio/install/install-visual-studio#step-2---download-visual-studio)에서 작동 중인 단추의 예를 확인할 수 있습니다.

### <a name="selectors"></a>선택기

> [!div class="op_single_selector"]
>
> - [macOS](../docs/core/tutorials/using-on-macos.md)
> - [Windows](../docs/core/tutorials/with-visual-studio.md)

[Azure 문서](https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-classic)에서 작동 중인 선택기의 예를 확인할 수 있습니다.

### <a name="step-by-steps"></a>단계별 작업

>[!div class="step-by-step"]
>[이전](../docs/csharp/expression-trees-interpreting.md)
>[다음](../docs/csharp/expression-trees-translating.md)

[C# 가이드](https://docs.microsoft.com/dotnet/csharp/tour-of-csharp/program-structure)에서 작동 중인 단계별 예제를 확인할 수 있습니다.
