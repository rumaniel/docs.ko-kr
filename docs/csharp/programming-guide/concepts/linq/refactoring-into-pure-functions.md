---
title: 순수 함수로 리팩터링(C#)
ms.date: 07/20/2015
ms.assetid: 2944a0d4-fd33-4e2e-badd-abb0f9be2fcc
ms.openlocfilehash: 4cf91ff078bd1c4582daa05475a91c4a4ecaba3e
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253108"
---
# <a name="refactoring-into-pure-functions-c"></a>순수 함수로 리팩터링(C#)

순수 함수 변환의 중요한 측면은 순수 함수를 사용하여 코드를 리팩터링하는 방법을 습득하는 것입니다.  
  
> [!NOTE]
> 함수형 프로그래밍에서 일반적인 부분은 순수 함수를 사용하여 프로그램을 리팩터링하는 것입니다. Visual Basic과 C++에서 이러한 리팩터링은 각 언어에서 함수의 사용과 결합됩니다. 그러나 C#에서는 함수를 메서드라고 합니다. 이 논의의 목적을 위해 순수 함수는 C#에서 메서드로 구현됩니다.  
  
 이 단원의 앞 부분에서 설명한 것처럼 순수 함수에는 두 가지 유용한 특징이 있습니다.  
  
- 순수 함수는 의도하지 않은 결과를 발생시키지 않습니다. 함수는 함수 외부에 있는 형식의 데이터나 변수를 변경하지 않습니다.  
  
- 순수 함수는 일관성이 있습니다. 동일한 입력 데이터의 집합이 제공되는 경우 항상 동일한 출력 값을 반환합니다.  
  
 함수형 프로그래밍으로 전환하는 한 가지 방법은 기존 코드를 리팩터링하여 의도하지 않은 불필요한 결과와 외부 종속성을 없애는 것입니다. 이런 식으로 기존 코드의 순수 함수 버전을 만들 수 있습니다.  
  
 이 항목에서는 순수 함수의 개념과 순수 함수가 의미하지 않는 것에 대해 설명합니다. [자습서: WordprocessingML 문서에서 내용 조작(C#)](./shape-of-wordprocessingml-documents.md) 자습서에서는 WordprocessingML 문서를 조작하는 방법을 보여 주며 순수 함수를 사용하여 리팩터링하는 방법에 대한 두 가지 예제를 제공합니다.  
  
## <a name="eliminating-side-effects-and-external-dependencies"></a>의도하지 않은 결과 및 외부 종속성 제거  
 다음 예제에서는 두 가지 비순수 함수와 순수 함수를 대조합니다.  
  
### <a name="non-pure-function-that-changes-a-class-member"></a>클래스 멤버를 변경하는 비순수 함수  
 다음 코드에서 `HyphenatedConcat` 함수는 클래스에서 `aMember` 데이터 멤버를 수정하기 때문에 순수 함수가 아닙니다.  
  
```csharp  
public class Program  
{  
    private static string aMember = "StringOne";  
  
    public static void HyphenatedConcat(string appendStr)  
    {  
        aMember += '-' + appendStr;  
    }  
  
    public static void Main()  
    {  
        HyphenatedConcat("StringTwo");  
        Console.WriteLine(aMember);  
    }  
}  
```  
  
 이 코드의 결과는 다음과 같습니다.  
  
```output  
StringOne-StringTwo  
```  
  
 이 출력은 수정되는 데이터가 `public` 또는 `private` 액세스 권한을 갖고 있는지 여부나 `static` 멤버 또는 인스턴스 멤버인지 여부와 무관합니다. 순수 함수는 함수 외부에 있는 데이터를 변경하지 않습니다.  
  
### <a name="non-pure-function-that-changes-an-argument"></a>인수를 변경하는 비순수 함수  
 또한 이 동일한 함수의 다음 버전은 매개 변수 `sb`의 내용을 수정하기 때문에 순수 함수가 아닙니다.  
  
```csharp  
public class Program  
{  
    public static void HyphenatedConcat(StringBuilder sb, String appendStr)  
    {  
        sb.Append('-' + appendStr);  
    }  
  
    public static void Main()  
    {  
        StringBuilder sb1 = new StringBuilder("StringOne");  
        HyphenatedConcat(sb1, "StringTwo");  
        Console.WriteLine(sb1);  
    }  
}  
```  
  
 `HyphenatedConcat` 함수가 <xref:System.Text.StringBuilder.Append%2A> 멤버 함수를 호출하여 첫 번째 매개 변수의 값(상태)을 변경했기 때문에 이 프로그램 버전은 첫 번째 버전과 동일한 출력을 생성합니다. 이러한 변경은 `HyphenatedConcat`에서 값에 의한 호출(call-by-value) 매개 변수 전달을 사용함에도 불구하고 발생합니다.  
  
> [!IMPORTANT]
> 참조 형식의 경우 값에 의해 매개 변수를 전달하면 개체에 대한 참조의 복사본이 전달됩니다. 이 복사본은 참조 변수가 새 개체에 할당될 때까지 원래 참조와 동일한 인스턴스 데이터와 연결되어 있습니다. 참조에 의한 호출(call-by-reference)을 사용하는 경우 함수에서 반드시 매개 변수를 수정해야 할 필요가 없습니다.  
  
### <a name="pure-function"></a>순수 함수  
이 다음 버전의 프로그램에서는 `HyphenatedConcat` 함수를 순수 함수로 구현하는 방법을 보여 줍니다.  
  
```csharp  
class Program  
{  
    public static string HyphenatedConcat(string s, string appendStr)  
    {  
        return (s + '-' + appendStr);  
    }  
  
    public static void Main(string[] args)  
    {  
        string s1 = "StringOne";  
        string s2 = HyphenatedConcat(s1, "StringTwo");  
        Console.WriteLine(s2);  
    }  
}  
```  
  
 이 버전은 동일한 출력 `StringOne-StringTwo`를 생성합니다. 연결된 값을 유지하기 위해 해당 값은 중간 변수 `s2`에 저장됩니다.  
  
 매우 유용할 수 있는 한 가지 방법은 로컬로는 순수하지 않지만(즉, 지역 변수를 선언하고 수정함) 전역적으로는 순수한 함수를 작성하는 것입니다. 이러한 함수는 유용한 조합성(composability) 특징을 많이 갖고 있지만 간단한 루프가 동일한 작업을 수행하는 경우 재귀를 사용해야 하는 등의 더욱 꼬인(convoluted) 함수형 프로그래밍 특징을 방지합니다.  
  
## <a name="standard-query-operators"></a>표준 쿼리 연산자  
 표준 쿼리 연산자의 중요한 특징은 순수 함수로 구현된다는 점입니다.  
  
 자세한 내용은 [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [순수 함수 변환 소개(C#)](./introduction-to-pure-functional-transformations.md)
- [함수형 프로그래밍과 명령형 프로그래밍 비교(C#)](./functional-programming-vs-imperative-programming.md)
