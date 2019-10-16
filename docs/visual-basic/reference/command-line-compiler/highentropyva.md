---
title: -highentropyva (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
ms.openlocfilehash: 58026ff84f1ff501bf767adebcfc01f7de5bf4a4
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005576"
---
# <a name="-highentropyva-visual-basic"></a>-highentropyva (Visual Basic)
[/Platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) 컴파일러 옵션으로 표시 된 실행 파일이 나 64 비트 실행 파일이 높은 엔트로피 ASLR (주소 공간 레이아웃 임의)을 지원 하는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 (선택 사항) 옵션은 기본적으로 off 이거나 `-highentropyva-`을 지정 하는 경우입니다. @No__t-0 또는 `-highentropyva+`을 지정 하는 경우 옵션은 on입니다.  
  
## <a name="remarks"></a>설명  
 이 옵션을 지정 하는 경우 커널에서 ASLR의 일부로 프로세스의 주소 공간 레이아웃을 임의화 하는 경우 호환 되는 버전의 Windows 커널에서 더 높은 수준의 엔트로피를 사용할 수 있습니다. 커널이 높은 수준의 엔트로피를 사용 하는 경우 스택 및 힙과 같은 메모리 영역에 더 많은 주소를 할당할 수 있습니다. 따라서 특정 메모리 영역의 위치를 추측하기 어려워집니다.  
  
 옵션을 on으로 설정 하면 대상 실행 파일과이 실행 파일이 종속 된 모든 모듈이 64 비트 프로세스로 실행 될 때 4gb 보다 큰 포인터 값을 처리할 수 있어야 합니다.  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
