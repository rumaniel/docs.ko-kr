---
title: '@(C# 컴파일러 옵션)'
ms.date: 07/20/2015
f1_keywords:
- '@'
helpviewer_keywords:
- response files, specifying for compilation [C#]
- '@ compiler option'
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
ms.openlocfilehash: d8e5c0ec148754c3e4cebfa32ad9f44a0bb0119e
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70202904"
---
# <a name="-c-compiler-options"></a>@(C# 컴파일러 옵션)
@ 옵션을 사용하면 컴파일러 옵션과 컴파일할 소스 코드 파일이 포함된 파일을 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
@response_file  
```  
  
## <a name="arguments"></a>인수  
 `response_file`  
 컴파일러 옵션이나 컴파일할 소스 코드 파일이 나열된 파일입니다.  
  
## <a name="remarks"></a>설명  
 컴파일러 옵션 및 소스 코드 파일은 명령줄에 지정된 것처럼 컴파일러에서 처리됩니다.  
  
 컴파일에 지시 파일을 둘 이상 지정하려면 여러 지시 파일 옵션을 지정합니다. 예:  
  
```console  
@file1.rsp @file2.rsp  
```  
  
 지시 파일에서 여러 컴파일러 옵션과 소스 코드 파일이 한 줄에 나타날 수 있습니다. 단일 컴파일러 옵션 사양은 한 줄에 표시되어야 합니다(여러 줄에 걸쳐 있을 수 없음). 지시 파일은 # 기호로 시작하는 주석을 포함할 수 있습니다.  
  
 지시 파일 내에서 컴파일러 옵션을 지정하는 것은 명령줄에서 해당 명령을 실행하는 것과 같습니다. 자세한 내용은 [명령줄에서 빌드](./how-to-set-environment-variables-for-the-visual-studio-command-line.md)를 참조하세요.  
  
 명령 옵션이 발견되면 컴파일러에서 처리합니다. 따라서, 명령줄 인수는 지시 파일에서 이전에 나열된 옵션을 재정의할 수 있습니다. 반대로 지시 파일의 옵션은 명령줄 또는 다른 지시 파일에서 이전에 나열된 옵션을 재정의합니다.  
  
 C#에서는 csc.exe 파일과 동일한 디렉터리에 있는 csc.rsp 파일을 제공합니다. csc.rsp에 대한 자세한 내용은 [-noconfig](./noconfig-compiler-option.md)를 참조하세요.  
  
 Visual Studio 개발 환경에서는 이 컴파일러 옵션을 설정할 수 없으며 프로그래밍 방식으로 변경할 수도 없습니다.  
  
## <a name="example"></a>예  
 다음은 샘플 지시 파일의 몇 줄입니다.  
  
```console  
# build the first output file  
-target:exe -out:MyExe.exe source1.cs source2.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
