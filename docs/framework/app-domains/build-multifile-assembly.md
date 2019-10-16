---
title: '방법: 다중 파일 어셈블리 빌드'
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- Al.exe
- command-line compilers
- assembly manifest, multifile assemblies
- assemblies [.NET Framework], compiling
- Assembly Linker
- code modules
- multifile assemblies
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 261c5583-8a76-412d-bda7-9b8ee3b131e5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b95d686529da83a5a52edb80219874530212dcc
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991264"
---
# <a name="how-to-build-a-multifile-assembly"></a>방법: 다중 파일 어셈블리 빌드

이 문서는 다중 파일 어셈블리를 만드는 방법을 설명하고 프로시저의 각 단계를 보여 주는 코드를 제공합니다.

> [!NOTE]
> C# 및 Visual Basic용 Visual Studio IDE는 단일 파일 어셈블리를 만드는 경우에만 사용할 수 있습니다. 다중 파일 어셈블리를 만들려면 명령줄 컴파일러나 Visual C++용 Visual Studio를 사용해야 합니다. 다중 파일 어셈블리는 .NET Framework에서만 지원됩니다.

## <a name="create-a-multifile-assembly"></a>다중 파일 어셈블리 만들기

1. 어셈블리의 다른 모듈에서 참조되는 네임스페이스가 모든 파일에 포함된 경우, 이 파일을 모두 코드 모듈로 컴파일합니다. 코드 모듈의 기본 확장명은 *.netmodule*입니다.

   예를 들어, `Stringer` 파일에는 `myStringer` 클래스를 포함하는 `Stringer` 네임스페이스가 있습니다. `Stringer` 클래스에는 `StringerMethod`라는 메서드가 들어 있습니다. 이 메서드는 한 줄을 콘솔에 출력합니다.

   ```cpp
   // Assembly building example in the .NET Framework.
   using namespace System;

   namespace myStringer
   {
       public ref class Stringer
       {
       public:
           void StringerMethod()
           {
               System::Console::WriteLine("This is a line from StringerMethod.");
           }
       };
   }
   ```

   ```csharp
   // Assembly building example in the .NET Framework.
   using System;

   namespace myStringer
   {
       public class Stringer
       {
           public void StringerMethod()
           {
               System.Console.WriteLine("This is a line from StringerMethod.");
           }
       }
   }
   ```

   ```vb
   ' Assembly building example in the .NET Framework.
   Imports System

   Namespace myStringer
       Public Class Stringer
           Public Sub StringerMethod()
               System.Console.WriteLine("This is a line from StringerMethod.")
           End Sub
       End Class
   End Namespace
   ```

2. 다음 명령을 사용하여 이 코드를 컴파일합니다.

   ```cpp
   cl /clr:pure /LN Stringer.cpp
   ```

   ```csharp
   csc /t:module Stringer.cs
   ```

   ```vb
   vbc /t:module Stringer.vb
   ```

   *module* 매개 변수에 **/t:** 컴파일러 옵션을 지정하면 파일이 어셈블리로 컴파일되지 않고 모듈로 컴파일됩니다. 컴파일러는 *Stringer.netmodule*이라는 모듈을 만드는데, 이 모듈은 어셈블리에 추가될 수 있습니다.

3. 필요한 컴파일러 옵션을 사용하여 다른 모든 모듈을 컴파일합니다. 이 옵션은 코드에서 참조되는 다른 모듈을 표시합니다. 이 단계에서는 **/addmodule** 컴파일러 옵션을 사용합니다.

   다음 예제에서 *클라이언트*라는 코드 모듈에는 진입점 `Main` 메서드가 있습니다. 이 진입점은 1단계에서 만든 *Stringer.dll* 모듈의 메서드를 참조합니다.

   ```cpp
   #using "Stringer.netmodule"

   using namespace System;
   using namespace myStringer; //The namespace created in Stringer.netmodule.

   ref class MainClientApp
   {
       // Static method Main is the entry point method.
   public:
       static void Main()
       {
           Stringer^ myStringInstance = gcnew Stringer();
           Console::WriteLine("Client code executes");
           myStringInstance->StringerMethod();
       }
   };

   int main()
   {
       MainClientApp::Main();
   }
   ```

   ```csharp
   using System;
   using myStringer;

   class MainClientApp
   {
       // Static method Main is the entry point method.
       public static void Main()
       {
           Stringer myStringInstance = new Stringer();
           Console.WriteLine("Client code executes");
           myStringInstance.StringerMethod();
       }
   }
   ```

   ```vb
   Imports System
   Imports myStringer

   Class MainClientApp
       ' Static method Main is the entry point method.
       Public Shared Sub Main()
           Dim myStringInstance As New Stringer()
           Console.WriteLine("Client code executes")
           myStringInstance.StringerMethod()
       End Sub
   End Class
   ```

4. 다음 명령을 사용하여 이 코드를 컴파일합니다.

   ```cpp
   cl /clr:pure /FUStringer.netmodule /LN Client.cpp
   ```

   ```csharp
   csc /addmodule:Stringer.netmodule /t:module Client.cs
   ```

   ```vb
   vbc /addmodule:Stringer.netmodule /t:module Client.vb
   ```

   다음 단계에서 어셈블리에 이 모듈이 추가될 것이므로 **/t:module** 옵션을 지정합니다. *클라이언트*의 코드는 *Stringer.netmodule*의 코드에 의해 생성된 네임스페이스를 참조하므로 **/addmodule** 옵션을 지정하세요. 컴파일러는 *Client.netmodule*이라는 모듈을 만드는데, 이 모듈에는 다른 모듈인 *Stringer.netmodule*에 대한 참조가 들어 있습니다.

   > [!NOTE]
   > C# 및 Visual Basic 컴파일러에서는 다음과 같은 두 구문을 사용하여 다중 파일 어셈블리를 직접 만들 수 있습니다.
   >
   > 두 번 컴파일에서 2파일 어셈블리를 만듭니다.
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /t:module Stringer.cs
   >   csc Client.cs /addmodule:Stringer.netmodule
   >   ```
   >
   >   ```vb
   >   vbc /t:module Stringer.vb
   >   vbc Client.vb /addmodule:Stringer.netmodule
   >   ```
   >
   > 한 번 컴파일에서 2파일 어셈블리를 만듭니다.
   >
   >   ```cpp
   >   cl /clr:pure /LN Stringer.cpp
   >   cl /clr:pure Client.cpp /link /ASSEMBLYMODULE:Stringer.netmodule
   >   ```
   >
   >   ```csharp
   >   csc /out:Client.exe Client.cs /out:Stringer.netmodule Stringer.cs
   >   ```
   >
   >   ```vb
   >   vbc /out:Client.exe Client.vb /out:Stringer.netmodule Stringer.vb
   >   ```

5. [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하면 어셈블리 매니페스트가 포함된 출력 파일을 만들 수 있습니다. 이 파일에는 어셈블리의 일부인 모든 모듈과 리소스의 참조 정보가 들어 있습니다.

    명령 프롬프트에 다음 명령을 입력합니다.

    **al** \<*module name*> \<*module name*> … **/main:** \<*method name*>  **/out:** \<*file name*>  **/target:** \<*assembly file type*>

    이 명령에서 *module name* 인수는 각 모듈의 이름을 지정하여 어셈블리에 포함합니다. **/main:** 옵션은 메서드 이름을 지정하는데, 이 메서드는 어셈블리의 진입점입니다. **/out:** 옵션은 출력 파일의 이름을 지정하는데, 이 파일에는 어셈블리 메타데이터가 들어 있습니다. **/target:** 옵션은 어셈블리를 콘솔 애플리케이션 실행 파일( *.exe*), Windows 실행 파일( *.win*) 또는 라이브러리 파일( *.lib*)로 지정합니다.

    다음 예제에서 *Al.exe*는 *myAssembly.exe*라는 콘솔 애플리케이션 실행 파일인 어셈블리를 만듭니다. 이 애플리케이션은 *Client.netmodule* 및 *Stringer.netmodule*이라는 두 개의 모듈과 어셈블리 메타데이터만 포함하는 *myAssembly.exe*라는 실행 파일로 구성됩니다. 이 어셈블리의 진입점은 `MainClientApp` 클래스에 있는 `Main` 메서드이며, 이 클래스는 *Client.dll*에 들어 있습니다.

    ```cmd
    al Client.netmodule Stringer.netmodule /main:MainClientApp.Main /out:myAssembly.exe /target:exe
    ```

    [MSIL 디스어셈블러(Ildasm.exe)](../tools/ildasm-exe-il-disassembler.md)를 사용하면 어셈블리의 콘텐츠를 검사 할 수 있으며, 파일이 어셈블리인지 모듈인지를 결정할 수 있습니다.

## <a name="see-also"></a>참고 항목

- [어셈블리 만들기](../../standard/assembly/create.md)
- [방법: 어셈블리 콘텐츠 보기](../../standard/assembly/view-contents.md)
- [런타임에서 어셈블리를 찾는 방법](../deployment/how-the-runtime-locates-assemblies.md)
- [다중 파일 어셈블리](multifile-assemblies.md)
