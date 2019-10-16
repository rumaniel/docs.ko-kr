---
title: -resource(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /resource
helpviewer_keywords:
- -resource compiler option [C#]
- /resource compiler option [C#]
- -res compiler option [C#]
- /res compiler option [C#]
- res compiler option [C#]
- resource compiler option [C#]
ms.assetid: 5212666e-98ab-47e4-a497-b5545ab15c7f
ms.openlocfilehash: e14bf59f5922a918b627af22c052c8efd9081e84
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602521"
---
# <a name="-resource-c-compiler-options"></a>-resource(C# 컴파일러 옵션)
출력 파일에 지정된 리소스를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-resource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 출력 파일에 포함하려는 .NET Framework 리소스 파일입니다.  
  
 `identifier` (선택 사항)  
 리소스의 논리적 이름으로, 리소스를 로드하는 데 사용되는 이름입니다. 기본값은 파일 이름입니다.  
  
 `accessibility-modifier` (선택 사항)  
 리소스의 접근성으로, public 또는 private입니다. 기본값은 public입니다.  
  
## <a name="remarks"></a>설명  
 리소스를 어셈블리에 연결하고 출력 파일에 리소스 파일을 추가하지 않으려면 [-linkresource](./linkresource-compiler-option.md)를 사용합니다.  
  
 기본적으로 리소스는 C# 컴파일러를 사용하여 생성될 때 어셈블리에서 public입니다. 리소스를 private로 만들려면 접근성 한정자로 `private`를 지정합니다. `public` 또는 `private` 이외의 다른 접근성은 허용되지 않습니다.  
  
 예를 들어 `filename`이 [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md)나 개발 환경에서 만들어진 .NET Framework 리소스 파일인 경우에는 <xref:System.Resources> 네임스페이스의 멤버를 사용하여 해당 파일에 액세스할 수 있습니다. 자세한 내용은 <xref:System.Resources.ResourceManager?displayProperty=nameWithType>을 참조하세요. 다른 모든 리소스의 경우에는 런타임에 `GetManifestResource` 클래스의 <xref:System.Reflection.Assembly> 메서드를 사용하여 리소스에 액세스합니다.  
  
 **-res**는 **-resource**의 약식입니다.  
  
 출력 파일에 있는 리소스의 순서는 명령줄에 지정된 순서에 따라 결정됩니다.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트에 리소스 파일을 추가합니다.  
  
2. **솔루션 탐색기**에서 포함할 파일을 선택합니다.  
  
3. **속성** 창에서 파일에 대한 **빌드 작업**을 선택합니다.  
  
4. **빌드 작업**을 **포함 리소스**로 설정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.FileProperties2.BuildAction%2A>을 참조하십시오.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 리소스 파일 `rf.resource`를 첨부합니다.  
  
```console  
csc -resource:rf.resource in.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
