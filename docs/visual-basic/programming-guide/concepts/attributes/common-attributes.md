---
title: 공통 특성 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 11fe4894-1bf9-4525-a36b-cddcd3a5d22b
ms.openlocfilehash: 58de23280f2e8765d945ac765d9455a89c45c9cb
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642398"
---
# <a name="common-attributes-visual-basic"></a>공통 특성 (Visual Basic)
이 항목에서는 Visual Basic 프로그램에서 가장 일반적으로 사용 되는 특성을 설명 합니다.  
  
- [전역 특성](#Global)  
  
- [사용되지 않는 특성](#Obsolete)  
  
- [조건부 특성](#Conditional)  
  
- [호출자 정보 특성](#CallerInfo)  
  
- [Visual Basic 특성](#VB)  
  
## <a name="Global"></a> 전역 특성  
 대부분의 특성은 클래스나 메서드와 같은 특정 언어 요소에 적용되지만 일부 특성은 전체 어셈블리나 모듈에 적용되는 전역 특성입니다. 예를 들어 다음과 같이 <xref:System.Reflection.AssemblyVersionAttribute> 특성을 사용하여 버전 정보를 어셈블리에 포함할 수 있습니다.  
  
```vb  
<Assembly: AssemblyVersion("1.0.0.0")>  
```  
  
 전역 특성 뒤의 소스 코드에서 모든 최상위 `Imports` 문 및 형식, 모듈 또는 네임 스페이스 선언 앞입니다. 전역 특성은 여러 소스 파일에 나타날 수 있지만 파일은 하나의 컴파일 패스에서 컴파일되어야 합니다. Visual Basic 프로젝트에 대 한 전역 특성 (파일을 자동으로 만들어집니다 Visual Studio에서 프로젝트를 만들면) AssemblyInfo.vb 파일에서 일반적으로 배치 됩니다.  
  
 어셈블리 특성은 어셈블리에 대한 정보를 제공하는 값입니다. 어셈블리 특성은 다음 범주로 구분됩니다.  
  
- 어셈블리 ID 특성  
  
- 정보 특성  
  
- 어셈블리 매니페스트 특성  
  
### <a name="assembly-identity-attributes"></a>어셈블리 ID 특성  
 name, version 및 culture의 세 가지 특성(해당하는 경우 강력한 이름 포함)이 어셈블리의 ID를 결정합니다. 이러한 특성은 어셈블리의 전체 이름을 구성하며 코드에서 어셈블리를 참조할 때 필요합니다. 특성을 사용하여 어셈블리의 버전 및 문화권을 설정할 수 있습니다. 그러나 이름 값은 어셈블리가 만들어질 때 어셈블리 매니페스트가 포함된 파일에 따라 컴파일러, [어셈블리 정보 대화 상자](/visualstudio/ide/reference/assembly-information-dialog-box)의 Visual Studio IDE 또는 어셈블리 링커(Al.exe)에서 설정됩니다. <xref:System.Reflection.AssemblyFlagsAttribute> 특성은 어셈블리의 여러 복사본이 공존할 수 있는지 여부를 지정합니다.  
  
 다음 표에서는 ID 특성을 보여 줍니다.  
  
|특성|용도|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyName>|어셈블리의 ID를 완전히 설명합니다.|  
|<xref:System.Reflection.AssemblyVersionAttribute>|어셈블리의 버전을 지정합니다.|  
|<xref:System.Reflection.AssemblyCultureAttribute>|어셈블리에서 지원하는 문화권을 지정합니다.|  
|<xref:System.Reflection.AssemblyFlagsAttribute>|어셈블리가 같은 컴퓨터, 같은 프로세스 또는 같은 애플리케이션 도메인에서 Side-by-side 실행을 지원하는지 지정합니다.|  
  
### <a name="informational-attributes"></a>정보 특성  
 정보 특성을 사용하여 어셈블리에 대한 추가 회사 또는 제품 정보를 제공할 수 있습니다. 다음 표에서는 <xref:System.Reflection?displayProperty=nameWithType> 네임스페이스에 정의된 정보 특성을 보여 줍니다.  
  
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
 `Obsolete` 특성은 프로그램 엔터티를 더 이상 사용이 권장되지 않는 항목으로 표시합니다. 나중에 사용되지 않음으로 표시된 엔터티를 사용할 때마다 특성 구성 방법에 따라 경고나 오류가 생성됩니다. 예를 들어:  
  
```vb  
<System.Obsolete("use class B")>   
Class A  
    Sub Method()  
    End Sub  
End Class  
  
Class B  
    <System.Obsolete("use NewMethod", True)>   
    Sub OldMethod()  
    End Sub  
  
    Sub NewMethod()  
    End Sub  
End Class  
```  
  
 이 예제에서는 `Obsolete` 특성이 `A` 클래스 및 `B.OldMethod` 메서드에 적용됩니다. `B.OldMethod`에 적용된 특성 생성자의 두 번째 인수가 `true`로 설정되므로 이 메서드는 컴파일러 오류를 일으키지만, `A` 클래스를 사용하면 경고가 생성됩니다. 그러나 `B.NewMethod`를 호출하면 경고나 오류가 생성되지 않습니다.  
  
 특성 생성자에 첫 번째 인수로 제공된 문자열은 경고 또는 오류의 일부로 표시됩니다. 예를 들어 이전 정의와 함께 사용할 경우 다음 코드에서는 두 개의 경고 및 하나의 오류가 생성됩니다.  
  
```vb  
' Generates 2 warnings:  
' Dim a As New A  
' Generate no errors or warnings:  
  
Dim b As New B  
b.NewMethod()  
  
' Generates an error, terminating compilation:  
' b.OldMethod()  
```  
  
 `A` 클래스에 대한 두 개의 경고가 각각 클래스 참조 선언 및 클래스 생성자에 대해 생성됩니다.  
  
 `Obsolete` 특성은 인수 없이 사용할 수 있지만 항목이 사용되지 않는 이유와 대신 사용이 권장되는 항목에 대한 설명을 포함합니다.  
  
 `Obsolete` 특성은 단일 사용 특성이고 특성을 허용하는 모든 엔터티에 적용할 수 있습니다. `Obsolete`는 <xref:System.ObsoleteAttribute>의 별칭입니다.  
  
## <a name="Conditional"></a> 조건부 특성  
 `Conditional` 특성을 사용하면 메서드 실행이 전처리 식별자에 따라 달라집니다. `Conditional` 특성은 <xref:System.Diagnostics.ConditionalAttribute>의 별칭이고 메서드 또는 특성 클래스에 적용할 수 있습니다.  
  
 이 예제에서 `Conditional`은 프로그램 관련 진단 정보 표시를 사용하거나 사용하지 않도록 설정하는 메서드에 적용됩니다.  
  
```vb  
#Const TRACE_ON = True  
Imports System  
Imports System.Diagnostics  
Module TestConditionalAttribute  
    Public Class Trace  
        <Conditional("TRACE_ON")>   
        Public Shared Sub Msg(ByVal msg As String)  
            Console.WriteLine(msg)  
        End Sub  
  
    End Class  
  
    Sub Main()  
        Trace.Msg("Now in Main...")  
        Console.WriteLine("Done.")  
    End Sub  
End Module  
```  
  
 `TRACE_ON` 식별자가 정의되지 않으면 추적 출력이 표시되지 않습니다.  
  
 `Conditional` 특성은 보통 `DEBUG` 식별자와 함께 사용하여 다음과 같이 릴리스 빌드가 아닌 디버그 빌드의 추적 및 로깅 기능을 사용하도록 설정합니다.  
  
```vb  
<Conditional("DEBUG")>   
Shared Sub DebugMethod()  
  
End Sub  
```  
  
 조건부로 표시된 메서드를 호출하면 지정된 전처리 기호가 있는지 여부에 따라 호출을 포함 또는 생략할지 결정됩니다. 기호가 정의되면 호출이 포함되고, 정의되지 않으면 호출이 생략됩니다. 다음과 같이 메서드를 `#if…#endif` 블록 내부에 포함하는 것보다 `Conditional`을 사용하는 것이 더 분명하고 더 정교하며 오류 가능성이 더 적습니다.  
  
```vb  
#If DEBUG Then  
    Sub ConditionalMethod()  
    End Sub  
#End If  
```  
  
 조건부 메서드는 클래스 또는 구조체 선언의 메서드여야 하고 반환 값을 포함하지 않아야 합니다.  
  
### <a name="using-multiple-identifiers"></a>여러 식별자 사용  
 한 메서드에 여러 `Conditional` 특성이 있을 경우 조건부 기호 중 하나 이상이 정의되면(즉, 기호가 OR 연산자를 통해 논리적으로 함께 연결되면) 메서드 호출이 포함됩니다. 이 예제에서는 `A` 또는 `B`가 있으면 메서드 호출이 발생합니다.  
  
```vb  
<Conditional("A"), Conditional("B")>   
Shared Sub DoIfAorB()  
  
End Sub  
```  
  
 AND 연산자를 통해 기호를 논리적으로 연결하는 결과를 얻으려면 순차적 조건부 메서드를 정의합니다. 예를 들어 아래 두 번째 메서드는 `A` 및 `B`가 둘 다 정의된 경우에만 실행됩니다.  
  
```vb  
<Conditional("A")>   
Shared Sub DoIfA()  
    DoIfAandB()  
End Sub  
  
<Conditional("B")>   
Shared Sub DoIfAandB()  
    ' Code to execute when both A and B are defined...  
End Sub  
```  
  
### <a name="using-conditional-with-attribute-classes"></a>특성 클래스와 함께 조건부 사용  
 `Conditional` 특성을 특성 클래스 정의에 적용할 수도 있습니다. 이 예제에서 사용자 지정 특성 `Documentation`은 DEBUG가 정의된 경우에만 메타데이터에 정보를 추가합니다.  
  
```vb  
<Conditional("DEBUG")>   
Public Class Documentation  
    Inherits System.Attribute  
    Private text As String  
    Sub New(ByVal doc_text As String)  
        text = doc_text  
    End Sub  
End Class  
  
Class SampleClass  
    ' This attribute will only be included if DEBUG is defined.  
    <Documentation("This method displays an integer.")>   
    Shared Sub DoWork(ByVal i As Integer)  
        System.Console.WriteLine(i)  
    End Sub  
End Class  
```  
  
## <a name="CallerInfo"></a> 호출자 정보 특성  
 호출자 정보 특성을 사용하여 메서드 호출자에 대한 정보를 얻을 수 있습니다. 소스 코드 파일 경로, 소스 코드 줄 번호 및 호출자의 멤버 이름을 얻을 수 있습니다.  
  
 멤버 호출자 정보를 얻으려면 선택적 매개 변수에 적용되는 특성을 사용합니다. 각 선택적 매개 변수는 기본값을 지정합니다. 다음 표에서는 <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> 네임스페이스에 정의된 호출자 정보 특성을 보여줍니다.  
  
|특성|설명|형식|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|호출자를 포함한 소스 파일의 전체 경로입니다. 컴파일 시간의 경로입니다.|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|메서드가 호출되는 소스 파일의 줄 번호입니다.|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|호출자의 메서드 이름 또는 속성 이름입니다. 자세한 내용은 [호출자 정보 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/caller-information.md)합니다.|`String`|  
  
 호출자 정보 특성에 대 한 자세한 내용은 참조 하세요. [호출자 정보 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/caller-information.md)합니다.  
  
## <a name="VB"></a> Visual Basic 특성  
 다음 표에서 Visual Basic에 관련 된 특성을 나열 합니다.  
  
|특성|용도|  
|---------------|-------------|  
|<xref:Microsoft.VisualBasic.ComClassAttribute>|COM 개체로 클래스 표시 되는 컴파일러를 나타냅니다.|  
|<xref:Microsoft.VisualBasic.HideModuleNameAttribute>|모듈 멤버를에 모듈에 필요한 자격만을 사용 하 여 액세스할 수 있습니다.|  
|<xref:Microsoft.VisualBasic.VBFixedStringAttribute>|입력 및 출력 파일을 사용 하 여 사용 하기 위해 구조의 고정 길이 문자열의 크기를 지정 함수입니다.|  
|<xref:Microsoft.VisualBasic.VBFixedArrayAttribute>|입력 및 출력 파일을 사용 하 여 사용 하기 위해 구조의 고정 배열의 크기를 지정 함수입니다.|  
  
### <a name="comclassattribute"></a>COMClassAttribute  
 사용 하 여 `COMClassAttribute` Visual Basic에서 COM 구성 요소를 만드는 과정을 간소화 하기 위해. COM 개체는 하지 않고.NET Framework 어셈블리에서 상당히 다른 `COMClassAttribute`, 다양 한 Visual Basic에서 COM 개체를 생성 하는 단계를 수행 해야 합니다. 로 표시 된 클래스 `COMClassAttribute`, 컴파일러가 이러한 단계의 대부분을 자동으로 수행 합니다.  
  
### <a name="hidemodulenameattribute"></a>HideModuleNameAttribute  
 사용 하 여 `HideModuleNameAttribute` 모듈 멤버에 모듈에 필요한 자격만을 사용 하 여 액세스할 수 있도록 합니다.  
  
### <a name="vbfixedstringattribute"></a>VBFixedStringAttribute  
 사용 하 여 `VBFixedStringAttribute` 고정 길이의 문자열을 만들려면 Visual Basic을 강제 합니다. 기본적으로 가변 길이 문자열 되며이 특성은 문자열을 파일을 저장할 때 유용 합니다. 다음 코드에서는이 보여 줍니다.  
  
```vb  
Structure Worker  
    ' The runtime uses VBFixedString to determine   
    ' if the field should be written out as a fixed size.  
    <VBFixedString(10)> Public LastName As String  
    <VBFixedString(7)> Public Title As String  
    <VBFixedString(2)> Public Rank As String  
End Structure  
```  
  
### <a name="vbfixedarrayattribute"></a>VBFixedArrayAttribute  
 사용 하 여 `VBFixedArrayAttribute` 크기에서 수정 된 배열을 선언할 수 있습니다. Visual Basic 문자열 처럼 배열은 기본적으로 가변 길이입니다. 이 특성은 파일에 데이터를 쓰거나 직렬화 하는 경우에 유용 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Reflection>
- <xref:System.Attribute>
- [Visual Basic 프로그래밍 가이드](../../../../visual-basic/programming-guide/index.md)
- [특성](../../../../standard/attributes/index.md)
- [리플렉션(Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)
- [리플렉션을 사용하여 특성 액세스(Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
