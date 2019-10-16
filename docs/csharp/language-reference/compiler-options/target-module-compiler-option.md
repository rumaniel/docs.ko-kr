---
title: -target:module(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /target:module
helpviewer_keywords:
- -target compiler options [C#], /target:module
- target compiler options [C#], /target:module
- /target compiler options [C#], /target:module
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
ms.openlocfilehash: 25421df2e9306071ce3506aaf7affd1b259d1c32
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602447"
---
# <a name="-targetmodule-c-compiler-options"></a>-target:module(C# 컴파일러 옵션)
이 옵션은 컴파일러에서 어셈블리 매니페스트를 생성하지 않도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-target:module  
```  
  
## <a name="remarks"></a>설명  
 기본적으로 이 옵션으로 컴파일하여 생성되는 출력 파일의 확장명은 .netmodule입니다.  
  
 어셈블리 매니페스트가 없는 파일은 .NET Framework 공용 언어 런타임에서 로드할 수 없습니다. 그러나 이러한 파일은 [-addmodule](./addmodule-compiler-option.md)을 통해 어셈블리의 어셈블리 매니페스트에 통합할 수 있습니다.  
  
 둘 이상의 모듈이 단일 컴파일에서 생성될 경우 한 모듈의 [내부](../keywords/internal.md) 형식을 컴파일에 포함된 다른 모듈에서 사용할 수 있습니다. 한 모듈의 코드가 다른 모듈의 `internal` 형식을 참조하는 경우 **-addmodule**을 통해 두 모듈을 모두 어셈블리 매니페스트에 통합해야 합니다.  
  
 Visual Studio 개발 환경에서는 모듈을 만들 수 없습니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>을 참조하세요.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 `in.netmodule`을 만듭니다.  
  
```console  
csc -target:module in.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [-target(C# 컴파일러 옵션)](./target-compiler-option.md)
- [C# 컴파일러 옵션](./index.md)
