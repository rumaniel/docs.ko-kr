---
title: -langversion (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
ms.openlocfilehash: 15f334f280c2aca83ba5b628a1137464c31c6282
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005560"
---
# <a name="-langversion-visual-basic"></a>-langversion (Visual Basic)
컴파일러가 지정 된 Visual Basic 언어 버전에 포함 된 구문만 허용 하도록 합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-langversion:version  
```  
  
## <a name="arguments"></a>인수  
 `version`  
 필수. 컴파일하는 동안 사용할 언어 버전입니다. 허용 되는 값은 `9`, `10`, `11`, `12`, `14`, `15`, `15.3`, `15.5`, `default` 및 `latest`입니다.

 @No__t-0을 부 버전 (예: `11.0`)을 사용 하 여 전체 숫자를 지정할 수도 있습니다.

 명령줄에서 `-langversion:?`을 지정 하 여 모든 가능한 값 목록을 볼 수 있습니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션은 컴파일러가 허용 하는 구문을 지정 합니다. 예를 들어 언어 버전을 9.0로 지정 하는 경우 컴파일러는 버전 10.0 이상 에서만 유효한 구문에 대 한 오류를 생성 합니다.  
  
 .NET Framework의 다른 버전을 대상으로 하는 응용 프로그램을 개발할 때이 옵션을 사용할 수 있습니다. 예를 들어 .NET Framework 3.5를 대상으로 하는 경우이 옵션을 사용 하 여 언어 버전 10.0에서 구문을 사용 하지 않도록 할 수 있습니다.  
  
 명령줄을 사용 하 여 @no__t를 직접 설정할 수 있습니다. 자세한 내용은 [특정 대상 .NET Framework 버전 지정](/visualstudio/ide/targeting-a-specific-dotnet-framework-version)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 코드는 Visual Basic 9.0에 대 한 `sample.vb`을 컴파일합니다.  
  
```console  
vbc -langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [특정 대상 .NET Framework 버전 지정](/visualstudio/ide/targeting-a-specific-dotnet-framework-version)
