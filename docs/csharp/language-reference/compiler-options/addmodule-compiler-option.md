---
title: -addmodule(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /addmodule
helpviewer_keywords:
- /addmodule compiler option [C#]
- -addmodule compiler option [C#]
- addmodule compiler option [C#]
ms.assetid: ed604546-0dc2-4bd4-9a3e-610a8d973e58
ms.openlocfilehash: 148a63c37cfbc4c60448adccde10947e91e22bb9
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970181"
---
# <a name="-addmodule-c-compiler-options"></a>-addmodule(C# 컴파일러 옵션)
이 옵션은 target:module 스위치로 만들어진 모듈을 현재 컴파일에 추가합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-addmodule:file[;file2]  
```  
  
## <a name="arguments"></a>인수  
 `file`, `file2`  
 메타데이터를 포함하는 출력 파일입니다. 파일에 어셈블리 매니페스트를 포함할 수 없습니다. 둘 이상의 파일을 가져오려면 파일 이름을 쉼표 또는 세미콜론으로 구분합니다.  
  
## <a name="remarks"></a>설명  
 **-addmodule**을 사용하여 추가된 모든 모듈은 런타임에 출력 파일과 동일한 디렉터리에 있어야 합니다. 즉, 컴파일 시간에 임의 디렉터리에 있는 모듈을 지정할 수 있지만 런타임에 모듈이 애플리케이션 디렉터리에 있어야 합니다. 런타임에 모듈이 애플리케이션 디렉터리에 없는 경우 <xref:System.TypeLoadException>이 발생합니다.  
  
 `file`에 어셈블리를 사용할 수 없습니다. 예를 들어, [-target:module](./target-module-compiler-option.md)을 사용하여 출력 파일이 만들어진 경우 **-addmodule**을 사용하여 해당 메타데이터를 가져올 수 있습니다.  
  
 출력 파일이 **-target:module** 이외의 **-target** 옵션으로 작성된 경우 해당 메타데이터를 **-addmodule**로 가져올 수 없지만 [-reference](./reference-compiler-option.md)로 가져올수 있습니다.  
  
 이 컴파일러 옵션은 Visual Studio에서 사용할 수 없습니다. 프로젝트에서 모듈을 참조할 수 없습니다. 또한 이 컴파일러 옵션은 프로그래밍 방식으로 변경할 수 없습니다.  
  
## <a name="example"></a>예  
 소스 파일 `input.cs`를 컴파일하고 `metad1.netmodule` 및 `metad2.netmodule`의 메타데이터를 추가하여 `out.exe`를 생성합니다.  
  
```console  
csc -addmodule:metad1.netmodule;metad2.netmodule -out:out.exe input.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
- [다중 파일 어셈블리](../../../framework/app-domains/multifile-assemblies.md)
- [방법: 다중 파일 어셈블리 빌드](../../../framework/app-domains/build-multifile-assembly.md)
