---
title: -linkresource(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /linkresource
helpviewer_keywords:
- /linkresource compiler option [C#]
- linkres compiler option [C#]
- /linkres compiler option [C#]
- -linkres compiler option [C#]
- -linkresource compiler option [C#]
- linkresource compiler option [C#]
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
ms.openlocfilehash: 454915454f3faf15933257f3e3e221afec51d0ee
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606759"
---
# <a name="-linkresource-c-compiler-options"></a>-linkresource(C# 컴파일러 옵션)
출력 파일에 .NET Framework 리소스에 대한 링크를 만듭니다. 리소스 파일은 출력 파일에 추가되지 않습니다. 이 점에서 출력 파일에 리소스 파일을 포함하는 [-resource](./resource-compiler-option.md) 옵션과 다릅니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 어셈블리에서 연결할 .NET Framework 리소스 파일입니다.  
  
 `identifier` (선택 사항)  
 리소스의 논리적 이름으로, 리소스를 로드하는 데 사용되는 이름입니다. 기본값은 파일 이름입니다.  
  
 `accessibility-modifier` (선택 사항)  
 리소스의 접근성으로, public 또는 private입니다. 기본값은 public입니다.  
  
## <a name="remarks"></a>설명  
 기본적으로 연결된 리소스는 C# 컴파일러로 생성될 때 어셈블리에서 public입니다. 리소스를 private로 만들려면 접근성 한정자로 `private`를 지정합니다. `public` 또는 `private` 이외의 다른 한정자는 허용되지 않습니다.  
  
 **-linkresource**에는 **-target:module** 이외의 [-target](./target-compiler-option.md) 옵션 중 하나가 필요합니다.  
  
 예를 들어 `filename`이 [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md)나 개발 환경에서 만들어진 .NET Framework 리소스 파일인 경우에는 <xref:System.Resources> 네임스페이스의 멤버를 사용하여 해당 파일에 액세스할 수 있습니다. 자세한 내용은 <xref:System.Resources.ResourceManager?displayProperty=nameWithType>을 참조하세요. 다른 모든 리소스의 경우에는 런타임에 `GetManifestResource` 클래스의 <xref:System.Reflection.Assembly> 메서드를 사용하여 리소스에 액세스합니다.  
  
 `filename`에 지정된 파일은 모든 형식일 수 있습니다. 예를 들어 네이티브 DLL을 어셈블리의 일부로 설정하면 전역 어셈블리 캐시에 설치하고 어셈블리의 관리 코드에서 액세스할 수 있습니다. 다음 중 두 번째 예제에서 이 작업을 수행하는 방법을 보여 줍니다. 어셈블리 링커에서도 동일한 작업을 수행할 수 있습니다. 다음 중 세 번째 예제에서 이 작업을 수행하는 방법을 보여 줍니다. 자세한 내용은 [Al.exe(어셈블리 링커)](../../../framework/tools/al-exe-assembly-linker.md) 및 [어셈블리 및 전역 어셈블리 캐시 사용](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)을 참조하세요.  
  
 **-linkres**는 **-linkresource**의 약식입니다.  
  
 이 컴파일러 옵션은 Visual Studio에서 사용할 수 없으며 프로그래밍 방식으로 변경할 수 없습니다.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 리소스 파일 `rf.resource`에 연결합니다.  
  
```console  
csc -linkresource:rf.resource in.cs  
```  
  
## <a name="example"></a>예  
 `A.cs`를 DLL로 컴파일하고, 네이티브 DLL N.dll에 연결한 다음 출력을 GAC(전역 어셈블리 캐시)에 넣습니다. 이 예제에서는 A.dll과 N.dll이 둘 다 GAC에 있습니다.  
  
```console  
csc -linkresource:N.dll -t:library A.cs  
gacutil -i A.dll  
```  
  
## <a name="example"></a>예  
 이 예제에서는 앞의 예제와 동일한 작업을 수행하지만 어셈블리 링커 옵션을 사용합니다.  
  
```console  
csc -t:module A.cs  
al -out:A.dll A.netmodule -link:N.dll   
gacutil -i A.dll  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [Al.exe(어셈블리 링커)](../../../framework/tools/al-exe-assembly-linker.md)
- [어셈블리 및 전역 어셈블리 캐시 사용](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
