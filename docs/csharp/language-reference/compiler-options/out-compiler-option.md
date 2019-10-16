---
title: -out(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /out
helpviewer_keywords:
- /out compiler option [C#]
- out compiler option [C#]
- -out compiler option [C#]
ms.assetid: 70d91d01-7bd2-4aea-ba8b-4e9807e9caa5
ms.openlocfilehash: 6c8408c0c613e361dae0c1db19f854e9421ca467
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970375"
---
# <a name="-out-c-compiler-options"></a>-out(C# 컴파일러 옵션)
**-out** 옵션은 출력 파일의 이름을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-out:filename  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 컴파일러에서 생성된 출력 파일의 이름입니다.  
  
## <a name="remarks"></a>설명  
 명령줄에서 컴파일에 대해 여러 출력 파일을 지정할 수 있습니다. 컴파일러는 **-out** 옵션 뒤에 하나 이상의 소스 코드 파일이 있을 것으로 예상합니다. 그런 다음 **-out** 옵션으로 지정된 출력 파일에 모든 소스 코드 파일이 컴파일됩니다.  
  
 만들려는 파일의 전체 이름과 확장명을 지정합니다.  
  
 출력 파일의 이름을 지정하지 않을 경우  
  
- .exe는 **Main** 메서드가 포함된 소스 코드 파일에서 해당 이름을 가져옵니다.  
  
- .dll 또는 netmodule은 첫 번째 소스 코드 파일에서 해당 이름을 가져옵니다.  
  
 한 출력 파일을 컴파일하는 데 사용되는 소스 코드 파일을 동일한 컴파일에서 다른 출력 파일의 컴파일에 사용할 수 없습니다.  
  
 명령줄 컴파일에서 여러 출력 파일을 만들 때는 출력 파일 중 하나만 어셈블리가 될 수 있고, **-out**을 사용하여 명시적으로 또는 암시적으로 지정된 첫 번째 출력 파일만 어셈블리가 될 수 있다는 것에 유의하세요.  
  
 컴파일의 일부로 생성된 모든 모듈은 컴파일할 때 함께 생성된 어셈블리와 연결된 파일이 됩니다. 연결된 파일을 보려면 [ildasm.exe](../../../framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 어셈블리 매니페스트를 확인합니다.  
  
 exe가 friend 어셈블리의 대상이 되려면 -out 컴파일러 옵션이 필요합니다. 자세한 내용은 [Friend 어셈블리](../../../standard/assembly/friend.md)를 참조하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **애플리케이션** 속성 페이지를 클릭합니다.  
  
3. **어셈블리 이름** 속성을 수정합니다.  
  
     이 컴파일러 옵션을 프로그래밍 방식으로 설정하려면: <xref:VSLangProj80.ProjectProperties3.OutputFileName%2A>은 프로젝트 형식(exe, 라이브러리 등)과 어셈블리 이름의 조합으로 결정되는 읽기 전용 속성입니다. 출력 파일 이름을 설정하려면 이러한 속성 중 하나 또는 둘 다를 수정해야 합니다.  
  
## <a name="example"></a>예  
 `t.cs`를 컴파일하고 출력 파일 `t.exe`를 만들 뿐만 아니라 `t2.cs`를 작성하고 모듈 출력 파일 `mymodule.netmodule`을 만듭니다.  
  
```console  
csc t.cs -out:mymodule.netmodule -target:module t2.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [Friend 어셈블리](../../../standard/assembly/friend.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
