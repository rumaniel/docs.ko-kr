---
title: -codepage(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /codepage
helpviewer_keywords:
- /codepage compiler option [C#]
- codepage compiler option [C#]
- -codepage compiler option [C#]
ms.assetid: 75942989-b69a-4308-90a0-840c73d2c478
ms.openlocfilehash: c85cd8935bcefd1353707624052b62ee982f7b07
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69603056"
---
# <a name="-codepage-c-compiler-options"></a>-codepage(C# 컴파일러 옵션)
이 옵션은 필수 페이지가 시스템에 대한 현재 기본 코드 페이지가 아닌 경우 컴파일 중에 사용할 코드 페이지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>인수  
 `id`  
 컴파일할 때 모든 소스 코드 파일에 사용할 코드 페이지의 ID입니다.  
  
## <a name="remarks"></a>설명  
 컴파일러는 먼저 모든 소스 파일을 UTF-8로 해석하려고 합니다. 소스 코드 파일이 UTF-8 이외의 인코딩에 있고 7비트 ASCII 문자가 아닌 문자를 사용하는 경우 **-codepage** 옵션을 통해 사용할 코드 페이지를 지정합니다. **-codepage**는 컴파일에 포함된 모든 소스 코드 파일에 적용됩니다.  
    
 시스템에서 지원되는 코드 페이지를 찾는 방법에 대한 자세한 내용은 [GetCPInfo](/windows/desktop/api/winnls/nf-winnls-getcpinfo)를 참조하세요.  
  
 이 컴파일러 옵션은 Visual Studio에서 사용할 수 없으며 프로그래밍 방식으로 변경할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
