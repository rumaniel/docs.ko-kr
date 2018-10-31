---
title: -rootnamespace
ms.date: 03/13/2018
f1_keywords:
- /rootnamespace
- rootnamespace
helpviewer_keywords:
- /rootnamespace compiler option [Visual Basic]
- -rootnamespace compiler option [Visual Basic]
- rootnamespace compiler option [Visual Basic]
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
ms.openlocfilehash: 2c7fb6c88477899a0cf08a467e8f23d687b90c90
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201901"
---
# <a name="-rootnamespace"></a>-rootnamespace
모든 형식 선언에 대한 네임스페이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-rootnamespace:namespace  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`namespace`|현재 프로젝트에 대 한 모든 형식 선언을 포함할를 네임 스페이스의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 만든 프로젝트를 컴파일하는 데 사용 하 여 Visual Studio 통합된 개발 환경에서 Visual Studio 실행 파일 (Devenv.exe)를 사용 하는 경우 `-rootnamespace` 의 값을 지정 하는 <xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> 속성입니다. 참조 [Devenv 명령줄 스위치](/visualstudio/ide/reference/devenv-command-line-switches) 자세한 내용은 합니다.  
  
 공용 언어 런타임은 MSIL 디스어셈블러를 사용 하 여 (`Ildasm.exe`) 출력 파일의 네임 스페이스 이름을 볼 수 있습니다.  
  
|Visual Studio 통합된 개발 환경에서-rootnamespace를 설정 하려면|  
|---|  
|1.  **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다. <br />2.  **응용 프로그램** 탭을 클릭합니다.<br />3.  값을 수정 합니다 **루트 Namespace** 상자입니다.|  
  
## <a name="example"></a>예제  
 다음 코드 컴파일을 `In.vb` 네임 스페이스의 모든 형식 선언을 포함 하 고 `mynamespace`입니다.  
  
```console
vbc -rootnamespace:mynamespace in.vb  
```  
  
## <a name="see-also"></a>참고자료

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
- [Ildasm.exe(IL 디스어셈블러)](../../../framework/tools/ildasm-exe-il-disassembler.md)  
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
