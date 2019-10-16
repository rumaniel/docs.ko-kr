---
title: -debug(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /debug
helpviewer_keywords:
- debug compiler option [C#]
- -debug compiler option [C#]
- /debug compiler option [C#]
ms.assetid: e2b48c07-01bc-45cc-a52c-92e9085eb969
ms.openlocfilehash: 8bb2b411dc867b6a43e52058dccf2ac980cf0b1e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922506"
---
# <a name="-debug-c-compiler-options"></a>-debug(C# 컴파일러 옵션)
**-debug** 옵션을 사용하면 컴파일러에서 디버깅 정보를 생성하여 출력 파일에 넣습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-debug[+ | -]  
-debug:{full | pdbonly}  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 `+` 또는 **-debug**를 지정하면 컴파일러에서 디버깅 정보를 생성하여 프로그램 데이터베이스(.pdb 파일)에 넣습니다. `-`를 지정하면 **-debug**를 지정하지 않은 것으로 적용되어 디버그 정보가 생성되지 않습니다.  
  
 `full` &#124; `pdbonly`  
 컴파일러에서 생성되는 디버깅 정보 형식을 지정합니다. **-debug:pdbonly**를 지정하지 않을 경우 적용되는 전체 인수를 통해 실행 중인 프로그램에 디버거를 연결할 수 있습니다. pdbonly를 지정하면 디버거에서 프로그램이 시작되는 경우 소스 코드 디버깅이 가능하지만, 실행 중인 프로그램이 디버거에 연결되는 경우 어셈블러만 표시됩니다.  
  
## <a name="remarks"></a>설명  
 디버그 빌드를 만들려면 이 옵션을 사용합니다. **-debug**, **-debug+** 또는 **-debug:full**을 지정하지 않으면 프로그램의 출력 파일을 디버그할 수 없습니다.  
  
 **-debug:full**을 사용하는 경우 JIT 최적화된 코드의 속도 및 크기와 **-debug:full**을 사용한 코드 품질이 일부 영향을 받는 것에 유의하세요. 릴리스 코드를 생성하는 경우 **-debug:pdbonly**를 사용하거나 PDB를 사용하지 않는 것이 좋습니다.  
  
> [!NOTE]
> **-debug:pdbonly** 및 **-debug:full** 간의 차이점 중 하나는 **-debug:full**을 사용하는 경우 컴파일러가 <xref:System.Diagnostics.DebuggableAttribute>를 내보낸다는 것입니다. 이 특성은 JIT 컴파일러에 디버그 정보를 사용할 수 있음을 알리는 데 사용됩니다. 따라서 **-debug:full**을 사용하는 경우 false로 설정된 <xref:System.Diagnostics.DebuggableAttribute>가 코드에 포함되어 있으면 오류가 발생합니다.  
  
 애플리케이션의 디버그 성능을 구성하는 방법에 대한 자세한 내용은 [쉽게 디버그할 수 있도록 이미지 만들기](../../../framework/debug-trace-profile/making-an-image-easier-to-debug.md)를 참조하세요.  
  
 .pdb 파일의 위치를 변경하려면 [-pdb(C# 컴파일러 옵션)](./pdb-compiler-option.md)를 참조하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **빌드** 속성 페이지를 클릭합니다.  
  
3. **고급** 단추를 클릭합니다.  
  
4. **디버그 정보** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DebugSymbols%2A>을 참조하세요.  
  
## <a name="example"></a>예  
 출력 파일 `app.pdb`에 디버깅 정보를 넣습니다.  
  
```console  
csc -debug -pdb:app.pdb test.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
