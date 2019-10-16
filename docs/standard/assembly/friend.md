---
title: Friend 어셈블리
ms.date: 08/20/2019
ms.assetid: b65ea7de-0801-477a-a39c-e914c2cc107c
dev_langs:
- csharp
- vb
ms.openlocfilehash: 6387e93bcd4efeec57ada9228dcaf015d053dbf7
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972704"
---
# <a name="friend-assemblies"></a>Friend 어셈블리

*friend 어셈블리*는 다른 어셈블리의 [내부](../../csharp/language-reference/keywords/internal.md)(C#) 또는 [Friend](../../visual-basic/language-reference/modifiers/friend.md)(Visual Basic) 형식 및 멤버에 액세스할 수 있는 어셈블리입니다. 어셈블리를 friend 어셈블리로 식별하는 경우 다른 어셈블리에서 액세스할 수 있도록 하기 위해 더 이상 형식 및 멤버를 public으로 표시할 필요가 없습니다. 다음과 같은 시나리오에서 특히 편리합니다.

- 유닛 테스트 중 테스트 코드는 별도의 어셈블리에서 실행되지만 테스트 중인 어셈블리에서 `internal`(C#) 또는 `Friend`(Visual Basic)로 표시된 멤버에 액세스해야 하는 경우.

- 클래스 라이브러리를 개발하고 있고 라이브러리에 대한 추가 사항이 별도의 어셈블리에 포함되어 있지만, 기존 어셈블리에서 `internal`(C#) 또는 `Friend`(Visual Basic)으로 표시된 멤버에 액세스해야 하는 경우.

## <a name="remarks"></a>설명

<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성을 사용하여 지정된 어셈블리에 대해 하나 이상의 friend 어셈블리를 식별할 수 있습니다. 다음 예제에서는 *어셈블리 A*에서 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성을 사용하고 *어셈블리 B* 어셈블리를 friend 어셈블리로 지정합니다. 그러면 *어셈블리 B* 어셈블리가 *어셈블리 A*에서 `internal`(C#) 또는 `Friend`(Visual Basic)로 표시된 모든 형식 및 멤버에 액세스할 수 있습니다.

> [!NOTE]
> *어셈블리 A*와 같은 다른 어셈블리의 내부 형식이나 내부 멤버에 액세스하는 *어셈블리 B*와 같은 어셈블리를 컴파일하는 경우 **/out** 컴파일러 옵션을 사용하여 출력 파일( *.exe* 또는 *.dll*)의 이름을 명시적으로 지정해야 합니다. 컴파일러가 외부 참조에 바인딩할 때 작성하고 있는 어셈블리에 대해 이름을 생성하지 않았기 때문에 이 과정이 필요합니다. 자세한 내용은 [/out(C#)](../../csharp/language-reference/compiler-options/out-compiler-option.md) 또는 [/out(Visual Basic)](../../visual-basic/reference/command-line-compiler/out.md)을 참조하세요.

```csharp
using System.Runtime.CompilerServices;
using System;

[assembly: InternalsVisibleTo("AssemblyB")]

// The class is internal by default.
class FriendClass
{
    public void Test()
    {
        Console.WriteLine("Sample Class");
    }
}

// Public class that has an internal method.
public class ClassWithFriendMethod
{
    internal void Test()
    {
        Console.WriteLine("Sample Method");
    }

}
```

```vb
Imports System.Runtime.CompilerServices
Imports System
<Assembly: InternalsVisibleTo("AssemblyB")>

' Friend class.
Friend Class FriendClass
    Public Sub Test()
        Console.WriteLine("Sample Class")
    End Sub
End Class

' Public class with a Friend method.
Public Class ClassWithFriendMethod
    Friend Sub Test()
        Console.WriteLine("Sample Method")
    End Sub
End Class
```

friend로 명시적으로 지정하는 어셈블리만 `internal`(C#) 또는 `Friend`(Visual Basic) 형식 및 멤버에 액세스할 수 있습니다. 예를 들어 *어셈블리 B*가 *어셈블리 A*의 friend이고 *어셈블리 C*가 *어셈블리 B*를 참조하는 경우, *어셈블리 C*는 *어셈블리 A*의 `internal`(C#)또는 `Friend`(Visual Basic) 형식에 액세스할 수 없습니다.

컴파일러는 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성에 전달된 friend 어셈블리 이름에 대해 몇 가지 기본적인 유효성 검사를 수행합니다. *어셈블리 A*가 *어셈블리 B*를 friend 어셈블리로 선언하는 경우, 유효성 검사 규칙은 다음과 같습니다.

- *어셈블리 A*에 강력한 이름을 지정한 경우 *어셈블리 B*에도 강력한 이름을 지정해야 합니다. 특성에 전달되는 friend 어셈블리 이름은 어셈블리 이름과 *어셈블리 B*에 서명하는 데 사용되는 강력한 이름 키의 공개 키로 구성되어야 합니다.

     <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 특성에 전달되는 friend 어셈블리 이름은 *어셈블리 B*의 강력한 이름일 수 없습니다. 어셈블리 버전, 문화권, 아키텍처 또는 공개 키 토큰을 포함하지 마세요.

- *어셈블리 A*에 강력한 이름을 지정하지 않은 경우 friend 어셈블리 이름은 어셈블리 이름만으로 구성되어야 합니다. 자세한 내용은 [방법: 서명되지 않은 friend 어셈블리 만들기](create-unsigned-friend.md)를 참조하세요.

- *어셈블리 B*에 강력한 이름을 지정하는 경우 프로젝트 설정이나 명령줄 `/keyfile` 컴파일러 옵션을 사용하여 *어셈블리 B*에 강력한 이름 키를 지정해야 합니다. 자세한 내용은 [방법: 서명된 friend 어셈블리 만들기](create-signed-friend.md)를 참조하세요.

 <xref:System.Security.Permissions.StrongNameIdentityPermission> 클래스도 형식을 공유하는 기능을 제공하지만 다음과 같은 차이점이 있습니다.

- <xref:System.Security.Permissions.StrongNameIdentityPermission>은 개별 형식에 적용되는 반면 friend 어셈블리는 전체 어셈블리에 적용됩니다.

- *어셈블리 A*에 *어셈블리 B*와 공유하려는 수백 개의 형식이 있는 경우 모든 형식에 <xref:System.Security.Permissions.StrongNameIdentityPermission>을 추가해야 합니다. friend 어셈블리를 사용하는 경우에는 friend 관계를 한 번만 선언하면 됩니다.

- <xref:System.Security.Permissions.StrongNameIdentityPermission>을 사용하는 경우 공유하려는 형식을 public으로 선언해야 합니다. friend 어셈블리를 사용하는 경우 공유 유형은 `internal`(C#) 또는 `Friend`(Visual Basic)로 선언됩니다.

모듈 파일(확장자가 *.netmodule*인 파일)에서 어셈블리의 `internal`(C#) 또는 `Friend`(Visual Basic) 형식 및 메서드에 액세스하는 방법에 관한 내용은 [/moduleassemblyname(C#)](../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md) 또는 [/moduleassemblyname(Visual Basic)](../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- <xref:System.Security.Permissions.StrongNameIdentityPermission>
- [방법: 서명되지 않은 friend 어셈블리 만들기](create-unsigned-friend.md)
- [방법: 서명된 friend 어셈블리 만들기](create-signed-friend.md)
- [.NET 어셈블리](index.md)
- [C# 프로그래밍 가이드](../../csharp/programming-guide/index.md)
- [프로그래밍 개념(Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
