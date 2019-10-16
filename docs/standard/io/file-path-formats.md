---
title: Windows 시스템의 파일 경로 형식
ms.date: 06/06/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- I/O, long paths
- long paths
- path formats, Windows
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 75261bc44b938432c9c22b90dc4db30ca00d630b
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170738"
---
# <a name="file-path-formats-on-windows-systems"></a>Windows 시스템의 파일 경로 형식

<xref:System.IO> 네임스페이스에 있는 많은 유형의 멤버는 파일 시스템 리소스에 대한 절대 또는 상대 경로를 지정할 수 있는 `path` 매개 변수를 포함합니다. 이 경로는 [Windows 파일 시스템 API](/windows/desktop/fileio/file-systems)에 전달됩니다. 이 토픽에서는 Windows 시스템에 사용할 수 있는 파일 경로의 형식을 설명합니다.

## <a name="traditional-dos-paths"></a>기존 DOS 경로

표준 DOS 경로는 다음 세 구성 요소로 구성될 수 있습니다.

- 볼륨 또는 드라이브 문자 다음에 볼륨 구분 기호(`:`).
- 디렉터리 이름. [디렉터리 구분 문자](<xref:System.IO.Path.DirectorySeparatorChar>)는 중첩된 디렉터리 계층 내에서 하위 디렉터리를 구분합니다.
- 선택적 파일 이름. [디렉터리 구분 문자](<xref:System.IO.Path.DirectorySeparatorChar>)는 파일 경로 및 파일 이름을 구분합니다.

세 구성 요소가 모두 존재하면 절대 경로입니다. 볼륨 또는 드라이브 문자가 지정되지 않았으며 디렉터리 이름이 [디렉터리 구분 문자](<xref:System.IO.Path.DirectorySeparatorChar>)로 시작하는 경우 현재 드라이브의 루트에 대한 상대 경로입니다. 그렇지 않으면 현재 디렉터리를 기준으로 하는 상대 경로입니다. 다음 표는 몇몇 가능한 디렉터리 및 파일 경로를 보여 줍니다.

|Path  |설명  |
| -- | -- |
| `C:\Documents\Newsletters\Summer2018.pdf` | 드라이브 C의 루트에서 시작하는 절대 파일 경로: |
| `\Program Files\Custom Utilities\StringFinder.exe` | 현재 드라이브의 루트에서 시작하는 절대 경로입니다. |
| `2018\January.xlsx` | 현재 디렉터리의 하위 디렉터리에 있는 파일에 대한 상대 경로입니다. |
| `..\Publications\TravelBrochure.pdf` | 현재 디렉터리의 피어인 디렉터리에 있는 파일에 대한 상대 경로입니다. |
| `C:\Projects\apilibrary\apilibrary.sln` | 드라이브 C의 루트에서 시작하는 파일에 대한 절대 파일 경로: |
| `C:Projects\apilibrary\apilibrary.sln` | C: 드라이브의 현재 디렉터리에서 시작하는 상대 경로입니다. |

> [!IMPORTANT]
> 마지막 두 경로 간의 차이점에 주목하십시오. 둘이 다 선택적 볼륨 지정자(두 경우 모두 C:)를 지정하지만, 첫 번째 경로는 지정한 볼륨의 루트로 시작하는 반면에, 두 번째 경로는 그렇지 않습니다. 따라서 첫 번째 경로는 드라이브 C의 루트 디렉터리에서 시작하는 절대 경로인 반면에, 두 번째 경로는 드라이브 C의 현재 디렉터리에서 시작하는 상대 경로입니다. 첫 번째 경로가 의도한 두 번째 양식을 사용하는 것은 Windows 파일 경로를 수반하는 버그의 일반적인 원인입니다.

<xref:System.IO.Path.IsPathFullyQualified%2A?displayProperty=nameWthType> 메서드를 호출하여 파일 경로가 정규화되는지(즉, 경로가 현재 디렉터리와 독립적이며 현재 디렉터리가 변경되어도 변경되지 않음) 여부를 결정할 수 있습니다. 참고로 그러한 경로는 상대 디렉터리 세그먼트(`.` 및 `..`)를 포함할 수 있으며 확인된 경로가 언제나 같은 위치를 가리키는 경우 여전히 정규화됩니다.

다음 예제에서는 절대 경로와 상대 경로 간의 차이점을 보여 줍니다. 예제를 실행하기 전에 디렉터리 D:\FY2018\가 존재하고 명령 프롬프트에서 D:\ 에 대한 현재 디렉터리를 설정하지 않은 것으로 가정합니다.

[!code-csharp[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/cs/paths.cs)]
[!code-vb[absolute-and-relative-paths](~/samples/snippets/standard/io/file-names/vb/paths.vb)]

## <a name="unc-paths"></a>UNC 경로

네트워크 리소스에 액세스하기 위해 사용하는 UNC(범용 명명 규칙) 경로는 다음과 같은 형식을 가집니다.

- \\\\로 시작하는 서버 또는 호스트 이름. 서버 이름에 NetBIOS 컴퓨터 이름 또는 IP/FQDN 주소(IPv4 및 v6을 지원함)가 올 수 있습니다.
- \\에 의해 호스트 이름과 구분되는 공유 이름. 서버 이름과 공유 이름이 함께 볼륨을 구성합니다.
- 디렉터리 이름. [디렉터리 구분 문자](<xref:System.IO.Path.DirectorySeparatorChar>)는 중첩된 디렉터리 계층 내에서 하위 디렉터리를 구분합니다.
- 선택적 파일 이름. [디렉터리 구분 문자](<xref:System.IO.Path.DirectorySeparatorChar>)는 파일 경로 및 파일 이름을 구분합니다.

다음은 UNC 경로의 몇 가지 예제입니다.

|Path  |설명  |
| -- | -- |
| `\\system07\C$\` | `system07`에 있는 C: 드라이브의 루트 디렉터리. |
| `\\Server2\Share\Test\Foo.txt` | \\\\Server2\\ 공유 볼륨의 Test 디렉터리에 있는 Foo.txt 파일입니다.|

UNC 경로는 언제나 정규화해야 합니다. 이 경로는 상대 디렉터리 세그먼트(`.` 및 `..`)를 포함할 수 있지만 정규화된 경로의 일부이어야 합니다. UNC 경로를 드라이브 문자에 매핑해야만 상대 경로를 사용할 수 있습니다.

## <a name="dos-device-paths"></a>DOS 디바이스 경로

Windows 운영 체제는 파일을 포함한 모든 리소스를 가리키는 통합된 개체 모델을 가지고 있습니다. 이러한 개체 경로는 콘솔 창에서 액세스할 수 있으며 구형 DOS 및 UNC 경로를 매핑하는 대상인 기호 링크의 특수 폴더를 통해 Win32 레이어에 표시됩니다. 이 특수 폴더는 다음 중 하나인 DOS 디바이스 경로 구문을 통해 액세스됩니다.

`\\.\C:\Test\Foo.txt`  
`\\?\C:\Test\Foo.txt`

드라이브 문자로 드라이브를 식별하는 것 외에, 볼륨 GUID로 볼륨을 식별할 수도 있습니다. 다음 양식을 사용합니다.

`\\.\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`
`\\?\Volume{b75e2c83-0000-0000-0000-602f00000000}\Test\Foo.txt`

> [!NOTE]
> DOS 디바이스 경로 구문은 .NET Core 1.1 및 .NET Framework 4.6.2부터 Windows에서 실행하는 .NET 구현에서 지원됩니다.

DOS 디바이스 경로는 다음 구성 요소로 구성됩니다.

- 경로를 DOS 디바이스 경로로 식별하는 디바이스 경로 지정자(`\\.\` 또는 `\\?\`).

   > [!NOTE]
   > `\\?\`는 .NET Core의 모든 버전 및 버전 4.6.2부터 .NET Framework에서 지원됩니다.

- “실제” 디바이스 개체의 바로 가기 링크입니다(드라이브 이름의 경우 C:, 볼륨 GUID의 경우 Volume{b75e2c83-0000-0000-0000-602f00000000}).

   디바이스 경로 지정자 뒤에 오는 DOS 디바이스 경로의 첫 번째 세그먼트는 볼륨 또는 드라이브를 식별합니다. (예를 들어 `\\?\C:\` 및 `\\.\BootPartition\`)

   호출된 UNC에 대한 특정 링크가 있습니다(당연히 `UNC`). 예:

  `\\.\UNC\Server\Share\Test\Foo.txt`  
  `\\?\UNC\Server\Share\Test\Foo.txt`

    디바이스 UNC의 경우, 서버/공유 부분이 볼륨을 구성합니다. 예를 들어 `\\?\server1\e:\utilities\\filecomparer\`에서 서버/공유 부분은 server1\utilities입니다. 이는 상대 디렉터리 경로를 사용하여 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> 같은 메서드를 호출할 때 중요하며, 볼륨을 지나서 탐색하는 것은 불가능합니다. 

DOS 디바이스 경로는 정의에 의해 정규화됩니다. 상대 디렉터리 세그먼트(`.` 및 `..`)는 허용되지 않습니다. 현재 디렉터리는 해당 사용에 포함되지 않습니다.

## <a name="example-ways-to-refer-to-the-same-file"></a>예제: 동일한 파일을 참조하는 방법

다음 예제는 <xref:System.IO> 네임스페이스에서 API를 사용할 때 파일을 참조할 수 있는 몇 가지 방법을 보여 줍니다. 이 예제는 <xref:System.IO.FileInfo> 개체를 인스턴스화하고 해당 개체의 <xref:System.IO.FileInfo.Name> 및 <xref:System.IO.FileInfo.Length> 속성을 사용하여 파일 이름 및 파일의 길이를 표시합니다.

[!code-csharp[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/cs/file-refs.cs)]
[!code-vb[referring-to-the-same-file](~/samples/snippets/standard/io/file-names/vb/file-refs.vb)]

## <a name="path-normalization"></a>경로 표준화

Windows API에 전달되는 거의 모든 경로는 정규화됩니다. 정규화 중에 Windows는 다음과 같은 단계를 수행합니다.

- 파일을 식별합니다.
- 현재 디렉터리를 부분적으로 정규화된 (상대) 경로에 적용합니다.
- 구성 요소 및 디렉터리 구분 기호를 정규화합니다.
- 상대 디렉터리 구성 요소(현재 디렉터리의 경우 `.` 및 부모 디렉터리의 경우 `..`)를 평가합니다.
- 특정 문자를 잘라냅니다.

이 정규화는 암시적으로 일어나지만 [GetFullPathName() 함수](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea) 호출을 래핑하는 <xref:System.IO.Path.GetFullPath%2A?displayProperty=nameWithType> 메서드를 호출하여 명시적으로 수행할 수도 있습니다. 또한 P/Invoke를 사용하여 Windows [GetFullPathName() 함수](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)를 직접 호출할 수도 있습니다.

### <a name="identifying-the-path"></a>경로 식별

경로 정규화의 첫 번째 단계는 경로의 형식 식별입니다. 경로는 몇 가지 범주 중 하나에 속합니다.

- 디바이스 경로인 경우. 즉, 구분 기호 두 개와 물음표 또는 마침표(`\\?` 또는 `\\.`)로 시작하는 경우.
- UNC 경로인 경우. 즉, 물음표 또는 마침표 없이 구분 기호 두 개로 시작하는 경우. 
- 정규화된 DOS 경로인 경우. 즉, 드라이브 문자, 볼륨 구분 기호 및 구성 요소 구분 기호(`C:\`)로 시작하는 경우.
- 구형 디바이스(`CON`, `LPT1`)를 지정하는 경우.
- 현재 드라이브의 루트를 기준으로 하는 경우. 즉, 단일 구성 요소 구분 기호(`\`)로 시작하는 경우.
- 지정한 드라이브의 현재 디렉터리를 기준으로 하는 경우. 즉, 드라이브 문자, 볼륨 구분 기호로 시작하고 구성 요소 구분 기호(`C:`)가 없는 경우.
- 현재 디렉터리를 기준으로 하는 경우. 즉, 다른 요소(`temp\testfile.txt`)로 시작하는 경우.

경로 형식은 현재 디렉터리가 일정한 방법으로 적용되는지 여부를 결정합니다. 경로의 "루트"가 무엇인지도 결정합니다.

### <a name="handling-legacy-devices"></a>구형 디바이스 처리

경로가 `CON`, `COM1` 또는 `LPT1` 같은 구형 DOS 디바이스인 경우 앞에 `\\.\`를 덧붙여 디바이스 경로로 변환한 다음, 반환합니다. 

구형 디바이스 이름으로 시작하는 경로는 언제나 <xref:System.IO.Path.GetFullPath(System.String)?displayProperty=nameWithType> 메서드에 의해 구형 디바이스로 해석됩니다. 예를 들어 `CON.TXT`에 대한 DOS 디바이스 경로는 `\\.\CON`이며, `COM1.TXT\file1.txt`에 대한 DOS 디바이스 경로는 `\\.\COM1`입니다.

### <a name="applying-the-current-directory"></a>현재 디렉터리 적용

경로가 정규화되지 않은 경우 Windows는 현재 디렉터리를 해당 경로에 적용합니다. UNC 및 디바이스 경로에는 현재 디렉터리가 적용되지 않습니다. 구분 기호 C:\\를 포함한 전체 드라이브에도 적용되지 않습니다.

경로가 단일 구성 요소 구분 기호로 시작하는 경우 현재 디렉터리의 드라이브를 적용합니다. 예를 들어 파일 경로가 `\utilities`이고 현재 디렉터리가 `C:\temp\`인 경우, 정규화하면 `C:\utilities`가 생성됩니다.

경로가 드라이브 문자, 볼륨 구분 기호로 시작하고 구성 요소 구분 기호가 없는 경우, 지정한 드라이브의 명령 셸에서 설정한 마지막 현재 디렉터리를 적용합니다. 마지막 현재 디렉터리가 설정되지 않은 경우 드라이브만 적용합니다. 예를 들어 파일 경로가 `D:sources`이고, 현재 디렉터리가 `C:\Documents\`이고, 드라이브 D:의 마지막 현재 디렉터리가 `D:\sources\`이면 결과는 `D:\sources\sources`입니다. 이러한 "드라이브 상대" 경로는 프로그램 및 스크립트 논리 오류의 일반적인 원인입니다. 문자와 콜론으로 시작하는 경로가 상대 경로가 아니라고 가정하는 것은 명백히 틀린 가정입니다.

경로가 구분 기호 이외의 요소로 시작하는 경우 현재 드라이브 및 현재 디렉터리를 적용합니다. 예를 들어 경로가 `filecompare`이고 현재 디렉터리가 `C:\utilities\`인 경우, 결과는 `C:\utilities\filecompare\`입니다.

> [!IMPORTANT]
> 현재 디렉터리는 프로세스에 따른 설정이므로 상대 경로는 멀티스레드 애플리케이션(즉, 대부분의 애플리케이션)에서 위험합니다. 스레드는 현재 디렉터리를 언제든지 변경할 수 있기 때문입니다. .NET Core 2.1부터 <xref:System.IO.Path.GetFullPath(System.String,System.String)?displayProperty=nameWithType> 메서드를 호출하여 상대 경로 및 기본 경로(현재 디렉터리)에서 확인하려는 기준이 되는 절대 경로를 가져올 수 있습니다. 

### <a name="canonicalizing-separators"></a>구분 기호 정규화

모든 슬래시(`/`)는 표준 Windows 구분 기호인 백슬래시(`\`)로 변환됩니다. 슬래시가 존재하는 경우 첫 번째 슬래시 다음에 오는 일련의 슬래시를 단일 슬래시로 축소합니다.

### <a name="evaluating-relative-components"></a>상대 구성 요소 평가

경로가 처리될 때 단일 또는 이중 마침표(`.` 또는 `..`)로 구성된 구성 요소 또는 세그먼트를 평가합니다. 

- 단일 마침표의 경우, 현재 디렉터리를 가리키므로 현재 세그먼트를 제거합니다.

- 이중 마침표의 경우, 부모 디렉터리를 가리키므로 현재 세그먼트 및 부모 세그먼트를 제거합니다.

   부모 디렉터리는 경로의 루트를 지나가지 않는 경우에만 제거합니다. 경로의 루트는 경로의 형식에 따라 달라집니다. 즉, DOS 경로의 경우 드라이브(`C:\`)이고, UNC(`\\Server\Share`) 경로의 경우 서버/공유이며, 디바이스 경로(`\\?\` 또는 `\\.\`)의 경우 디바이스 경로 접두사입니다.

### <a name="trimming-characters"></a>문자 잘라내기

앞에서 제거한 일련의 구분 기호 및 상대 세그먼트와 함께 일부 추가 문자를 정규화 중에 제거합니다.

- 세그먼트가 단일 마침표로 끝나는 경우 해당 마침표를 제거합니다. (단일 또는 이중 마침표의 세그먼트는 이전 단계에서 정규화되었습니다. 마침표 3개 이상의 세그먼트는 정규화되지 않으며 실제로 유효한 파일/디렉터리 이름입니다.)

- 경로가 구분 기호로 끝나지 않는 경우 모든 후행 마침표와 공백(U+0020)을 제거합니다. 마지막 세그먼트가 단순히 단일 또는 이중 마침표인 경우, 이는 위의 상대 구성 요소 규칙에 포함됩니다. 

   이 규칙은 공백 뒤에 후행 구분 기호를 추가하면 후행 공백을 사용하여 디렉터리 이름을 만들 수 있음을 의미합니다.  

   > [!IMPORTANT]
   > 후행 공백을 사용하여 디렉터리 또는 파일 이름을 만들지 **말아야** 합니다. 후행 공백은 디렉터리 액세스를 어렵게 또는 불가능하게 만들 수 있으며, 해당 이름이 후행 공백을 포함하는 디렉터리 또는 파일의 처리를 시도할 때 흔히 애플리케이션이 실패합니다.

## <a name="skipping-normalization"></a>정규화 건너뛰기

일반적으로 Windows API에 전달되는 경로는 (결과적으로) [GetFullPathName 함수](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)에 전달되고 정규화됩니다. 여기에 중요한 한 가지 예외가 있는데, 바로 마침표 대신에 물음표로 시작하는 디바이스 경로입니다. 경로는 `\\?\`로 시작하지 않는 한(canonical 백슬래시 사용에 주의) 정규화됩니다.

정규화를 건너뛰려는 이유는 무엇입니까? 세 가지 중요한 이유가 있습니다.

1. 일반적으로 사용할 수 없지만 올바른 경로에 액세스. 예를 들어 `hidden.`이라는 파일 또는 디렉터리는 다른 방법으로 액세스할 수 없습니다. 

1. 이미 일반화된 경우 일반화를 건너뛰어서 성능을 개선.

1. .NET Framework에 한하여, `MAX_PATH`를 건너뛰려면 경로 길이가 259문자보다 더 큰 경로를 허용하는지 확인합니다. 대부분의 API는 이 크기를 허용하지만, 몇 가지 예외가 있습니다.

> [!NOTE]
> .NET Core는 암시적으로 긴 경로를 처리하며 `MAX_PATH` 검사를 수행하지 않습니다. `MAX_PATH` 검사는 .NET Framework에만 적용됩니다.

정규화 및 최대 경로 검사를 건너뛰는 것은 두 디바이스 경로 구문 간에만 차이점이 있으며, 다른 면에서는 동일합니다. 정규화를 건너뛸 때에는 "일반적인" 애플리케이션이 처리하기 어려운 경로를 생성하기 쉽기 때문에 주의해야 합니다.

`\\?\`로 시작하는 경로는 [GetFullPathName 함수](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)에 명시적으로 전달하더라도 여전히 정규화됩니다.

참고로 `MAX_PATH` 문자보다 큰 경로는 `\\?\` 없이 [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamea)에 전달할 수 있습니다. 이는 Windows에서 처리할 수 있는 최대 문자열 크기까지 임의 길이의 경로를 지원합니다.

## <a name="case-and-the-windows-file-system"></a>대/소문자 및 Windows 파일 시스템

Windows 이외의 사용자와 개발자가 혼동을 일으키는 Windows 파일 시스템의 특징은 경로 및 디렉터리 이름이 대/소문자를 구분하지 않는다는 것입니다. 즉, 디렉터리 및 파일 이름은 생성될 때 사용하는 문자열의 대/소문자를 반영합니다. 예를 들어 다음 메서드 호출은

```csharp
Directory.Create("TeStDiReCtOrY");
```

```vb
Directory.Create("TeStDiReCtOrY")
```

TeStDiReCtOrY라는 디렉터리를 생성합니다. 해당 대/소문자를 변경하기 위해 디렉터리 또는 파일을 이름 변경하는 경우, 디렉터리 또는 파일 이름은 이름 변경할 당시에 사용한 문자열의 대/소문자를 반영합니다. 예를 들어 다음 코드는 test.txt라는 파일을 Test.txt로 이름 변경합니다.

[!code-csharp[case-and-renaming](~/samples/snippets/standard/io/file-names/cs/rename.cs)]
[!code-vb[case-and-renaming](~/samples/snippets/standard/io/file-names/vb/rename.vb)]

그러나 디렉터리 및 파일 이름 비교는 대/소문자를 구분하지 않습니다. "test.txt"라는 파일을 검색하는 경우, .NET 파일 시스템 API는 비교 시 대/소문자를 무시합니다. Test.txt, TEST.TXT, test.TXT 및 다른 어떤 대/소문자 조합도 "test.txt"와 일치합니다.
