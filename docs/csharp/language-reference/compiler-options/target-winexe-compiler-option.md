---
title: -target:winexe(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /target:winexe
helpviewer_keywords:
- /target compiler options [C#], /target:winexe
- -target compiler options [C#], /target:winexe
- target compiler options [C#], /target:winexe
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
ms.openlocfilehash: 981f1b0b6ca9f708bb022a3662ab181a4f472040
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606386"
---
# <a name="-targetwinexe-c-compiler-options"></a>-target:winexe(C# 컴파일러 옵션)
**-target:winexe** 옵션을 사용하면 컴파일러가 Windows 프로그램 실행 파일(EXE)을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-target:winexe  
```  
  
## <a name="remarks"></a>설명  
 실행 파일은 .exe 확장명으로 생성됩니다. Windows 프로그램은 .NET Framework 라이브러리나 Windows API를 통해 사용자 인터페이스를 제공하는 프로그램입니다.  
  
 [-target:exe](./target-exe-compiler-option.md)를 사용하여 콘솔 애플리케이션을 만듭니다.  
  
 [-out](./out-compiler-option.md) 옵션을 사용하여 지정하지 않으면 [Main](../../programming-guide/main-and-command-args/index.md) 메서드가 포함된 입력 파일의 이름이 출력 파일의 이름으로 사용됩니다.  
  
 명령줄에서 지정된 경우, 다음 **-out** 또는 [-target](./target-compiler-option.md) 옵션까지의 모든 파일이 Windows 프로그램을 만드는 데 사용됩니다.  
  
 .exe 파일로 컴파일되는 소스 코드 파일에 **Main** 메서드가 하나만 있어야 합니다. [-main](./main-compiler-option.md) 옵션을 사용하면 코드에 **Main** 메서드를 포함하는 클래스가 둘 이상 있는 경우 **Main** 메서드를 포함하는 클래스를 지정할 수 있습니다.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **애플리케이션** 속성 페이지를 클릭합니다.  
  
3. **출력 형식** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>을 참조하세요.  
  
## <a name="example"></a>예  
 `in.cs`를 Windows 프로그램으로 컴파일합니다.  
  
```console  
csc -target:winexe in.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [-target(C# 컴파일러 옵션)](./target-compiler-option.md)
- [C# 컴파일러 옵션](./index.md)
