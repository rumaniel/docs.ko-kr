---
title: -moduleassemblyname(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /moduleassemblyname
helpviewer_keywords:
- moduleassemblyname compiler option [C#]
- /moduleassemblyname compiler option [C#]
- .moduleassemblyname compiler option [C#]
ms.assetid: d464d9b9-f18d-423b-95e9-66c7878fd53a
ms.openlocfilehash: 7562c0609d61b2388f5063bc480a4dfc715155db
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970083"
---
# <a name="-moduleassemblyname-c-compiler-option"></a>-moduleassemblyname(C# 컴파일러 옵션)
.netmodule에서 public이 아닌 형식에 액세스할 수 있는 어셈블리를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>인수  
 `assembly_name`  
 .netmodule에서 public이 아닌 형식에 액세스할 수 있는 어셈블리의 이름입니다.  
  
## <a name="remarks"></a>설명  
 **-moduleassemblyname**은 .netmodule을 빌드할 때와 다음 조건이 충족되는 경우 사용해야 합니다.  
  
- .netmodule은 기존 어셈블리의 public이 아닌 형식에 액세스해야 합니다.  
  
- .netmodule을 빌드할 어셈블리의 이름을 알아야 합니다.  
  
- 기존 어셈블리는 friend 어셈블리(friend assembly)에 .netmodule을 빌드할 어셈블리에 대한 액세스를 부여합니다.  
  
 .netmodule 빌드 방법에 대한 자세한 내용은 [-target:module(C# 컴파일러 옵션)](./target-module-compiler-option.md)을 참조하세요.  
  
 friend 어셈블리에 대한 자세한 내용은 [Friend 어셈블리](../../../standard/assembly/friend.md)를 참조하세요.  
  
 개발 환경 내에서는 이 옵션을 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
 이 컴파일러 옵션은 Visual Studio에서 사용할 수 없으며 프로그래밍 방식으로 변경할 수 없습니다.  
  
## <a name="example"></a>예  
 이 샘플에서는 private 형식을 사용하여 어셈블리를 빌드하므로 friend 어셈블리가 csman_an_assembly라는 어셈블리에 액세스할 수 있습니다.  
  
```csharp  
// moduleassemblyname_1.cs  
// compile with: -target:library  
using System;  
using System.Runtime.CompilerServices;  
  
[assembly:InternalsVisibleTo ("csman_an_assembly")]  
  
class An_Internal_Class   
{  
    public void Test()   
    {   
        Console.WriteLine("An_Internal_Class.Test called");   
    }  
}  
```  
  
## <a name="example"></a>예  
 이 샘플은 어셈블리 moduleassemblyname_1.dll에 public이 아닌 형식에 액세스하는 .netmodule을 빌드합니다. 이 .netmodule이 csman_an_assembly라는 어셈블리에 빌드될 것임을 알기 때문에 **-moduleassemblyname**을 지정하여 .netmodule이 friend 어셈블리(friend assembly)에 csman_an_assembly에 대한 액세스를 부여한 어셈블리의 public이 아닌 형식에 액세스하도록 할 수 있습니다.  
  
```csharp  
// moduleassemblyname_2.cs  
// compile with: -moduleassemblyname:csman_an_assembly -target:module -reference:moduleassemblyname_1.dll  
class B {  
    public void Test() {  
        An_Internal_Class x = new An_Internal_Class();  
        x.Test();  
    }  
}  
```  
  
## <a name="example"></a>예  
 이 코드 샘플에서는 이전에 빌드한 어셈블리와 .netmodule을 참조하여 csman_an_assembly 어셈블리를 빌드합니다.  
  
```csharp  
// csman_an_assembly.cs  
// compile with: -addmodule:moduleassemblyname_2.netmodule -reference:moduleassemblyname_1.dll  
class A {  
    public static void Main() {  
        B bb = new B();  
        bb.Test();  
    }  
}  
```  
  
**An_Internal_Class.Test 호출됨**

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
