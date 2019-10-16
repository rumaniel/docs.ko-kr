---
title: '연습: Visual Studio에 관리되는 어셈블리의 형식 포함'
ms.date: 08/19/2019
ms.assetid: 55ed13c9-c5bb-4bc2-bcd8-0587eb568864
dev_langs:
- csharp
- vb
ms.openlocfilehash: 1f32bd840efa97b62097a2d051c25d519785b381
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972734"
---
# <a name="walkthrough-embed-types-from-managed-assemblies-in-visual-studio"></a>연습: Visual Studio에 관리되는 어셈블리의 형식 포함

강력한 이름의 관리되는 어셈블리에서 형식 정보를 포함하는 경우 애플리케이션에서 유형을 느슨하게 연결하여 버전 독립성을 확보할 수 있습니다. 즉, 새로운 버전마다 다시 컴파일하지 않고도 관리되는 라이브러리의 모든 버전에서 형식을 사용하도록 프로그램을 작성할 수 있습니다.

형식 포함은 Microsoft Office의 자동화 개체를 사용하는 애플리케이션과 같은 COM interop에서 자주 사용됩니다. 형식 정보를 포함하면 서로 다른 컴퓨터의 서로 다른 Microsoft Office 버전에서 동일한 빌드의 프로그램을 작동할 수 있습니다. 그러나 완전 관리형 솔루션에서도 형식 포함을 사용할 수 있습니다.

포함할 수 있는 공용 인터페이스를 지정한 후 이러한 인터페이스를 구현하는 런타임 클래스를 만듭니다. 클라이언트 프로그램은 공용 인터페이스가 포함된 어셈블리를 참조하고 참조의 `Embed Interop Types` 속성을 `True`로 설정하여 디자인 타임에 해당 인터페이스의 형식 정보를 포함할 수 있습니다. 그러면 클라이언트 프로그램은 해당 인터페이스로 형식이 지정된 런타임 개체의 인스턴스를 로드할 수 있습니다. 이는 명령줄 컴파일러를 사용하고 `/link` 컴파일러 옵션을 사용하여 어셈블리를 참조하는 것과 같습니다. 

강력한 이름의 런타임 어셈블리의 새 버전을 만들면 클라이언트 프로그램을 다시 컴파일할 필요가 없습니다. 클라이언트 프로그램은 공용 인터페이스의 포함된 형식 정보를 통해 사용 가능한 런타임 어셈블리 버전을 계속 사용합니다.

이 연습에서는 다음을 수행합니다.

1. 포함할 수 있는 형식 정보가 있는 공개 인터페이스와 함께 강력한 이름의 어셈블리를 만듭니다.
1. 공용 인터페이스를 구현하는 강력한 이름의 런타임 어셈블리를 만듭니다.
1. 공용 인터페이스에서 형식 정보를 포함하고 런타임 어셈블리에서 클래스의 인스턴스를 만드는 클라이언트 프로그램을 만듭니다.
1. 런타임 어셈블리를 수정하고 다시 빌드합니다.
1. 클라이언트 프로그램을 실행하면 다시 컴파일하지 않고도 클라이언트 프로그램이 런타임 어셈블리의 새 버전을 사용하는지 확인할 수 있습니다.

[!INCLUDE[note_settings_general](../../../includes/note-settings-general-md.md)]

## <a name="conditions-and-limitations"></a>조건 및 제한 사항

다음 조건에서는 어셈블리의 형식 정보를 포함할 수 있습니다. 

- 어셈블리는 하나 이상의 공용 인터페이스를 제공합니다.
- 포함된 인터페이스는 고유한 GUID가 있는 `ComImport` 특성 및 `Guid` 특성으로 주석이 추가됩니다.
- 어셈블리는 `ImportedFromTypeLib` 특성이나 `PrimaryInteropAssembly` 특성, 그리고 어셈블리 수준의 `Guid` 특성으로 주석이 추가됩니다. Visual C# 및 Visual Basic 프로젝트 템플릿에는 기본적으로 어셈블리 수준의 `Guid` 특성이 포함됩니다.

형식 포함의 기본 기능은 COM interop 어셈블리를 지원하는 것이므로 완전 관리형 솔루션에 형식 정보를 포함할 때 다음과 같은 제한 사항이 적용됩니다.

- COM interop 관련 특성만 포함됩니다. 다른 특성은 무시됩니다.
- 형식이 제네릭 매개 변수를 사용하고 제네릭 매개 변수의 형식이 포함된 형식인 경우 해당 형식을 어셈블리 경계를 넘어 사용할 수 없습니다. 어셈블리 경계를 넘어가는 예로는 다른 어셈블리에서 메서드를 호출하는 경우 또는 다른 어셈블리에 정의된 형식에서 형식이 파생되는 경우를 들 수 있습니다.
- 상수는 포함되지 않습니다.
- <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> 클래스는 포함된 형식을 키로 지원하지 않습니다. 포함된 형식을 키로서 지원하도록 고유한 사전 형식을 구현할 수 있습니다.

## <a name="create-an-interface"></a>인터페이스 만들기

첫 번째 단계는 형식 동등 인터페이스 프로젝트를 만드는 것입니다. 

1. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
   
1. **새 프로젝트 만들기** 대화 상자에서 **템플릿 검색** 상자에 *class library*를 입력합니다. 목록에서 C# 또는 VB **클래스 라이브러리(.NET Framework)** 템플릿을 선택한 후 **다음**을 선택합니다. 
   
1. **새 프로젝트 구성** 대화 상자에서 **프로젝트 이름**에 *TypeEquivalenceInterface*를 입력한 다음 **만들기**를 선택합니다. 새 프로젝트가 만들어집니다.
   
1. **솔루션 탐색기**에서 *Class1.cs* 또는 *Class1.vb* 파일을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택하여 파일 이름을 *Class1*에서 *ISampleInterface*로 바꿉니다. 클래스의 이름도 `ISampleInterface`로 바꿀지 묻는 메시지가 표시되면 **예**라고 답합니다. 이 클래스는 클래스의 공용 인터페이스를 나타냅니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceInterface** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다. 
   
1. **속성** 화면의 왼쪽 창에서 **빌드**를 선택하고 **출력 경로**를 *C:\TypeEquivalenceSample* 같은 컴퓨터의 위치로 설정합니다. 이 연습 전체에서 동일한 위치를 사용합니다. 
   
1. **속성** 화면의 왼쪽 창에서 **서명**을 선택한 다음 **어셈블리에 서명** 확인란을 선택합니다. **강력한 이름 키 파일 선택** 드롭다운 목록에서 **새로 만들기**를 선택합니다. 
   
1. **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 *key.snk*를 입력합니다. **암호로 내 키 파일 보호** 확인란의 선택을 취소한 다음 **확인**을 선택합니다.
   
1. 코드 편집기에서 *ISampleInterface* 클래스를 열고 콘텐츠를 다음 코드로 바꾸어 `ISampleInterface` 인터페이스를 만듭니다.
   
   ```csharp
   using System;
   using System.Runtime.InteropServices;
   
   namespace TypeEquivalenceInterface
   {
       [ComImport]
       [Guid("8DA56996-A151-4136-B474-32784559F6DF")]
       public interface ISampleInterface
       {
           void GetUserInput();
           string UserInput { get; }
       }
   }
   ```
   
   ```vb
   Imports System.Runtime.InteropServices
   
   <ComImport()>
   <Guid("8DA56996-A151-4136-B474-32784559F6DF")>
   Public Interface ISampleInterface
       Sub GetUserInput()
       ReadOnly Property UserInput As String
   End Interface
   ```
   
1. **도구** 메뉴에서 **GUID 만들기**를 선택하고 **GUID 만들기** 대화 상자에서 **레지스트리 형식**을 선택합니다. **복사**를 선택한 다음 **끝내기**를 선택합니다.
   
1. 코드의 `Guid` 특성에서 샘플 GUID를 복사한 GUID로 바꾸고 중괄호( **{ }** )를 제거합니다.
   
1. **솔루션 탐색기**에서 **속성** 폴더를 펼치고 *AssemblyInfo.cs* 또는 *AssemblyInfo.vb* 파일을 선택합니다. 코드 편집기에서 파일에 다음 특성을 추가합니다.
   
   ```csharp
   [assembly: ImportedFromTypeLib("")]
   ```
   
   ```vb
   <Assembly: ImportedFromTypeLib("")>
   ```
   
1. **파일** > **모두 저장**을 선택하거나 **Ctrl**+**Shift**+**S**를 눌러 파일과 프로젝트를 저장합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceInterface** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다. 클래스 라이브러리 DLL 파일이 컴파일되고 지정된 빌드 출력 경로에 저장됩니다(예: *C:\TypeEquivalenceSample*).

## <a name="create-a-runtime-class"></a>런타임 클래스 만들기

다음으로 동등한 형식의 런타임 프로젝트를 만듭니다.

1. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
   
1. **새 프로젝트 만들기** 대화 상자에서 **템플릿 검색** 상자에 *class library*를 입력합니다. 목록에서 C# 또는 VB **클래스 라이브러리(.NET Framework)** 템플릿을 선택한 후 **다음**을 선택합니다. 
   
1. **새 프로젝트 구성** 대화 상자에서 **프로젝트 이름**에 *TypeEquivalenceRuntime*을 입력한 다음 **만들기**를 선택합니다. 새 프로젝트가 만들어집니다.
   
1. **솔루션 탐색기**에서 *Class1.cs* 또는 *Class1.vb* 파일을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택하여 파일 이름을 *Class1*에서 *SampleClass*로 바꿉니다. 클래스의 이름도 `SampleClass`로 바꿀지 묻는 메시지가 표시되면 **예**라고 답합니다. 이 클래스는 `ISampleInterface` 인터페이스를 구현합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceInterface** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 
   
1. **속성** 화면 왼쪽 창에서 **빌드**를 선택한 다음 **출력 경로**를 TypeEquivalenceInterface 프로젝트에 사용한 것과 동일한 위치로 설정합니다(예: *C:\TypeEquivalenceSample*).
   
1. **속성** 화면의 왼쪽 창에서 **서명**을 선택한 다음 **어셈블리에 서명** 확인란을 선택합니다. **강력한 이름 키 파일 선택** 드롭다운 목록에서 **새로 만들기**를 선택합니다. 
   
1. **강력한 이름 키 만들기** 대화 상자의 **키 파일 이름**에 *key.snk*를 입력합니다. **암호로 내 키 파일 보호** 확인란의 선택을 취소한 다음 **확인**을 선택합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceRuntime** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **참조**를 선택합니다. 
   
1. **참조 관리자** 대화 상자에서 **찾아보기**를 선택하고 출력 경로 폴더를 찾습니다. *TypeEquivalenceInterface.dll* 파일을 선택하고 **추가**를 선택한 다음 **확인**을 선택합니다.
   
1. **솔루션 탐색기**에서 **참조** 폴더를 펼치고 **TypeEquivalenceInterface** 참조를 선택합니다. **속성** 창에서 아직 설정하지 않았다면 **특정 버전**을 **False**로 설정합니다.
   
1. 코드 편집기에서 *SampleClass* 클래스 파일을 열고 콘텐츠를 다음 코드로 바꾸어 `SampleClass` 클래스를 만듭니다.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using TypeEquivalenceInterface;
   
   namespace TypeEquivalenceRuntime
   {
       public class SampleClass : ISampleInterface
       {
           private string p_UserInput;
           public string UserInput { get { return p_UserInput; } }
   
           public void GetUserInput()
           {
               Console.WriteLine("Please enter a value:");
               p_UserInput = Console.ReadLine();
           }
       }
   }
   ```
   
   ```vb
   Imports TypeEquivalenceInterface
   
   Public Class SampleClass
       Implements ISampleInterface
   
       Private p_UserInput As String
       Public ReadOnly Property UserInput() As String Implements ISampleInterface.UserInput
           Get
               Return p_UserInput
           End Get
       End Property
   
       Public Sub GetUserInput() Implements ISampleInterface.GetUserInput
           Console.WriteLine("Please enter a value:")
           p_UserInput = Console.ReadLine()
       End Sub
   End Class
   ```
   
1. **파일** > **모두 저장**을 선택하거나 **Ctrl**+**Shift**+**S**를 눌러 파일과 프로젝트를 저장합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceRuntime** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다. 클래스 라이브러리 DLL 파일이 컴파일되고 지정된 빌드 출력 경로에 저장됩니다.

## <a name="create-a-client-project"></a>클라이언트 프로젝트 만들기

마지막으로 인터페이스 어셈블리를 참조하는 형식 동등 클라이언트 프로그램을 만듭니다.

1. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.
   
1. **새 프로젝트 만들기** 대화 상자에서 **템플릿 검색** 상자에 *console*을 입력합니다. 목록에서 C# 또는 VB **콘솔 앱(.NET Framework)** 템플릿을 선택한 후 **다음**을 선택합니다. 
   
1. **새 프로젝트 구성** 대화 상자에서 **프로젝트 이름**에 *TypeEquivalenceClient*를 입력한 다음 **만들기**를 선택합니다. 새 프로젝트가 만들어집니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceClient** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 
   
1. **속성** 화면 왼쪽 창에서 **빌드**를 선택한 다음 **출력 경로**를 TypeEquivalenceInterface 프로젝트에 사용한 것과 동일한 위치로 설정합니다(예: *C:\TypeEquivalenceSample*).
   
1. **솔루션 탐색기**에서 **TypeEquivalenceClient** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **참조**를 선택합니다. 
   
1. **참조 관리자** 대화 상자에서 **TypeEquivalenceInterface.dll** 파일이 이미 나열되어 있다면 선택합니다. 그렇지 않다면 **찾아보기**를 선택해 출력 경로 폴더를 찾고, *TypeEquivalenceInterface.dll* 파일( *TypeEquivalenceRuntime.dll*이 아님)을 선택하고 **추가**를 선택합니다. **확인**을 선택합니다.
   
1. **솔루션 탐색기**에서 **참조** 폴더를 펼치고 **TypeEquivalenceInterface** 참조를 선택합니다. **속성** 창에서 **Interop 형식 포함**을 **True**로 설정합니다.
   
1. 코드 편집기에서 *Program.cs* 또는 *Module1.vb* 파일을 열고 콘텐츠를 다음 코드로 바꾸어 클라이언트 프로그램을 만듭니다.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using TypeEquivalenceInterface;
   using System.Reflection;
   
   namespace TypeEquivalenceClient
   {
       class Program
       {
           static void Main(string[] args)
           {
               Assembly sampleAssembly = Assembly.Load("TypeEquivalenceRuntime");
               ISampleInterface sampleClass =
                   (ISampleInterface)sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass");
               sampleClass.GetUserInput();
               Console.WriteLine(sampleClass.UserInput);
               Console.WriteLine(sampleAssembly.GetName().Version.ToString());
               Console.ReadLine();
           }
       }
   }
   ```
   
   ```vb
   Imports TypeEquivalenceInterface
   Imports System.Reflection
   
   Module Module1
   
       Sub Main()
           Dim sampleAssembly = Assembly.Load("TypeEquivalenceRuntime")
           Dim sampleClass As ISampleInterface = CType( _
               sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass"), ISampleInterface)
           sampleClass.GetUserInput()
           Console.WriteLine(sampleClass.UserInput)
           Console.WriteLine(sampleAssembly.GetName().Version)
           Console.ReadLine()
       End Sub
   
   End Module
   ```
   
1. **파일** > **모두 저장**을 선택하거나 **Ctrl**+**Shift**+**S**를 눌러 파일과 프로젝트를 저장합니다.
   
1. **Ctrl**+**F5**를 눌러 프로그램을 빌드하고 실행합니다. 콘솔 출력은 어셈블리 버전 **1.0.0.0**을 반환합니다. 
   
## <a name="modify-the-interface"></a>인터페이스 수정

이제 인터페이스 어셈블리를 수정하고 해당 버전을 변경합니다. 

1. Visual Studio에서 **파일** > **열기** > **프로젝트/솔루션**을 선택하고 **TypeEquivalenceInterface** 프로젝트를 엽니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceInterface** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 
   
1. **속성** 화면의 왼쪽 창에서 **애플리케이션**을 선택한 다음 **어셈블리 정보**를 선택합니다. 
   
1. **어셈블리 정보** 대화 상자에서 **어셈블리 버전** 및 **파일 버전** 값을 *2.0.0.0*으로 변경한 다음 **확인**을 선택합니다.
   
1. *SampleInterface.cs* 또는 *SampleInterface.vb* 파일을 열고 다음 코드 줄을 `ISampleInterface` 인터페이스에 추가합니다.
   
   ```csharp
   DateTime GetDate();
   ```
   
   ```vb
   Function GetDate() As Date
   ```
   
1. **파일** > **모두 저장**을 선택하거나 **Ctrl**+**Shift**+**S**를 눌러 파일과 프로젝트를 저장합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceInterface** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다. 새 버전의 클래스 라이브러리 DLL 파일이 컴파일되고 빌드 출력 경로에 저장됩니다.

## <a name="modify-the-runtime-class"></a>런타임 클래스 수정

또한 런타임 클래스를 수정하고 해당 버전을 업데이트합니다. 

1. Visual Studio에서 **파일** > **열기** > **프로젝트/솔루션**을 선택하고 **TypeEquivalenceRuntime** 프로젝트를 엽니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceRuntime** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 
   
1. **속성** 화면의 왼쪽 창에서 **애플리케이션**을 선택한 다음 **어셈블리 정보**를 선택합니다. 
   
1. **어셈블리 정보** 대화 상자에서 **어셈블리 버전** 및 **파일 버전** 값을 *2.0.0.0*으로 변경한 다음 **확인**을 선택합니다.
   
1. *SampleClass.cs* 또는 *SampleClass.vb* 파일을 열고 다음 코드를 `SampleClass` 클래스에 추가합니다.
   
   ```csharp
    public DateTime GetDate()
    {
        return DateTime.Now;
    }
   ```
   
   ```vb
   Public Function GetDate() As DateTime Implements ISampleInterface.GetDate
       Return Now
   End Function
   ```
   
1. **파일** > **모두 저장**을 선택하거나 **Ctrl**+**Shift**+**S**를 눌러 파일과 프로젝트를 저장합니다.
   
1. **솔루션 탐색기**에서 **TypeEquivalenceRuntime** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택합니다. 새 버전의 클래스 라이브러리 DLL 파일이 컴파일되고 빌드 출력 경로에 저장됩니다.

## <a name="run-the-updated-client-program"></a>업데이트된 클라이언트 프로그램 실행 

빌드 출력 폴더 위치로 이동하여 *TypeEquivalenceClient.exe*를 실행합니다. 이제 프로그램을 다시 컴파일하지 않고도 콘솔 출력에 `TypeEquivalenceRuntime` 어셈블리의 새 버전 *2.0.0.0*이 반영됩니다.

## <a name="see-also"></a>참고 항목

- [/link(C# 컴파일러 옵션)](../../csharp/language-reference/compiler-options/link-compiler-option.md)
- [/link(Visual Basic)](../../visual-basic/reference/command-line-compiler/link.md)
- [C# 프로그래밍 가이드](../../csharp/programming-guide/index.md)
- [프로그래밍 개념(Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
- [어셈블리를 사용한 프로그램](program.md)
- [.NET 어셈블리](index.md)
