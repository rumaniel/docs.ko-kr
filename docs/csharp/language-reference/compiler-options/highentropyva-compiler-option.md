---
title: -highentropyva(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /highentropyva
helpviewer_keywords:
- /highentropyva compiler option [C#]
- -highentropyva compiler option [C#]
- highentropyva compiler option [C#]
ms.assetid: eaf409b3-384e-49dd-9417-62453658f421
ms.openlocfilehash: b710bb829f6a7591159d2f2e6bacc670d21c42d1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606850"
---
# <a name="-highentropyva-c-compiler-options"></a>-highentropyva(C# 컴파일러 옵션)
**-highentropyva** 컴파일러 옵션은 특정 실행 파일이 높은 엔트로피 ASLR(Address Space Layout Randomization)을 지원하는지 여부를 Windows 커널에 알려줍니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 이 옵션은 [-platform:anycpu](./platform-compiler-option.md) 컴파일러 옵션으로 표시된 실행 파일이나 64비트 실행 파일이 높은 엔트로피 가상 주소 공간을 지원하도록 지정합니다. 이 옵션은 기본적으로 비활성화되어 있습니다. **-highentropyva+** 또는 **-highentropyva**를 사용하여 설정합니다.  
  
## <a name="remarks"></a>설명  
 **-highentropyva** 옵션은 Windows 커널의 호환되는 버전에서 ASLR의 일부로 프로세스의 주소 공간 레이아웃을 임의로 선택할 때 보다 높은 수준의 엔트로피를 사용할 수 있게 합니다. 더 높은 수준의 엔트로피를 사용하면 스택 및 힙과 같은 메모리 영역에 더 많은 주소를 할당할 수 있습니다. 따라서 특정 메모리 영역의 위치를 추측하기 어려워집니다.  
  
 **-highentropyva** 컴파일러 옵션을 지정하면 대상 실행 파일과 이 실행 파일이 종속된 모든 모듈이 64비트 프로세스로 실행될 때 4GB(기가바이트)보다 큰 포인터 값을 처리할 수 있어야 합니다.
