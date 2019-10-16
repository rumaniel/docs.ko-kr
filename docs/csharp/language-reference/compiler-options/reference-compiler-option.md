---
title: -reference(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /reference
helpviewer_keywords:
- /r compiler option [C#]
- reference compiler option [C#]
- r compiler option [C#]
- /reference compiler option [C#]
- -r compiler option [C#]
- metadata import [C#]
- public type information [C#]
- -reference compiler option [C#]
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
ms.openlocfilehash: 247fb222eaacdb5ee60df2dded3a857f0395eb34
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606576"
---
# <a name="-reference-c-compiler-options"></a>-reference(C# 컴파일러 옵션)
**-reference** 옵션을 사용하면 컴파일러가 지정된 파일의 [public](../keywords/public.md) 형식 정보를 현재 프로젝트로 가져오므로 지정된 어셈블리 파일의 메타데이터를 참조할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-reference:[alias=]filename  
-reference:filename  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 어셈블리 매니페스트가 들어 있는 파일의 이름입니다. 둘 이상의 파일을 가져오려면 각 파일에 대해 별도 **-reference** 옵션을 포함합니다.  
  
 `alias`  
 어셈블리에 있는 모든 네임스페이스를 포함하는 루트 네임스페이스를 나타내는 유효한 C# 식별자입니다.  
  
## <a name="remarks"></a>설명  
 둘 이상의 파일에서 가져오려면 각 파일에 대해 **-reference** 옵션을 포함합니다.  
  
 가져오는 파일에 매니페스트가 포함되어 있어야 합니다. 출력 파일이 [-target:module](./target-module-compiler-option.md) 이외의 [-target](./target-compiler-option.md) 옵션 중 하나로 컴파일된 상태여야 합니다.  
  
 **-r**은 **-reference**의 약식입니다.  
  
 [-addmodule](./addmodule-compiler-option.md)을 사용하여 어셈블리 매니페스트를 포함하지 않는 출력 파일에서 메타데이터를 가져옵니다.  
  
 다른 어셈블리(어셈블리 B)를 참조하는 어셈블리(어셈블리 A)를 참조하면 다음과 같은 경우 어셈블리 B를 참조해야 합니다.  
  
- 어셈블리 A에서 사용하는 형식이 형식에서 상속되거나 어셈블리 B의 인터페이스를 구현하는 경우  
  
- 어셈블리 B의 반환 형식이나 매개 변수 형식을 사용하는 필드, 속성, 이벤트 또는 메서드를 호출하는 경우  
  
 [-lib](./lib-compiler-option.md)를 사용하여 어셈블리 참조 중 하나 이상이 있는 디렉터리를 지정합니다. **-lib** 항목에서는 컴파일러가 어셈블리를 검색하는 디렉터리에 대해서도 설명합니다.  
  
 컴파일러가 모듈이 아니라 어셈블리의 형식을 인식하려면 강제로 형식을 확인하도록 해야 하며, 이 작업을 위해 형식의 인스턴스를 정의할 수 있습니다. 컴파일러를 위해 어셈블리의 형식 이름을 확인하는 다른 방법이 있습니다. 예를 들어 어셈블리의 형식에서 상속하는 경우 컴파일러가 형식 이름을 인식합니다.  
  
 때로는 하나의 어셈블리 내에서 동일한 구성 요소의 두 가지 버전을 참조해야 합니다. 이렇게 하려면 각 파일에 대한 **-reference** 스위치의 별칭 하위 옵션을 사용하여 두 파일을 구분합니다. 이 별칭은 구성 요소 이름에 대한 한정자로 사용되며, 파일 중 하나의 구성 요소로 확인됩니다.  
  
 자주 사용되는 .NET Framework 어셈블리를 참조하는 csc 지시 파일(.rsp)이 기본적으로 사용됩니다. 컴파일러에서 csc.rsp를 사용하지 않도록 하려면 [-noconfig](./noconfig-compiler-option.md)를 사용합니다.  
  
> [!NOTE]
> Visual Studio에서 **참조 추가** 대화 상자를 사용합니다. 자세한 내용은 [방법: 참조 관리자를 사용하여 참조 추가 또는 제거](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager). `-reference`를 사용한 참조 추가와 **참조 추가** 대화 상자를 사용한 참조 추가의 동작이 같도록 하려면 추가하는 어셈블리에 대한 **Interop 형식 포함** 속성을 **False**로 설정합니다. 이 속성의 기본값은 **True**입니다.  
  
## <a name="example"></a>예  
 이 예제에서는 [extern 별칭](../keywords/extern-alias.md) 기능을 사용하는 방법을 보여 줍니다.  
  
 소스 파일을 컴파일하고, 이전에 컴파일된 `grid.dll` 및 `grid20.dll`에서 메타데이터를 가져옵니다. 두 DLL에는 동일한 구성 요소의 서로 다른 버전이 포함되어 있으며, 두 **-reference**를 별칭 옵션과 함께 사용하여 소스 파일을 컴파일합니다. 옵션은 다음과 같습니다.  

```console
-reference:GridV1=grid.dll -reference:GridV2=grid20.dll  
```
  
 이렇게 하면 외부 별칭 `GridV1` 및 `GridV2`가 설정되며, 프로그램에서 `extern` 문을 통해 사용됩니다.  
  
```csharp  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 이 작업이 완료되면 다음과 같이 컨트롤 이름 앞에 `GridV1`을 추가하여 `grid.dll`에서 그리드 컨트롤을 참조할 수 있습니다.  
  
```csharp  
GridV1::Grid  
```  
  
 또한, 다음과 같이 컨트롤 이름 앞에 `GridV2`를 추가하여 `grid20.dll`에서 그리드 컨트롤을 참조할 수 있습니다.  
  
```csharp  
GridV2::Grid   
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
