---
title: -filealign(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /filealign
helpviewer_keywords:
- /alignment compiler option [C#]
- filealign compiler option [C#]
- -filealign compiler option [C#]
- /sections compiler option [C#]
- alignment compiler option [C#]
- sections compiler option [C#]
- -sections compiler option [C#]
- /filealign compiler option [C#]
- file sharing [C#]
- -alignment compiler option [C#]
- section alignment [C#]
ms.assetid: 15cf1c98-3798-4ced-9f08-60619308a073
ms.openlocfilehash: aed8b412ea1580f7dfa4f87333598d76a85b5e64
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69603016"
---
# <a name="-filealign-c-compiler-options"></a>-filealign(C# 컴파일러 옵션)
**-filealign** 옵션을 사용하여 출력 파일의 섹션 크기를 지정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-filealign:number  
```  
  
## <a name="arguments"></a>인수  
 `number`  
 출력 파일의 섹션 크기를 지하는 값입니다. 유효한 값은 512, 1024, 2048, 4096 및 8192입니다. 이러한 값은 바이트 단위입니다.  
  
## <a name="remarks"></a>설명  
 각 섹션은 **-filealign** 값의 배수인 경계에 맞춰집니다. 고정된 기본값이 없습니다. **-filealign**을 지정하지 않으면 공용언어 런타임에서 컴파일 시간에 기본값을 선택합니다.  
  
 섹션 크기를 지정하면 출력 파일의 크기에 영향을 줍니다. 섹션 크기를 수정하면 더 작은 디바이스에서 실행되는 프로그램에 유용할 수 있습니다.  
  
 출력 파일의 섹션에 대한 정보를 확인하려면 [DUMPBIN](/cpp/build/reference/dumpbin-options)을 사용하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **빌드** 속성 페이지를 클릭합니다.  
  
3. **고급** 단추를 클릭합니다.  
  
4. **파일 맞춤** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.FileAlignment%2A>을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
