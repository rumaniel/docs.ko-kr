---
title: 공통 특성(C#)
ms.date: 07/20/2015
ms.assetid: 785a0526-6c0e-4599-8c61-ccdc88dd9965
ms.openlocfilehash: 7988dad410c6e51869ec9d7e40d94e874443a5f8
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595465"
---
# <a name="common-attributes-c"></a>공통 특성(C#)
이 항목에서는 C# 프로그램에서 가장 일반적으로 사용되는 특성을 설명합니다.  
  
- [전역 특성](#Global)  
  
- [사용되지 않는 특성](#Obsolete)  
  
- [조건부 특성](#Conditional)  
  
- [호출자 정보 특성](#CallerInfo)  
  
## <a name="Global"></a> 전역 특성  
 대부분의 특성은 클래스나 메서드와 같은 특정 언어 요소에 적용되지만 일부 특성은 전체 어셈블리나 모듈에 적용되는 전역 특성입니다. 예를 들어 다음과 같이 <xref:System.Reflection.AssemblyVersionAttribute> 특성을 사용하여 버전 정보를 어셈블리에 포함할 수 있습니다.  
  
```csharp  
[assembly: AssemblyVersion("1.0.0.0")]  
```  
  
 전역 특성은 소스 코드에서 최상위 `using` 지시문 뒤 그리고 형식, 모듈 또는 네임스페이스 선언 앞에 나타납니다. 전역 특성은 여러 소스 파일에 나타날 수 있지만 파일은 하나의 컴파일 패스에서 컴파일되어야 합니다. C# 프로젝트에서 전역 특성은 AssemblyInfo.cs 파일에 삽입됩니다.  
  
 어셈블리 특성은 어셈블리에 대한 정보를 제공하는 값입니다. 어셈블리 특성은 다음 범주로 구분됩니다.  
  
- 어셈블리 ID 특성  
  
- 정보 특성  
  
- 어셈블리 매니페스트 특성  
  
### <a name="assembly-identity-attributes"></a>어셈블리 ID 특성  
 name, version 및 culture의 세 가지 특성(해당하는 경우 강력한 이름 포함)이 어셈블리의 ID를 결정합니다. 이러한 특성은 어셈블리의 전체 이름을 구성하며 코드에서 어셈블리를 참조할 때 필요합니다. 특성을 사용하여 어셈블리의 버전 및 문화권을 설정할 수 있습니다. 그러나 이름 값은 어셈블리가 만들어질 때 어셈블리 매니페스트가 포함된 파일에 따라 컴파일러, [어셈블리 정보 대화 상자](/visualstudio/ide/reference/assembly-information-dialog-box)의 Visual Studio IDE 또는 어셈블리 링커(Al.exe)에서 설정됩니다. <xref:System.Reflection.AssemblyFlagsAttribute> 특성은 어셈블리의 여러 복사본이 공존할 수 있는지 여부를 지정합니다.  
  
 다음 표에서는 ID 특성들을 보여 줍니다.  
  
|특성|용도|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyName>|어셈블리의 ID를 모두 설명합니다.|  
|<xref:System.Reflection.AssemblyVersionAttribute>|어셈블리의 버전을 지정합니다.|  
|<xref:System.Reflection.AssemblyCultureAttribute>|어셈블리에서 지원하는 문화권을 지정합니다.|  
|<xref:System.Reflection.AssemblyFlagsAttribute>|어셈블리가 같은 컴퓨터, 같은 프로세스 또는 같은 애플리케이션 도메인에서 Side-by-side 실행을 지원하는지 지정합니다.|  
  
### <a name="informational-attributes"></a>정보 특성  
 정보 특성을 사용하여 어셈블리와 연관된 회사 또는 제품에 대한 추가적인 정보를 제공할 수 있습니다. 다음 표에서는 <xref:System.Reflection?displayProperty=nameWithType> 네임스페이스에 정의된 정보 특성을 보여 줍니다.  
  
|특성|용도|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyProductAttribute>|어셈블리 매니페스트에 대한 제품 이름을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyTrademarkAttribute>|어셈블리 매니페스트에 대한 상표를 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|어셈블리 매니페스트에 대한 정보 버전을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyCompanyAttribute>|어셈블리 매니페스트에 대한 회사 이름을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyCopyrightAttribute>|어셈블리 매니페스트에 대한 저작권을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyFileVersionAttribute>|Win32 파일 버전 리소스에 대한 특정 버전 번호를 사용하도록 컴파일러에 지시합니다.|  
|<xref:System.CLSCompliantAttribute>|어셈블리가 CLS(공용 언어 사양)을 준수하는지 여부를 나타냅니다.|  
  
### <a name="assembly-manifest-attributes"></a>어셈블리 매니페스트 특성  
 어셈블리 매니페스트 특성을 사용하여 어셈블리 매니페스트의 정보를 제공할 수 있습니다. 정보에는 제목, 설명, 기본 별칭 및 구성이 포함됩니다. 다음 표에서는 <xref:System.Reflection?displayProperty=nameWithType> 네임스페이스에 정의된 어셈블리 매니페스트 특성을 보여 줍니다.  
  
|특성|용도|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyTitleAttribute>|어셈블리 매니페스트에 대한 어셈블리 제목을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyDescriptionAttribute>|어셈블리 매니페스트에 대한 어셈블리 설명을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyConfigurationAttribute>|어셈블리 매니페스트에 대한 어셈블리 구성(예: 정품 또는 디버그)을 지정하는 사용자 지정 특성을 정의합니다.|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|어셈블리 매니페스트에 대한 친숙한 기본 별칭을 정의합니다.|  
  
## <a name="Obsolete"></a> 사용되지 않는 특성  
 `Obsolete` 특성은 프로그램 엔터티를 더 이상 사용이 권장되지 않는 항목으로 표시합니다. 나중에 사용되지 않음으로 표시된 엔터티를 사용할 때마다 특성 구성 방법에 따라 경고나 오류가 생성됩니다. 예를 들면 다음과 같습니다:  
  
```csharp  
[System.Obsolete("use class B")]  
class A  
{  
    public void Method() { }  
}  
class B  
{  
    [System.Obsolete("use NewMethod", true)]  
    public void OldMethod() { }  
    public void NewMethod() { }  
}  
```  
  
 이 예제에서는 `Obsolete` 특성이 `A` 클래스 및 `B.OldMethod` 메서드에 적용됩니다. `B.OldMethod`에 적용된 특성 생성자의 두 번째 인수가 `true`로 설정되므로 이 메서드는 컴파일러 오류를 일으키지만, `A` 클래스를 사용하면 경고가 생성됩니다. 그러나 `B.NewMethod`를 호출하면 경고나 오류가 생성되지 않습니다.  
  
 특성 생성자에 첫 번째 인수로 제공된 문자열은 경고 또는 오류의 일부로 표시됩니다. 예를 들어 이전 정의와 함께 사용할 경우 다음 코드에서는 두 개의 경고 및 하나의 오류가 생성됩니다.  
  
```csharp  
// Generates 2 warnings:  
// A a = new A();  
  
// Generate no errors or warnings:  
B b = new B();  
b.NewMethod();  
  
// Generates an error, terminating compilation:  
// b.OldMethod();  
```  
  
 `A` 클래스에 대한 두 개의 경고가 각각 클래스 참조 선언 및 클래스 생성자에 대해 생성됩니다.  
  
 `Obsolete` 특성은 인수 없이 사용할 수 있지만 항목이 사용되지 않는 이유와 대신 사용이 권장되는 항목에 대한 설명을 포함합니다.  
  
 `Obsolete` 특성은 단일 사용 특성이고 특성을 허용하는 모든 엔터티에 적용할 수 있습니다. `Obsolete`는 <xref:System.ObsoleteAttribute>의 별칭입니다.  
  
## <a name="Conditional"></a> 조건부 특성  
 `Conditional` 특성을 사용하면 메서드 실행이 전처리 식별자에 따라 달라집니다. `Conditional` 특성은 <xref:System.Diagnostics.ConditionalAttribute>의 별칭이고 메서드 또는 특성 클래스에 적용할 수 있습니다.  
  
 이 예제에서 `Conditional`은 프로그램 관련 진단 정보 표시를 사용하거나 사용하지 않도록 설정하는 메서드에 적용됩니다.  
  
```csharp  
#define TRACE_ON  
using System;  
using System.Diagnostics;  
  
public class Trace  
{  
    [Conditional("TRACE_ON")]  
    public static void Msg(string msg)  
    {  
        Console.WriteLine(msg);  
    }  
}  
  
public class ProgramClass  
{  
    static void Main()  
    {  
        Trace.Msg("Now in Main...");  
        Console.WriteLine("Done.");  
    }  
}  
```  
  
 `TRACE_ON` 식별자가 정의되지 않으면 추적 출력이 표시되지 않습니다.  
  
 `Conditional` 특성은 보통 `DEBUG` 식별자와 함께 사용하여 다음과 같이 릴리스 빌드가 아닌 디버그 빌드의 추적 및 로깅 기능을 사용하도록 설정합니다.  
  
```csharp  
[Conditional("DEBUG")]  
static void DebugMethod()  
{  
}  
```  
  
 조건부로 표시된 메서드를 호출하면 지정된 전처리 기호가 있는지 여부에 따라 호출을 포함 또는 생략할지 결정됩니다. 기호가 정의되면 호출이 포함되고, 정의되지 않으면 호출이 생략됩니다. 다음과 같이 메서드를 `#if…#endif` 블록 내부에 포함하는 것보다 `Conditional`을 사용하는 것이 더 분명하고 더 정교하며 오류 가능성이 더 적습니다.  
  
```csharp  
#if DEBUG  
    void ConditionalMethod()  
    {  
    }  
#endif  
```  
  
 조건부 메서드는 클래스 또는 구조체 선언의 메서드여야 하고 반환 값을 포함하지 않아야 합니다.  
  
### <a name="using-multiple-identifiers"></a>여러 식별자 사용  
 한 메서드에 여러 `Conditional` 특성이 있을 경우 조건부 기호 중 하나 이상이 정의되면(즉, 기호가 OR 연산자를 통해 논리적으로 함께 연결되면) 메서드 호출이 포함됩니다. 이 예제에서는 `A` 또는 `B`가 있으면 메서드 호출이 발생합니다.  
  
```csharp  
[Conditional("A"), Conditional("B")]  
static void DoIfAorB()  
{  
    // ...  
}  
```  
  
 AND 연산자를 통해 기호를 논리적으로 연결하는 결과를 얻으려면 순차적 조건부 메서드를 정의합니다. 예를 들어 아래 두 번째 메서드는 `A` 및 `B`가 둘 다 정의된 경우에만 실행됩니다.  
  
```csharp
[Conditional("A")]  
static void DoIfA()  
{  
    DoIfAandB();  
}  
  
[Conditional("B")]  
static void DoIfAandB()  
{  
    // Code to execute when both A and B are defined...  
}  
```  
  
### <a name="using-conditional-with-attribute-classes"></a>특성 클래스와 함께 조건부 사용  
 `Conditional` 특성을 특성 클래스 정의에 적용할 수도 있습니다. 이 예제에서 사용자 지정 특성 `Documentation`은 DEBUG가 정의된 경우에만 메타데이터에 정보를 추가합니다.  
  
```csharp  
[Conditional("DEBUG")]  
public class Documentation : System.Attribute  
{  
    string text;  
  
    public Documentation(string text)  
    {  
        this.text = text;  
    }  
}  
  
class SampleClass  
{  
    // This attribute will only be included if DEBUG is defined.  
    [Documentation("This method displays an integer.")]  
    static void DoWork(int i)  
    {  
        System.Console.WriteLine(i.ToString());  
    }  
}  
```  
  
## <a name="CallerInfo"></a> 호출자 정보 특성  
 호출자 정보 특성을 사용하여 메서드 호출자에 대한 정보를 얻을 수 있습니다. 소스 코드 파일 경로, 소스 코드 줄 번호 및 호출자의 멤버 이름을 얻을 수 있습니다.  
  
 멤버 호출자 정보를 얻으려면 선택적 매개 변수에 적용되는 특성을 사용합니다. 각 선택적 매개 변수는 기본값을 지정합니다. 다음 표에서는 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 네임스페이스에 정의된 호출자 정보 특성을 보여줍니다.  
  
|특성|설명|형식|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|호출자를 포함한 소스 파일의 전체 경로입니다. 컴파일 시간의 경로입니다.|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|메서드가 호출되는 소스 파일의 줄 번호입니다.|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|호출자의 메서드 이름 또는 속성 이름입니다. 자세한 내용은 [호출자 정보(C#)](../caller-information.md)를 참조하세요.|`String`|  
  
 호출자 정보 특성에 대한 자세한 내용은 [호출자 정보(C#)](../caller-information.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Reflection>
- <xref:System.Attribute>
- [C# 프로그래밍 가이드](../../index.md)
- [특성](../../../../standard/attributes/index.md)
- [리플렉션(C#)](../reflection.md)
- [리플렉션을 사용하여 특성 액세스(C#)](./accessing-attributes-by-using-reflection.md)
