---
title: 호출자 정보
description: 호출자 정보 인수 특성을 사용 하 여 메서드에서 호출자 정보를 가져오는 방법을 설명 합니다.
ms.date: 04/25/2017
ms.openlocfilehash: e7bbc3830a95bd25cfc2fb369b204d367b775815
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106589"
---
# <a name="caller-information"></a>호출자 정보

호출자 정보 특성을 사용하여 메서드 호출자에 대한 정보를 얻을 수 있습니다. 소스 코드 파일 경로, 소스 코드 줄 번호 및 호출자의 멤버 이름을 얻을 수 있습니다. 이 정보는 추적, 디버깅 및 진단 도구를 만드는 데 도움이 됩니다.

이 정보를 얻으려면 각각 기본값이 있는 선택적 매개 변수에 적용되는 특성을 사용합니다. 다음 표에서는 [system.runtime.compilerservices](/dotnet/api/system.runtime.compilerservices) 네임 스페이스에 정의 된 호출자 정보 특성을 보여 줍니다.

|특성|설명|형식|
|---------|-----------|----|
|[CallerFilePath](/dotnet/api/system.runtime.compilerservices.callerfilepathattribute)|호출자를 포함한 소스 파일의 전체 경로입니다. 컴파일 시간의 파일 경로입니다.|`String`
|[CallerLineNumber](/dotnet/api/system.runtime.compilerservices.callerlinenumberattribute)|메서드가 호출되는 소스 파일의 줄 번호입니다.|`Integer`|
|[CallerMemberName](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)|호출자의 메서드 또는 속성 이름입니다. 이 항목의 뒷부분에 나오는 멤버 이름 섹션을 참조 하세요.|`String`|

## <a name="example"></a>예제

다음 예제에서는 이러한 특성을 사용 하 여 호출자를 추적할 수 있는 방법을 보여 줍니다.

```fsharp
open System.Diagnostics
open System.Runtime.CompilerServices
open System.Runtime.InteropServices

type Tracer() =
    member __.DoTrace(message: string,
                      [<CallerMemberName; Optional; DefaultParameterValue("")>] memberName: string,
                      [<CallerFilePath; Optional; DefaultParameterValue("")>] path: string,
                      [<CallerLineNumber; Optional; DefaultParameterValue(0)>] line: int) =
        Trace.WriteLine(sprintf "Message: %s" message)
        Trace.WriteLine(sprintf "Member name: %s" memberName)
        Trace.WriteLine(sprintf "Source file path: %s" path)
        Trace.WriteLine(sprintf "Source line number: %d" line)
```

## <a name="remarks"></a>설명

호출자 정보 특성은 선택적 매개 변수에만 적용할 수 있습니다. 호출자 정보 특성을 사용 하면 컴파일러에서 호출자 정보 특성을 사용 하 여 데코레이팅된 각 선택적 매개 변수에 대 한 적절 한 값을 기록 합니다.

호출자 정보 값은 컴파일 시간에 리터럴로 중간 언어(IL) 내로 내보내집니다. 예외에 대 한 [StackTrace](/dotnet/api/system.diagnostics.stacktrace) 속성의 결과와 달리 결과는 난독 처리의 영향을 받지 않습니다.

선택적 인수를 명시적으로 제공하여 호출자 정보를 제어하거나 호출자 정보를 숨길 수 있습니다.

## <a name="member-names"></a>멤버 이름

[`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) 특성을 사용 하 여 멤버 이름을 `String` 호출 된 메서드에 대 한 인수로 지정 하지 않을 수 있습니다. 이 기술을 사용 하 여 이름 바꾸기 리팩터링에서 값을 `String` 변경 하지 않는 문제를 방지할 수 있습니다. 이 이점은 다음 작업에 특히 유용합니다.

- 추적 및 진단 루틴 사용.
- 데이터를 바인딩할 때 [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) 인터페이스를 구현 합니다. 이 인터페이스에서는 컨트롤에서 업데이트된 정보를 표시할 수 있도록 바운드 컨트롤의 속성이 변경되었음을 알리는 개체의 속성을 사용할 수 있습니다. [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) 특성이 없으면 속성 이름을 리터럴로 지정 해야 합니다.

다음 차트에서는 CallerMemberName 특성을 사용할 때 반환 되는 멤버 이름을 보여 줍니다.

|호출 발생 범위|멤버 이름 결과|
|-------------------|------------------|
|메서드, 속성 또는 이벤트|호출에서 시작한 메서드, 속성 또는 이벤트의 이름입니다.|
|생성자|".ctor" 문자열|
|정적 생성자|".cctor" 문자열|
|소멸자|"Finalize" 문자열|
|사용자 정의 연산자 또는 변환|멤버에 대해 생성되는 이름입니다(예: "op_Addition").|
|특성 생성자|특성이 적용되는 멤버의 이름입니다. 특성이 멤버 내에 있는 어떤 요소인 경우(예: 매개 변수, 반환 값 또는 제네릭 형식 매개 변수) 이 결과는 그 요소와 관련된 멤버의 이름입니다.|
|포함하는 멤버가 없음(예: 어셈블리 수준 또는 형식에 적용되는 특성)|선택적 매개 변수의 기본값입니다.|

## <a name="see-also"></a>참고자료

- [특성](attributes.md)
- [명명 된 인수](parameters-and-arguments.md#named-arguments)
- [선택적 매개 변수](parameters-and-arguments.md#optional-parameters)
