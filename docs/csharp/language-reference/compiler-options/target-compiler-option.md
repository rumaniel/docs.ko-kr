---
title: -target(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /target
helpviewer_keywords:
- target compiler options [C#]
- /target compiler options [C#]
- assemblies [C#], compiling
- -target compiler options [C#]
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
ms.openlocfilehash: 073660fa732c04cdc987af5617b894a277ebcc0f
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970122"
---
# <a name="-target-c-compiler-options"></a>-target(C# 컴파일러 옵션)
**-target** 컴파일러 옵션은 다음 네 가지 형태 중 하나로 지정할 수 있습니다.  
  
 [/target:appcontainerexe](./target-appcontainerexe-compiler-option.md)  
 [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)] 앱에 대한 .exe 파일을 만듭니다.  
  
 [/target:exe](./target-exe-compiler-option.md)  
 .exe 파일을 만듭니다.  
  
 [/target:library](./target-library-compiler-option.md)  
 코드 라이브러리를 만듭니다.  
  
 [/target:module](./target-module-compiler-option.md)  
 모듈을 만듭니다.  
  
 [/target:winexe](./target-winexe-compiler-option.md)  
 Windows 프로그램을 만듭니다.  
  
 [/target:winmdobj](./target-winmdobj-compiler-option.md)  
 중간 .winmdobj 파일을 만듭니다.  
  
 **-target:module**을 지정하지 않으면 **-target**은 .NET Framework 어셈블리 매니페스트가 출력 파일에 배치되도록 합니다. 자세한 내용은 [.NET의 어셈블리](../../../standard/assembly/index.md) 및 [공통 특성](../../programming-guide/concepts/attributes/common-attributes.md)을 참조하세요.  
  
 어셈블리 매니페스트는 컴파일의 첫 번째 .exe 출력 파일 또는 .exe 출력 파일이 없는 경우 첫 번째 DLL에 배치됩니다. 예를 들어 다음 명령줄에서 매니페스트는 `1.exe`에 배치됩니다.  
  
```console  
csc -out:1.exe t1.cs -out:2.netmodule t2.cs  
```  
  
 컴파일러는 컴파일당 하나의 어셈블리 매니페스트만 만듭니다. 컴파일의 모든 파일에 대한 정보가 어셈블리 매니페스트에 배치됩니다. **-target:module**을 사용하여 생성된 파일을 제외한 모든 출력 파일에 어셈블리 매니페스트가 포함될 수 있습니다. 명령줄에서 여러 출력 파일을 생성하는 경우 하나의 어셈블리 매니페스트만 만들 수 있으며, 명령줄에 지정된 첫 번째 출력 파일로 이동해야 합니다. 첫 번째 출력 파일이 **-target:exe**, **-target:winexe**, **-target:library** 또는 **-target:module** 중 무엇이든 관계없이 동일한 컴파일에서 생성된 다른 출력 파일은 모듈( **-target:module**)이어야 합니다.  
  
 어셈블리를 만드는 경우 <xref:System.CLSCompliantAttribute> 특성을 사용하여 코드의 전체 또는 일부를 CLS 규격으로 지정할 수 있습니다.  
  
```csharp  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
- [-subsystemversion(C# 컴파일러 옵션)](./subsystemversion-compiler-option.md)
