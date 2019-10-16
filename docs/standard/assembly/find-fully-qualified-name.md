---
title: '방법: 어셈블리의 정규화된 이름 찾기'
ms.date: 08/20/2019
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
author: rpetrusha
ms.author: ronpet
dev_langs:
- csharp
- vb
- cpp
ms.openlocfilehash: 4fc670adc80a6f4ce7b36074185dcd3bb85fbc67
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991304"
---
# <a name="how-to-find-an-assemblys-fully-qualified-name"></a>방법: 어셈블리의 정규화된 이름 찾기

전역 어셈블리 캐시에서 .NET Framework 어셈블리의 정규화된 이름을 찾으려면 전역 어셈블리 캐시 도구([Gacutil.exe](../../framework/tools/gacutil-exe-gac-tool.md))를 사용합니다. [방법: 전역 어셈블리 캐시의 내용 보기](../../framework/app-domains/how-to-view-the-contents-of-the-gac.md)를 참조하세요.

.NET Core 어셈블리와 전역 어셈블리 캐시에 없는 .NET Framework 어셈블리의 경우, 여러 방법으로 정규화된 어셈블리 이름을 가져올 수 있습니다.

- 코드를 사용하여 콘솔이나 변수로 정보를 출력하거나 [Ildasm.exe(IL 디스어셈블러)](../../framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 정규화된 이름이 포함된 어셈블리의 메타데이터를 검사할 수 있습니다.

- 애플리케이션에서 어셈블리를 이미 로드한 경우 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType> 속성의 값을 검색하여 정규화된 이름을 가져올 수 있습니다. 해당 어셈블리에 정의된 <xref:System.Type>의 <xref:System.Type.Assembly> 속성을 사용하여 <xref:System.Reflection.Assembly> 개체에 대한 참조를 검색할 수 있습니다. 예제에서는 그림을 제공합니다.

- 어셈블리의 파일 시스템 경로를 알고 있는 경우`static`(C#) 또는 `Shared`(Visual Basic) <xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> 메서드를 호출하여 정규화된 어셈블리 이름을 가져올 수 있습니다. 다음은 간단한 예제입니다.

  ```csharp
  using System;
  using System.Reflection;

  public class Example
  {
     public static void Main()
     {
        Console.WriteLine(AssemblyName.GetAssemblyName(@".\UtilityLibrary.dll"));
     }
  }
  // The example displays output like the following:
  //   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

  ```vb
  Imports System.Reflection

  Public Module Example
     Public Sub Main
        Console.WriteLine(AssemblyName.GetAssemblyName(".\UtilityLibrary.dll"))
     End Sub
  End Module
  ' The example displays output like the following:
  '   UtilityLibrary, Version=1.1.0.0, Culture=neutral, PublicKeyToken=null
  ```

- [Ildasm.exe(IL 디스어셈블러)](../../framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 정규화된 이름이 포함된 어셈블리의 메타데이터를 검사할 수 있습니다.

버전, 문화권 및 어셈블리 이름과 같은 어셈블리 특성 설정에 대한 자세한 내용은 [어셈블리 특성 설정](set-attributes.md)을 참조하세요. 어셈블리에 강력한 이름을 지정하는 방법에 대한 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](create-use-strong-named.md)을 참조하세요.

## <a name="example"></a>예

다음 예제는 지정된 클래스를 포함하는 어셈블리의 정규화된 이름을 콘솔에 표시하는 방법을 보여 줍니다. 이 예제는 <xref:System.Type.Assembly?displayProperty=nameWithType> 속성을 사용하여 해당 어셈블리에 정의된 형식에서 어셈블리에 대한 참조를 검색합니다.

```cpp
#using <System.dll>
#using <System.Data.dll>

using namespace System;
using namespace System::Reflection;

ref class asmname
{
public:
    static void Main()
    {
        Type^ t = System::Data::DataSet::typeid;
        String^ s = t->Assembly->FullName->ToString();
        Console::WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
};

int main()
{
    asmname::Main();
}
```

```csharp
using System;
using System.Reflection;

class asmname
{
    public static void Main()
    {
        Type t = typeof(System.Data.DataSet);
        string s = t.Assembly.FullName.ToString();
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s);
    }
}
```

```vb
Imports System
Imports System.Reflection

Class asmname
    Public Shared Sub Main()
        Dim t As Type = GetType(System.Data.DataSet)
        Dim s As String = t.Assembly.FullName.ToString()
        Console.WriteLine("The fully qualified assembly name " +
            "containing the specified class is {0}.", s)
    End Sub
End Class
```

## <a name="see-also"></a>참고 항목

- [어셈블리 이름](names.md)
- [어셈블리 만들기](create.md)
- [강력한 이름의 어셈블리 만들기 및 사용](create-use-strong-named.md)
- [전역 어셈블리 캐시](../../framework/app-domains/gac.md)
- [런타임에서 어셈블리를 찾는 방법](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [어셈블리를 사용한 프로그램](program.md)
