---
title: '방법: 서명되지 않은 friend 어셈블리 만들기'
ms.date: 08/19/2019
ms.assetid: 78cbc4f0-b021-4141-a4ff-eb4edbd814ca
dev_langs:
- csharp
- vb
ms.openlocfilehash: 9d5699f772dba994b10408d15422faa3c5931f45
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991691"
---
# <a name="how-to-create-unsigned-friend-assemblies"></a>방법: 서명되지 않은 friend 어셈블리 만들기

이 예제에서는 서명되지 않은 어셈블리와 함께 friend 어셈블리를 사용하는 방법을 보여 줍니다.

## <a name="create-an-assembly-and-a-friend-assembly"></a>어셈블리 및 friend 어셈블리 만들기

1. 명령 프롬프트를 엽니다.

2. 다음 코드를 포함하는 *friend_unsigned_A*라는 C# 또는 Visual Basic 파일을 만듭니다. 이 코드는 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성을 사용하여 *friend_unsigned_B*를 friend 어셈블리로 선언합니다.

   ```csharp
   // friend_unsigned_A.cs
   // Compile with:
   // csc /target:library friend_unsigned_A.cs
   using System.Runtime.CompilerServices;
   using System;

   [assembly: InternalsVisibleTo("friend_unsigned_B")]

   // Type is internal by default.
   class Class1
   {
       public void Test()
       {
           Console.WriteLine("Class1.Test");
       }
   }

   // Public type with internal member.
   public class Class2
   {
       internal void Test()
       {
           Console.WriteLine("Class2.Test");
       }
   }
   ```

   ```vb
   ' friend_unsigned_A.vb
   ' Compile with:
   ' vbc -target:library friend_unsigned_A.vb
   Imports System.Runtime.CompilerServices
   Imports System

   <Assembly: InternalsVisibleTo("friend_unsigned_B")>

   ' Friend type.
   Friend Class Class1
       Public Sub Test()
           Console.WriteLine("Class1.Test")
       End Sub
   End Class

   ' Public type with Friend member.
   Public Class Class2
       Friend Sub Test()
           Console.WriteLine("Class2.Test")
       End Sub
   End Class
   ```

3. 다음 명령을 사용하여 *friend_unsigned_A*를 컴파일하고 서명합니다.

   ```csharp
   csc /target:library friend_unsigned_A.cs
   ```

   ```vb
   vbc -target:library friend_unsigned_A.vb
   ```

4. 다음 코드를 포함하는 *friend_unsigned_B*라는 C# 또는 Visual Basic 파일을 만듭니다. *friend_unsigned_A*는 *friend_unsigned_B*를 friend 어셈블리로 지정하기 때문에 *friend_unsigned_B*는 *friend_unsigned_A*의 `internal`(C#) 또는 `Friend`(Visual Basic) 형식과 멤버에 액세스할 수 있습니다.

   ```csharp
   // friend_unsigned_B.cs
   // Compile with:
   // csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs
   public class Program
   {
       static void Main()
       {
           // Access an internal type.
           Class1 inst1 = new Class1();
           inst1.Test();

           Class2 inst2 = new Class2();
           // Access an internal member of a public type.
           inst2.Test();

           System.Console.ReadLine();
       }
   }
   ```

   ```vb
   ' friend_unsigned_B.vb
   ' Compile with:
   ' vbc -r:friend_unsigned_A.dll friend_unsigned_B.vb
   Module Module1
       Sub Main()
           ' Access a Friend type.
           Dim inst1 As New Class1()
           inst1.Test()

           Dim inst2 As New Class2()
           ' Access a Friend member of a public type.
           inst2.Test()

           System.Console.ReadLine()
       End Sub
   End Module
   ```

5. 다음 명령을 사용하여 *friend_unsigned_B*를 컴파일합니다.

   ```csharp
   csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs
   ```

   ```vb
   vbc -r:friend_unsigned_A.dll friend_unsigned_B.vb
   ```

   컴파일러에서 생성된 어셈블리 이름은 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성에 전달된 friend 어셈블리 이름과 일치해야 합니다. `/out` 컴파일러 옵션을 사용하여 출력 어셈블리( *.exe* 또는 *.dll*)의 이름을 명시적으로 지정해야 합니다. 자세한 내용은 [/out(C# 컴파일러 옵션)](../../csharp/language-reference/compiler-options/out-compiler-option.md) 또는 [-out(Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md)을 참조하세요.

6. *friend_unsigned_B.exe* 파일을 실행합니다.

   프로그램에서 두 개의 문자열 **Class1.Test** 및 **Class2.Test**가 출력됩니다.

## <a name="net-security"></a>.NET 보안

<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성과 <xref:System.Security.Permissions.StrongNameIdentityPermission> 클래스 간에는 유사점이 있습니다. 주요 차이점은 <xref:System.Security.Permissions.StrongNameIdentityPermission>은 코드의 특정 섹션을 실행하는 보안 권한을 요구할 수 있는 반면, <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성은 `internal` 또는 `Friend`(Visual Basic) 형식 및 멤버의 표시 유형을 제어한다는 것입니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [.NET 어셈블리](index.md)
- [friend 어셈블리](friend.md)
- [방법: 서명된 friend 어셈블리 만들기](create-signed-friend.md)
- [C# 프로그래밍 가이드](../../csharp/programming-guide/index.md)
- [프로그래밍 개념(Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
