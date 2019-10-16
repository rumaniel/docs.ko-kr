---
title: -bugreport(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /bugreport
helpviewer_keywords:
- /bugreport compiler option [C#]
- -bugreport compiler option [C#]
- bugreport compiler option [C#]
ms.assetid: f39665e3-4f6f-4357-88a2-3274c7bec0c1
ms.openlocfilehash: 0989678be070910c410d71717fe66679e1b70557
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69603073"
---
# <a name="-bugreport-c-compiler-options"></a>-bugreport(C# 컴파일러 옵션)
나중에 분석하기 위해 파일에 디버그 정보를 포함하도록 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-bugreport:file  
```  
  
## <a name="arguments"></a>인수  
 `file`  
 버그 보고서를 포함하려는 파일의 이름입니다.  
  
## <a name="remarks"></a>설명  
 **-bugreport** 옵션은 `file`에 다음 정보를 포함하도록 지정합니다:  
  
- 컴파일에 포함된 모든 소스 코드 파일의 복사본입니다.  
  
- 컴파일에 사용된 컴파일러 옵션 목록입니다.  
  
- 컴파일러, 런타임 및 운영 체제에 대한 버전 정보입니다.  
  
- .NET Framework 및 SDK와 함께 제공되는 어셈블리를 제외하고 16진수로 저장된 참조된 어셈블리 및 모듈입니다.  
  
- 컴파일러 출력입니다(있는 경우).  
  
- 메시지가 표시되는 문제에 대한 설명입니다.  
  
- 메시지가 표시되는 문제 해결 방법에 대한 설명입니다.  
  
 **-errorreport:prompt** 또는 **-errorreport:send**와 함께 이 옵션을 사용할 경우 파일의 정보가 Microsoft Corporation에 전송됩니다.  
  
 모든 소스 코드 파일의 복사본이 `file`에 저장되기 때문에 최대한 짧은 프로그램으로 의심스러운 코드 결함을 재현하는 것이 좋습니다.  
  
 이 컴파일러 옵션은 Visual Studio에서 사용할 수 없으며 프로그래밍 방식으로 변경할 수 없습니다.  
  
 생성된 파일 내용에 의해 소스 코드가 노출되어, 의도하지 않게 정보가 공개될 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [-errorreport(C# 컴파일러 옵션)](./errorreport-compiler-option.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
