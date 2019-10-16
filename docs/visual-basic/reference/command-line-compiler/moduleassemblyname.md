---
title: -moduleassemblyname
ms.date: 03/13/2018
helpviewer_keywords:
- moduleassemblyname compiler option [Visual Basic]
- /moduleassemblyname compiler option [Visual Basic]
- -moduleassemblyname compiler option [Visual Basic]
ms.assetid: 013a57b6-f425-4dd3-b333-512d72c42f55
ms.openlocfilehash: 5b26e36346858d95526f5d5ce7d4645bea1dbe05
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005472"
---
# <a name="-moduleassemblyname"></a>-moduleassemblyname
이 모듈이 속할 어셈블리의 이름을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`assembly_name`|이 모듈에 포함 될 어셈블리의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-1 옵션이 지정 된 경우에만 컴파일러에서 `-moduleassemblyname` 옵션을 처리 합니다. 이렇게 하면 컴파일러가 모듈을 만듭니다. 컴파일러에서 만든 모듈은 `-moduleassemblyname` 옵션으로 지정 된 어셈블리에만 유효 합니다. 모듈을 다른 어셈블리에 저장 하는 경우 런타임 오류가 발생 합니다.  
  
 @No__t-0 옵션은 다음 조건이 충족 되는 경우에만 필요 합니다.  
  
- 모듈의 데이터 형식은 참조 된 어셈블리의 `Friend` 형식에 액세스할 수 있어야 합니다.  
  
- 참조 된 어셈블리에는 모듈이 빌드되는 어셈블리에 대 한 friend 어셈블리 액세스 권한이 부여 됩니다.  
  
 모듈을 만드는 방법에 대 한 자세한 내용은 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)을 참조 하세요. Friend 어셈블리에 대 한 자세한 내용은 [Friend 어셈블리](../../../standard/assembly/friend.md)를 참조 하세요.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령 프롬프트에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조

- [방법: 다중 파일 어셈블리 빌드](../../../framework/app-domains/build-multifile-assembly.md)
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [-main](../../../visual-basic/reference/command-line-compiler/main.md)
- [-reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
- [-addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)
- [.NET 어셈블리](../../../standard/assembly/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Friend 어셈블리](../../../standard/assembly/friend.md)
