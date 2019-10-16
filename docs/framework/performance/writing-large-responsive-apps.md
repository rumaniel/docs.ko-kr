---
title: 대형 응답성 .NET Framework 응용 프로그램 작성
ms.date: 03/30/2017
ms.assetid: 123457ac-4223-4273-bb58-3bc0e4957e9d
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 4e4b5822306fa8f4e6b4437f4a1bef92b53a86b9
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046140"
---
# <a name="writing-large-responsive-net-framework-apps"></a>대형 응답성 .NET Framework 응용 프로그램 작성
이 문서에서는 규모가 큰 .NET Framework 앱이나 파일 또는 데이터베이스와 같이 많은 양의 데이터를 처리하는 앱의 성능을 향상시키기 위한 팁을 제공합니다. 이러한 팁은 C# 및 Visual Basic 컴파일러를 관리 코드로 다시 작성하면서 수집되었으며, C# 컴파일러의 실제 몇 가지 예를 포함하고 있습니다. 
  
 .NET Framework는 앱을 빌드하는 생산성이 뛰어납니다. 강력하고 안전한 언어와 풍부한 라이브러리 컬렉션이 앱 빌드의 생산성을 높여 줍니다. 그러나 우수한 생산성에는 책임이 따르기 마련입니다. .NET Framework의 모든 기능을 사용하되, 필요한 경우 코드의 성능을 조정할 준비가 되어 있어야 합니다. 
  
## <a name="why-the-new-compiler-performance-applies-to-your-app"></a>새 컴파일러 성능을 앱에 적용하는 이유  
 .NET 컴파일러 플랫폼("Roslyn") 팀은 Visual Studio에서 코드를 모델링 및 분석하고, 도구를 빌드하며, 보다 풍부한 코드 인식 환경을 가능하게 해주는 새로운 API를 제공하기 위해 C# 및 Visual Basic 컴파일러를 관리 코드로 다시 작성했습니다. 컴파일러를 다시 작성하고 새 컴파일러에서 Visual Studio 환경을 빌드한 결과, 규모가 큰 모든 .NET Framework 앱 또는 많은 데이터를 처리하는 모든 앱에 적용 가능한 유용한 성능 분석 정보가 드러났습니다. C# 컴파일러의 분석 정보 및 예를 활용하기 위해 컴파일러에 대해 알 필요는 없습니다. 
  
 Visual Studio에서는 컴파일러 API를 사용하여 식별자 및 키워드 색 지정, 구문 완성 목록, 오류를 나타내는 물결선, 매개 변수 팁, 코드 문제, 코드 동작 등 사용자가 선호하는 모든 IntelliSense 기능을 빌드합니다. Visual Studio는 개발자가 코드를 입력하고 변경하는 동안 이 도움말을 제공하며, Visual Studio는 컴파일러가 개발자가 편집한 코드를 지속적으로 모델링하는 동안 응답성을 유지해야 합니다. 
  
 최종 사용자는 앱과 상호 작용할 때 앱이 응답성을 유지할 것을 기대합니다. 입력이나 명령 처리가 차단되어서는 안 됩니다. 사용자가 입력을 계속하면 도움말은 신속하게 나타나거나 표시되지 않아야 합니다. 앱은 앱이 느리다고 느끼게 하는 오랜 계산으로 UI 스레드를 차단하는 것을 피해야 합니다. 
  
 Roslyn 컴파일러에 대 한 자세한 내용은 [.NET COMPILER PLATFORM SDK](../../csharp/roslyn-sdk/index.md)를 참조 하세요.
  
## <a name="just-the-facts"></a>팩트  
 성능을 조정하고 응답성 있는 .NET Framework 앱을 만들 때는 다음 팩트를 고려하세요. 
  
### <a name="fact-1-dont-prematurely-optimize"></a>팩트 1: 중간에 최적화 안 함  
 필요 이상으로 복잡한 코드를 작성하면 유지 관리, 디버깅 및 개선 비용이 발생합니다. 숙련된 프로그래머는 코딩 문제를 해결하는 방법에 대한 직관적인 감각을 지니고 있으며 보다 효율적인 코드를 작성합니다. 그러나 때로는 코드를 너무 이르게 최적화합니다. 예를 들어, 단순 배열이면 충분한 경우에 해시 테이블을 사용하거나 단순히 값을 다시 계산하는 대신 메모리를 누수시킬 수 있는 복잡한 캐싱을 사용합니다. 숙련된 프로그래머라 하더라도 성능에 대해 테스트하고 문제를 발견할 경우 코드를 분석해야 합니다. 
  
### <a name="fact-2-if-youre-not-measuring-youre-guessing"></a>팩트 2: 측정 하지 않는 경우 추측 하 게 됩니다.  
 프로필과 측정값은 거짓말하지 않습니다. 프로필은 CPU가 완전히 로드되었는지 여부나 사용자가 디스크 I/O에서 차단되었는지 여부를 보여 줍니다. 프로필을 보면 할당하는 메모리의 종류와 양을 알 수 있을 뿐만 아니라 CPU가 GC([가비지 수집](../../standard/garbage-collection/index.md))에 많은 시간을 소비하고 있는지 여부도 알 수 있습니다. 
  
 앱의 핵심 사용자 환경 또는 시나리오에 대한 성능 목표를 설정하고 성능을 측정하기 위한 테스트를 작성해야 합니다. 과학적인 방법을 적용하여 실패 테스트를 조사합니다. 즉, 프로필을 사용하여 사용자를 안내하고, 문제가 무엇일지 가설을 세우고, 실험이나 코드 변경으로 가설을 테스트합니다. 정기 테스트로 시간의 흐름에 따른 기준 성능 측정값을 설정하여 성능 저하를 일으키는 변경 내용을 구분할 수 있습니다. 엄격한 방식으로 성능 작업에 접근하면 불필요한 코드 업데이트로 시간을 낭비하는 일이 없습니다. 
  
### <a name="fact-3-good-tools-make-all-the-difference"></a>팩트 3: 모든 차이점을 지 원하는 좋은 도구  
 좋은 도구를 사용하면 가장 큰 성능 문제(CPU, 메모리 또는 디스크)에 신속하게 파고들어 해당 병목 현상을 일으키는 코드를 찾을 수 있습니다. Microsoft는 [Visual Studio Profiler](/visualstudio/profiling/beginners-guide-to-performance-profiling) 및 [perfview](https://www.microsoft.com/download/details.aspx?id=28567)와 같은 다양 한 성능 도구를 제공 합니다. 
  
 PerfView는 디스크 I/O, GC 이벤트 및 메모리와 같은 깊이 있는 문제에 집중하는 데 도움을 주는 놀랄 만큼 강력한 도구로서 무료입니다. 성능 관련 ETW([Windows용 이벤트 추적](../wcf/samples/etw-tracing.md)) 이벤트를 캡처하여 앱, 프로세스, 스택 및 스레드 단위 정보를 쉽게 볼 수 있습니다. PerfView는 앱에서 할당하는 메모리의 양과 종류뿐만 아니라 함수 또는 호출 스택으로 인해 메모리가 할당되는 양이 어느 정도인지를 보여 줍니다. 자세한 내용은 도구에 포함된 다양한 도움말 항목, 데모 및 비디오(예: Channel 9의 [PerfView 자습서](https://channel9.msdn.com/Series/PerfView-Tutorial))를 참조하세요. 
  
### <a name="fact-4-its-all-about-allocations"></a>팩트 4: 할당에 대 한 모든 것입니다.  
 응답성 있는 .NET Framework 앱을 빌드하는 것은 거품 정렬 대신 빠른 정렬을 사용하는 등 알고리즘에 대한 문제라고 생각할 수 있지만 그렇지 않습니다. 응답성 있는 앱을 빌드하는 데 있어서 가장 큰 요인은 메모리를 할당하는 것이며, 특히 앱의 규모가 매우 크거나 앱이 많은 양의 데이터를 처리하는 경우에 그렇습니다. 
  
 새 컴파일러 API를 사용하여 응답성 있는 IDE 환경을 빌드하는 작업의 거의 전부는 할당을 피하고 캐싱 전략을 관리하는 것에 관련되었습니다. PerfView 추적은 새 C# 및 Visual Basic 컴파일러의 성능이 거의 CPU 바인딩이 아니라는 사실을 보여 줍니다. 이러한 새 컴파일러는 수십만 또는 수백만 개의 코드 줄을 읽고 메타데이터를 읽거나 생성된 코드를 내보낼 때 I/O 바인딩일 수 있습니다. UI 스레드 지연은 거의 전부 가비지 컬렉션 때문입니다. .NET Framework GC는 성능을 위해 많이 조정되었고 앱 코드가 실행되는 동안 해당 작업의 많은 부분을 동시에 수행합니다. 그러나 한 번의 할당으로 많은 비용이 드는 [gen2](../../standard/garbage-collection/fundamentals.md) 컬렉션이 트리거되어 모든 스레드가 중지될 수 있습니다. 
  
## <a name="common-allocations-and-examples"></a>일반 할당 및 예제  
 이 섹션의 예제 식에는 작게 보이는 할당이 숨겨져 있습니다. 그러나 규모가 큰 앱이 식을 충분한 횟수로 실행하면 수백 MB 심지어 GB의 할당이 발생할 수 있습니다. 예를 들어, 편집기에서 개발자의 입력을 시뮬레이션한 1분간의 테스트 결과 GB 메모리가 할당되어 성능 팀이 입력 시나리오에 집중하게 되었습니다. 
  
### <a name="boxing"></a>boxing  
 [Boxing](../../csharp/programming-guide/types/boxing-and-unboxing.md)은 일반적으로 스택 또는 데이터 구조에 있는 값 형식이 개체에 래핑되면 발생합니다. 즉, 데이터를 유지하기 위한 개체를 할당한 다음 개체에 대한 포인터를 반환합니다. .NET Framework는 경우에 따라 메서드 시그니처 또는 스토리지 위치 형식 때문에 값을 boxing합니다. 값 형식을 개체에 래핑하면 메모리 할당이 발생합니다. boxing 작업이 많으면 앱에 대한 MB 또는 GB의 메모리 할당이 발생할 수 있습니다. 즉, 앱으로 인해 많은 GC가 발생합니다. .NET Framework 및 언어 컴파일러는 가능한 한 boxing을 피하지만, 경우에 따라 전혀 예기치 않게 boxing이 발생하기도 합니다. 
  
 PerfView에서 boxing을 보려면 추적을 열고 앱의 프로세스 이름 아래에서 GC Heap Alloc Stacks를 검토합니다(PerfView는 모든 프로세스에 대해 보고한다는 사실에 주의). 할당 아래에 <xref:System.Int32?displayProperty=nameWithType> 및 <xref:System.Char?displayProperty=nameWithType>과 같은 형식이 보이면 값 형식을 boxing하고 있는 것입니다. 이러한 형식 중 하나를 선택하면 해당 형식이 boxing된 스택 및 함수가 표시됩니다. 
  
 **예제 1: 문자열 메서드 및 값 형식 인수**  
  
 이 샘플 코드는 잠재적으로 불필요하고 과도한 boxing을 보여 줍니다.  
  
```csharp  
public class Logger  
{  
    public static void WriteLine(string s) { /*...*/ }  
}  
  
public class BoxingExample  
{  
    public void Log(int id, int size)  
    {  
        var s = string.Format("{0}:{1}", id, size);  
        Logger.WriteLine(s);  
    }  
}  
```  
  
 이 코드는 로깅 기능을 제공하므로 앱이 `Log` 함수를 자주 호출할 수 있으며 심지어 수백만 번 호출할 수도 있습니다. 문제는 `string.Format`에 대한 호출이 <xref:System.String.Format%28System.String%2CSystem.Object%2CSystem.Object%29> 오버로드 확인으로 이어진다는 사실입니다. 
  
 이 오버로드가 수행되려면 .NET Framework가 `int` 값을 개체에 boxing하여 이 메서드 호출에 전달해야 합니다. 부분적인 해결 방법은 `id.ToString()` 및 `size.ToString()`을 호출하고 모든 문자열(개체임)을 `string.Format` 호출에 전달하는 것입니다. `ToString()`을 호출하면 문자열이 할당되지만 해당 할당은 어쨌든 `string.Format` 내부에서 발생합니다. 
  
 `string.Format`에 대한 이 기본 호출을 단순한 문자열 연결이라고 간주할 수 있으므로 대신 이 코드를 작성할 수 있습니다.  
  
```csharp  
var s = id.ToString() + ':' + size.ToString();  
```  
  
 그러나 코드의 해당 줄은 <xref:System.String.Concat%28System.Object%2CSystem.Object%2CSystem.Object%29>로 컴파일되므로 boxing 할당이 발생합니다. .NET Framework는 문자 리터럴을 boxing하여 `Concat`을 호출해야 합니다.  
  
 **예제 1에 대한 해결 방법**  
  
 전체 해결 방법은 간단합니다. 문자 리터럴을 문자열 리터럴로 바꾸기만 하면 됩니다. 그러면 문자열이 이미 개체이기 때문에 boxing이 발생하지 않습니다.  
  
```csharp  
var s = id.ToString() + ":" + size.ToString();  
```  
  
 **예제 2: 열거형 boxing**  
  
 이 예제에서는 열거형 형식을 자주 사용해서(특히, 사전 조회 작업에서) 새 C# 및 Visual Basic 컴파일러에서 엄청난 양의 할당이 발생했습니다. 
  
```csharp  
public enum Color  
{  
    Red, Green, Blue  
}  
  
public class BoxingExample  
{  
    private string name;  
    private Color color;  
    public override int GetHashCode()  
    {  
        return name.GetHashCode() ^ color.GetHashCode();  
    }  
}  
```  
  
 이 문제는 매우 미묘합니다. PerfView는 이를 <xref:System.Enum.GetHashCode> boxing으로 보고하는데, 메서드가 구현상의 이유로 열거형 형식의 기본 표현을 boxing하기 때문입니다. PerfView에서 자세히 보면 <xref:System.Enum.GetHashCode>에 대한 호출마다 두 개의 boxing 할당을 볼 수 있습니다. 컴파일러가 boxing 하나를 삽입하고 .NET Framework가 나머지 boxing을 삽입하는 것입니다. 
  
 **예제 2에 대한 해결 방법**  
  
 <xref:System.Enum.GetHashCode>를 호출하기 전에 기본 표현으로 캐스팅하여 두 할당을 모두 쉽게 피할 수 있습니다.  
  
```csharp  
((int)color).GetHashCode()  
```  
  
 열거형 형식에 대한 boxing의 또 다른 일반적인 소스는 <xref:System.Enum.HasFlag%28System.Enum%29?displayProperty=nameWithType> 메서드입니다. <xref:System.Enum.HasFlag%28System.Enum%29>으로 전달된 인수는 boxing되어야 합니다. 대부분의 경우 <xref:System.Enum.HasFlag%28System.Enum%29?displayProperty=nameWithType>에 대한 호출을 비트 테스트로 바꾸면 보다 간단하고 할당도 발생하지 않습니다. 
  
 첫 번째 성능 팩트를 염두에 두고(즉, 너무 이르게 최적화하지 말 것) 서둘러 이 방식으로 모든 코드를 다시 작성하려고는 하지 마세요. 이러한 boxing 비용에 주의하되 앱을 프로파일링하고 핫 스폿을 찾은 다음에만 코드를 변경하세요. 
  
### <a name="strings"></a>문자열  
 문자열 조작은 할당이 발생하는 가장 큰 원인 중 몇 가지를 차지하며, PerfView에서 흔히 상위 5가지 할당을 차지하곤 합니다. 프로그램에서는 serialization, JSON 및 REST API에 문자열을 사용합니다. 열거형 형식을 사용할 수 없을 때 시스템과 상호 작용하기 위한 프로그램 상수로 문자열을 사용할 수 있습니다. 프로파일링에 문자열이 성능에 많은 영향을 미치고 있다고 표시되는 경우 <xref:System.String>, <xref:System.String.Format%2A>, <xref:System.String.Concat%2A>, <xref:System.String.Split%2A>, <xref:System.String.Join%2A> 등과 같은 <xref:System.String.Substring%2A> 메서드에 대한 호출을 찾습니다. <xref:System.Text.StringBuilder>를 사용하여 많은 조각에서 하나의 문자열을 만드는 비용을 방지하는 것도 유용하지만 <xref:System.Text.StringBuilder> 개체를 할당하는 것조차 관리해야 하는 병목 현상이 될 수 있습니다. 
  
 **예제 3: 문자열 작업**  
  
 C# 컴파일러에는 서식이 지정된 XML 문서 주석의 텍스트를 쓰는 이 코드가 포함되었습니다.  
  
```csharp  
public void WriteFormattedDocComment(string text)  
{  
    string[] lines = text.Split(new[] { "\r\n", "\r", "\n" },  
                                StringSplitOptions.None);  
    int numLines = lines.Length;  
    bool skipSpace = true;  
    if (lines[0].TrimStart().StartsWith("///"))  
    {  
        for (int i = 0; i < numLines; i++)  
        {  
            string trimmed = lines[i].TrimStart();  
            if (trimmed.Length < 4 || !char.IsWhiteSpace(trimmed[3]))  
            {  
                skipSpace = false;  
                break;  
            }  
        }  
        int substringStart = skipSpace ? 4 : 3;  
        for (int i = 0; i < numLines; i++)  
            WriteLine(lines[i].TrimStart().Substring(substringStart));  
    }  
    else { /* ... */ }  
```  
  
 이 코드가 많은 문자열 조작을 수행하는 것을 볼 수 있습니다. 이 코드에서는 라이브러리 메서드를 사용하여 줄을 별도의 문자열로 분할하고, 공백을 잘라내며, `text` 인수가 XML 문서 주석인지 확인하고, 줄에서 부분 문자열을 추출합니다. 
  
 `WriteFormattedDocComment` 내의 첫 번째 줄에서 `text.Split` 호출은 호출될 때마다 요소가 3개인 새 배열을 인수로 할당합니다. 컴파일러는 이 배열을 할당할 때마다 코드를 내보내야 합니다. 그 이유는 컴파일러가 <xref:System.String.Split%2A>이 배열을 다른 코드에 의해 배열이 수정(그러면 `WriteFormattedDocComment`에 대한 후속 호출에 영향을 미치게 됨)될 수 있는 어딘가에 저장하는지 여부를 알 수 없기 때문입니다. 또한 <xref:System.String.Split%2A>에 대한 호출은 `text`의 모든 줄에 대해 문자열 하나를 할당하고 작업을 수행하기 위해 다른 메모리를 할당합니다. 
  
 `WriteFormattedDocComment`에는 <xref:System.String.TrimStart%2A> 메서드에 대한 세 개의 호출이 포함되어 있습니다. 두 개의 호출은 작업 및 할당을 중복하는 안쪽 루프에 있습니다. 설상가상으로 인수 없이 <xref:System.String.TrimStart%2A> 메서드를 호출하면 문자열 결과 외에 빈 배열(`params` 매개 변수에 대한)이 할당됩니다. 
  
 마지막으로, 일반적으로 새 문자열을 할당하는 <xref:System.String.Substring%2A> 메서드에 대한 호출이 있습니다. 
  
 **예제 3에 대한 해결 방법**  
  
 앞의 예제와 달리, 약간의 편집으로 이러한 할당을 해결할 수 없습니다. 한 걸음 물러나 문제를 살펴보고 다르게 접근해야 합니다. 예를 들어, `WriteFormattedDocComment()`에 대한 인수는 메서드에 필요한 모든 정보가 포함된 문자열이므로 코드는 많은 부분 문자열을 할당하는 대신 더 많은 인덱싱을 수행할 수 있다는 사실을 알 수 있습니다. 
  
 컴파일러의 성능 팀은 다음과 같은 코드로 이러한 모든 할당을 해결했습니다.  
  
```csharp  
private int IndexOfFirstNonWhiteSpaceChar(string text, int start) {  
    while (start < text.Length && char.IsWhiteSpace(text[start])) start++;  
    return start;  
}  
  
private bool TrimmedStringStartsWith(string text, int start, string prefix) {  
    start = IndexOfFirstNonWhiteSpaceChar(text, start);  
    int len = text.Length - start;  
    if (len < prefix.Length) return false;  
    for (int i = 0; i < len; i++)  
    {  
        if (prefix[i] != text[start + i]) return false;  
    }  
    return true;  
}  
  
// etc... 
```  
  
 `WriteFormattedDocComment()`의 첫 번째 버전에서는 배열, 여러 부분 문자열 및 잘라낸 부분 문자열과 함께 빈 `params` 배열을 할당했습니다. "///"도 확인 합니다. 수정된 코드에서는 인덱싱만 사용하며 아무것도 할당하지 않습니다. 공백이 아닌 첫 번째 문자를 찾은 다음 문자 단위로 문자를 검사 하 여 문자열이 "///"로 시작 하는지 확인 합니다. 새 코드에서는 <xref:System.String.TrimStart%2A> 대신 `IndexOfFirstNonWhiteSpaceChar` 를 사용 하 여 공백이 아닌 문자가 발생 하는 첫 번째 인덱스 (지정 된 시작 인덱스 뒤의)를 반환 합니다. 해결 방법이 완벽하지는 않지만 완벽한 솔루션을 위해 유사한 해결 방법을 적용하는 방법을 확인할 수 있습니다. 코드 전체에 이 접근 방식을 적용하여 `WriteFormattedDocComment()`에서 모든 할당을 제거할 수 있습니다. 
  
 **예 4: StringBuilder**  
  
 이 예제에서는 <xref:System.Text.StringBuilder> 개체를 사용합니다. 다음 함수에서는 제네릭 형식의 전체 형식 이름을 생성합니다.  
  
```csharp  
public class Example  
{  
    // Constructs a name like "SomeType<T1, T2, T3>"  
    public string GenerateFullTypeName(string name, int arity)  
    {  
        StringBuilder sb = new StringBuilder();  
  
        sb.Append(name);  
        if (arity != 0)  
        {  
            sb.Append("<");  
            for (int i = 1; i < arity; i++)  
            {  
                sb.Append("T"); sb.Append(i.ToString()); sb.Append(", ");  
            }  
            sb.Append("T"); sb.Append(i.ToString()); sb.Append(">");  
        }  
  
        return sb.ToString();  
    }  
}  
```  
  
 초점은 새 <xref:System.Text.StringBuilder> 인스턴스를 만드는 줄에 있습니다. 이 코드에서는 `sb.ToString()`에 대한 할당과 <xref:System.Text.StringBuilder> 구현 내의 내부 할당이 발생하지만 문자열 결과를 원하는 경우 해당 할당을 제어할 수 없습니다. 
  
 **예제 4에 대한 해결 방법**  
  
 `StringBuilder` 개체 할당을 해결하려면 개체를 캐시합니다. throw될 수 있는 단일 인스턴스를 캐시하는 것만으로도 성능을 현저히 향상시킬 수 있습니다. 다음은 함수의 새 구현이며, 여기에는 새로운 첫 번째 줄과 마지막 줄을 제외한 모든 코드가 생략되어 있습니다.  
  
```csharp  
// Constructs a name like "MyType<T1, T2, T3>"  
public string GenerateFullTypeName(string name, int arity)  
{  
    StringBuilder sb = AcquireBuilder();  
    /* Use sb as before */  
    return GetStringAndReleaseBuilder(sb);  
}  
```  
  
 핵심 부분은 새 `AcquireBuilder()` 및 `GetStringAndReleaseBuilder()` 함수입니다.  
  
```csharp  
[ThreadStatic]  
private static StringBuilder cachedStringBuilder;  
  
private static StringBuilder AcquireBuilder()  
{  
    StringBuilder result = cachedStringBuilder;  
    if (result == null)  
    {  
        return new StringBuilder();  
    }  
    result.Clear();  
    cachedStringBuilder = null;  
    return result;  
}  
  
private static string GetStringAndReleaseBuilder(StringBuilder sb)  
{  
    string result = sb.ToString();  
    cachedStringBuilder = sb;  
    return result;  
}  
```  
  
 새 컴파일러는 스레딩을 사용하므로 이러한 구현에서는 Thread 정적 필드(<xref:System.ThreadStaticAttribute> 특성)를 사용하여 <xref:System.Text.StringBuilder>를 캐시하고 사용자는 `ThreadStatic` 선언을 포기할 수 있습니다. Thread 정적 필드는 이 코드를 실행하는 각 스레드에 대해 고유한 값을 유지합니다. 
  
 `AcquireBuilder()`는 캐시된 <xref:System.Text.StringBuilder> 인스턴스가 있는 경우 이를 지우고 필드 또는 캐시를 null로 설정한 후 해당 인스턴스를 반환합니다. 그러지 않으면 `AcquireBuilder()`는 새 인스턴스를 만들어 반환하고 null로 설정된 필드 또는 캐시를 그대로 둡니다. 
  
 <xref:System.Text.StringBuilder>에 대한 작업을 완료했으면 `GetStringAndReleaseBuilder()`를 호출하여 문자열 결과를 가져오고 필드 또는 캐시에 <xref:System.Text.StringBuilder> 인스턴스를 저장한 다음 결과를 반환합니다. 드물게 발생하기는 하지만 실행이 이 코드에 다시 들어가서 여러 <xref:System.Text.StringBuilder> 개체를 만들 수 있습니다. 코드는 나중에 사용하기 위해 마지막으로 해제된 <xref:System.Text.StringBuilder> 인스턴스만 저장합니다. 이 간단한 캐싱 전략 덕분에 새 컴파일러에서 할당이 현저히 감소했습니다. .NET Framework 및 MSBuild(“MSBuild”) 부분에서는 비슷한 기법을 사용하여 성능을 향상합니다. 
  
 이 간단한 캐싱 전략은 크기 한도를 포함하므로 좋은 캐시 디자인을 준수합니다. 그러나 이제는 원본보다 코드가 많아져 유지 관리 비용이 더 듭니다. 성능 문제를 발견한 경우에만 캐싱 전략을 채택해야 하며, PerfView에 <xref:System.Text.StringBuilder> 할당이 중요한 기여 요소라는 사실이 표시되어 있습니다. 
  
### <a name="linq-and-lambdas"></a>LINQ 및 람다  
LINQ (언어 통합 쿼리)는 람다 식과 함께 생산성 기능의 예입니다. 그러나 시간이 지남에 따라 성능에 상당한 영향을 줄 수 있으며 코드를 다시 작성 해야 할 수도 있습니다.
  
 **예 5: 람다, List\<t > 및 IEnumerable\<t >**  
  
 이 예제에서는 이름 문자열이 제공될 경우 [LINQ 및 기능 스타일 코드](https://blogs.msdn.microsoft.com/charlie/2007/01/27/anders-hejlsberg-on-linq-and-functional-programming/)를 사용하여 컴파일러 모델에서 기호를 찾습니다.  
  
```csharp  
class Symbol {  
    public string Name { get; private set; }  
    /*...*/  
}  
  
class Compiler {  
    private List<Symbol> symbols;  
    public Symbol FindMatchingSymbol(string name)  
    {  
        return symbols.FirstOrDefault(s => s.Name == name);  
    }  
}  
```  
  
 새 컴파일러와 새 컴파일러에서 빌드된 IDE 환경에서는 `FindMatchingSymbol()`을 매우 자주 호출하며, 이 함수의 코드 한 줄에는 숨겨진 할당이 여러 개 있습니다. 해당 할당을 검토하려면 먼저 함수의 코드 한 줄을 두 줄로 분할합니다.  
  
```csharp  
Func<Symbol, bool> predicate = s => s.Name == name;  
     return symbols.FirstOrDefault(predicate);  
```  
  
 첫 번째 줄에서 [람다 식은](../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) `s => s.Name == name` 지역 변수 `name`를 [통해 닫습니다](https://blogs.msdn.microsoft.com/ericlippert/2003/09/17/what-are-closures/) . 즉, 이 코드에서는 `predicate`를 유지하는 [대리자](../../csharp/language-reference/keywords/delegate.md)에 대한 개체를 할당할 뿐만 아니라 `name`의 값을 캡처하는 환경을 유지하기 위한 정적 클래스를 할당합니다. 컴파일러는 다음과 같은 코드를 생성합니다.  
  
```csharp  
// Compiler-generated class to hold environment state for lambda  
private class Lambda1Environment  
{  
    public string capturedName;  
    public bool Evaluate(Symbol s)  
    {  
        return s.Name == this.capturedName;  
    }  
}  
  
// Expanded Func<Symbol, bool> predicate = s => s.Name == name;  
Lambda1Environment l = new Lambda1Environment() { capturedName = name };  
var predicate = new Func<Symbol, bool>(l.Evaluate);  
```  
  
 이제 두 `new` 할당(환경 클래스에 대한 할당 하나와 대리자에 대한 할당 하나)은 명시적입니다. 
  
 이제 `FirstOrDefault`에 대한 호출을 살펴봅니다. <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 형식에 대한 이 확장 메서드는 할당도 발생시킵니다. `FirstOrDefault`는 해당 첫 번째 인수로 <xref:System.Collections.Generic.IEnumerable%601> 개체를 사용하기 때문에 다음 코드에 대한 호출을 확장할 수 있습니다(설명을 위해 약간 단순화되어 있음).  
  
```csharp  
// Expanded return symbols.FirstOrDefault(predicate) ... 
     IEnumerable<Symbol> enumerable = symbols;  
     IEnumerator<Symbol> enumerator = enumerable.GetEnumerator();  
     while(enumerator.MoveNext())  
     {  
         if (predicate(enumerator.Current))  
             return enumerator.Current;  
     }  
     return default(Symbol);  
```  
  
 `symbols` 변수의 형식은 <xref:System.Collections.Generic.List%601>입니다. <xref:System.Collections.Generic.List%601> 컬렉션 형식은 <xref:System.Collections.Generic.IEnumerable%601>를 구현하고 <xref:System.Collections.Generic.IEnumerator%601>가 <xref:System.Collections.Generic.List%601>로 구현하는 열거자(`struct` 인터페이스)를 영리하게 정의합니다. 클래스 대신 구조를 사용하면 일반적으로 힙 할당을 피하게 되어 가비지 수집 성능에 영향을 줄 수 있습니다. 일반적으로 열거자는 호출 스택에서 반환됨에 따라 열거자 구조를 사용하는 언어의 `foreach` 루프와 함께 사용됩니다. 개체에 대한 공간을 마련하기 위해 호출 스택 포인터를 증분하는 것은 힙 할당에서 수행하는 방식과 관련하여 GC에 영향을 미치지 않습니다. 
  
 확장된 `FirstOrDefault` 호출의 경우 코드에서는 `GetEnumerator()`에 대해 <xref:System.Collections.Generic.IEnumerable%601>를 호출해야 합니다. `symbols` 형식의 `enumerable` 변수에 `IEnumerable<Symbol>`를 할당하면 실제 개체가 <xref:System.Collections.Generic.List%601>라는 정보가 손실됩니다. 즉, 코드에서 `enumerable.GetEnumerator()`로 열거자를 페치하면 .NET Framework가 반환된 구조를 boxing하여 열거자를 `enumerator` 변수에 할당해야 합니다. 
  
 **예제 5에 대한 해결 방법**  
  
 해결 방법은 다음과 같이 `FindMatchingSymbol`을 다시 작성하여 해당 코드 한 줄을 여전히 간결하고, 읽고 이해하기 쉬우며, 유지 관리하기 쉬운 6줄의 코드로 바꾸는 것입니다.  
  
```csharp  
public Symbol FindMatchingSymbol(string name)  
    {  
        foreach (Symbol s in symbols)  
        {  
            if (s.Name == name)  
                return s;  
        }  
        return null;  
    }  
```  
  
 이 코드에서는 LINQ 확장 메서드, 람다 또는 열거자를 사용하지 않으며 할당도 발생하지 않습니다. 컴파일러가 `symbols` 컬렉션이 <xref:System.Collections.Generic.List%601>이고, boxing을 피하기 위한 올바른 형식을 사용하여 결과 열거자(구조)를 로컬 변수에 바인딩할 수 있다는 사실을 알 수 있기 때문에 할당이 없습니다. 이 함수의 원래 버전은 C#의 표현 기능과 .NET Framework의 생산성을 보여 주는 좋은 예였습니다. 보다 효율적인 이 새 버전은 유지 관리할 복잡할 코드를 추가하지 않고 이러한 품질을 유지합니다. 
  
### <a name="async-method-caching"></a>비동기 메서드 캐싱  

다음 예제에서는 [async](../../csharp/programming-guide/concepts/async/index.md) 메서드에 캐시된 결과를 사용하려고 할 때 발생하는 일반적인 문제를 보여 줍니다.
  
 **예제 6: 비동기 메서드의 캐싱**  
  
 새 C# 및 Visual Basic 컴파일러에 빌드된 Visual Studio IDE 기능은 구문 트리를 자주 가져오고, 컴파일러는 Visual Studio의 응답성을 유지하기 위해 이렇게 할 때 비동기 메서드를 사용합니다. 다음은 구문 트리를 가져오기 위해 작성할 수 있는 코드의 첫 번째 버전입니다.  
  
```csharp  
class SyntaxTree { /*...*/ }  
  
class Parser { /*...*/  
    public SyntaxTree Syntax { get; }  
    public Task ParseSourceCode() { /*...*/ }  
}  
  
class Compilation { /*...*/  
    public async Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        var parser = new Parser(); // allocation  
        await parser.ParseSourceCode(); // expensive  
        return parser.Syntax;  
    }  
}  
```  
  
 `GetSyntaxTreeAsync()`를 호출하면 `Parser`가 인스턴스화되고 코드가 구문 분석된 다음 <xref:System.Threading.Tasks.Task> 개체인 `Task<SyntaxTree>`가 반환된다는 사실을 알 수 있습니다. 비용이 많이 드는 부분은 `Parser` 인스턴스를 할당하고 코드를 구문 분석하는 것입니다. 함수는 호출자가 구문 분석 작업을 기다리고, 사용자 입력에 대한 응답성을 유지하도록 UI 스레드를 해제할 수 있도록 <xref:System.Threading.Tasks.Task>를 반환합니다. 
  
 몇 가지 Visual Studio 기능에서는 동일한 구문 트리를 가져오려고 할 수 있으므로, 구문 분석 결과를 캐시하는 다음과 같은 코드를 작성하여 시간을 절약하고 할당을 줄일 수 있습니다. 그러나 이 코드에서는 할당이 발생합니다.  
  
```csharp  
class Compilation { /*...*/  
  
    private SyntaxTree cachedResult;  
  
    public async Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        if (this.cachedResult == null)  
        {  
            var parser = new Parser(); // allocation  
            await parser.ParseSourceCode(); // expensive  
            this.cachedResult = parser.Syntax;  
        }  
        return this.cachedResult;  
    }  
}  
```  
  
 캐싱이 포함된 새 코드에 `SyntaxTree`라는 `cachedResult` 필드가 있는 것을 볼 수 있습니다. 이 필드가 null이면 `GetSyntaxTreeAsync()`가 작동하고 결과를 캐시에 저장합니다. `GetSyntaxTreeAsync()`개체를 `SyntaxTree` 반환 합니다. 문제는 `async` 형식의 `Task<SyntaxTree>` 함수가 있고 `SyntaxTree` 형식의 값을 반환하는 경우 컴파일러가 결과를 유지하기 위해 Task를 할당하는 코드를 내보낸다는 점입니다(`Task<SyntaxTree>.FromResult()` 사용). Task는 완료됨으로 표시되고 결과는 즉시 사용 가능합니다. 새 컴파일러 코드에서 이미 완료된 <xref:System.Threading.Tasks.Task> 개체가 너무 자주 발생했는데, 이러한 할당을 해결함으로써 응답성이 현저히 향상되었습니다. 
  
 **예제 6에 대한 해결 방법**  
  
 완료 <xref:System.Threading.Tasks.Task> 된 할당을 제거 하려면 완료 된 결과를 사용 하 여 작업 개체를 캐시 하면 됩니다.  
  
```csharp  
class Compilation { /*...*/  
  
    private Task<SyntaxTree> cachedResult;  
  
    public Task<SyntaxTree> GetSyntaxTreeAsync()  
    {  
        return this.cachedResult ??   
               (this.cachedResult = GetSyntaxTreeUncachedAsync());  
    }  
  
    private async Task<SyntaxTree> GetSyntaxTreeUncachedAsync()  
    {  
        var parser = new Parser(); // allocation  
        await parser.ParseSourceCode(); // expensive  
        return parser.Syntax;  
    }  
}  
```  
  
 이 코드에서는 `cachedResult`의 형식이 `Task<SyntaxTree>`로 변경되고 `async`의 원래 코드를 유지하는 `GetSyntaxTreeAsync()` 도우미 함수가 채택되었습니다. 이제 `GetSyntaxTreeAsync()`는 `cachedResult`가 null이 아닌 경우 이를 반환하기 위해 [null 병합 연산자](../../csharp/language-reference/operators/null-coalescing-operator.md)를 사용합니다. `cachedResult`가 null인 경우 `GetSyntaxTreeAsync()`는 `GetSyntaxTreeUncachedAsync()`를 호출하고 결과를 캐시합니다. 일반적으로 코드가 그러는 것처럼 `GetSyntaxTreeAsync()`는 `GetSyntaxTreeUncachedAsync()`에 대한 호출을 기다리지 않습니다. await를 사용하지 않는다는 말은 `GetSyntaxTreeUncachedAsync()`에서 해당 <xref:System.Threading.Tasks.Task> 개체를 반환할 때 `GetSyntaxTreeAsync()`가 즉시 <xref:System.Threading.Tasks.Task>를 반환한다는 의미입니다. 이제 캐시된 결과가 <xref:System.Threading.Tasks.Task>이므로 캐시된 결과를 반환하기 위한 할당이 없습니다. 
  
### <a name="additional-considerations"></a>추가 고려 사항  
 다음은 규모가 큰 앱이나 많은 데이터를 처리하는 앱에서 발생할 수 있는 잠재적 문제에 대한 몇 가지 추가 사항입니다. 
  
 **사전**  
  
 사전은 많은 프로그램에서 보편적으로 사용되며 매우 편리하고 본질적으로 효율적이기는 하지만, 빈번히 부적절하게 사용됩니다. Visual Studio 및 새 컴파일러에서 분석에는 단일 요소를 포함했거나 비어 있는 사전이 많이 표시됩니다. 빈 <xref:System.Collections.Generic.Dictionary%602>에는 10개의 필드가 포함되어 있고 이는 x86 컴퓨터의 힙에서 48바이트를 차지합니다. 매핑 또는 결합형 데이터 구조와 일정 시간 조회 기능이 필요한 경우 사전은 유용합니다. 그러나 보유한 요소가 몇 개 되지 않는 경우 사전을 사용하면 많은 공간을 낭비하게 됩니다. 대신, 예를 들어 `List<KeyValuePair\<K,V>>`를 반복적으로 검토할 수 있으며 이는 원래 빠릅니다. 데이터가 포함된 사전을 로드한 다음 이 사전에서 읽기 위한 용도로만 사전을 사용하는 경우(매우 일반적인 패턴), 정렬된 배열과 함께 N(log(N)) 조회 기능을 사용하는 것이 거의 더 빠를 것입니다(사용 중인 요소 수에 따라 다름). 
  
 **클래스 및 구조체**  
  
 어떤 면에서는 클래스와 구조가 앱을 조정하는 것과 관련하여 전통적인 공간/시간 절충 사항을 제공합니다. 클래스는 필드를 포함하지 않는 경우에도 x86 컴퓨터에서 12바이트의 오버헤드를 발생시키지만, 클래스 인스턴스를 나타내는 포인터만 사용하므로 전달 비용이 별로 들지 않습니다. 구조는 boxing되지 않은 경우 힙 할당을 발생시키지 않지만, 큰 구조를 함수 인수 또는 반환 값으로 전달하면 구조의 모든 데이터 멤버를 원자적으로 복사하기 위한 CPU 시간이 걸립니다. 구조를 반환하는 속성에 대한 반복 호출을 감시하고, 해당 속성 값을 로컬 변수에 캐시하여 과도한 데이터 복사를 방지합니다. 
  
 **캐시**  
  
 일반적인 성능 트릭은 결과를 캐시하는 것입니다. 그러나 크기 한도 또는 삭제 정책이 없는 캐시는 메모리 누수가 될 수 있습니다. 많은 양의 데이터를 처리할 때 많은 메모리를 캐시에 유지하면 캐시된 조회의 이점을 무력화시킬 만큼의 가비지 컬렉션이 발생할 수 있습니다. 
  
 이 문서에서는 앱의 응답성에 영향을 미칠 수 있는 성능 병목 현상 증상을 어떻게 알 수 있어야 하는지에 대해 설명했습니다(특히, 대규모 시스템이나 많은 양의 데이터를 처리하는 시스템의 경우). 일반적인 원인으로는 boxing, 문자열 조작, LINQ 및 람다, 비동기 메서드의 캐싱, 크기 제한 또는 삭제 정책이 없는 캐싱, 부적절한 사전 사용 및 구조 전달이 있습니다. 앱을 조정할 때는 다음과 같은 4가지 팩트에 주의하세요.  
  
- 너무 이르게 최적화하지 말 것 – 문제를 찾을 때는 생산성을 유지하고 앱을 조정합니다. 
  
- 프로필은 거짓말하지 않음 – 측정하는 것이 아니라면 추측하는 것일 뿐입니다. 
  
- 좋은 도구가 모든 차별화를 이뤄냄 – PerfView를 다운로드하여 사용해 봅니다. 
  
- 결국은 모두 할당에 관련된 문제임 – 이 부분이 바로 컴파일러 플랫폼 팀이 새 컴파일러의 성능을 향상시키기 위해 대부분의 시간을 사용하는 부분입니다. 
  
## <a name="see-also"></a>참고자료

- [이 항목의 프레젠테이션 비디오](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B333)
- [초보자를 위한 성능 프로파일링 지침](/visualstudio/profiling/beginners-guide-to-performance-profiling)
- [성능](index.md)
- [.NET 성능 팁](https://docs.microsoft.com/previous-versions/dotnet/articles/ms973839(v%3dmsdn.10))
- [Channel 9 PerfView 자습서](https://channel9.msdn.com/Series/PerfView-Tutorial)
- [.NET Compiler Platform SDK](../../csharp/roslyn-sdk/index.md)
- [GitHub의 dotnet/roslyn 리포지토리](https://github.com/dotnet/roslyn)
