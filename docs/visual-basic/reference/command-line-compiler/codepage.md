---
title: -codepage (Visual Basic)
ms.date: 03/09/2018
helpviewer_keywords:
- -codepage compiler option [Visual Basic]
- codepage compiler option [Visual Basic]
- -codepage compiler option [Visual Basic]
ms.assetid: be36ec33-6800-4505-838c-4124564f5cc9
ms.openlocfilehash: e4cdc27ab021fe055f157b78946538f2b76870e1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002365"
---
# <a name="-codepage-visual-basic"></a>-codepage (Visual Basic)
컴파일할 때 모든 소스 코드 파일에 사용할 코드 페이지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-codepage:id  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`id`|필수. 컴파일러는 `id`으로 지정 된 코드 페이지를 사용 하 여 소스 파일의 인코딩을 해석 합니다.|  
  
## <a name="remarks"></a>설명  
 특정 인코딩으로 저장 된 소스 코드를 컴파일하려면 `-codepage`을 사용 하 여 사용할 코드 페이지를 지정할 수 있습니다. @No__t-0 옵션은 컴파일의 모든 소스 코드 파일에 적용 됩니다. 자세한 내용은 [.NET Framework의 문자 인코딩](../../../standard/base-types/character-encoding.md)을 참조 하세요.  
  
 소스 코드 파일이 시그니처와 함께 현재 ANSI 코드 페이지, 유니코드 또는 u t f-8을 사용 하 여 저장 된 경우에는 `-codepage` 옵션이 필요 하지 않습니다. 사용자가 **인코딩** 대화 상자에서 다른 인코딩을 지정 하지 않는 한 Visual Studio는 기본적으로 현재 ANSI 코드 페이지를 사용 하 여 모든 소스 코드 파일을 저장 합니다. Visual Studio는 **인코딩** 대화 상자를 사용 하 여 다른 코드 페이지로 저장 된 소스 코드 파일을 엽니다.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
